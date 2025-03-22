This file needs to be modified if you want memory stats  (and mem limits) in your containers : `_/etc/default/grub_` if you're on Debian, or `/boot/cmdline.txt` if you're on Raspberry pi
  
Test it with `docker info`, if you see  
```  
WARNING: No memory limit support  
WARNING: No swap limit support  
```  
then you need to modify the file.  
  
References:  
* https://web.archive.org/web/20170625185736/https://awhitehatter.me/debian-jessie-wdocker/  
* https://stackoverflow.com/questions/45541242/docker-stats-shows-zero-memory-usage-even-for-running-containers