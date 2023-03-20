# Designing Resilient Architectures


## Overview

- SQS: Decoupling Mechanism for architecture
- Determine how to design a multi-tier architecture
- Global Availability Zone - ALWAYS


## Exam Questions

It's better to do the labs than read the documentation.

Anecdotally, the questions are really clear, there's no ambiguity if you really parse each question. There's always something that discounts one of the two best questions.

Keep the pillars of well-architected systems in mind. The question will always say "high availabity" or "low cost".


### Solutions Architect

- EC2 Ephemeral volume - you lose your data if you terminate the instance (stop), if you reset it's OK.
- EBS is an Independent Lifecycle from EC2 instance
- Exam question, we need 12000 iops, so which one do you pick? 
  - You need Provisioned IOPS SSD (io1) (32000 iops) because gp2 (general purpose SSD) is only 10000 IOPS
  - Provisioned is for large database workloads, production environments
  - st1, sc1 is good for log processing, data warehouses, when storage cost is more important than other considerations
- EBS Volume Types: https://aws.amazon.com/iq/
  - gp2, io1, st1, sc1: LOTS OF EXAM QUESTIONS ON THIS TABLE - see photo in phone
- Can only attach EBS volume to 1 instance at a time, EFS can work with multiple EC2 instances.
- Supports NFS version v4.0 and 4.1 - need to know EFS is NFS compatible
- S3 supports server-side encryption: SSE-S3, SSE-KMS, SSE-C
  - C = customer
  - S3 = ?? probably what you assume
  - KMS = ??   probably what you assume
- S3 has a multi-part upload API
  - Use this for large files
- S3: AWS will never move data to a different region unless you tell us to
  - Data soverignty laws
- EBS: You can move across AZs within a region by creating a snapshot
  - To get volume into new AZ: You restore the snapshot to a new volume, and you select the AZ
- EBS: Snapshots go to S3
- S3 Replicates across all AZs in a region
  - except "IA one-zone" which only has 1 zone
- S3 Exam question, how to save cost? Set up lifecycle policy!
  - 30 days: move to IA,
  - 60 days: move to Glacier
  - delete after 365 days.
- Durability: "Am I going to lose my data, eleven nines."
- Availability: "Can I go get my data right now? Ever?"
- EFS is block storage, S3 is object storage
- CloudFormation Exam Questions
  - A free service, you only pay for resources it uses
  - is important to High Availability because you can create and replicate resources easily
  - What's a template? The JSON or YAML text file
  - What's a stack? The actual stack of resources created in the account
- Storage gateway: know the types and what they are meant for
  - LOOK IT UP

## Sysops (NOT the focus today)

## Associate Developer (NOT the focus today)

- CloudFormation: what's wrong with a template, what's missing from a template


## Elastic Block Store

[Whitepaper: AWS Storage Services Overview]()

- MiB is Million bytes 
  - not megabytes (GiB is 1000x1000x1000)
- Different Volume Types
  - gp2, io1, st1, sc1
  - max size you can get of any one is 16 TB
- Snapshots
- Supports Encryption
- Independent Lifecycle than EC2 instance

- EBS snapshots are backed up to S3


## EFS - Know that efs exists

- Network filesystem, can attach to multiple efs instances
- Supports NFS version v4.0 and 4.1 - need to know EFS is NFS compatible


## S3

- Cross-region replication, cross-account replication
- 5 terabytes is limit on object size
- 11 nines
- supports server-side encryption: SSE-S3, SSE-KMS, SSE-C
- Supports versioning files as you update but you are paying for new versions
- multi-part upload API
- cross-region replication
- S3 Storage Classes Table = see photo
  - There is S3-RRS: 4 nines reduced-redundancy
  - probably NOT on exam: https://aws.amazon.com/s3/reduced-redundancy/
- Charged for a minimum of 30 days
- S3 Replicates across all AZs in a region
  - except "IA one-zone" which only has 1 zone
- S3 Exam question, how to save cost? Set up lifecycle policy!
  - 30 days: move to IA,
  - 60 days: move to Glacier
  - delete after 365 days.
- Durability: "Am I going to lose my data, eleven nines."
- Availability: "Can I go get my data right now? Ever?"
- Glacier
  - Retrieval options: expedited, standard, bulk
  - Deep archive is always a few hours


## Cloudfront: CDN Service

It will be on the exam.

We'll talk about it later.

One person used it to host a video.


## AWS CloudFormation

Associate developer certification goes in depth about CloudFormation templates.

- Free
- Infrastructure as code
- Model your entire infrastructure as text: YAML or JSON
- Uses templates and stacks to provision resources
- "stack" - create, update, delete resources as a single unit
- What's a template? The JSON or YAML text file
- What's a stack? The actual stack of resources created in the account
- Declarative - aka idempotent, reapplying won't create a second set... must use tags?


## Storage Gateway

- Hybrid environment - move data between on-prem and the cloud
- Exam Question: know the types and what they are meant for


## Availability Zones Diagram

- AWS contains regions (currently: 22 regions)
- Regions contain Availability Zones (AZs)
  - At least 2 AZs in every region, typically 3
  - Each AZ can have multiple data centers (typically 3 data centers)


### High Availability (HA)

- You need to deploy in at least 2 AZs for HA.


### Diagram

AWS contains Regions, Regions each contain their own AZs

- Regions are NOT connected by lines
- AZs are connected by lines
