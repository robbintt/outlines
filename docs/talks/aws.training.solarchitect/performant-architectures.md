# Performant Architectures



## Exam Questions

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


## Topics


### RDS

- You pick a maintenance window and they apply the maintenance
- Automated backups
- Multi AZ deployments
- Encryption at rest and in transit
- Scalability: Read Replicas - same AZ or different AZ
  - Send some read requests there
- Exam Question: Which engines does RDS support read replica for?  All except oracle?

### DynamoDB

- key-value and document database
- nosql
- single-digit millisecond performance
- multi-master available
  - now also available in aurora
- multi-region available (up to you)
- durable
- RCU: Read Capacity Unit: One strongly consistent read per second OR 2 eventually consistent reads per second
  - Item up to 4kb in size
  - Need this for developer, I need so many reads/writes per second
- WCU: Write Capacity Unit - item up to 1kb in size
  - 1 write per second


### CloudFront

- Fast CDN service
  - Dynamic or Static Content
- Global Edge Network
- Origins: S3, EC2, ELB, HTTP servers
  - Even if you have an on-prem HTTP server, you can still use cloudfront
- Security: AWS Shield, AWS WAF (firewall)
- Protect Private Content

### Elasticache

memcached and redis - sysops and devops ask you to distinguish

One of these: memcached, redis


### Scale Up

- Increase size of hardware
  - more processing, more storage
  - Bigger EC2 instances



### Scale Out

- Adding more servers
- Share the workload
- Can be done on the flo

- Scale Out: I need better performance, should I increase the size of my instance or add a server? 
  - The answer is ALWAYS add a server: scale out, add instances, use EC2 instance
  - Trent: This goes into HA as well, instances can fail, we want to have a lot of instances
  - Trent: Probably save a lot of money scaling out with spot instances because they are so cheap, especially for http workers


### Load Balancers

Exam Anecdote: More exam questions about classic load balancer

- Classic Load Balancer
  - Layer 4 and Layer 7 (4 = transport layer, 7 = application layer)
  - Sticky sessions per user
  - Manages SSL - does all 4 protocols
  - Exam Question: Load Balancer checks health of ec2 instances behind load balancer
    - Question: "What happens then?"
      - Load balancer just stops routing requests until the instance is replaced or healthy
      - Auto scale manages health of the instance
- Application Load Balancer
  - Layer 7 (application layer)
  - Route traffic to targets
  - only HTTP, HTTPS protocols support
  - Sysops & network certs
  - native ipv6
  - Target Groups: cannot assign instances, must make them a member of a target group
    - concept is specific to application load balancer, not done with classic load balancer
  - sticky sessions
  - advanced routing
- Network Load Balancer
  - All about transport (layer 4)
  - Best performance load balancer
  - static IP support
    - Exam question: always use DNS name of load balancer, don't point your website at the load balancer IP address
  - TLS offloading
  - Supports SSL now


### Auto Scaling

Better fault tolerance, better availability, better cost management

- Cost Management
  - Elastic: Adjust number of instances
- Health Check: terminate unhealthy instance and start a new one
- Cattle vs Pets
- Launch systems based on launch configuration
- Scaling policy
  - if cpu > 95 add x instances
  - any other metric, whatever is good for application


### EC2 Instance Types

- Know the family and what they are for.
- Exam Question EC2 Families: They might ask you what CPU instance type based on your needs
- You don't need to know how many versions for each family, just know the family.

#### Some Handy mnemonics someone made up

- T Family: general - burstable, good for dynamic workloads
- M family: main for application - static, good for consistent workloads
- C family: compute - good for small memory footprint and high compute
- R family: RAM - high memory to CPU ratio
- X family: extreme - high memory for CPU, general in-memory usage
- P family: pictures - general graphics 
- F family: FPGA
- G family: graphics intensive applications
- H family: HDD backed
- I family: SDD
- D family: Dense - High disk ratio



