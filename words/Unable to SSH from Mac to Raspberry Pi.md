I run into this issue in April 2025. It seems to have started either with a MacOs update, or when I switched routers.

This is also the subject and answer in [[this StackExchange question]()](https://unix.stackexchange.com/questions/792280/cannot-ssh-from-mac-os-laptop-to-one-host-but-works-for-all-others).

I tried different SSH clients to no avail. The connection only failed from my Mac to a Raspberry Pi, and worked from and to anything else.

After a lot of digging, I ended up solving it with:
```
ssh -o 'IPQoS=none' your_user@your_target_ip
```

You can make this fix permanent by adding it to your ~/.ssh/config file:

```
host your_target_ip
    ipqos none
```

I wish I could contextualize the answer with why it solved the problem, but I have no idea. :/