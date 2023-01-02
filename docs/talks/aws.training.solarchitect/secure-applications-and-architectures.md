# Specify Secure Applications

Security is Job 0 on AWS.

- big part of exam: how to secure application tiers
- how to secure data
- networking infrastructure for a single VPC application
  - cloud guru vpc (I did this last night)


## Exam Questions

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

## Shared Responsibility Model

Shared between AWS and the customer (me).


## AAA: Authenticate, Authorize, Audit

### Authenticate

- IAM Username/Password
- Access Key (+ MFA)
- Federation

### Authorize

- IAM Policies

### Audit

- CloudTrail - region specific logging


### IAM Groups

- Groups can be nested
- Attach IAM Policy to group
- You don't want to attach policies to users.
- Users can be in multiple groups
- There is no default group for all users
- Exam Question: By default users have access to nothing
  - You must attach an IAM policy (or group with an IAM policy)

### IAM Roles

- Identity created for specific permissions
- Can be assumed by people who need it (and have perms to do so)
- Roles can be assumed by users, applications, or assigned to resources/services.
  - You can only assume one role at a time
- When asked, always pick IAM roles over access keys
- Best solution for giving access to security in multiple accounts
  - Cross account ??
- Best way to give access to other organizations
- Need to use API to enumerate roles for a user, then compare permissions


### Web Identity Federation

- AWS Security Token Service (STS)
  - Temporary credentials for access to resources (e.g. 24 hour max)


### IAM Policies

- There is a great simulation tool for testing
- Attach permissions
  - specify type of access
  - actions that can be performed
  - resources on which actions can be performed
  - etc
  - Principle of least privilege
- JSON format

#### Calculating Permissions

- Everything implicitly denied
- Explicit allows override implicit denies
- Explicit denies override explicit allows


### AWS CloudTrail

- Logging (see page for details)


### S3 Security

- Bucket Policy
- ACL (Access Control Lists)
  - Applied to specific objects within the bucket


### Encryption

- Encrypt S3 Buckets
  - Off by default
- S3 Versioning
  - Once turned on, cannot turn off
  - maybe possible to suspend
  - Increases storage costs, previous versions are not deleted


### Security Groups versus ACLs - Whiteboarding

See the guru 10 part VPC lab course I took last night (udemy) for more VPC details.

- VPC goes in a region
- Security group is a firewall
- Security group vs Access Control List (SG vs ACL)
  - ACL attached to subnet
    - So it applies to all EC2 instances
  - Security Group attached to EC2 instance
- Exam question: What is the biggest size and smallest size for VPC CIDR.
  - Biggest: /16
  - Smallest: /28
  - [The allowed block size is between a /28 netmask and /16 netmask.](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Subnets.html#targetText=When%20you%20create%20a%20VPC,255.255%20(172.16%2F12%20prefix))
- Exam Question: Only 1 IGW can be attached to 1 VPC
  - I am not getting enough bandwidth, can I attack an additional internet gateway?
    - NO you can ONLY have 1
- ACL you can set allow or deny
- Security in layers, so we want Firewall, ACL, and Security Group
- Security Group is stateful -- ACL is stateless
  - This matters because ACL will not allow outbound response during a single network action
  - Security group allows 2-way connection


### Networking in General

"Need to know networking to pass the exam."


