# My dev notifications workflow
Originally published on [[2022-03-10]] at https://alkoclick.medium.com/my-dev-notifications-workflow-349d4bcbf90c

---


As a dev by trade, I was recently a bit frustrated with having notifications across multiple channels: The VCS, the project management tool, email and of course Slack. So I set out to find a slightly more conscious workflow that would allow me to control where and how I get notified.

At the end of it, I had just a single platform (Slack) for all notifications, and I check my email once a day, which honestly feels great. Here’s my setup.

## Solution Design

### Tools
* Github: Produces 10-20 notifications per day, usually someone is blocked until reply.
* JIRA: Produces 1-10 notifications of low-mid priority. Replies are usually asynchronous and can wait.
* Email: Outside of Github/JIRA notifications and some vendor marketing, this usually has async work items that require high effort and decisions.
* Slack: Produces a constant stream of notifications at any priority. Usually low effort to resolve. People expect fast responses if seen online. 

### Goals
* Reduce the overhead of context switching between platforms to check all notifications
* Have an "off" button for developer focus time
* Be able to instantly respond to small tasks when online
* Clearly know when I have "caught up" with everything and deserve peace of mind
* No notifications should be dropped

## Practical Implementation

Slack is the "instant" notifications platform. It has good integrations with everything, and is the primary company workspace. 

So we set up the other 2 notifications platforms with Slack:

## JIRA -> Slack
There's a nice integration for that path. It does pretty much everything you need, and it's probably already on your workspace. [Read the docs](https://slack.com/help/articles/218475657-Jira-for-Slack). After enabling this, disable JIRA from emailing you: 
* Uncheck everything in the marketing [email notifications center](https://id.atlassian.com/gateway/api/marketing/email-preferences)
* Disable autowatching issues everywhere you can (e.g on your personal settings)
* I think I did something more too, to disable notifications but it's basically impossible to find due to JIRA UX so... /shrug

![[Pasted image 20220310165516.png]]

## GitHub -> Slack
GitHub is harder, because there's 2 ways the [integration between GitHub and Slack](https://slack.github.com/) is configured, and they both have different shortcomings. Also none of them really push notifications for *every* possible email you could actually get from GitHub, so yeah, don't get your hopes up. So how do we make this work?

#### Slack integration
There's of course [an official integration](https://github.com/integrations/slack), and by default the workflow is that you have to subscribe to repositories, in order to receive notifications for them. That's annoying, because in the Cloud team we create new repositories all the time and either folks would have to ping "Hey, I created this new repo", or you... don't get notifications for it. Uncool. We can of course subscribe to the notifications of the entire org as well... with all its 336 current repositories. Also uncool.

There is hope! Look at this feature called [scheduled reminders](https://github.com/integrations/slack#scheduled-reminders). Some product owner went nuts with it and thankfully, it includes "real-time notifications". See this:
![[Pasted image 20220310171806.png]]

This is almost exactly what we need! It covers about 90% of notifications we receive, and as an added bonus, can send out scheduled reminders for open PRs. The most important missing case is that we won't get notified if someone creates a new comment in a PR that we are taking part in, but didn't create. We will also not get notified for security events.

Ugh! This is pretty frustrating, because by default the notifications we get in email are already filtered properly and are more customizeable. Can we make sure that we also get those, so that we never miss a notification, even if we get some duplicates? Let's try.

* We can set up [email notifications in our Slack DMs](https://slack.com/help/articles/206819278-Send-emails-to-Slack), or in a personal notifications channel
* We create the following Gmail filter that will forward GitHub notifications to that Slack DM
```xml
<feed xmlns="http://www.w3.org/2005/Atom" xmlns:apps="http://schemas.google.com/apps/2006">

<title>Mail Filters</title>

<id>tag:mail.google.com,2008:filters:z0000001646340861019*8632063207270361537</id>

<updated>2022-03-10T15:31:13Z</updated>

<author>

<name>Alexandros Papageorgiou Koufidis</name>

<email>alexandros.papageorgiou.koufidis@vanmoof.com</email>

</author>

<entry>

<category term="filter"/>

<title>Mail Filter</title>

<id>tag:mail.google.com,2008:filter:z0000001646340861019*8632063207270361537</id>

<updated>2022-03-10T15:31:13Z</updated>

<content/>

<apps:property name="from" value="notifications@github.com"/>

<apps:property name="label" value="Github"/>

<apps:property name="shouldMarkAsRead" value="true"/>

<apps:property name="forwardTo" value="AUTOGENERATED_SLACK_EMAIL"/>

<apps:property name="sizeOperator" value="s_sl"/>

<apps:property name="sizeUnit" value="s_smb"/>

</entry>

</feed>
```

This shows up in Slack in the following way

![[Pasted image 20220310164328.png]]

These are not the most readable, but since this is your second layer, usually you just read the title and decide if this is something worth looking deeper in. 

## Email
At the end of this, we have email as the "slow" platform. I can check it once or twice a day. Very low traffic in general, and usually it's some larger proposal, or discussions with third parties outside the company (VanMoof, [they're hiring!](https://www.vanmoof.com/careers))

## Areas for improvement
* Improve filter to avoid duplicate events in Github Slack notifications & emails forwarded
* Formatting emails

## Rejected ideas
* Team notifications channel (different people have different goals)
* Github notifications with opt-in for new repositories (too much manual work to subscribe/unsubscribe, danger of missing notifications for new repos)