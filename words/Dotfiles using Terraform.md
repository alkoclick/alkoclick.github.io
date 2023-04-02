Most of the current state-of-the-art in the dotfiles space functions like this:
* Symlink your repo files into host system locations
* Organize your dotfiles into folders that are automagically used
* Watch for changes in the remote, pull & apply automatically

This design works well for most cases, and is simple to even build yourself. However, there were some issues with it that bothered me.


#### The templating problem
Symlinking stuff is good. But what if you wanna template your gitconfig using a user provided email address & name? You need some sort of template syntax, as well as a concept of "variables", that are either local to each device and not tracked in your dotfiles, or tracked in the dotfiles and mapping from a device identifier to these variables.

However, the templating problem is the smallest of the issues.

#### The removal problem
Let's say you have a config file overriding some settings e.g for apt repositories. You no longer need it, so working on computer A you remove it, commit the change to the repository, and push. You pull the changes on another device and check the results. But your override is still there on device B. It was never removed, because after you pull, the file is no longer in the repo so your dotfiles by definition don't know what to remove.

The problem is the workflow proposed above doesn't have a concept of "state", i.e what has been previously done by the repo on this device. This is also why most dotfiles repositories are idempotent - they have to, otherwise they end up redoing the same changes again and again. I'm normally a strong supporter of idempotence in scripts, but in this case, it's an artificial constraint which doesn't even fully solve the problem.

You can get around this problem by
* Manually removing things
* Writing removal/cleanup scripts
* A rudimentary representation of state by saving the last applied commit sha, then git diffing your way into planning a changeset of additions/removals

All 3 solutions are a bad place to be, imo. But the requirements to solve this problem clearly outline some of the things Terraform excels at: Tracking state, calculating and applying changes based on that while offering a strong set of utilities and a templateable language.


### Terraform
Besides the aforementioned, we get some additional bonuses:
* Providers and ecosystem
* Standardized syntax
* Extra practice

#articles 