I try to follow a [3-2-1 principle](https://www.backblaze.com/blog/the-3-2-1-backup-strategy/):
* 3 backups
* in at least 2 devices
* 1 of which is off-site (a different location)

I also place more importance on raw "source data" than the databases and metadata that tools build around them. So I'd much rather make sure that my music catalogue is preserved well, than my Jellyfin installation as a whole. But ideally you'd like both to be recoverable.

## Paperless
You may also wanna check out my [Paperless backup  restoration guide](Paperless%20backup%20%20restoration%20guide.md).
#### Documents
* Syncthing to desktop
* Backrest to store encrypted in my local S3 (garage), every 4 hours
#### Database
* Backrest to store encrypted in my local S3 (garage), every 4 hours

## Immich
#### Media

#### Database


## Jellyfin

#### Music
Syncthing to my Nothing phone
#### Videos
Not backed up (except perhaps my own work)
#### Books

#### Database


## Torrents


## Backrest
Backrest is the backup service itself. Besides the configurations for the plans and repositories, it also holds the encryption key for the fails, without which backups are unrecoverable. Additionally, it lives in the same drive as many of the apps above, meaning it would be exposed to many of the same risks. For this reason, I back up the Json config to a password manager, as [they themselves recommend](https://garethgeorge.github.io/backrest/introduction/getting-started).