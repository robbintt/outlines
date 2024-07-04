# Image Shrinking for ext4

Original use case: I have a debian sid image from a 256 gb ext4 lvm volume.  It contains 18 GB of data. I want it to be 18 GB, and then I want to compress it and store it in archive.

This image will only be used if my debian sid image is borked.

I would like to quickly reproduce the process in the future.



## Getting the image

Background: The debian volume does not contain /home or other "user data" directories. It is also intended that flatpaks, docker images, and snaps should not be in the debian volume.

### Current method to get the image file

1. boot debian recovery usb
2. dd the debian lvm volume directly to an image on a data partition
3. It will be 256GB since that is the size of the drive. Mostly not used.

### Future method to get the image

Test this out when there is a good opportunity. Maybe read up as well, and ideally validate (probably not, since the consequences are just reinstall debian sid)

1. Can we remount the filesystem read-only while in the live filesystem? I think so.
2. use dd on the filesystem while it is read-only.

## Resizing the image

After you have the file, you can boot back into debian.

1. e2fsck, resize2fs -M /dev/loop0 - shrink the partition to the minimum possible size within the file (filesize does not change)
    - reference these commands where needed
2. calculate bytes from the blocksize * blocks, get it right or you lose data...
    - this is in the resize2fs data
3. truncate -s SIZE filename.img
4. reattach to loop0 and e2fsck
    - reference these commands where needed


## Compressing the image

use zstd -9. 9 is the top standard speed compression level. This compressed a truncated image from 18 GB to 6.4 GB.
