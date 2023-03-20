# Define Operationally Excellent Architectures

5.1 Choose design features in solutions that enable operational excellence.

- metrics: latency, http, 4xx errors, 5xx errors, etc.
- cloudwatch can give metrics on ec2 based on what we can measure
- can't measure how much data you have stored on ebs volume - no metric
- cloudwatch custom metrics - you can report your own metrics to cloudwatch then set alarms


## Exam Questions

- CodeDeploy: Amazon EC2, Fargate, lambda, on-prem servers

## Infrastructure as Code


### CloudFormation

- Version your infrastructure
  - Applications can rely on specific changes to infrastructure

- Branch your infastructure (e.g. git)
  - Work on multiple things concurrently
  - Run version 2 while working on version 3.

- Audit changes
  - Traceability: who and why


### AWS CodeCommit

Not on SA Associate - but on developer. Need to know codesuite.

- Fully managed source control service
- HA, durable
- Encryption
- IAM
- No limit on repo size
- Does it support LFS? Need to think about what LFS even is...


### AWS CodeDeploy

- Fully managed deployment services
- Blue/Green Deployments
- Deployment Health Tracking
- Automatically rollback if failure is detected
- Exam Question: Amazon EC2, Fargate, lambda, on-prem servers


### AWS CodePipeline

- We skipped over this, don't really need to know about it for this purpose.
