I've made this note because I keep forgetting what the utility is called :/

Not very complex tbh, just run `pg_dump` (should be installed alongside psql in most distros)

E.g `pg_dump -f archive.sql`

To [restore](https://www.postgresql.org/docs/current/backup-dump.html#BACKUP-DUMP-RESTORE)
`psql -X dbname < archive.sql` (consider enabling `--set ON_ERROR_STOP=on`)