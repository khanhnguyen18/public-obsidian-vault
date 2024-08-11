# Practice Test 1

## 1 Mainternance EC2 -> Auto Scaling
- Auto Scaling group to provision another replacement instance immediately.
- Solution
  1. Put intance in standby state:
  2. Suspend ReplaceUnhealthy: EC2 Auto Scaling stop replaces intances
- Out Of Scope
  - Take Snapshot on AMI: is not time/resource optimal
  - Delete the Auto Scaling group: It's not recommended
## 2. UDP Protocol -> Fast Regional Failover
- Continue use DNS service
- Solution
  - [AWS Global Accelerator](aws-ass-solution-architect.md#170-global-accelator)
	  - [[aws-ass-solution-architect#170. Global Accelerator|AWS Global Accelerator]]
- Out of scope:
  - [ELB](aws-ass-solution-architect.md#70-elastic-load-balancing-elb) [[aws-ass-solution-architect#70. Elastic Load Balancing (ELB)|ELB]] Single Region
  - Route 53:

## 3. RDS Multi-AZ vs Read-Replica
*Solution*:
- Multi-az atleast 2 AZs: Sync + Read-Replica winthin an AZ, Cross AZ, Or Cross-Region: Async

## 4 RDS Customize
- Specialized customizations to the underlying Oracle database as well as its host operating system (OS)
- Improve the availability of the Oracle database layer
- Solution :
  + multi-AZ configuration of Amazon RDS Custom for Oracle that allows DBA to access and customize the database environment and the underlying operating system

## 5
- Enforce compliance and regulatory guidelines for objects stored in Amazon S3
- Key requirements is to provide adequate protection against accidental deletion of objects.

#### ⭐ Solution
- MFA delete for S3
- Enable versionning

## 6 GuardDuty
- Company use EC2 + API Gateway + RDS + ELB + CloudFront. Suggest use GuardDuty. Which data sources supported by GuardDuty
#### Solution
- [GuardDuty](aws-ass-solution-architect.md#314-amazon-guardduty)
	- [[aws-ass-solution-architect#AWS Solution Architect#314 Amazon GuardDuty|GuardDuty Wiki]]

## 7 Role(Design Secure Architectures)

- delegate access to a set of users from dev environment -> access some resources in PROD ENV
- Solution:
  - Create IAM role with the required permissions to access the resources in PROD.

## 8 API Gateway
- APP stateful and stateless client-server communications via API
- Solution:
  - API Gateway for create stateful API that enable stateless and create Websocket APIS enable stateless
  - [api-gateway](aws-ass-solution-architect.md#api-gateway)
  * [[aws-ass-solution-architect#API GATEWAY|API GATEWAY Wiki]]
- Domain: Design High-Performing Architectures
## 9 EC2 AMI Region
Action:
- Create EC2 instance
  1A is running in Region A
- Then take snapshot of 1A the create AMI -> Copy to Region B
- Provision 1B using new AMI in Region B
- Question: What entities exist in Region B
- Solution:
  - 1 EC2
  - 1 AMI
  - 1 Snapshot

## 10
- Technology blogger write comparative pricing for various storage types available on AWS Cloud
  + Create 1 DB test file
  + Copy to S3 Standard storage class, 100 GB EBS GP2, EFS Standard Storage
- Solution
  - S3 Standart < EFS < Amazon EFs
  - Explanation
    - EBS -> Resource you use: 0,1/GB -> 100GB is 10USD
    - EFS 0,3 USD /GB
    - S3 0,023 per GB

## 11 Video Analytic
- 10 app with 70 Terabyte for eache app
- 2 weeks to carry out data migration from on-premies data -> AWS
- Most cost effective
- Solution
  - AWS Site-to-Site VPN
  - 10 AWS Snowball [Snowball](aws-ass-solution-architect.md#aws-snow-family)
	  - [[aws-ass-solution-architect#AWS Snow Family|Snow family wiki]]

## 12 S3 cross origin
- Upload large video
- The MOST cost-effective options to improve the file upload speed into Amazon S3
- Solution:
  - Amazon S3 Transfer Acceleration [S3TA](aws-ass-solution-architect.md#amazon-s3-transfer-acceleration)
	  - [[#42 S3 feature only be suspended and not disable|S3TA Wiki]]
  - Use multipart uploads
## 13
- US headquarters is preparing a spreadsheet of the new product catalog
- The spreadsheet is saved on an Amazon Elastic File System (Amazon EFS) created in us-east-1 region.
- The sourcing team counterparts from Asia Pacific and Europe also want to collaborate on this spreadsheet.
+ Solution
  - EFS: can be accessed in other AWS regions by using an inter-region VPC peering connection
+ Out of Scope:
  + S3
    - not POSIX compliant
    - not allow in-place edit of an object
  + RDS: one would need to write custom code to replicate the spreadsheet functionality running off of the database
  + EFS copy: each team would work on "its own file" instead of a single file accessed and updated by all teams
## 14: S3 - Reduce cost
- Create assets in S3, accessed by a large number of users for the first few days and the frequency of access falls down drastically after a week.
- assets would be accessed occasionally after the first week, but they must continue to be immediately accessible when required
  -> Suggest a way to lower the storage cost
- SOLUTION
  - S3 One-IA in 30 days(Minimum)


## 15: EC2 - ALB - Ec2 Auto Scaling - Aurora
- been tasked to make the application more resilient to periodic spikes in request rates.
- SOLUTION
  - [Aurora Replica](aws-ass-solution-architect.md#aurora-replica)
	  - [[aws-ass-solution-architect#Aurora Replica|Aurora Replica Wiki]]
  - Cloudfront in front of [ALB](aws-ass-solution-architect.md#application-load-balancer-alb):
	  - [[aws-ass-solution-architect#70. Elastic Load Balancing (ELB)|ELB Wiki]]
- WRONG ANSWER
  + [Global Accelerator](aws-ass-solution-architect.md#170-global-accelator)
	  - [[aws-ass-solution-architect#170. Global Accelerator|Global Accelerator]]
  
## 16: EC2 Cost
- 24*7 Prod
- SOLUTION
  - RI for PROD and on-demain on DEV
- Review [Ec2]
+ Out of Scope:

## 17: SMB - 200 terrabyte - Window
- Want AWS access
- SOLUTION
  - Amazon FSx File Gateway + Amazon FSx for Windows File Server.
- OUT OF SCOPE:
  - Storage Gateway’s File Gateway  + S3:
  - FSx File Gateway + EFS:
  - Storage Gateway’s File Gateway  + EFS
## 18 Realtime data
- Mobile Game publish result on leaderboard
- Should handle major traffic spikes;
- SOLUTION
  - [Kinesis Data Stream](aws-ass-solution-architect.md#kinesis-data-stream) + [Lambda](##lambda) + Dynamo DB
	  - [[aws-ass-solution-architect#Kinesis Data Stream|Kinesis Data Stream Wiki]]
	  - [[aws-ass-solution-architect#218. Lambda|Lambda]]
	  - [[aws-ass-solution-architect#Dynamo DB - Summary|Dynamo DB - Summary]]
- OUT OF SCOPE:
  - Using EC2 instances as part of the solution architecture. The use-case seeks to minimize the management overhead required to maintain the solution. However, Amazon EC2 instances involve several maintenance activities such as managing the guest operating system and software deployed to the guest operating system, including updates and security patches, etc.
## 19 Notification System SNS + Lambda
- Off-season -> 100 TPS
- Peak football season -> 5000 TPS -> significant number  notifications are not being deleveried
- Suggest best solution for this
- SOLUTION
  + Amazon SNS message deliveries to AWS Lambda have crossed the account concurrency quota for AWS Lambda, so the team needs to contact AWS support to raise the account limit
- OUT OF SCOPE:
  + Lambda - SNS: fully managed services - serverless

## 20 Your data center and AWS Cloud
- dedicated, encrypted, low latency connection between Datacenter and AWS Cloud
- set aside sufficient time to account for the operational overhead of establishing this connection.
+ SOLUTION
  + [AWS Direct Connect](aws-ass-solution-architect.md#aws-direct-connect) + VPN
	  * [[aws-ass-solution-architect#AWS Directory Service for Microsoft Active Directory (AWS Managed Microsoft AD)|Direct connect Wiki]]
  ![aws-direct-connect-and-aws-site-to-site-vpn](https://docs.aws.amazon.com/images/whitepapers/latest/aws-vpc-connectivity-options/images/aws-direct-connect-and-aws-site-to-site-vpn.png)
+ OUT OF SCOPE:
  - [AWS Transit Gateway](aws-ass-solution-architect.md#aws-transit-gateway)
	  - [[aws-ass-solution-architect#AWS Transit Gateway|AWS Transit Gateway]]
  - AWS Direct Connect for both: cannot provide an encrypted connection between a data center and AWS Cloud
  - [AWS site-to-site VPN](aws-ass-solution-architect.md#aws-site-to-site-vpn)
	  * [[aws-ass-solution-architect#AWS site-to-site VPN|AWS site-to-site VPN]]
## 21 Big file Image S3
- 3 GB file -> Using S3TA for faster image upload
- which of the following is correct regarding the charges for this image transfer
- SOLUTION
  - Does not need to Pay any transfer charges
    - S3: No transfer charge for Data from the internet
    - S3TA did not result in an accelerated transfer [S3TA](aws-ass-solution-architect.md#amazon-s3-transfer-accelerations3ta).
		- [[aws-ass-solution-architect#S3 Transfer Acceleration(S3TA)|S3TA]]
- WRONG ANSWER
## 22 car-as-a-sensor service
- Severless component of AWS

- SOLUTION
  - SQS Queue + AWS Lambda + DynamoDB
    - SQS Queue : Auto Scaling
    - Lambda
- OUT OF SCOPE
  1. [Kinesis Data Firehose](aws-ass-solution-architect.md#kinesis-firehose) + DynamoDB: cannot directly write into a DynamoDB table
	  - [[aws-ass-solution-architect#Firehose|Firehose]]

- WRONG ANSWER

## 24 ASW IAM
- Recommend
- SOLUTION:
  - Configure AWS CloudTrail to log all AWS IAM Action
  - Enable MFA
- [IAM Best practice](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html)
  *Wrong Answer*

## 25 EC2 Scaling at last day of the month
- Payroll App need 10 instance for peak usage hour and 2 EC2 for not.
- Solution:
  - Create [scheduled action](aws-ass-solution-architect.md#asg---schedule-action) kicks-off at the designated hour on the last day of the month
	  - [[##action]]

## 26 EC2 CPU uilization
- ASG + ALB
- Solution:
  - Configure the Auto Scaling group to use [Target tracking policy](aws-ass-solution-architect.md#asg---target-tracking-policy) and set the CPU utilization as the target metric with a target value of 50%
- Wrong Anaswer:
  - Simple and Step: not have target mectric for CPU utilization
  - Cloudwatch Alarm: ASG Could not use directly
## 27 S3 Policy
- Requires permissions to list an Amazon S3 bucket and delete objects from that bucket
- Create  IAM policy for this.
- The group is not able delete object now
- SOLUTION:
  - Correct

  {
  "Action": [
  "s3:DeleteObject"
  ],
  "Resource": [
  "arn:aws:s3:::example-bucket/*"
  ],
  "Effect": "Allow"
  }
- API actions are unique to each service

## 28 Aurora

- 5 multi-az read replica -> failover target
- tier-1(16 tera), tier-1(32 tera), tier-10(16), tier-15(16), tier-15(32)
- Failover
- Solution :
  + Tier-1(32 terra): In the event of a failover, Amazon Aurora will promote the Read Replica that has the highest priority (the lowest numbered tier). If two or more Aurora Replicas share the same priority, then Amazon RDS promotes the replica that is largest in size

## 29 Rest API with ASG + ALB + Dynamot
- static content in S3. On analyzing the usage trends, it is found that 90% of the read requests are for commonly accessed data across all users.
- Improve application Performace
- Solution:
  - Dynamo DB with DAX + CloudFron for Amazone S3
- Wrong Answer:
  - Resdis: Although you can integrate Redis with DynamoDB, it's much more involved than using DAX which is a much better fit.
  - Amazon ElastiCache Memcached cannot be used as a cache to serve static content from Amazon S3

## 30 Ec2 + ALB
- Path for specify a micro service
- Solution:
  - Path base routing

## 31 EC2 via EC2 API
- Volumn types that connot be use as a *boot volumne*
  *Solution*:
- Cold Hard disk drive(sc1)
- Throuput Optimized Hardis Drive(st1)
- [EBS](aws-ass-solution-architect.md#ebs)
	- [[aws-ass-solution-architect#EBS|EBS Wiki]]
  *Wrong Answer*:
- gp2
- instance store
- Provisioned IOPS Solid state drive (io1)

## 32 EC2 Placement Group
Nasa find landing sites. University use High Performace Computing(HPC)

*Solution :*
- KPC workload  need to achieve low-latency network performance necessary for tightly-coupled node-to-node communication that is typical of HPC applications
- EC2 deployed in a cluster placement group so that the underlying workload can benefit from low network latency and high network throughput. Cluster placement groups pack instances close together inside an Availability Zone
- [Placement Group](aws-ass-solution-architect.md#ec2---placement-group)
		- [[aws-ass-solution-architect#EC2 - Placement Group|Placement Group Wiki]]
  *Wrong answer:*
- Partition Placement Group: EC2 could place in another AZ -> Will not have low-latency network performance
- Spread Placement Group: Distinct crack
## 33 EC2 instance
- App with hight random I/O Performance
- access to a dataset that is replicated across the instances by the application itself.
- Most cost-optimal and resource efficient
- the specialized task would continue to be processed even if any instance goes down, as the underlying application would ensure the replacement instance has access to the required dataset.
  *Solution :*
- Instance Store
  *Wrong*
- EFS implies that extra resources would have to be provisioned (compared to using instance store where the storage is located on disks that are physically attached to the host instance itself)
- EBs based volumes would need to use provisioned IOPS (io1) as the storage type and that would incur additional costs. As we are looking for the most cost-optimal solution,
- EC2 with s3: wrong

## 34 Track location of truck
- Want data points to be accessailbe in realtyp
- The company wants these data points to be accessible in real-time in its analytics platform via a REST API
  *Solution*
- Leverage Amazone API Gateway with Kinesis Data Analytics
- you can use Amazon API Gateway to create a REST API that handles incoming requests having location data from the trucks and sends it to the Kinesis Data Analytics application on the back end.


## 35 Fasted Way to upload file to S3
*Solution:
- [S3TA](aws-ass-solution-architect.md#amazon-s3-transfer-accelerations3ta) + Multipart upload
	- [[#52 S3 protect data store in S3 and EC2]]
	* [[aws-ass-solution-architect#S3 - Multipart Upload|Multipart Upload Wiki]]
		- 
  *Incorrect Option*
- Single Operation:  In general, when your object size reaches 100 megabytes, you should consider using multipart uploads instead of uploading the object in a single operation. Multipart upload provides improved throughput - you can upload parts in parallel to improve throughput
- FTP compressed file -> EC2(same with bucket)

## 36 Security DymanoDB delete some table
*Solution*
- Use permissions boundary to control the maximum permissions employees can grant to the IAM principals
  ![](https://d2908q01vomqb2.cloudfront.net/22d200f8670dbdb3e253a90eee5098477c95c23d/2018/07/02/delegated-admin-01.png)
- [](https://aws.amazon.com/blogs/security/delegate-permission-management-to-developers-using-iam-permissions-boundaries/)
  *Incorrect Options*
- CTO review IAM rols
- Only root user have full DB access
- Remove full db access for al IAM user
## 37 Illegal AWS API
- seek an automated solution that can trigger near-real-time warnings in case such an event recurs.
  *Solution*
- Create Amazon CloudWatch metric filter that process AWS CloudTrail logs having API call details
- AWS CloudTrail log data can be ingested into Amazon CloudWatch to monitor and identify your AWS account activity against security threats, and create a governance framework for security best practices.
  - You can analyze log trail event data in CloudWatch using features such as Logs Insight, Contributor Insights, Metric filters, and CloudWatch Alarms.
- Create alarm base on metric's rate and send to *SNS*
- *Note*:
  - AWS CloudTrail Insights helps AWS users identify and respond to unusual activity associated with write API calls by continuously analyzing CloudTrail management events.
  - Insights events are logged when AWS CloudTrail detects unusual write management API activity in your account.
  - If you have AWS CloudTrail Insights enabled and CloudTrail detects unusual activity, Insights events are delivered to the destination Amazon S3 bucket for your trail. You can also see the type of insight and the incident time when you view Insights events on the CloudTrail console. Unlike other types of events captured in a CloudTrail trail, Insights events are logged only when CloudTrail detects changes in your account's API usage that differ significantly from the account's typical usage patterns.
    *Incorrect Options*
- AWS Cloudtrail -> Kinesis(not connect)
- Athena -> Quicksight -> Not near-real-time
- Trust Advisour -> check Cloudwatch -> Create Alarm(but only when server litmit is reached). We need a solution that raises an alarm when the number of API calls randomly increases or an abnormal pattern is detected
## 38 Football livestream only on USD
*Solution*
- Use georestriction to prevent users in specific geographic locations from accessing content that you're distributing through a Amazon CloudFront web distribution
- Use Amazon Route 53 based geolocation routing policy to restrict distribution of content to only the locations in which you have distribution rights
  *Incorrect Options*
- Route 53 latency-based routing, weight routing
## 39 Optimize website loading
*Solution*
- CloudFront with a custom origin pointing to the on-premises servers
  *Incorrect Options*
- S3: Company has dynamic website
- Route 53 geo-proximity
- Cloudfront with a custom origin pointing to the DNS Record: Distract
## 40 S3 Storage Class
- accesses the audit reports only twice in a financial year
- The underlying data to create these audit reports is stored on Amazon S3, runs into hundreds of Terabytes and should be available with millisecond latency.
- Cost Optimal
  *Solution*
- Amazon S3 Standard-Infrequent Access (S3 Standard-IA)

## 41 Shield Advance
- Costs incurred are much higher than expected
  *Solution*
- Consolidated billing has not been enabled. All the AWS accounts should fall under a single consolidated billing for the monthly fee to be charged only once
  - If your organization has multiple AWS accounts, then you can subscribe multiple AWS Accounts to AWS Shield Advanced by individually enabling it on each account using the AWS Management Console or API.
  - You will pay the monthly fee once as long as the AWS accounts are all under a single consolidated billing, and you own all the AWS accounts and resources in those accounts.
## 42 S3 feature only be suspended and not disable


*Solution*
- Versioning

## 43 S3 Delete KMS key

*Solution*
- As the AWS KMS key was deleted a day ago, it must be in the 'pending deletion' status and hence you can just cancel the KMS key deletion and recover the key

## 44 - AWS cloud architecture that throttles requests in case of sudden traffic spikes
*Solution*
- API Gateway + SQS + Kinesis
  - API Gateway: Amazon API Gateway throttles requests to your API using the *token bucket algorithm*, where a token counts for a request.  Specifically, API Gateway sets a limit on a steady-state rate and a burst of request submissions against all APIs in your account. In the token bucket algorithm, the burst is the maximum bucket size.
  - Amazon SQS: Amazon SQS offers *buffer* capabilities to smooth out temporary volume spikes without losing messages or increasing latenc

Incorrect
- Amazon Gateway Endpoints, Amazon Simple Queue Service (Amazon SQS) and Amazon Kinesis
  +  A Gateway Endpoint is a gateway that you specify as a target for a route in your route table for traffic destined to a supported AWS service. This cannot help in throttling or buffering of requests

- Elastic Load Balancer, Amazon SQS, AWS Lambda
  + Elastic Load Balancer cannot throttle requests
- Amazon SQS, Amazon SNS and AWS Lambda
  +
- AWS Steps Function

## 45 integrate data on-premieses
Requirement
integrate analytical app from *on-premieses* with *AWS* via NFS
*Solution*
- [AWS Storage File gateway](aws-ass-solution-architect.md#178-storage-gateway)

## 46 The real-time status data for these devices
Requirement
- Real-time status data for these devices must be fed into a communications application for notifications
  Solution
- [Amazon Kinesis Data Streams](aws-ass-solution-architect.md#kinesis-data-stream)
  Out of scope
- *SNS*: notification service and cannot be used for real-time processing of data.
- *SQS*: multiple applications need to consume the same data stream concurrently, Kinesis is a better choice when compared to the combination of SQS with SNS

## 47 S3
Requirement
- Upload directly using single Bucket
- scalability issue at 5000 request per second
  Solution
- Create customer-specific custom prefixes:
  - [S3](aws-ass-solution-architect.md#s3)
    Incorrect
- *Bucket for each customer*: inefficeint way of handling resource(~Bucket is unique~)
- *Using EFS:*  a costlier storage option compared to Amazon S3
- *Bucket for daily data*: inefficeint way of handling resource(~Bucket is unique~)

## 48 S3 retention date
*Requirement*
- different retention periods for different objects
  *Solution*
- When you apply a retention period to an object version explicitly, you specify a Retain Until Date for the object version
  - Amazon S3 stores the Retain Until Date setting in the object version's metadata and protects the object version until the retention period expires.
- Different versions of a single object can have different retention modes and periods
  - For example, suppose that you have an object that is 15 days into a 30-day retention period, and you PUT an object into Amazon S3 with the same name and a 60-day retention period. In this case, your PUT succeeds, and Amazon S3 creates a new version of the object with a 60-day retention period. The older version maintains its original retention period and becomes deletable in 15 days.
    *Incorrect*
- The bucket default settings will override any explicit retention mode or period you request on an object version -> in invert way
- When you use bucket default settings, you specify a Retain Until Date for the object version
  -> When you use bucket default settings, you don't specify a Retain Until Date. Instead, you specify a duration, in either days or years, for which every object version placed in the bucket should be protected.
- You cannot place a retention period on an object version through a bucket default setting
  -> You can place a retention period on an object version either explicitly or through a bucket default setting.
## 49. ECS with EC2 or Fargate

*Solution*
- ECS with EC2 launch type is charged based on EC2 instances and EBS volumes used
  - Amazon ECS with Fargate launch type is charged based on vCPU and memory resources that the containerized application requests
- [](aws-ass-solution-architect.md#ecs)
  *Wrong*

## 50 EC2 + ALB
*Requirement*
- access from *3 country*
- Block access from *2 countries* and only allow for *home country*

*Solution*
- WAF on ALB in VPC [](aws-ass-solution-architect.md#aws-web-application-firewalaws-waf)
  *Wrong*
- Security Group for EC2: Security Groups cannot restrict access based on the user's geographic location.
- Geo Retriction of CloudFront in a VPC: Cloudfront work on Edge, not on VPC
- Security Group for ALB: Security Groups cannot restrict access based on the user's geographic location.

## 51 Cloudfront cache
- Certain content types that bypass the regional edge cache, and go directly to the origin.

*Solution*
- Proxy methods PUT/POST/PATCH/OPTIONS/DELETE go directly to the origin
- Dynamic content, as determined at request time (cache-behavior configured to forward all headers)
  *Wrong*
- E-commerce assets such as product photos:
- User-generated videos
- Static content such as style sheets, JavaScript files

## 52 S3 protect data store in S3 and EC2


*Solution*
- GuardDuty for S3, Inspector for EC2

*Wrong*
- Amazon Inspector for both
- Inspector for S3 and GuardDuty for EC2
- GuardDuty for both


## 53 - massive volumes of data
*Requirement*
- Data
  - Hot: processed and stored quickly in a parallel and distributed fashion
  - Cold: needs to be kept for reference with quick access for reads and updates at a low cost.

*Solution*
Amazon FSx for Lustre:

*Wrong*
Amazon FSx for Windows File Server: Therefore you cannot reference the "cold data" with quick access for reads and updates at low cost
EMR: EMR does not offer the same storage and processing speed as FSx for Lustre. So it is not the right fit for the given high-performance workflow scenario.
AWS Glue not offer the same storage and processing speed

## 54 - Solution for high Avaibility
An e-commerce company is looking for a solution with high availability, as it plans to migrate its flagship application to a fleet of Amazon Elastic Compute Cloud (Amazon EC2) instances. The solution should allow for content-based routing as part of the architecture.


*Solution*
- ~Use an Application Load Balancer for distributing traffic to the Amazon EC2 instances spread across different Availability Zones (AZs). Configure Auto Scaling group to mask any failure of an instance~
  - ALB) is best suited for load balancing HTTP and HTTPS traffic and provides advanced request routing targeted at the delivery of modern application architectures, including microservices and containers: content-based routing which can be configured via the Application Load Balancer
  - EC2


*Wrong*
- Use a Network Load Balancer for distributing traffic to the Amazon EC2 instances spread across different Availability Zones (AZs). Configure a Private IP address to mask any failure of an instance
  - 
- Use an Auto Scaling group for distributing traffic to the Amazon EC2 instances spread across different Availability Zones (AZs). Configure a Public IP address to mask any failure of an instance
- Use an Auto Scaling group for distributing traffic to the Amazon EC2 instances spread across different Availability Zones (AZs). Configure an elastic IP address (EIP) to mask any failure of an instance

## 55 S3 Lifecycle Invalid

*Solution*
- Amazon S3 Intelligent-Tiering => Amazon S3 Standard
- Amazon S3 One Zone-IA => Amazon S3 Standard-IA
- [Link](aws-ass-solution-architect.md#s3---lifecycle-transtion)
	 - [[#55 S3 Life cycle Invalid|Life cycle Invalid Wiki]]
  *Wrong*
- Amazon S3 Standard => Amazon S3 Intelligent-Tiering
- Amazon S3 Standard => Amazon S3 Intelligent-Tiering
- Amazon S3 Standard-IA => Amazon S3 One Zone-IA

## 56
A geological research agency maintains the seismological data for the last 100 years.
The data has a velocity of 1GB per minute.
You would like to store the data with only the most relevant attributes to build a predictive model for earthquakes.


*Solution*
- Ingest the data in *Amazon Kinesis Data Firehose* and use an intermediary *AWS Lambda function* to filter and transform the incoming stream before the output is dumped on *Amazon S3*
  *Wrong*

- Ingest the data in *Amazon Kinesis Data Analytics* and use *SQL queries to filter* and transform the data before writing to *Amazon S3*
  - Kinesis Data Analytics cannot directly ingest data from the source as it ingests data either from Kinesis Data Streams, Kinesis Data Firehose
- Ingest the data in *Amazon Kinesis Data Streams* and use an intermediary A**WS Lambda functio**n to filter and transform the incoming stream before the output is dumped on Amazon S3
  * Kinesis Data Streams cannot directly write the output to Amazon S3. Unlike Amazon Kinesis Data Firehose, KDS does not offer a ready-made integration via an intermediary AWS Lambda function to reliably dump data into Amazon S3.You will need to do a lot of custom coding to get the AWS Lambda function to process the incoming stream and then store the transformed output to Amazon S3 with the constraint that the buffer is maintained reliably and no transformed data is lost. So this option is incorrect.
- *EMR and use Spark Streaming transformations before writing to Amazon S3*: Using an EMR cluster would imply managing the underlying infrastructure so it’s ruled out because the correct solution for the given use-case should require the least amount of infrastructure maintenance

## 57 AWS account root user
*Solution*
- Enable Multi Factor Authentication (MFA) for the AWS account root user account
- Create a strong password for the AWS account root user

*Wrong*
Encrypt the access keys and save them on Amazon S3 - AWS recommends that if you don't already have an access key for your AWS account root user, don't create one unless you absolutely need to. Even an encrypted access key for the root user poses a significant security risk. Therefore, this option is incorrect.
Create AWS account root user access keys and share those keys only with the business owner - AWS recommends that if you don't already have an access key for your AWS account root user, don't create one unless you absolutely need to. Hence, this option is incorrect.

*Send an email to the business owner with details of the login username and password for the AWS root user*. This will help the business owner to troubleshoot any login issues in future - AWS recommends that you should never share your AWS account root user password or access keys with anyone. Sending an email with AWS account root user credentials creates a security risk as it can be misused by anyone reading the email. Hence, this option is incorrect.


## 58 SQS FIFO
- The development team at the bank expects a peak rate of about 1000 messages per second to be processed via SQS.
- It is important that the messages are processed in order.


*Solution*
- Use Amazon SQS FIFO (First-In-First-Out) queue in batch mode of 4 messages per operation to process the messages at the peak rate
  + By default, FIFO queues support up to 300 messages per second (300 send, receive, or delete operations per second). When you batch 10 messages per operation (maximum), FIFO queues can support up to 3,000 messages per second
    *Wrong*

## 59 Gaming Aurora US
- Expand to Europe And Asisia
- It needs the games table to be accessible globally but needs the users and games_played tables to be regional only.

*Solution*
Use an *Amazon Aurora Global Database* for the games table and use *Amazon Aurora* for the users and games_played tables

*Wrong*
Amazon DynamoDB and Amazon Aurora have a completely different APIs, due to Amazon Aurora being SQL and Amazon DynamoDB being NoSQL

## 60 Streaming Service
- S3 in data lake *around the world*.
- The data lake has a staging zone where intermediary query results are kept only for 24 hours. These results are also heavily referenced by other parts of the analytics pipeline.
- Most cost-effective

*Solution*
- Store the intermediary query results in Amazon S3 Standard storage class
  * As there is no minimum storage duration charge and no retrieval fee (remember that intermediary query results are heavily referenced by other parts of the analytics pipeline),

*Wrong*
Store the intermediary query results in Amazon S3 One Zone-Infrequent Access storage class
* have a minimum storage duration charge of 30 days
  Store the intermediary query results in Amazon S3 Glacier Instant Retrieval storage class
* The minimum storage duration charge is 90 days, so this option is NOT cost-effective because intermediary query results need to be kept only for 24 hours. Hence this option is not correct.
  Store the intermediary query results in Amazon S3 Standard-Infrequent Access storage class
* The minimum storage duration charge is 30 days, so this option is NOT cost-effective because intermediary query results need to be kept only for 24 hours. Hence this option is not correct.

## 61
A large financial institution operates an on-premises data center with hundreds of petabytes of data managed on Microsoft’s Distributed File System (DFS)


*Solution*
- Amazon FSx for Windows File Server
  * Amazon FSx supports the use of Microsoft’s Distributed File System (DFS) to organize shares into a single folder structure up to hundreds of PB in size
  * [](aws-ass-solution-architect.md#amazon-fsx-for-windows-file-server)
    *Wrong*

## 62
A company uses Amazon DynamoDB as a data store for various kinds of customer data, such as user profiles, user events, clicks, and visited links. Some of these use-cases require a high request rate (millions of requests per second), low predictable latency, and reliability. The company now wants to add a caching layer to support high read volumes.

*Solution*
Amazon DynamoDB Accelerator (DAX) [](aws-ass-solution-architect.md#dynamodb-acceleratordax)
- [[aws-ass-solution-architect#DynamoDB Accelerator(DAX)]]
Amazon ElastiCache [](aws-ass-solution-architect.md#amazon-elasticache)
- [[aws-ass-solution-architect#Amazon ElastiCache]]

*Wrong*
Amazon Relational Database Service (Amazon RDS)
Amazon Redshift
Amazon OpenSearch Service

## 63
- A US-based healthcare startup is building an interactive diagnostic tool for COVID-19 related assessments. The users would be required to capture their personal health records via this tool. As this is sensitive health information, the backup of the user data must be kept encrypted  (Amazon S3). The startup does not want to provide its own encryption keys but still wants to maintain an audit trail of when an encryption key was used and by whom.


*Solution*
- Use server-side encryption with AWS Key Management Service keys (SSE-KMS) to encrypt the user data on Amazon S3
- https://assets-pt.media.datacumulus.com/aws-saa-pt/assets/pt1-q22-i1.jpg
  *Wrong*
- Use server-side encryption with Amazon S3 managed keys (SSE-S3) to encrypt the user data on Amazon S3 - When you use Server-Side Encryption with Amazon S3-Managed Keys (SSE-S3), each object is encrypted with a unique key. However this option does not provide the ability to audit trail the usage of the encryption keys.

- Use server-side encryption with customer-provided keys (SSE-C) to encrypt the user data on Amazon S3 - With Server-Side Encryption with Customer-Provided Keys (SSE-C), you manage the encryption keys and Amazon S3 manages the encryption, as it writes to disks, and decryption when you access your objects. However this option does not provide the ability to audit trail the usage of the encryption keys.

- Use client-side encryption with client provided keys and then upload the encrypted user data to Amazon S3 - Using client-side encryption is ruled out as the startup does not want to provide the encryption keys.
## 64 Spot Instaces
A company runs a data processing workflow that takes about 60 minutes to complete. The workflow can withstand disruptions and it can be started and stopped multiple times.
Which is the most cost-effective solution to build a solution for the workflow?
solution



## 65 Amazon GuardDuty
- A financial services company uses Amazon GuardDuty for analyzing its AWS account metadata to meet the compliance guidelines. However, the company has now decided to stop using Amazon GuardDuty service.
  All the existing findings have to be deleted and cannot persist anywhere on AWS Cloud.
- *Solution*
- Disable the service in the general settings
  - Disabling the service will delete all remaining data, including your findings and configurations before relinquishing the service permissions and resetting the service. So, this is the correct option for our use case.
    *Wrong*
- You can stop Amazon GuardDuty from analyzing your data sources at any time by choosing to suspend the service in the general settings. This will immediately stop the service from analyzing data, but does not delete your existing findings or configurations.