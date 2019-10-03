# Exam Questions

These are copied from each section of the day-long course

## Resilient Architecture: 930 AM - 1030 AM

### Solutions Architect Exam

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

