# Backup Management with S3 Glacier

The most economical bulk offsite storage for a few terabytes of data in 2022 is `AWS S3 Glacier Flexible Retrieval` with bulk data retrieval. The bulk retrieval parameter must be specified during data restore and will take up to 12 hours for retrieval.

Note: Glacier deep archive could be 10x more economical but carries risks. `Bulk` restore costs are 0.025 per 1000 objects and 0.0025 per GB.

Future: Model glacier deep archive costs. 10x cheaper is huge. If objects can be reduced by using zip, then this would only cost about $2.50 per terabyte.


## How to set up a bucket with glacier

TODO, did this manually in the past, write a terraform module.



## How to restore all objects in a bucket

There is no recursive restore option. Restore must be implemented.

The following implementation was tested separately but not as a single script as below. Parallelism can probably be increased, consider logging object name each attempt to stdout as well

The flag `--restore-priority=bulk` was also not tested but will save cost so has been added.

```
#!/bin/bash

set +ex

# Execute this script and capture errors to a file, then grep the file for error types
# ./restore-glacier-object-list.sh > restore-results-my-bucket.txt 2>&1

BUCKETNAME="my-bucket"

# grep this file for NoSuchKey or other errors
FILENAME="glacier-restore-$BUCKETNAME.txt"

# read all the glacier object paths and store them in a file, one line per object
aws s3api list-objects-v2 --bucket $BUCKETNAME --query "Contents[?StorageClass=='GLACIER']" --output text | awk 'BEGIN {FS="\t"}; {print $2}' > $FILENAME

# consume the file, this parallelism cap is defensive to avoid too many concurrent requests to aws, consider much more, perhaps 10x as many if your machine will support it.
parallel -j 30 -q -a $FILENAME aws s3api restore-object --restore-request Days=7 --restore-priority=bulk --bucket "$BUCKETNAME" --key "{}"
```

## How to download a restored object

After 12 hours, all objects are guaranteed (by AWS) restored. This is for "bulk" retrieval, as depicted above.

The flag `--force-glacier-transfer` must be used to download objects with aws cli.


### Verify files or add new files to the bucket: `s3 sync` with the existing bucket

These 2 operations will verify the `size` and `timestamp` parameters match.

*WARNING: Sync is destructive for the destination if the timestamp is older or the size is incorrect.*

Format below is <source> <destination>.

Below, we first sync to the bucket, then we sync from the bucket. This considers any local change should overwrite or update new objects to the bucket, then the second command downloads objects that are in the bucket that don't exist locally.

- `cd my-bucket; aws s3 sync --force-glacier-transfer . s3://my-bucket`
- `cd my-bucket; aws s3 sync --force-glacier-transfer s3://my-bucket .`

Note: You may wish to use the flag `--size-only` if files repeatedly transfer. There is a documented bug in some related to filenames with special characters causing files to resync, and timestamps are typically not relevant if size is the same size for backups and backups flow into the backup space from user space, although not universally true, especially if you have multiple user spaces flowing into a backup that need reconciled.
  
  
## Sync new files to the bucket without considering glacier objects

Typically archive updates are additive, so we don't want to affect what's already in the archive. It saves time and prevents errors to avoid enumerating what was changed, so `aws s3 sync` is preferred. This 
  
- `cd my-bucket; aws s3 sync . s3://my-bucket --size-only`
  - `--size-only` is optional, it excludes date comparison. This helps avoid accidental updates if your local files have a date change without content change
  

### Deleting from a bucket with sync

NOT RECOMMENDED for operating on buckets that contain source of truth (only use for cache buckets).

Consider deleting the individual objects using `s3 rm` instead of trying to delete with sync.

Deleting with sync is very dangerous because it removes any files in <destination> that are not in <source>.

1. before removing the files from local, sync from the bucket to local. Otherwise files added to the bucket from somewhere else would be deleted, since they aren't yet in local.
2. remove the desired files from local
3. run another s3 sync with the `--delete` flag. WARNING, this could delete any remote file not on your local. Not advised for backup operations.

