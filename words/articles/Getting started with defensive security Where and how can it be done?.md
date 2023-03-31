### Getting started with defensive security: Where and how can it be done?

[[2021-01-18]]

![](https://cdn-images-1.medium.com/max/800/0*nfF-HHwOaDlpW8QU)

Photo by [Haley Hamilton](https://unsplash.com/@haleywayphotography?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

### Introduction

Hey there! You’re probably here because you care at least a little about security in software development. You may have even read a book or done a course on security, or penetration testing, or white-hat hacking, but how do those lessons translate to your real-world projects? I mean, where do you even start adding more “security” to an application?

There’s a lot of possible angles and while it’s good to grasp different sides of a problem, noone expects you to do everything! In this article we’ll discuss some actionable tasks that belong to the realm of penetration testing, application development, DevOps and a handful of blue-team ops. Have fun!

### Summary

Intended audience: Junior-medior developers who have an interest in learning more about security

Intended use: This post is not a checklist to cover every box, but rather a list of possible action items. There’s a lot of questions that can be good to try and answer and don’t be afraid to Google them for a quickstart. Some of them probably apply to you or your organization, some won’t, and that’s okay! You can get started on most of the action items withing minutes or hours, though completing them well may take quite longer. I can definitely vouch they’ll teach you a lot though ;)

Intended flow: An ideal first step would be to pick a few that look quite interesting, then approach a colleague who is more experienced in that particular area, and start asking questions! If you’re more the “talks to machines, not people” type you can… reconsider that approach and try to talk to a colleague instead. Really, it’s worth it.

I’ve added a “Supervisor approval” bullet for the sections where you should probably check in with someone before even firing things up.

### End-User Layer

![](https://cdn-images-1.medium.com/max/800/0*4SnMKM-FbEQw1Ll3)

Photo by [Richy Great](https://unsplash.com/@richygreat?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

**Fuzzing**  
Whatever your application does, it probably has some sort of data input. Consider running a fuzzer on it! A fuzzer is a tool that tries all kinds of random input, especially with unexpected symbols, then validates the output. A fuzzer for example would tell you that some strings cause unexpected results in a form input or a path parameter.  
Tool suggestion: [fuff](https://github.com/ffuf/ffuf)  
Supervisor approval: Recommended

**Load testing**  
Every organization wants some load testing, but preciously few actually have something in place. Especially as a newbie to a project, running some kind of load test is relatively easy, doesn’t require thorough understanding of the project’s codebase, and it will teach you so, so much about how the system behaves! Additionally, you get some pretty unique knowledge about how the system doesn’t work, which you can then share with your team.  
Tool suggestion(s): [JMeter](https://github.com/apache/jmeter), [Artillery.io](https://artillery.io/), [Gatling](https://gatling.io/)  
Supervisor approval: **REQUIRED if you target anything outside localhost**

### Application Layer

![](https://cdn-images-1.medium.com/max/800/0*O4smfR_0aIq5UTY8)

Photo by [Johannes Plenio](https://unsplash.com/@jplenio?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

**Identify core dependencies**  
This is something that is not in itself a security action, but will be useful for a lot of other tasks: Identify the core dependencies of the application (e.g database, message queue systems, external services). This is usually easily done once you find the configuration files, especially for testing/staging, as they will have all this info. Once you’ve found those, it’s often a good idea to document those somewhere, e.g the project’s readme file, if they aren’t there already! Note that in a decent org, you may not have access to prod config files and rightfully so.

**Secret management**  
Most applications require access to some sort of secrets, such as database passwords to function as expected in production. How are those being injected into the application? Common approaches include: a config file with inline secrets, environment variables, a secrets manager, or any combination of the above. Is the mechanism secure? Could a compromised application read or write into the secrets mechanism? Are those secrets reused anywhere? How is “human” access to those secrets controlled?

**Anomaly monitoring in access logs**  
Do you have monitoring in place? Usually there’s going to be a Prometheus/Grafana or ELK combo somewhere that you can look up. Do you have any interesting metrics, such as endpoints usage or any form of access logs? Search for irregular access patterns in them! A simple first test is to search for control characters (such as `<,{`) in the paths accessed, as it may indicate injection attempts.  
Tool suggestion(s): Existing anomaly detection functions in your monitoring

**Vulnerable dependencies**  
Outdated dependencies can lead to a world of hurt and using vulnerable dependencies is a mistake that most software teams still make today, because they’re unaware. Are your dependencies vulnerable or obsolete? To find out, look to whatever tool you are using for building, as nearly all of them have some kind of dependency checker.  
Tool suggestion(s): `npm audit` , `maven dependency-check plugin`,etc. Just search for (your build tool name) dependency vulnerability check

### System Layer

![](https://cdn-images-1.medium.com/max/800/0*G9Rq3L2Bcvco_ELN)

Photo by [Clint Patterson](https://unsplash.com/@cbpsc1?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

**Access controls**  
Are you able to SSH or RDP into the staging/prod machines? If so, why? How was that access arranged and who else has that access? Is there a policy around that access or is it just “everyone on the internal network”?

**Vulnerable dependencies**  
Dependencies don’t just exist in your application layer, but also on the OS itself. Are the packages on the server up to date? Does your application run on a runtime that could itself be outdated, such as the JVM? Are there any other services collocated with your application that run vulnerable versions?

**Process isolation**  
Whatever the system under your code’s runtime, it has to run your process somehow. If the user that launches the process is compromised, what else can it access on the server? Similarly, if other processes are compromised, can they access your code? Does it have its own user? A typical good practice dating way back is that each service, especially those with internet traffic, has its own user and read/write access only to its application folder, nowhere else!

### Network Layer

![](https://cdn-images-1.medium.com/max/800/0*bXfjYN5JztaZomIP)

Photo by [Alina Grubnyak](https://unsplash.com/@alinnnaaaa?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

**DNS Nameservers**  
DNS is the system used to connect hostnames to IPs that users can connect to. Who owns the DNS nameservers possibly used to serve your core dependencies e.g the database, or resource streams? Could that provider choose (or be made) to return invalid results, pointing DNS requests for your services to malicious hosts? DNSSEC is a set of frameworks that can help verify the servers you are connecting to are indeed the ones you intended (kinda like HTTPS). Do your nameservers comply with it?   
Tool suggestion(s): `dig`

**DNS Resolvers/Upstream**  
Who owns the DNS resolvers your application (or work machine) uses? A DNS resolver is a component that reads incoming DNS queries and directs them to the appropriate destination, which is usually an “upstream” resolver, or a nameserver. Is your application using something like BIND or Unbound as a localhost stub resolver? If so, it probably forwards those queries to an upstream recursive resolver. Commonly this would be something like 1.1.1.1 (Cloudflare) or 8.8.8.8 (Google). If so, are all queries forwarded there, or only the ones outside your domain? If all queries are forwarded there, are you comfortable with Cloudflare or Google having access to all your requests with their path and query parameters? Are there realistic alternative resolvers on your platform and infrastructure?  
Tool suggestion(s): `dig`

**Data egress**  
If data in your application is compromised, the attacker will need some way to exfiltrate it back to their possession. This is most commonly done via HTTP requests to servers the attacker controls, though DNS queries have also been employed. If you have some half-decent network security policies, you may already be blocking some of the problematic HTTP traffic, so how much of it are you blocking? Outside of HTTP, do you have any measures in place to prevent DNS data exfiltration?  
Tool suggestion(s): Talk to experienced people, this is usually complex

**Outdated TLS protocols**  
I’m going to assume your services use TLS (see: HTTPS) because they absolutely should be. Which version of TLS are your hosts on? Is it supported and not considered insecure? As you may be aware, the TLS protocol is negotiated by both the client and the server and they agree on a common choice. What is the lowest TLS version that your servers are willing to negotiate?  
Tool suggestion(s): Your browser, [curl](https://github.com/curl/curl)

**Network analyzer**  
Are you able to run a Wireshark or a similar packet analysis tool in a staging/prod server? If not, what’s stopping you, besides common sense? Is there any policy in place, whether automated or not? If you were to set something up, what kind of traffic would you see?  
Tool suggestion(s): [Wireshark](https://gitlab.com/wireshark/wireshark)  
Supervisor approval: **REQUIRED — Based on how wide the network is, consider talking to a network admin and even your org’s legal team.**

### Development Layer

![](https://cdn-images-1.medium.com/max/800/0*4lw84HE8vWiqKvT8)

Photo by [James Harrison](https://unsplash.com/@jstrippa?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

**Secrets in VCS**  
Are there any secrets in your VCS history? There’s lots of stuff (AWS credentials, DB secrets and whatnot) which is confidential info that should never be committed, since an attacker can then just look it up. There’s tools that will automatically detect these for you (usually by looking for specific keywords and/or high entropy strings). You can even automate their runs into pipelines!  
Tool suggestion(s): [gitleaks](https://github.com/zricethezav/gitleaks)

### Closing words

Hopefully this guide has illuminated some of the paths of security for you, or at least given you some useful ideas for tools to play with! Either way, have fun and don’t be the person who says: “We’ll add security later” ;)