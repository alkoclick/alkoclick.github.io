# Stuck on initramfs
This can happen due to corrupt partitions on your drive

Your best bet to actually see the error is to start by trying `exit`

This will probably tell you to manually `fsck` some partition. In my case in my [[Lenovo Thinkbook s13]] I needed to run `fsck /dev/vgubuntu-root`