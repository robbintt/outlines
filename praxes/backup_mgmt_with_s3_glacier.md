# Backup Management with S3 Glacier

The most economical bulk offsite storage for a few terabytes of data in 2022 is `AWS S3 Glacier Flexible Retrieval` with bulk data retrieval. The bulk retrieval parameter must be specified during data restore and will take up to 12 hours for retrieval.

Note: Glacier deep archive could be 10x more economical but carries risks. `Bulk` restore costs are 0.025 per 1000 objects and 0.0025 per GB.

Future: Model glacier deep archive costs. 10x cheaper is huge. If objects can be reduced by using zip, then this would only cost about $2.50 per terabyte.

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
