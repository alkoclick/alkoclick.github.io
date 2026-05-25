There is a pattern for apps that were never designed to be cloud native: You try to stop them in Kubernetes, they do nothing for 30 seconds, then abruptly terminate. Indico follows this pattern too, and it's a problem, as it adds 30 seconds of overhead to any operation, making it quite likely that your users (and your automated checks) will experience this impact. Why does this happen and how can we fix it? 

Follow me as we peer into the abyss:
![](../media/Pasted%20image%2020260525110855.jpg)

## The issue
Let's see what happens from the Kubernetes side: Upon receiving a termination signal, the control plane sends a SIGTERM to every container in the pod. This signal reaches the main process (pid 1). The containers are then allowed to terminate gracefully with a default period of 30 seconds. If they fail to do so, then the control plane sends a SIGKILL, then cleans up the resources.

Where does this SIGTERM go to then? Well, PID 1 (the entrypoint) in the Indico container is the `docker-entrypoint.sh` script, as you can see defined in the dockerfile [here](https://github.com/indico/indico-containers/blob/52d3203b44fdc5ed51082b8adc0b9d21a466ff6f/indico-prod/worker/Dockerfile#L56). Here you can see the script in its entirety:

```
#!/bin/bash

source /opt/indico/.venv/bin/activate

exec "$@"
```

*Okay, so this passes control over to whatever argument has been given, which is by default... nothing?* 

![](../media/Pasted%20image%2020260525111106.jpg)

Yep, it is by default nothing, and the user of this container has to pass an explicit argument for the script to run, either `run_indico.sh` or `run_celery.sh`. As you can reasonably guess, this lets the user either run the Indico server, or a Celery worker. Yes, the developers could have chosen a default, but I get their decision.

Now, in the `run_indico.sh` script we [do the following](https://github.com/indico/indico-containers/blob/master/indico-prod/worker/run_indico.sh), in order:
1. Run some basic DB checks
2. Run migrations if required
3. Do a weird-ass container in container fetch for Latex (don't ask me I guess there's a reason)
4. Call uwsgi

![](../media/Pasted%20image%2020260525111723.jpg)

So the call stack so far looks like this:
`docker-entrypoint.sh` -> `run_indico.sh` -> `uwsgi /etc/uwsgi.ini`

The docker entrypoint execs to pass control over to the run_indico script so it's actually completely out of the picture. Indeed, if we `ps -aux` we can see this in practice:
```
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND                                                             
indico         1  0.0  0.0   4496   372 ?        Ss   May22   0:00 /bin/bash /opt/indico/run_indico.sh
```

*Okay, and it then calls uwsgi so then uwsgi must be failing to interpret SIGTERMs somehow right?* 

Hah, you wish it were that simple. You see, without explicit handling, the script is neither processing nor forwarding SIGTERMs down to uwsgi. As this confused Stack Overflow user [asking for help](https://unix.stackexchange.com/questions/146756/forward-sigterm-to-child-in-bash) finds out, you have to either run a loop to trap the incoming signal, or just exec to completely pass the control flow over to the next step.

*Okay, so we just exec uwsgi and call it a day, right? RIGHT?* 

Hah, you wish it were that simple. You see the UWSGI project has (had) a long running convention of using SIGTERM for a reload rather than a termination because... honestly no good reason, by their own admission in the ["Things to know"](https://uwsgi.readthedocs.io/en/latest/ThingsToKnow.html) page:

> Fortunately, this bad choice has been fixed in uWSGI 2.1

This was already [reported in 2015](https://github.com/unbit/uwsgi/issues/849), and has kept surprising people across the ecosystem, e.g these [Netbox folks](https://github.com/netbox-community/netbox/issues/16043). For a shutdown (not graceful), uwsgi uses SIGQUIT. If you are one of those weirdos who think there is value in terminating when receiving the termination signal, you are advised to use the `die-on-term` option for uwsgi, [configurable](https://uwsgi.readthedocs.io/en/latest/Options.html) in the `/etc/uwsgi.ini` file. Piece of cake... right?

![](../media/Pasted%20image%2020260525111317.jpg)

*Okay, I can kinda guess there is a curve ball coming, give it to me straight, what is it?* 

Oof, okay. There was a bug with die-on-term reported fixed in 2.0.27 and it didn't actually do anything.  Thankfully, we are on version 2.0.31 of uwsgi as confirmed by running `uwsgi --version`. So we dodge this one. 

## Solutions
So, in total:
- We need to ensure SIGTERM reaches uwsgi, and
- We need to ensure uwsgi actually terminates on SIGTERM

#### SIGTERM should reach UWSGI
We have 2 paths here:
1. Use `exec` to call uwsgi (should make uwsgi PID 1)
2. Adapt the script to use traps and forward the signal (run_indico.sh remains PID 1)

My recommendation is to use exec.

#### UWSGI should shut down when receiving SIGTERM

1. Upgrade uwsgi to 2.1.0+ (Is it even out? It doesn't seem to have a release changelog entry? [Will it ever be out?](https://github.com/unbit/uwsgi/issues/2037))
2. Ensure the `die-on-term` option is enabled in the `uwsgi.ini` file

Notably, we can also take a different path: Use [Docker stop signals](https://docs.docker.com/reference/dockerfile#stopsignal) to instruct the container to use SIGQUIT instead of SIGTERM to terminate. Kubernetes will then [use this signal instead of SIGTERM](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/#pod-termination-stop-signals). There is also a feature in Alpha from 1.33.0 onwards which allows you to define custom stop signals per pod, bypassing the need to build it into the Docker image.

My recommendation is to enable `die-on-term` in the `uwsgi.ini` [here](https://github.com/indico/indico-containers/blob/master/indico-prod/worker/uwsgi.ini). 

## Patch solution
The quick and dirty patch solution that someone running Indico in Kubernetes can apply until there is a fix:

```
lifecycle:
	preStop:
	  exec:
		# Currently the start script doesn't handle passing sigterm to UWSGI and the uWSGI master falls in one of these PIDs
		command: ["kill","14", "15", "16"]
```

![Pasted image 20260525113001](../media/Pasted%20image%2020260525113001.jpg)


This will send a SIGTERM to the UWSGI main process which in my tests always lands in those PIDs. This is ridiculously fragile, kinda stupid and meant as an extremely low effort patch whose trashiness should motivate you to switch it out ASAP. I have nevertheless looked the devil in the eye, tested this and it successfully cleanly exits uwsgi within about 3 seconds. 

But a curious reader might say: *Hey Alex, this is a kill with no arguments... it's passing a SIGTERM. HOW DOES THAT WORK?* 

Dear curious reader, I'm still figuring that out. But I suspect that the SIGTERM behaviour is now in uwsgi mainline. 
