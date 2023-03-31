[Tom Callaway's tweet](https://twitter.com/spotfoss/status/1511359144137265156) about sharing an Open Source story inspired me to write down this adventure, that happened to me a few years ago.

## Background

In 2019, I was a technical student at CERN, working in the BE-ICS-TI section, which translates to "Beams -> Industrial ControlS -> Technical Infrastructure". In short, my team was working on the monitoring systems for the control systems that managed the main CERN beams. The accelerator was off during that time, and all the teams were hard at work evolving their systems.

-- Add pic here --

Our team's backbone (and backend) was [C2MON](https://github.com/c2mon/c2mon), a Prometheus-like system for monitoring DAQs (Data Acquisition Systems) and PLCs (Programmable Logic Controllers) and producing events for consumers via a Message Queue architecture. C2MON had a pretty complex, albeit typical for its time deployment infrastructure and it was deployed on VMs managed by another team. I was working on porting the entire thing into Kubernetes, and to do that I was also replacing the existing deprecated Spotify docker-maven plugin with Google's [Jib](https://github.com/GoogleContainerTools/jib).


## Trouble on my left, trouble on my right

[Cage the Elephant: Trouble](https://www.youtube.com/watch?v=lA-gGl6qihQ)

I noticed a had a weird bug. When using Jib via Maven, pushing the image to CERN's Gitlab container registry failed, but only if I was pushing to an existing path. It succeeded with a normal `docker push` and it succeeded once for new images.

In slightly more technical detail:
* Jib uses a Kaniko-like logic, which doesn't require docker present at the build machine
* Under the hood, Jib uses Google's core [HTTP Java client](https://github.com/googleapis/google-http-java-client/)
* CERN used [CEPH](https://ceph.io/) for block storage
* CERN's on-premise enterprise Gitlab installation used the CEPH block storage with an S3 interface implementation

At this point I was really convinced that this was a PEBKAC, because everyone involved here were software titans, and I still so fresh. Like the error was either in Google's HTTP library, in Gitlab's container registry implementation, in the AWS S3 standard... or in my code. Sure, I had worked self-employed and written plenty of production code over time, but clearly I was in way over my head.

So let's try to debug this thing and figure out what we're doing wrong! I activated debug mode on Maven and the plugin, I got inundated with 10000 lines of output and I started digging.

I started by logging each command that JIB was doing one by one, then replicating it with CURL. Eventually I found a command where Gitlab (CEPH) returns a 307, and then I could execute it with the returned URL and get 200. However, Jib returned 403 when trying to run the same URL. 

I could replicate JIB's exact request via curl and also get 403. I noticed that there were some slashes in the path that were percent encoded in Gitlab's (CEPH's) 307 response, but when Jib was performing the request it was removing the percent encoding. 

It all came down to this:  JiB executed:

```
curl (...) 'https://s3.cern.ch/...Amz-Credential=.../20190401/us-east-1/s3/aws4_request&...'
```

while the location returned from the 307 was
```
'https://s3.cern.ch/...Amz-Credential=...%2F20190401%2Fus-east-1%2Fs3%2Faws4_request&...'
```

Alright, this is great! We have a replication command working, so I put up a [Github issue to Jib](https://github.com/GoogleContainerTools/jib/issues/1590). 


## What's an RFC anyway?

On the ticket, Googlers confirmed my suspicion and even (to my horror) brought up a thing called the RFC (Request For Comment, used to define the HTTP standard). They helped me understand that according to the specification, the slashes could be optionally percent encoded, and that according to the same specification, software should not treat encoded vs unencoded params differently. In other words, their implementation followed the RFC to the letter. Here's how it works in practice (note that `URL` is the default core Java implementation and `GenericURL` is the Google implementation):

```
URL url3 = new URL("http://example.com?query=string%2Fpart");
System.out.println(url3);
System.out.println(new GenericUrl(url3));
System.out.println(new GenericUrl(url3).toURL().toString());
	
prints

http://example.com?query=string%2Fpart
http://example.com?query=string/part
http://example.com?query=string/part
```


Meanwhile, my report also gathered some internal attention and soon enough I was pointed to this code and comment by a confused engineer, years ago:

```
    if (key == "X-Amz-Credential") {
      /* FIXME(rzarzynski): I can't find any comment in the previously linked
       * Amazon's docs saying that X-Amz-Credential should be handled in this
       * way. */
      canonical_qs_map[key.to_string()] = val.to_string();
    } else {
      canonical_qs_map[aws4_uri_recode(key, true)] = aws4_uri_recode(val, true);
    }
```

Aha! That was it! On the CEPH side, the X-Amz-Credential header was being reencoded with percent encoding, while the header sent by Jib did not have slashes encoded! This ended up failing the validation and returning a 403.

I wasn't the only one to have noticed either: Independently, this [had been fixed upstream](https://github.com/ceph/ceph/pull/23652/files) in CEPH during my investigation, and the new version already contained the fix.

So, the segment above was fixed to: 
```
    // while awsv4 specs ask for all slashes to be encoded, s3 itself is relaxed
    // in its implementation allowing non-url-encoded slashes to be present in
    // presigned urls for instance
    canonical_qs_map[aws4_uri_recode(key, true)] = aws4_uri_recode(val, true);
```

About 2 weeks later CERN deployed the new CEPH and the bug was resolved!

## Conclusions

This little adventure taught me a few important lessons:
* Open source software means open debugging
* People, whether maintainers or not, know so much helpful information ; just talk to them!
* Developers may often predict a problem before it happens, but that doesn't mean that they have the time and priorities to fix it
* RFCs are the duct tape holding the computing universe together
* Trust no code, verify every assumption

Thanks for making it to down here! This has been part 1 of 5 from my 5 days at Kubecon series, find the next parts here:

https://twitter.com/alkoclick/status/1526149072318611457