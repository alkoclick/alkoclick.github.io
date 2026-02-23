These are some guides for restoring files to an [Immich](https://immich.app) installation. I run mine using docker compose, and you can see my setup [here](https://codeberg.org/alkoclick/hypatia/src/branch/main/immich). I take my backups using [Backrest](https://garethgeorge.github.io/backrest/) which is a great UI and control panel for [Restic](https://restic.net). If you'd like to understand the logic behind this you can read more about [My backup strategy](My%20backup%20strategy.md).

Relevant official docs: https://docs.immich.app/administration/backup-and-restore/#database

## Before we begin
For a general idea, my immich install has about 140 Gb of media, the database backups are around 200Mb, it takes about a minute to create a backup and 2 minutes to restore one.

One important note: Immich caches stuff in your browser a lot! This can mess up your tests if you plan on deleting and recreating stuff, use incognito tabs and new sessions to avoid hitting this!
#### Preparation: Making your life easy
Okay, let's say you wanna bring back something you destroyed accidentally. To do that, first you need to figure out what its filename was, and where it was stored. If you're on default settings (no storage template) this is basically undoable, because your assets are all in paths like
`/IMMICH_BASE/upload/07/42/filename.extension` which is a hashed path and impossible to unwind.

So first you need to activate [the storage engine](https://docs.immich.app/administration/storage-template). Do that, generate some backups over the next few days, and then we talk again. I use this template `{{y}}/{{MM}}/{{dd}}/{{filename}}`

## Restoring a single file - deleted from filesystem
Great, so let's take it from the top again, shall we?
Let's say you want to bring back something you destroyed accidentally. We assume you know when this picture or video was taken, at least roughly. We also assume you deleted this file using the filesystem, not the immich UI (so the immich DB maintains the rows for the file). You can find out more info about the image, including its filename and metadata by selecting it in the Immich UI. Notably, the image thumbnail will load there, unless it has been deleted as well, as thumbnails are stored in a separate location (`/thumbs` in the immich storage directory). 

1. Go to the backrest UI
2. Browse the snapshots for the file
3. Select the file/folder you want to restore and "restore to location"
4. The default location provided is `$FOLDER-backrest-restore-$RANDOMHASH`. I usually prefer to remove the random hash (unless I'm doing multiple restoration attempts). It's practical to keep the suffix though so you can clearly differentiate when you're doing shell work in the next steps
5. CD to the restored folder's parent
6. The restoration will probably have messed up permissions, and it belongs to the backrest user (for me root), so you may need `sudo chown -R $USER:USER $FOLDER-backrest-restore` and `chmod 755 $FOLDER-backrest-restore`. Immich has 644 on its files. You can tighten the permissions further, but that's what immich runs on my install.
7. If you are restoring a whole folder, then you simply `sudo mv $FOLDER-backrest-restore/$FOLDER $FOLDER`. If you are restoring a file, just use the relevant subpaths of that!
8. You are now done!

## Restoring a single file deleted from Immich
I'm gonna assume that you can't just find it in the Immich trash can, which is a thing you should check out btw, as that's where deleted files go by default.

Honestly, the easiest way is to grab it from the backrest snapshot browser, download it, then reupload it. If however there is some other property you are trying to restore (e.g it might have been in a bunch of collections or something), then you need to restore the database. See below for that one.

#### Restoring the whole Immich database
Let's say you got into serious trouble with an upgrade, or did an accental major oopsie. How do you restore the whole DB? As a reminder, the DB is separate to the actual media - restoring it will bring back the references to your files, but not the files themselves! For restoring files, see above.

First of all, if you are doing this as an exercise, here's how to [trigger a backup manually](https://docs.immich.app/administration/backup-and-restore/#creating-a-backup). 

Restoring a whole DB backup is surprisingly easy as in the later versions of Jellyfin (2.5.0 onwards) they have added a UI for it! You can [read the instructions here](https://docs.immich.app/administration/backup-and-restore/#restore-from-settings). Basically just go to the "Maintenance" section of the UI and choose a backup to restore. For me, the whole restoration process took all of two minutes.

After the restoration, the server will restart. Existing websocket sessions will be rereestablished. If you have any files you need to restore as well, now is the time.