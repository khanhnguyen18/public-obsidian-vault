# Practice Test 1

## 1 Mainternance EC2 -> Auto Scaling
- Auto Scaling group to provision another replacement instance immediately.
- *Solution*
  1. Put intance in standby state: 
  2. Suspend ReplaceUnhealthy: EC2 Auto Scaling stop replaces intances
- *Out Of Scope*
  - Take Snapshot on AMI: is not time/resource optimal
  - Delete the Auto Scaling group: It's not recommended
## 2. UDP Protocal -> Fast Reginal Failover
- Continue use DNS service
- *Solution*
  - [AWS Global Accelator](aws-ass-solution-architect.md#170-global-accelator)
- *Out of scope*: 
  - *ELB* : [ELB](aws-ass-solution-architect.md#70-elastic-load-balancing-elb) Single Region
  - *Route 53*: 

## 3. RDS Multi-AZ vs Read-Replica
**Solution**:
- Multi-az atleast 2 AZs: Sync + Read-Replica winthin an AZ, Cross AZ, Or Cross-Region: Async

## 4 RDS Customize
- Specialized *customizations* to the underlying Oracle database as well as its host operating system (OS)
- Improve the *availability* of the Oracle database layer
- *Solution* :
  + multi-AZ configuration of Amazon RDS Custom for Oracle that allows DBA to access and customize the database environment and the underlying operating system

## 5
- Enforce compliance and regulatory guidelines for objects stored in Amazon S3
- Key requirements is to provide adequate protection against accidental deletion of objects.
  
#### ⭐ Solution
- MFA delete for S3
- Enable versionning

## 6 GuardDuty
- Company use EC2 + API Gateway + RDS + ELB + CloudFront. Suggest use *GuardDuty*. Which data sources supported by GuardDuty
#### Solution
- [](aws-ass-solution-architect.md#314-amazon-guardduty) 

## 7 Role(Design Secure Architectures)

- delegate access to a set of users from dev environment -> access some resources in PROD ENV
- *Solution*:
  - Create IAM role with the required permissions to access the resources in PROD.

## 8 API Gateway
- APP *stateful* and *stateless client-server* communications via API 
- Solution:
  - API Gateway for create stateful API that enable stateless and create Websocket APIS enable stateless
  - [](aws-ass-solution-architect.md#api-gateway)
- Domain: Design High-Performing Architectures
## 9 EC2 AMI Region
Action: 
- Create EC2 instance
*1A* is running in Region A
- Then take snapshot of 1A the create AMI -> Copy to Region B
- Provision *1B* using new AMI in Region B 
- *Question*: What entities exist in Region B
- *Solution*:
  - 1 EC2
  - 1 AMI
  - 1 Snapshot

## 10 
- *Technology blogger* write comparative pricing for *various storage types available* on AWS Cloud
  + Create 1 DB test file
  + Copy to *S3 Standard storage class*, *100 GB EBS GP2*, *EFS Standard Storage*
- Solution
  - S3 Standart < EFS < Amazon EFs
  - Explanation
    - EBS -> Resource you use: 0,1/GB -> 100GB is 10USD
    - EFS 0,3 USD /GB
    - S3 0,023 per GB

## 11 Video Analytic
- 10 app with 70 Terabyte for eache app
- 2 weeks to carry out data migration from *on-premies data* -> *AWS*
- Most cost effective
- Solution
  - AWS Site-to-Site VPN
  - 10 AWS Snowball [](aws-ass-solution-architect.md#aws-snow-family)

## 12 S3 cross origin
- Upload large video 
- The MOST cost-effective options to improve the file upload speed into Amazon S3
- *Solution*:
  - Amazon S3 Transfer Acceleration [](aws-ass-solution-architect.md#amazon-s3-transfer-acceleration)
  - Use multipart uploads
## 13
- US headquarters is preparing a spreadsheet of the *new product catalog*
- The spreadsheet is saved on an Amazon Elastic File System (Amazon EFS) created in us-east-1 region.
- The sourcing team counterparts from Asia Pacific and Europe also want to collaborate on this spreadsheet.
+ *Solution*
  - EFS: can be accessed in other AWS regions by using an inter-region VPC peering connection
+ *Out of Scope*:
  + S3
    - not POSIX compliant
    - not allow in-place edit of an object
  + RDS: one would need to write custom code to replicate the spreadsheet functionality running off of the database
  + EFS copy: each team would work on "its own file" instead of a single file accessed and updated by all teams
## 14: S3 - Reduce cost
- Create assets in S3, accessed by a large number of users for the first few days and the frequency of access falls down drastically after a week.
- assets would be accessed occasionally after the first week, but they must continue to be immediately accessible when required
-> Suggest a way to lower the storage cost
- *SOLUTION*
  - S3 One-IA in 30 days(Minimum)


## 15: EC2 - ALB - Ec2 Auto Scaling - Aurora
- been tasked to make the application more resilient to periodic spikes in request rates.
- *SOLUTION*
  - [Aurora Replica](aws-ass-solution-architect.md#aurora-replica)
  - Cloufront in front of [ALB](aws-ass-solution-architect.md#application-load-balancer-alb): 
- *WRONG ANSWER*
  + [Global Accelerator](aws-ass-solution-architect.md#170-global-accelator)
## 16: EC2 Cost
- 24*7 Prod
- *SOLUTION*
  - RI for *PROD* and on-demain on *DEV*
- Review [Ec2]
+ *Out of Scope*:

## 17: SMB - 200 terrabyte - Window
- Want AWS access
- *SOLUTION*
  - Amazon FSx File Gateway + Amazon FSx for Windows File Server.
- *OUT OF SCOPE*:
  - Storage Gateway’s File Gateway  + S3: 
  - FSx File Gateway + EFS:
  - Storage Gateway’s File Gateway  + EFS
## 18 Realtime data
- *Mobile Game* publish result on *leaderboard*
- Should handle major traffic spikes; 
- *SOLUTION*
  - [Kinesis Data Stream](aws-ass-solution-architect.md#kinesis-data-stream) + [Lambda](##lambda) + Dynamo DB 
- *OUT OF SCOPE*:
  - Using *EC2 instances* as part of the solution architecture. The use-case seeks to minimize the management overhead required to maintain the solution. However, Amazon EC2 instances involve several maintenance activities such as managing the guest operating system and software deployed to the guest operating system, including updates and security patches, etc. 
## 19 Notification System SNS + Lambda
- Off-season -> 100 TPS
- Peak football season -> 5000 TPS -> significant number  notifications are not being *deleveried*
- Suggest best solution for this
- *SOLUTION*
  + Amazon SNS message deliveries to AWS Lambda have crossed the *account concurrency quota for AWS Lambda*, so the team needs to contact AWS support to raise the account limit
- *OUT OF SCOPE*:
  + Lambda - SNS: fully managed services - serverless

## 20 Your data center and AWS Cloud
- dedicated, encrypted, low latency *connection* between *Datacenter* and *AWS Cloud*
- set aside sufficient time to account for the operational overhead of establishing this connection.
+ *SOLUTION*
  + [AWS Direct Connect](aws-ass-solution-architect.md#aws-direct-connect) + VPN
  - https://docs.aws.amazon.com/images/whitepapers/latest/aws-vpc-connectivity-options/images/aws-direct-connect-and-aws-site-to-site-vpn.png
+ *OUT OF SCOPE*:
  - [AWS Transit Gateway](aws-ass-solution-architect.md#aws-transit-gateway)
  - *AWS Direct Connect for both*: cannot provide an encrypted connection between a data center and AWS Cloud
  - [AWS site-to-site VPN](aws-ass-solution-architect.md#aws-site-to-site-vpn)
## 21 Big file Image S3
- 3 GB file -> Using S3TA for faster image upload
- which of the following is correct regarding the charges for this image transfer
- *SOLUTION*
  - Does not need to Pay any transfer charges 
    - S3: No transfer charge for Data *from the internet* 
    - *S3TA* did not result in an accelerated transfer[](aws-ass-solution-architect.md#amazon-s3-transfer-accelerations3ta).
- *WRONG ANSWER*
## 22 car-as-a-sensor service
- Serverless component of AWS

- *SOLUTION*
  - SQS Queue + AWS Lambda + DynamoDB
    - SQS Queue : Auto Scaling
    - Lambda
- *OUT OF SCOPE*
  1. [Kinesis Data Firehose]() + DynamoDB: cannot directly write into a DynamoDB table
  2. 
  
- *WRONG ANSWER*

## 40
- AWS Steps Function

## 45
- AWS Storage gateway

## 48 S3 retention date


###