I run into this issue when upgrading my [My raspberry pi 4B personal server setup](My%20raspberry%20pi%204B%20personal%20server%20setup.md) from Debian 11 bullseye to Debian 12 Bookworm.

The solution was found [here](https://forums.raspberrypi.com/viewtopic.php?t=365941). In short:

```
sudo umount /boot 
sudo sed -i "s:/boot:/boot/firmware:" /etc/fstab 
sudo mkdir /boot/firmware 
sudo mount /boot/firmware
```

The cause was that the mount location has been updated and if you are upgrading (which Raspberry heavily dis-recommends btw) then it'll end up in the wrong location.