# Cheap Raid Server


## Working Free Space

When your storage is 80% full, consider it full due to difficulty shuffling data. So add a 80% multiplier on any storage requirements and get a 30% overhead for required stuff.

- ref: https://jrs-s.net/2016/11/08/depressing-storage-calculator/

## What is the base cost of a software RAID server

### Hardware or software raid?

According to this reddit post, hardware raid is incredibly out of date.


## Raid Configurations Available today

According to the below, only btrfs RAID10 is stable. This has great redundancy except 2 adjacent disk stripes during failure, so there is stripe single redundancy...


## Used Hard Drives

- LTT on why these drives are out there today (2022): https://www.youtube.com/watch?v=xQMQW4sbXf8
  - crypto mining aka "chia mining", these drives are "barely used", just written once...
  - they had 2300-2600 hours of poweron time... that's only 100 days?
    - expected lifetime 50k-60k, manufacturer says 45k hours is the reliability standard
    - linus recommends 20k to 25k hours as the safe ceiling
  - This video shows a lot of drive metrics (SMART attrs) that can predict drive failure up to 70% of the time
  - Video also shows how to determine the drive was used for mining (1 write, low reads, lots of poweron hours)
  - WD drives didn't record reads and writes...
  - DIY NAS best deal was 80gb per dollar, seagate was the cheapest brand on ebay and had reads/writes.
  - However, the 18TB shucked drives are only $170 (provided they are not SMR), which are the same price...
    - Linux recommends used, i guess to save on electronic waste?


## Shingled Drives / SMR

Do not use random consumer drives for RAID arrays... ;(

- Check out the SMR section here for understanding what drives don't use it lately: https://www.reddit.com/r/DataHoarder/wiki/hardware

The exact easystore shucked drive, post 2019 WD Red drives, are shingled/SMR.

According to this thread, that is not true for larger drives, they converge on helium filled: https://www.reddit.com/r/DataHoarder/comments/wlingk/should_i_buy_cmr_or_smr/

However, shucking can require power pin reroute, which I don't want to mess with.

> For occasional backups and cold storage, SMR is perfectly fine. In my experience, WD SMR is implemented much better than Seagate. But for WD 8-20TB are all CMR. Seagate 10-20TB are CMR.

- ref: https://raid.wiki.kernel.org/index.php/Linux_Raid
- ref 2: https://raid.wiki.kernel.org/index.php/Timeout_Mismatch

> In 2019, a new technology called shingled magnetic recording (SMR) started becoming mainstream. Whereas drive usage limits on conventional drives are advisory, burst limits especially on SMR drives are mandatory, and interfere with raid operation. While all manufacturers have been quietly introducing SMR on their desktop lines, WD unfortunately also introduced it on their "suitable for NAS/RAID" WD Red drives. Unfortunately, combining SMR and RAID is not a good idea, with many reports of new WD Reds simply refusing to be added to an existing array.

> While conventional desktop drives (which use conventional magnetic recording or CMR) may take up to two minutes to give up reading, SMR drives are even worse - there are reports of them stalling for over 10 minutes as the drive shuffles everything around to make space.

> For SMR drives, the drive should report that the trim command is supported. Unfortunately, some (many?) cheaper SMR drives do not, and due to the nature of SMR drives that don't support trim will have problems, leading to exactly the grief many have reported - the drive stalling for ever almost as it has to rewrite masses of data. Note, however, that SMR drives come in at least three types - DM (device managed) which may or may not support trimming, and HM (host managed) which shouldn't be a problem as they leave it to the computer to sort out. 


## Types of RAID

- apparently RAID5 has some risks after drive fail, mainly a second drive will possibly fail when data is being redistributed.
  - https://www.reddit.com/r/sysadmin/comments/uu8115/raid5_ideal_configuration_is_35_or_9_drives_plus/
- RAID10 aka RAID (1+0) is recommended for 2-drive redundancy
- Apparently SSDs are safer for RAID5 but it seems their max size is 2 TB, at 9 drives == 16TB
  - So, SSD could be technically viable with multiple RAID servers
  - However, cost is probably not viable, since `2 * 9 * $160*1.1 == $3168` for 16 TB, cost is like 6x


### RAID6

The main problem with RAID6 seems to be software RAID support, BTRFS discourages it for production: https://www.phoronix.com/news/Btrfs-Warning-RAID5-RAID6

- RAID6 considered unstable for btrfs: https://btrfs.wiki.kernel.org/index.php/Status#RAID56

RAID6 has 2 redundant drives, this seems good if I build a system from unreliable parts.

This seems suitable for having tons of drives. How would it work with mismatched drives, e.g. does it batch the smaller drives to bring them up to "effectively 2 redundant drives"? There must be some algorithm... e.g. if I had 1 8tb disk and 10 2 tb disks, and I have an 8tb disk, does that mean that I can still have an arbitrary disk fail and keep all my data? Or does that mean that the initial max storage calculated will be much lower for mismatch drive scenarios?

Post explaining redundancy and bad reads in a drive failure scenario, explaining why RAID5 is dangerous and RAID6 provides additional bad read redundancy in this case: https://www.reddit.com/r/DataHoarder/comments/b57u7r/at_what_point_is_raid_6_worth_it/ejbsj55/



### RAID10

RAID10 is RAID1+0. It is 50% redundant and would be good for critical data storage, but I don't need that.


## Expensive RAID5 server

Hard drive cost: $1534.50
Total effective storage: 65.48 terabytes

- $306.90 after tax per 18tb easystore: https://shucks.top/
- 16.37 terabytes true storage after converting 18,000 GB by /1024/1024/1024/1024
  - (terabytes on computer are actually tib)
  - https://www.bestbuy.com/site/questions/wd-easystore-18tb-external-usb-3-0-hard-drive-black/6427995/question/833048c7-e97b-38e8-b8fe-f6e48d6aea8e
- 5 drives and 18tb/drive = 81.85 tb
- and 4/5 storage to redundancy = 65.48 terabytes effective
- Cost of $306.90 * 5 + base cost of RAID server


## Cheaper RAID server

- Still pretty expensive, how much space do we get?  Probably 8/18 * 65.48 == 29.1 TB
- So we get 44% of the space for 60% of the cost of drives, so drives are 50% more expensive, plus the base cost
- 8 tb easystores are typically $187 after tax
- 5 * 187 = $935

