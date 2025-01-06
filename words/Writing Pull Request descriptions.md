## Introduction
In December 2024, fellow engineer Alice Rum and I organised an event titled "Pull Request Awards" in Miro. The overall style was a light-hearted take on "Academy Awards but for Code". During that event, I also wrote [Thoughts from reading 1000 iac Pull Requests in one day](Thoughts%20from%20reading%201000%20iac%20Pull%20Requests%20in%20one%20day.md). 

This piece is focused on the descriptions of pull requests, why they are meaningful, and how to improve them. We shall speak very little of code quality itself, because that's the domain of each language. 

See also:
* [Pull Request Awards](Pull%20Request%20Awards.md)
* [Practical example of improving a Pull Request description](Practical%20example%20of%20improving%20a%20Pull%20Request%20description.md)

Let's start with a couple of key thoughts on why we write PRs and PR descriptions.

### Pull requests are containers
A pull request is not a code change. A pull request is a transparent container around the change.

You might say, okay great, but we can do without the container right? Yes and no. You can drink water with no container, but a glass or bottle makes that experience a lot more convenient. 

To use a food analogy, you've probably noticed that most beers come with dedicated glasses to drink them in. The glass by itself is only a container. Nevertheless, the experience of pouring and drinking the beer changes drastically between glasses, which affects the actual flavour! The brewer can design a glass that best showcases the features of the beer they wanna exhibit.

### Pull requests are sociotechnical containers
A pull request is a [Sociotechnical systems](Sociotechnical%20systems.md) container around the idea of a change. Organisations typically call this the "change management process". This is a fairly deep topic, and organisations have poured millions into researching, documenting and enforcing such processes. I consider our field somewhat lucky to have such a widely established convention.

On the social level, pull requests are the process of proposing a code change to the organisation, and then implementing it. The change gets shared, reviewed and approved by other humans.

On the technical level, PRs are the process of proposing a code change to a codebase and implementing it. The change gets built, tested, validated and if accepted repeats all those steps once it gets to the main branch.

Alright, now that we know what purpose PRs serve, let's hop onto descriptions themselves.

### Descriptions are not necessary (yet often vital)
You can merge PRs without a description. You've probably written plenty of those yourself! Besides, other than the PR description there's a bunch of other "free text" locations to discuss and document the proposed change:
* Code comments near the affected lines
* Project documentation in the repository (e.g README files)
* Project documentation in external tools (e.g Confluence)
* The commit description(s)
* The task description (e.g in Jira or Trello)
* Distributed, often undocumented knowledge across team members

It's easy to dismiss this as typical overengineering by competing vendors and processes, yet each of those serves, a different purpose. That doesn't make them necessary though.

Code comments live near the code. They typically explain how and why a block of code works. At any point in the project's lifecycle someone who reads the code will be able to see them. It's usually matched to some specific code, but not to a specific code change. It can, and should be updated.

The project documentation living in the repository or in external tools is typically higher level as it's not matched to a specific block of code. It discusses and explains the thought process behind the project's architecture, or design decisions. It's updated independently of code changes.

The commit description lives in git history. It's the opposite of a code comment as it is immutable and only describes a single group of code changes. It's not immediately apparent to someone reading the code today, but only someone exploring the project history. 

The task description lives outside all of these systems. It's typically the point of interaction between the rest of the organisation and the specific team. It's usually updated up until the point when the code change gets executed, and then no more.

The shared knowledge pool lives in each team member, and each member has different representation of it. In async cultures, the latency of read/write to this knowledge pool is high, while in sync cultures it's typically low. It's low cost to read/write to (e.g just tell your colleague something), but has no eventual consistency. Primary and replica nodes can be hard to differentiate. Sync cultures usually take on this organisational memory debt in exchange for organisational agility, though just like tech debt you need to pay it back eventually.

### Templates
Templates are a social construct for setting shared expectations on PRs. Like any other social construct, they are malleable, so feel free to adapt them to your use case. Nevertheless, if you engage them in good faith they're usually decent. A great thing to document is your motivation, thinking process and expectations. This is the least apparent in code and most to you while authoring the change.

If you struggle to write good PR descriptions, here's a basic template: 
```
### Motivation

<!-- Why did you make the changes, i.e., detail the motivation for PR. -->

### Proposed changes

<!-- What are the changes, i.e., list the issues addressed by the PR. -->

### Unrelated changes (optional)

<!-- Are there changes not related to the issue itself, i.e., renaming other things, fixing unrelated bug(s). If there are no unrelated changes, remove this section. -->

### Notes (optional)

<!-- Any additional information that may be relevant to the review of the PR, i.e., how to test. -->

### Related PRs/issues (optional)

<!-- Any PRs or issues that are connected with this PR. -->
```

### Personal workflows
Knowing the above, here's some things I typically do:
* I typically dedicate most of my effort to writing a good commit description, then use that to form 90% of the PR description
* My PR description will sometimes have some extra context around how/when the PR will be merged
* I self-review my PRs as a first pass, and try to add comments to guide the reviewer
* Whenever PR comments ask about unclear code, I document the answers in code comments, not in a PR comment
* While working on bigger projects, I will invest a lot of effort in documenting the design and plan up front, and run those through the organisational processes
* I will then work very close and synced with another colleague to execute these designs. Our PR descriptions will generally be lightweight, except for high-impact changes, or when interacting with other teams
* After completing bigger pieces of work, I look to create a documentation page in the repository or external knowledge base related to the project, then I look to share that documentation to humans (e.g in Slack channels, or via a presentation)
