
These are some guides for restoring files to a [Jellyfin](https://jellyfin.org) installation. I run mine using docker compose, and you can see my setup [here](https://codeberg.org/alkoclick/hypatia/src/branch/main/immich). I take my backups using [Backrest](https://garethgeorge.github.io/backrest/) which is a great UI and control panel for [Restic](https://restic.net). If you'd like to understand the logic behind this you can read more about [My backup strategy](My%20backup%20strategy.md).

For official docs see [here](https://jellyfin.org/docs/general/administration/backup-and-restore/#restore-from-a-built-in-backup).

## Before we begin
For a general idea, my Jellyfin media is around 150 Gb of music, and around 50Gb of videos. My entire jellyfin config folder is around 1.1 Gb. The database backups produced via the UI are sized at around 20 Mb and 900 Mb with and without metadata included respectively.

*Note: In most of my other backup processes, I prefer to use the UI backup modes, as I find them easier and friendlier. In this case even though Jellyfin offers a way to backup via the UI, I chose not to use that and do my entire backup flow using Backrest targeting the data paths. For background on this see the section "Backups from the UI" at the bottom of this article.*

*Note no 2: Jellyfin uses absolute paths on some things like playlist files. Avoid changing paths during the restoration process if you can help it.*

## Restoring the whole DB

* Start by using Backrest to restore the latest usable snapshot to your filesystem
* The restored copy has permissions 700 by default, run a `chmod -R 755 $TARGET` on it
* Move it where the old config used to be (or alongside it, if you're running a test)
* Remember that the Backrest restorations have one extra parent directory, double check that the contents of the folder are what you expect them to be!
* If testing, I like to create a copy of the docker compose in a new folder, change the port mapping and container name and run on that. 
* Ensure that the docker-compose mount for the config directory points to the restored folder, not the original one (if it's even still around)
* Just start up Jellyfin!

## Backups from the UI:
As of 10.11.6 when I am writing this, Jellyfin has no automated backup mechanism. There is a UI page for backups in the admin panel, which allows you to take a snapshot of the DB and potentially include metadata as well.

What is missing:
* A mechanism to automate taking the snapshots on a schedule
* A mechanism to automate pruning older snapshots
* This may have been user error, but my restore tests, even with metadata included did not have the thumbnails and playlists, which I found surprising

I can use API calls to create the backups but will I still need a manual mechanism for pruning. Because of these missing features, it's simpler to just use Backrest hooks to stop it, take a snapshot, then start it back up

As mentioned earlier:
> The database backups produced via the UI are sized at around 20 Mb and 900 Mb with and without metadata included respectively.

In my tests it took:
* 2m to run the restore without metadata
* 3m to run the restore with metadata

You can do this restoration also on a clean install but you need to move the backups under /config/data/backups (and make that folder) as there is no filebrowser.