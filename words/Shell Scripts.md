## CLI tools list
[https://dev.to/lissy93/cli-tools-you-cant-live-without-57f6](https://dev.to/lissy93/cli-tools-you-cant-live-without-57f6)

## Shebang

```
#!/usr/bin/env bash
```

## Check OS

Fetched from: [https://github.com/billdeitrick/dotfiles/blob/master/scripts/symlink.fish](https://github.com/billdeitrick/dotfiles/blob/master/scripts/symlink.fish)
```sh
switch (uname)
    case Darwin
        set DOTFILE_SYMLINK_ROOT ~/Documents/dev/dotfiles
    case Linux
        set DOTFILE_SYMLINK_ROOT "/mnt/c/Users/$LOGNAME/dev/dotfiles"

        # WSL detection inspired by [https://stackoverflow.com/questions/38086185/how-to-check-if-a-program-is-run-in-bash-on-ubuntu-on-windows-and-not-just-plain](https://stackoverflow.com/questions/38086185/how-to-check-if-a-program-is-run-in-bash-on-ubuntu-on-windows-and-not-just-plain)
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

## Make all links in the markdown style
```shell
fd -e "md" -x sed -i "" -E "s/(^| )(https?:[^ ]+)/\1[\2](\2)/g" {}
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

## Mass rename files
```shell
 find . -type f | sed -n 's/\(\(.*\)yt1s.com - \(.*\)\)/mv "\1" "\2\3"/p' | tee | bash
```

## Curl with timing

First echo this into a file named curl-format.txt
```
     time_namelookup:  %{time_namelookup}s\n
        time_connect:  %{time_connect}s\n
     time_appconnect:  %{time_appconnect}s\n
    time_pretransfer:  %{time_pretransfer}s\n
       time_redirect:  %{time_redirect}s\n
  time_starttransfer:  %{time_starttransfer}s\n
                     ----------\n
          time_total:  %{time_total}s\n

```

Then:
```sh
curl --user-agent "tester-alex-papa-miro" -w "@curl-format.txt" -X GET --location -s -k -I "TARGET"
```

## AWS IP lookup function
```shell 
aws_lookup_ip() {
  if [ $# -lt 1 ]
  then
    echo "Usage: $funcstack[1] <IP or list of IPs separated by commas>"
    return
  fi

  QUERY_FMT="NetworkInterfaces[*].{ Type: InterfaceType, Description: Description, AZ: AvailabilityZone, PublicIP: Association.PublicIp, PrivateIP: PrivateIpAddress}"
  aws ec2 describe-network-interfaces --output table --query $QUERY_FMT --max-items 500 --filters "Name=addresses.private-ip-address,Values=$1"
  aws ec2 describe-network-interfaces --output table --query $QUERY_FMT --max-items 500 --filters "Name=association.public-ip,Values=$1"
}
```

## Convert a bunch of 4k vids to lower res single threaded
```
fdfind --threads 1 --exec ffmpeg -i {/} -map_metadata 0 -vf scale=1920:1080 -c:a copy {/.}_1080.mp4
```


## SSH keygen
Originally fetched from: https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent
```shell
ssh-keygen -t ed25519 -C "your_email@example.com"
```

## Dropship ssh key into authorized_keys

```
cat ~/.ssh/id_ed25519.pub | ssh USER@HOST "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys && chmod 600 ~/.ssh/authorized_keys"
```

shorter form if you're sure that authorized_keys exists and has correct permissions:
```
cat ~/.ssh/id_ed25519.pub | ssh USER@HOST "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"
```