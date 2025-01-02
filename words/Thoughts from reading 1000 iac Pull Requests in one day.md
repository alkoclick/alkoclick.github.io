
While organising [Pull Request Awards](alkoclick/words/Pull%20Request%20Awards.md) in Miro in 2024, I went over approximately 1000 Pull Requests in a single infrastructure as code repository. Most of them were a mix of Terragrunt + Terraform or Ansible. 

There were a few things that stood out to me:
* I was able to spot two common clusters of repeated PRs, that collectively accounted for over 30% of the total. Because typically these are contributed per team, noone had previously surfaced the load these things generated, yet this exercise was able to easily call them out.
* So many people hit various IAM issues, and make repeated PRs
	* A very common issue is the 60 char limit
	* Another issue is the max policy size
	* And of course lack of clarity on the exact permissions required by a service
- There were some folks who consistently make greats PRs, at least in my eyes. Not every PR is perfect, but many of the top PRs are theirs. PR-Influencers?
- In the same vein, and I realise this sounds kinda obvious, there are some people who are consistently great and very thorough reviewers.
	- Could we somehow map those so we have a clearer view of team dynamics? E.g a basketball team typically has its players perform distinct roles, even though all of them can do mostly everything, and they have a common base skillset
- People seem to create far better PR descriptions in repos that they are “guests” in, presumably because they have less shared context with the readers/reviewers and decide to explain it instead
	- See also: [Writing Pull Request descriptions](Writing%20Pull%20Request%20descriptions.md)