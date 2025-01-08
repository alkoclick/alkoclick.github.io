This post was originally a section over at [Writing Pull Request descriptions](Writing%20Pull%20Request%20descriptions.md).

 Besides the PR description there's a bunch of "free text" locations to discuss and document a code change:
* Code comments near the affected lines
* Project documentation in the repository (e.g README files)
* Project documentation in external tools (e.g Confluence)
* The commit description(s)
* The task description (e.g in Jira or Trello)
* Distributed, often undocumented knowledge across team members

Code comments live near the code. They typically explain how and why a block of code works. At any point in the project's lifecycle someone who reads the code will be able to see them. It's usually matched to some specific code, but not to a specific code change. It can, and should be updated.

The project documentation living in the repository or in external tools is typically higher level as it's not matched to a specific block of code. It discusses and explains the thought process behind the project's architecture, or design decisions. It's updated independently of code changes.

The commit description lives in git history. It's the opposite of a code comment as it is immutable and only describes a single group of code changes. It's not immediately apparent to someone reading the code today, but only someone exploring the project history. 

The task description lives outside all of these systems. It's typically the point of interaction between the rest of the organisation and the specific team. It's usually updated up until the point when the code change gets executed, and then no more.

The shared knowledge pool lives in each team member, and each member has different representation of it. In async cultures, the latency of read/write to this knowledge pool is high, while in sync cultures it's typically low. It's low cost to read/write to (e.g just tell your colleague something), but has no eventual consistency. Primary and replica nodes can be hard to differentiate. Sync cultures usually take on this organisational memory debt in exchange for organisational agility, though just like tech debt you need to pay it back eventually.