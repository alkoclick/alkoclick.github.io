Git-based package manager, built on Ruby. Originally built for Mac, Homebrew also runs on Linux. The port used to be called Linuxbrew but is now named just Homebrew as well.

There are some interesting GH issues where the impact of Homebrew on Github servers is analyzed. It is brought up that as many as 10 dedicated servers are needed just to keep up with Homebrew's traffic! One of the interesting observations in that thread is also that deep git clones are actually less costly than shallow clones.

Homebrew packages available on the "main" repository need to be manually approved, and are added using git commits to a repo. Individual sources called "taps" are also available. There are also "casks", precompiled artifacts for specific Mac versions (which is only possible thanks to the fact that the Mac-universe has relatively few hardware configurations).

I use Homebrew because it has a good list of DevOps-related packages and it moves faster than the APT repos (which are super stable, but often many versions behind).