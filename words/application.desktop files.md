# application.desktop files
Used in most Linux distros, including Arch, [[Ubuntu]], Mint

They often live in `~/.local/share/applications/`


Example contents:
```
[Desktop Entry]  
Name=Obsidian  
Exec=/usr/local/bin/obsidian %u
Terminal=false  
Type=Application  
Icon=obsidian.png  
StartupWMClass=obsidian  
Comment=Obsidian  
Categories=Office;  
MimeType=text/html;x-scheme-handler/obsidian;
```

The %u thingie is so that [[Obsidian links]]  can be opened I think, based on [this piece](https://forum.obsidian.md/t/obsidian-uri-set-up-for-linux-obsidian-desktop/7494/4)

Note that exec is an absolute path, but icon doesn't specify a path. Icons search in a few preconfigured directories, including `$HOME/.icons`

Useful docs links:
[File spec](https://people.gnome.org/~shaunm/admin-guide/menustructure-6.html)
[Icons spec](https://specifications.freedesktop.org/icon-theme-spec/icon-theme-spec-latest.html)

#ubuntu #linux