## Backup Drive Final Config - DRAFT

All archives/backups stored in a common root directory. A single rsync should synchronize any two backups.

1. 2 TB Internal Storage Drive - Hot
2. 2 TB rsync Mirror Internal Storage Drive - Disconnected / Cold
3. 2 TB rsync Mirror External Storage Drive - Stored / Cold
4. Offsite rsync (Amazon S3 or Google Nearline)


## Backup Sources

All data should be stored in sparkleshare repositories.

Make a `backups` sparkleshare repository too.  This can be rotated on ingestion.

1. Windows PC - Store no data here - SparkleShare, git
	- "Received Media" - Shared Drive with Linux (games, media)
		- Should get backed up somehow, maybe a different root though
		- All this media should be non-original, movies, books, games, etc.
2. Mac Laptop - Store no data here - SparkleShare, git
3. Linux PC - Store no data here - Sparkleshare, git
4. Servers - Data stored here usually will be ingested into `backups` or have its own backup protocol.

