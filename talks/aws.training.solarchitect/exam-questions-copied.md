# Exam Questions

These are copied from each section of the day-long course

## Resilient Architecture

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


## Design Cost Optimized Architectures

- How often and how quickly do you need to access your data?
- How large is your data set?
- How transient is your data?
  - Clickstream
- How much are you prepared to pay to store the data?

- Durability: The average, expected annual data loss
- S3 Resiliency: Almost all S3 Resilient against single AD (except for 1-zone IA)
- Throughput oriented, lowest cost: Cold HDD (sc1) 
- Exam Question: I have an on demand instance, it costs $10/hour, I started at 930 AM and terminated at 1100 AM.
  - You will get charged for 2 hours (not 1.5 hours)
  - Some instances you can pay per second


## Define Operationally Excellent Architectures

5.1 Choose design features in solutions that enable operational excellence.

- metrics: latency, http, 4xx errors, 5xx errors, etc.
- cloudwatch can give metrics on ec2 based on what we can measure
- can't measure how much data you have stored on ebs volume - no metric
- cloudwatch custom metrics - you can report your own metrics to cloudwatch then set alarms
- CodeDeploy: Amazon EC2, Fargate, lambda, on-prem servers


## Performant Architectures

- Elasticache - 
- Whenever they say "relational" - use RDS
- Whenever they say "nosql" - DynamoDB
- Whenever they say "data warehouse" - "Redshift!"
- Not going to get tested on relational vs nonrelational
  - not an exam question, interview question!
- 6 RDS Flavors - know them - look on the RDS homepage (mysql, postgres, etc)
  - Not going to get tested on using aurora vs rds choices
  - Do know what engines are supported
- RDS: Which engines does RDS support read replica for?
  - Question: "offload main database because it's hit hard"
    - Use READ REPLICA
  - Question: "You need HA" and then multi AZ deployment
    - Use MULTI AZ DEPLOYMENT
- Bring content closer to viewers and increase performance of website: CloudFront
  - Can cache dynamic or static content
  - Your clients are complaining that viewing your videos is really slow
- Scale Out: I need better performance, should I increase the size of my instance or add a server? 
  - The answer is ALWAYS add a server: scale out, add instances, use EC2 instance
  - Exam Question
- Exam Anecdote: More exam questions about classic load balancer
  - Heard from 2 recent exam takers
- Exam Question: Load Balancer checks health of ec2 instances behind load balancer
  - Question: "What happens then?"
    - Load balancer just stops routing requests until the instance is replaced or healthy
    - Auto scale manages health of the instance (replaces unhealthy instances with healthy instances)
- Network Load Balancer: always use DNS name of load balancer, don't point your website at the load balancer IP address
- EC2 Families: They might ask you what CPU instance type based on your needs


## Specify Secure Applications

Security is Job 0 on AWS.

- big part of exam: how to secure application tiers
- how to secure data
- networking infrastructure for a single VPC application
  - acloud.guru vpc training lab (very long)


- IAM User: Console access versus programmatic access
  - Console requires username + password
  - Guaranteed exam question: Programmatic access just needs access key and secret
    - Not username / password
- IAM Policy: By default users have access to nothing
  - You must attach an IAM policy (or group with an IAM policy)
- IAM Roles: When asked, always pick IAM roles over access keys
- Exam questions will try to confuse you: cloudtrail vs. cloudwatch
  - cloudtrail is a trail - logs
  - cloudwatch is like watching - metrics
- VPC: What is the biggest size and smallest size for VPC CIDR.
  - Biggest: /16
  - Smallest: /28
  - [The allowed block size is between a /28 netmask and /16 netmask.](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Subnets.html#targetText=When%20you%20create%20a%20VPC,255.255%20(172.16%2F12%20prefix))
- VPC: Only 1 IGW can be attached to 1 VPC
  - I am not getting enough bandwidth, can I attack an additional internet gateway?
    - NO you can ONLY have 1

### Shared Responsibility Model

Shared between AWS and the customer (me).
