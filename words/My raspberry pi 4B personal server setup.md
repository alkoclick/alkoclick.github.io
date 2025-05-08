
For a few years now I've been running a Raspberry Pi 4B at home. Around the start of 2025 I decided to upgrade my setup with more open source tooling, and also to make my existing stuff a bit more sturdy for when my SD card eventually fails. It's also part of the effort to [DeGooglify my life](DeGooglify%20my%20life.md). This is where I am now.

## Hardware
* Raspberry Pi 4B (arm64 architecture), 4 CPUs, 4Gs RAM
* SD card for the OS
* SSD using SATA+power cable

## Software
You can find the whole config here: 
https://github.com/alkoclick/personal-server

I use Jellyfin as my media server for books, music, videos and radio.

I use Paperless-ngx for document storage and management. 

I use Syncthing to mirror my music library to my phone for offline listening, and my documents to my desktop as a lightweight backup solution.

I use Glances as a fancy web UI 'top' alternative for monitoring.

I tried Calibre for my books, but it turned out to be a tad too heavy for my poor server.

I use qBitTorrent to access movies and music. It's using a shared volume with Jellyfin so that downloaded stuff becomes available near-instantly. 

I use dashy as a dashboarding solution with pretty colours and easy links to my stuff.

I use dozzle to check logs for any of my containers, and a quick overview of memory usage.

I use Tailscale to enable access to all of these remotely. I run one pod per service (sidecar pattern)

Stuff I run into while setting this up:
* [Fix for no memory info in docker](Fix%20for%20no%20memory%20info%20in%20docker.md)
* [Impressions on Linux torrenting clients](Impressions%20on%20Linux%20torrenting%20clients.md)

