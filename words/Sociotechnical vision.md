
Do you remember the 3d glasses that were somewhat popular around 2000?

![](https://upload.wikimedia.org/wikipedia/commons/4/44/Chick_Quest.png)
<a href="https://commons.wikimedia.org/wiki/File:Chick_Quest.png">Irisblixten</a>, <a href="https://creativecommons.org/licenses/by-sa/4.0">CC BY-SA 4.0</a>, via Wikimedia Commons

They are called red-cyan stereoscopic glasses. They work by filtering out colour ranges so that your left and your right eye end up seeing slightly different pictures, both of which have partial depth information. When you look through both eyes, the image is overlaid and your brain perceives a more complex picture (the stereoscopic illusion) than the individual pictures.

Sociotechnical vision is the term I use for viewing systems through the individual lenses of social and technical work, then overlaying them to perceive a more complex system. The field of [Sociotechnical systems](/Sociotechnical%20systems.md) is fascinating to me and I wholeheartedly recommend reading more about it.

In this article, we'll practice Sociotechnical vision on a simple example. Let's say you have created an alert.

## Technical

Let's turn on the cyan technical eye, that solely sees technical systems and interactions. In that case we'd see something like this:

![SociotechnicalVisionTechnical](../media/SociotechnicalVisionTechnical.jpg)

The above diagram maps a fairly typical alert delivery diagram:
* PromQL, the query language to write the alert in
* Repository that controls a simple alert manager config
* Prometheus, the system that does the monitoring
* Prometheus alert manager
* Monitored service
* Grafana, which can display your alert and other metrics
* OpsGenie, a tool to manage and reach on call staff
* Responder phone
* Slack channel to receive alerts in
* Feature platform, which we will assume can disable the feature causing the alert

## Social

Now let's turn on the other eye, the red one, and look at the social side of the same space:

![SociotechnicalVisionSocial](../media/SociotechnicalVisionSocial.jpg)

This diagram maps some of the organisational aspects of alert creation, response and delivery:
* Alert created after incident due to policy
* Alert has to follow company conventions
* Alert requires approval by o11y team
* Human on call rotation
* Group of engineers following the alerts channel
* Grafana is not accessible by all team members
* Feature platform is unclear to a lot of engineers, they haven't used it

Notice that the human side has a lot more actions. One of the powerful features of humans is that they can generally adapt to unexpected scenarios, and are usually authorised to act accordingly. Most incidents I've observed are solved by humans taking actions.

## Sociotechnical

Let's overlay them:

![SociotechnicalVisionFull](../media/SociotechnicalVisionFull.jpg)

Okay now, this requires a zoom to even understand what's going on 😅 This diagram helps our brains perceive a picture that's more than the sum of its parts.

If we were to describe the diagram, in short:
1. Humans create an alert
2. Machines manage and deliver the alert
3. Humans have to be available to respond
4. Humans have to access, know and use technical systems to respond successfully

A few things stand out for me:
* Notice the terminal states highlighted in grey. These are fail states. Typically an operator arriving there is out of immediate options, besides escalating to an unknown other, if they exist and are reachable
* Notice the spectacular amount of wasted effort if our operator reaches the final step, the feature management service, and cannot use it
* Notice the mingling of social and technical actions. This system cannot reach a success state without the collaboration of humans and machines
* The moment when control passes from machine to human is quite important. In aviation, they call it "transfer of control" and in their field, this is often where the failures that kill people actually happen
* There is a single success state here, but systems with this amount of complexity typically will have way more success and fail states

Equipped with the above, we are now able to ask (and answer) questions such as:

> How can we improve average time to understanding an issue?

We'd need to make sure our alert evaluation interval is fast, the alert fires as soon as it has enough data, and that the alert is clear and unique for the responder to parse or look up. That last part is usually the most of the time, yet it's invisible if you're looking purely on the technical side.

> How can we improve average time to mitigation?

Besides the above, we'd need to make sure that all responders can access the feature platform, know how to use it, and have permissions to hit the "disable" button on a feature. We'd need to have an on-call rotation to reliably have a responder available. Besides the main on-call responder, we may be able to enlist additional responders if the alert successfully propagates to Grafana and Slack, and the responders can access and do follow those. 

## Conclusions

Sociotechnical vision is the ability of seeing a system via a social, technical and finally a sociotechnical lens. Typically only the last one actually represents the system's complexity. Meaningful ways to describe and improve the system usually surface when you see that full complexity. 

In short, failing or refusing to see the organisational aspect of any tech system is like working with your one eye permanently closed 😉