Tested on [[Ubuntu]]

`sudo apt-get install libpam-u2f`

`mkdir -p ~/.config/Yubico`
(You can also set this up on /etc apparently, that may be safer)

`pamu2fcfg > ~/.config/Yubico/u2f_keys`

`m /etc/pam.d/sudo`

The following setup will allow using Yubikeys for sudo when available, otherwise fall back to password

```
session    required   pam_env.so readenv=1 user_readenv=0
session    required   pam_env.so readenv=1 envfile=/etc/default/locale user_readenv=0
auth       sufficient pam_u2f.so
@include common-auth
@include common-account
@include common-session-noninteractive
```

The trick is to use `sufficient`, which means that when available, YubiKey auth is good enough for sudo. It also has to go before the common-auth, otherwise password will always be required.