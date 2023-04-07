If you're not familiar with them, dotfiles are generally customization files for things you use, e.g .gitconfig or .bashrc. You can read a much, much better introduction in [this ArchWiki page](https://wiki.archlinux.org/title/Dotfiles). Extract from it:

> User-specific application configuration is traditionally stored in so called [dotfiles](https://en.wikipedia.org/wiki/dotfile "wikipedia:dotfile") (files whose filename starts with a dot). It is common practice to track dotfiles with a [version control system](https://wiki.archlinux.org/title/Version_control_system "Version control system") such as [Git](https://wiki.archlinux.org/title/Git "Git") to keep track of changes and synchronize dotfiles across various hosts.

You can find my dotfiles [here](https://github.com/alkoclick/dotfiles). My dotfiles repo run on Terraform! You can read more about [dotfiles using Terraform here](Dotfiles%20using%20Terraform.md).

## Cool things my dotfiles repo does

Here's a quick list of the various things going on in my repository.
See anything you like! Feel free to copy it, or reach out to talk about it.
You can find my contact info on [my about page](https://alkoclick.space/about)

## Package management

After a lot of thought & research I've settled with the following 2 package managers: Apt & Homebrew.
This repository thus manages all non-system packages for those tools as code. It looks like this:

```terraform
  brew_packages = [
    "aws-vault",
    "fzf",
    "gitleaks",
    "httpie",
    ...
```

#### Installing programs

Besides packages for those managers, the repo also does some installations of tooling that is either 
outside those managers, or is required to make them work, such as: 

* Obsidian
* Brave
* 1Password CLI
* Homebrew

## GPG + SSH key generation

The repo generates an SSH key pair and a GPG key. In this way, it makes the assumption 
that you will be using 1 pair per machine, not per user. 

The keys are then uploaded into Github and the GPG key is injected in the local gitconfig. 
They'd uploaded be on Gitlab as well, but the provider doesn't natively support it.

## Configuration files

Speaking of gitconfig, the repo supports both the traditional approach of copying configuration files, as well as a more powerful templating functionality. 

In the former case, we just copy things like:
* .bashrc
* starship.toml

In the latter case, we can reuse the output of other modules and e.g inject the user's email into the gitconfig. 

## Configuration as code

Thanks to the shell provider we can actually as-code pretty much anything, including the desktop environment!
Some of the shiniest examples are system settings that are commonly configured by scripting

Examples include: 
* dconf
* gsettings

## Self-containerize

The entire repo actually packs itself into a neat container, so you can have a working environment on-the-go, e.g for debugging Kubernetes clusters or running online IDEs. This builds on every push.

The container has some functionalities removed, such as dconf/gsettings (it doesn't have an interface) and key pairs (it's temporary).

## Parameterizing

Some values, like user email and name are customizable via Terraform variables.
This allows for e.g separation between work and personal emails.

