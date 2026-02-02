I recently started testing out having an android device as my main compute. If you're interested you can read more about that in [[My android setup]]. [Termux](https://wiki.termux.com/wiki/Main_Page) has been a great help in that! I downloaded it through F-droid, set it up, and soon after found myself wanting to create a basic dotfile repo, which required ssh keys, which required me copying the output into the system clipboard.

I got paste working by using Ctrl-Alt-V, as recommended [here](https://www.reddit.com/r/termux/comments/v23xki/how_to_paste_using_keyboard_shortcuts/). In another post, the author (I think) recommended Ctrl-Y and Ctrl-P which laos sometimes worked for me but were very hit-and-miss. Regardless, we want to copy and paste command output, so we need [this](https://www.reddit.com/r/termux/comments/grcxsd/how_can_i_copy_the_output_of_a_command_directly/): `termux-clipboard-set` and `termux-clipboard-get`. To get those, you need to run:

```shell
pkg install termux-api
```

You then also need to install the actual [Termux-api](https://github.com/termux/termux-api) app, e.g [here in F-droid](https://github.com/termux/termux-api), otherwise your commands will do nothing, which is exactly the problem I run into and figured out thanks to [this response](https://www.reddit.com/r/termux/comments/14932pw/i_recently_installed_termux_but_im_not_able_to/).

That's it! The set command works both with arguments (e.g `termux-clipboard-set blaba`) and with piping (e.g `cat blabla.txt | termux-clipboard-set`). I tend to alias these copy commands, so I added this to my `~/.bashrc`:

```
alias cs=termux-clipboard-set
```

And now I can just use `cat file.txt | cs`