# Tricking Homebrew to avoid installing a dependency
### Tricking [[Homebrew]] to avoid installing a dependency
[[2021-12-11]]

![](https://cdn-images-1.medium.com/max/800/0*ZbKd2-BKD5Okj2Jp)

“Cellar” Photo by [Matt Twyman](https://unsplash.com/@mgtwyman?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

tl;dr:

`mkdir -p $HOMEBREW_CELLAR/gcc/11.2.0_3/bin`

### Background

I’m currently building a container as a portable dev environment for my [[Dotfiles]], and one of the things I installed was [[Terraform]], via Homebrew.

I quickly noticed my [[Docker]] build times and sizes had immediately skyrocketed by almost 1Gb. Terraform takes about 60Mb, what’s going on?

Well, Terraform in Homebrew in Linux [depends on gcc](https://github.com/Homebrew/homebrew-core/blob/master/Formula/terraform.rb#L25).

This is pretty annoying because the download in 350Mb and the unpacked size >500Mb, and also [gcc takes a decade to actually build](https://stackoverflow.com/questions/24966404/brew-install-gcc-too-time-consuming).

Even worse, we actually already have THE EXACT SAME VERSION of gcc in the container.

Installing without dependencies is next to impossible in Homebrew, because the cli arg for it is actually a no-op since early 2021.

So, to skip installing gcc, we need to trick Homebrew into thinking it’s installed. Turns out that the main check Homebrew does for deps is just the bin folder existence for the version it wanted to install. I haven’t been able to verify if it also checks for the presence of the binary in your path as well, but I assume you already have it there, that’s the entire reason we’re doing this :)

### Applying this strategy to arbitrary dependencies that you’ve already installed outside Homebrew

```
brew info PKG_TO_INSTALL # Note the dependencies it wants  
brew install DEPENDENCY # Install the dependency once to study it  
ls -la $HOMEBREW_CELLAR/DEPENDENCY #Note the version installed  
brew uninstall DEPENDENCY # No longer needed  
mkdir -p $HOMEBREW_CELLAR/DEPENDENCY/VERSION/bin

brew info PKG_TO_INSTALL # It should now appear green!
```