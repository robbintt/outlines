# Design Cost Optimized Architectures


- How often and how quickly do you need to access your data?

- How large is your data set?

- How transient is your data?
  - Clickstream

- How much are you prepared to pay to store the data?

- Durability: The average, expected annual data loss
- S3 Standard, S3 IA (infrequent access), S3 Archive
- Does your data require high IOPS?
  - EBS block storage
  - Throughput - HDD
  - IOPS - SSD
    - Remember the "provisioned iops" ssd has much higher IOPS...  32000 iops
      - cannot be boot volume
      - probably need to pay monthly or annual instead of by minute/hour

- S3 Resiliency: Almost all S3 Resilient against single AD (except for 1-zone IA)

- Throughput oriented, lowest cost: Cold HDD (sc1) 

- Exam Question: I have an on demand instance, it costs $10/hour, I started at 930 AM and terminated at 1100 AM.
  - You will get charged for 2 hours (not 1.5 hours)
  - Some instances you can pay per second

### Spot Instances

- Cheapest option, up to 90% off the price
- You place a bid on amazon EC2 instances, you get unused extra capacity.
- Instance can get terminated at any time.
- **You get a 2 minute warning, so there's solutions.**
- Apparently we can predict this and shut down the application.
- Also apparently you don't get kicked off these very often most of the time, but you COULD BE!!

### Availability Zones are load balanced behind the scenes

- But instructor says this is changing, so all users will have the same AZ in the future
- Users are binned because everyone would use the first one: us-east-1a

### Reserved Instances - RI

- Up to 75% discount compared to on-demand instances
- Capacity Reservation - 1 to 3 years
- AWS particular AZ can run out of capacity on-demand for a particular type of instance
- RI Marketplace


### Lambda

- acloud.guru is 100% lambda
  - He says he didn't pay a cent for the first 18 months!
- 1 million requests per month free, forever
- Developer exam question: what is the max time you can set for lambda?


### API Gateway

- Used for lambda, we did not touch on the details very much
