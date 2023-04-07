I orchestrate my [**dotfiles**](https://github.com/alkoclick/dotfiles) repo using Terraform. This article describes why I made this decision, and why I rejected alternatives.


## Dotfiles 101
First of all, if you haven't read about dotfiles, you can read my article [here](dotfiles). Most of the current state-of-the-art solutions in the dotfiles space function like this:
1. Symlink your repo files into host system locations
2. Organize your dotfiles into folders that are automagically used
3. Watch for changes in the remote, pull & apply automatically

This design works well for most cases, and is simple to even build yourself. However, there were some issues with it that bothered me.


## The templating problem
Symlinking stuff is a good start. But what if you wanna template your gitconfig using a user provided email address & name? You need some sort of template syntax, as well as a concept of "variables", that are either local to each device and not tracked in your dotfiles, or tracked in the dotfiles and mapping from a device identifier to these variables.

However, the templating problem is not the only issue.


## The removal problem
There is a fundamental problem with most solutions, and it's visible when you remove a thing. Let's say you have a config file overriding some settings e.g for apt repositories. You no longer need it, so working on computer A you remove it, commit the change to the repository, and push. You pull the changes on another device and check the results. But your override is still there on device B. It was never removed, because after you pull, the file is no longer in the repo so your dotfiles by definition don't know what to remove.

The problem with the workflow above lies in the absence of some "state", i.e what has been previously done by the repo on this device. This is also why most dotfiles repositories are idempotent - they have to, otherwise they end up redoing the same changes again and again. I'm normally a strong supporter of idempotence in scripts, but in this case, it's an artificial constraint which doesn't even fully solve the underlying problem. The problem is reapplying the same changes. Idempotence is a crutch so that reapplying the same changes doesn't hurt so much.

You can get around this problem by
* Manually removing things
* Writing removal/cleanup scripts
* Creating a rudimentary representation of state by saving the last applied commit sha, then git diffing your way into planning a changeset of additions/removals

All 3 solutions are a bad place to be, in my opinion. 


### Terraform
The requirements to solve this problem clearly outline the need for some of the things in which Terraform excels:
* tracking state
* calculating and applying changes based on a state 
* offering a strong set of utility functions
* templating blocks 

Besides the aforementioned, we also get the following additional bonuses:
* Providers and ecosystem
* Standardized syntax
* Extra practice (if you're an SRE)


### Conclusions
This is a solution that works well for me. I have consciously not included a "when not to use Terraform for dotfiles" paragraph. This is because if the problems narrated above don't affect you, then, by all means, please keep doing what you're doing! Terraform is not a silver bullet for all problems. But if you are like me and want a more advanced setup out of your dotfiles, it can be pretty effective. That's all for now, and stay curious!


#articles 