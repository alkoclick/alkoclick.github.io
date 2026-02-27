I try to follow a [3-2-1 principle](https://www.backblaze.com/blog/the-3-2-1-backup-strategy/):
* 3 backups
* in at least 2 devices
* 1 of which is off-site (a different location)

## Backrest
[Backrest](https://garethgeorge.github.io/backrest/) is at the heart of my backup strategies as it is the backup service itself. Besides its simple and powerful UI, it has support for hooks to run before and after snapshots, which is extremely useful. I've given it access to the docker socket, so it can stop a container before taking a snapshot and resume it afterwards. Other than the configurations for the plans and repositories, it also holds the encryption key for the fails, without which backups are unrecoverable. Additionally, it lives in the same drive as many of the apps above, meaning it would be exposed to many of the same risks. For this reason, I back up the Json config to a password manager, as [they themselves recommend](https://garethgeorge.github.io/backrest/introduction/getting-started).

## Paperless
You may also wanna check out my [Paperless backup restoration guide](Paperless%20backup%20restoration%20guide.md).
#### Documents
* Syncthing to desktop
* Backrest to store encrypted in my local S3 (garage, Cal), every 4 hours
#### Database
* Backrest to store encrypted in my local S3 (garage, Cal), every 4 hours. Includes a backrest hook to stop the container before the startup and start it again after.

## Immich
I have also collected the details of working with Immich backups in this [Immich backup restoration guide](Immich%20backup%20restoration%20guide.md).
#### Media
* Backrest nightly backups
* Syncthing to my desktop (should probably get removed)
* Not a full backup, but the majority of pictures are taken with my phone and stay there for ~60 days
#### Database
* Every 6 hours via immich cron, included in the backrest backups 

## Jellyfin
Annoyingly, Jellyfin does not provide a way to automatically take DB backups on schedule yet. My workflow is thus based on stopping the container using a backrest hook, taking a snapshot of the config directory and starting it back up. 
You may also want to read the [Jellyfin backup restoration guide](Jellyfin%20backup%20restoration%20guide.md).

#### Music
* Syncthing to my Nothing phone
* Backrest to store encrypted in my local S3 (garage, Meg)
#### Videos
My movie collection rotates often, so it is not backed up. I do however keep my own creations in a separate folder where they are backed up in my local S3 (garage, S3)
#### Books

#### Database/Config
* Backrest nightly backup. Includes a backrest hook to stop the container before the startup and start it again after.

## Torrents
I haven't yet decided if I want to back this up or not
