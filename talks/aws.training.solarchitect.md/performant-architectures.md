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

