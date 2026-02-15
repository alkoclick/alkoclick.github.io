These are some guides for restoring files to a [Paperless](https://docs.paperless-ngx.com) installation. I run mine using docker compose, and you can see my setup [here](https://codeberg.org/alkoclick/hypatia/src/branch/main/paperless). I take my backups using [Backrest](https://garethgeorge.github.io/backrest/) which is a great UI and control panel for [Restic](https://restic.net). If you'd like to understand the logic behind this you can read more about [My backup strategy](My%20backup%20strategy.md).

#### Restoring a single file
* Keep in mind that the backrest restore restores a folder containing whatever you have chosen to restore, not the structure directly!
* The restored object has root owner, due to backrest, needs `sudo chown -R $USER:$USER target`
* Remember that there's an entry both in `documents/originals` and in `documents/archive` for the file!
* The path of least resistance is probably to actually download the file to device from a snapshot and reupload it via paperless, unless it had useful metadata or sth


#### Restoring a whole install
* You have to individually restore the paperless-media and paperless-data folders from backup
* As in the single file examples, the restored folders have root as their owner so you need to  `sudo chown -R $USER:$USER target`
* If you are testing:
	* Place both folders in a new directory (e.g paperless-restore-test)
	* Copy over your docker compose in there, and any env files you use (paperless.env for me)
	* Modify your docker compose to:
		* modify the compose file name, e.g pap-restore
		* remove unecessary containers (e.g tailscale or syncthing)
		* point the mounted volumes to your restored ones
		* update the exposed ports to new ones to avoid conflicting with your existing install
	* Start up your installation (`docker compose up --detach`)
	* Check if the logs are okay `docker logs -f pap-restore-paperless-webserver-1`
	* Test logging in via the port you've specified to expose
	* Your docs should be good!
* If you are doing this for real
	* Ensure that the main paperless instance is stopped, as well as any sync processes (e.g syncthing) by running `docker compose down`
	* Move the old folders, if they exist, out of the way (e.g `mv paperless_media paperless_media.bak`)
	* Copy the restored folders into the location your install expects (e.g `cp paperless_media_restored paperless_media`)
	* Remember again, you need both paperless_media and paperless_data!
	* Start up your install normally (`docker compose up --detach`)
	* You should be good!