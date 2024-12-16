
This should become an article but for now it's my braindump, sorry
* Had the opportunity to review a lot of PRs (1K), noticed similartites
* Great PRs != Acceptable PRs
* We will speak very little of code quality, because that's the domain of each language. 
* Social level: Pull requests are the process of proposing a code change to the organisation, and then implementing it
* Technical level: PRs are the process of proposing a code change to a codebase and implementing it
* The PR itself is a sociotechnical container around the idea of a change
	* Note that this is an extremely deep topic, and organisations have poured millions into researching, documenting and enforcing things such as the "Change management process". Change is not easy, and our field is somewhat lucky to have such a widely adopted convention
* Async cultures focus more on this because sync cultures transfer context more in-person. This does hurt the organisational memory of sync cultures as it becomes attached to people and is harder to record
* When is it worth investing? Most of the time tbh
	* Keep in mind friction is a factor here. Friction in writing means less stuff getting written
* Dependency PRs should be automated, and do some research on other common types you can automate (e.g if you're updating teams constantly find out if you can sync them)
* Do one thing No sideeffects
* Lines changed: 0 < Optimal < A lot
* Keep in mind that git history is not immediately apparent in code - do not confuse this with app documentation
* A great thing to document is your motivation, thinking process and expectations, this is the least apparent in code and most to you
* Fancy restaurants, or even your grandma will introduce a plate as they are serving it. This serves to improve the quality of the experience - you are guided to pay attention to the individual flavors, or a compelling story about the "actual thing" being served. PRs work the same way as a package for code changes
* To stick with food metaphors, you've probably noticed that most beers come with dedicated glasses to drink them in. The glass by itself is only a container. Nevertheless, the experience of pouring and drinking the beer changes drastically between glasses, which affects the actual flavour! The brewer can design one that best showcases the features of the beer they wanna exhibit
* Good PRs can actually improve your code quality as they help you figure out things to improve, or test, or change the way you implement stuff.
* Templates are a social construct for setting shared expectations on PRs. Like any other social construct, they are malleable, so feel free to adapt them to your use case. Nevertheless, if you engage them in good faith they're usually decent
* If you struggle to write good PR descriptions, here's a template: ...
* 

Bring up examples of PRs:
* One that can be improved, and discuss the improvements

Can be improved
https://github.com/kwebio/kweb-core/pull/232
Good stuff:
- Summary
- Calling out decisions explicitly
- Polite/pleasant tone
- Considering public api and downstream consumers

Could be improved:
* Missing links
	* "Concurrency trap that sanity spotted" where?
	* "Unused by anything besides a count" where?
* Reproducibility
	* If you look at the heap of a kweb app? Can you provide an example heap or program that demonstrates this?
* used a GPG key that I've since removed
* Describe impact of change, what should people expect
* Title is vague