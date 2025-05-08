While setting up [My raspberry pi 4B personal server setup](alkoclick/words/My%20raspberry%20pi%204B%20personal%20server%20setup.md), I wanted to set up a torrent client to have an easy upload pathway into my Jellyfin library. Jellyfin doesn't provide any easy "upload" plugin, and rather than download externally and copy stuff over, I wanted to be able to upload directly.

I was aware that I should be avoiding μTorrent, and that they have a fairly bad reputation. 

I initially tried to work with Transmission, which seems to be the default Ubuntu client. While it was okay (the UI is archaic, but hey, minimalism), I run into the issue where it would completely hog my CPU and even caused my RPI to end up unresponsive 3-4 times within the 24 hours I was running it for. It also seemed unable to run in "passive mode" which required me to set up port-forwarding on my LAN, which is always a pretty bad feeling. Even with all of these things in place it'd sometimes fail to access its own parts (some kind of permissions issue?) leading it to download (and throw away) gigabytes in its failed quest to complete some stuck downloads. 

After reading some threads of people who had similar issues, I took a look on Deluge and qBittorrent. qBitttorrent seemed in a better shape, so I went for that.

I grabbed the docker image from the [Linuxserver folks](https://hub.docker.com/r/linuxserver/qbittorrent/) in Dockerhub, adapted the UID and GID because I'm mounting volumes shared to my Jellyfin, and got to work - it worked quite nicely.