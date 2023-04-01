# Shell Scripts
## CLI tools list
https://dev.to/lissy93/cli-tools-you-cant-live-without-57f6

## Check OS

Fetched from: https://github.com/billdeitrick/dotfiles/blob/master/scripts/symlink.fish
```sh
switch (uname)
    case Darwin
        set DOTFILE_SYMLINK_ROOT ~/Documents/dev/dotfiles
    case Linux
        set DOTFILE_SYMLINK_ROOT "/mnt/c/Users/$LOGNAME/dev/dotfiles"

        # WSL detection inspired by https://stackoverflow.com/questions/38086185/how-to-check-if-a-program-is-run-in-bash-on-ubuntu-on-windows-and-not-just-plain
        if grep -qE "(Microsoft|WSL)" /proc/version
            set IS_SYMLINK_WSL 1
        else
            set IS_SYMLINK_WSL 0
        end
    case '*'
        echo "MY FISH DOESN'T KNOW THESE WATERS!"
        exit 1

end
```

## GNU Sed (Ubuntu) to find and replace with newlines

```sh
sed -i "s/ q /\nq /g" "VanMoof x EthicalOs.md"
```

## BSD Sed (mac) to insert  content at first line
```shell
sed -i '' '1i\

# Title
  

' 'filename.md'
```

## Random string of length 30
```shell
cat /dev/urandom | base64 | head -c 30
```

or in a mode that allows you to both see and pipe this:
```bash
`EMAIL=_____@vanmoof.com && PASS=$(cat /dev/urandom | base64 | head -c 30) && echo $PASS && aws iam create-login-profile --password-reset-required --user-name $EMAIL --password $PASS`
```


## Command exists
```sh
if ! command -v lazygit &> /dev/null
then
	sudo eget -q --tag v0.31.3 --to=/usr/local/bin/ jesseduffield/lazygit --verify-sha256=78eff8d126178594a06107c8faff7f27343f4e63281d14fbbc62f6fbb38e5110
fi
```


## File exists
```sh
if test -f "~/.ssh/id_rsa.pub"; then
  echo "Exists"
fi
```