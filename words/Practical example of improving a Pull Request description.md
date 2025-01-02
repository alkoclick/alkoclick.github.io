Following up on [Writing Pull Request descriptions](Writing%20Pull%20Request%20descriptions.md) , this article will focus on how we can improve the description of a PR. Much of the advice comes down to good technical writing (see also [Google Technical Writing Course](Google%20Technical%20Writing%20Course.md)), with its focus on clarity and brevity. However, some of the advice is also about how to write text that is specifically meant to accompany a block of code, yet has a different lifecycle than the block of code.

This is the PR we will discus: [kweb-core#232](https://github.com/kwebio/kweb-core/pull/232)

## Reviewing the PR

#### Good stuff

Let's start with outlining what this PR generally has going well for it:
- It starts with a summary
- It calls out technical decisions by the author explicitly to invite discussion
- It documents how the author arrived at making this particular change
- It uses a polite and (hopefully) pleasant tone
- It considers the public api and downstream consumers and their experience

Now let's address what can be improved.

#### Title
The title is vague, especially for such a small changeset. That makes it hard to understand the contents when scrolling the PR list, or when looking at the tab title. A far better title would be something like: "Replace ElementCreator ConcurrentQueue with AtomicInteger", which is much more specific.

#### Reproducibility
For many PRs in public repos, Minimal Reproducible Examples are required. For performance related PRs, which have to navigate a nuanced landscape of hardware and software, this is essential. However the author (me) has provided no way to reproduce this. Even the workflow and findings are kinda hard to follow:

> "If you look at the heap of a kweb app"

What kind of app, small, medium, large? What kind of features? What usage pattern are we talking about? Can you provide an example heap or program that demonstrates this?

#### Impact
While the PR claims a large performance improvement, it does not quantify it. This makes it unclear for the consumers to know whether there's been an improvement at all, or what they should expect. 

Part of the reason for that is that there is no shared frame of reference for the improvement, as it depends on the application chosen. Using a Minimal Reproducible Example would have addressed this. Alternatively, any of the [kweb demos](https://github.com/kwebio/kweb-demos) could have been used and they would also provide a quantifiable reference.

#### Missing links
We've established that there are no ways to validate anything this PR claims immediately. One of the lesser reasons is the lack of links to things, e.g:

> "Concurrency trap that @sanity spotted"

Where was this spotted?

> "Unused by anything besides a count"

Which count and where? Was that count unimportant?
