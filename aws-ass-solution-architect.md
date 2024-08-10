# AWS Solution Architect

## Link


open "/Users/P836088/project/markdown-documents/work/AWS/AWS-Certified-Solutions-Architect-Slides-v37.pdf"


## 11. IAM Introduction: Users, Groups, Policies

- Global service
- Root account use
- Policies is define permission of user
- Apply least previledge principle


## 13. IAM Role

 ![alt text](image-40.png)

* Statment consist of
  * Sid
  * Effect
  * Principal
  * Action
  * Resource


## Section 5

### 30. AWS Budget setup

 ![alt text](image-39.png)o

## 31. EC2 
### EC2 - Pricing
- https://aws.amazon.com/ec2/pricing/


### 32.

## 57

* EBS snapshot archive: 75% cheaper

## EFS
- Provides a simple, scalable, fully managed elastic NFS file system for use with AWS Cloud services and on-premises resources.
- Storing data within and across multiple Availability Zones (AZs) for high availability and durability
- EC2 instances can access your file system across AZs, regions, and VPCs 
- On-premises servers can access using AWS Direct Connect or AWS VPN.

- #1.13: You can connect to EFS file systems from EC2 instances in other AWS regions using an inter-region VPC peering connection, and from on-premises servers using an AWS VPN connection


## 69. High Availability and Scalability

* High Avallability usually goes hand in hand with horizontal
* High availability means running your application / system in at least 2 data centers == AZ)

• Horizontal Scaling: Increase number of instances 😊 scale out / in)

* Auto Scaling Group
* Load Balancer

• High Availability:

* Run instances for the same application across multi AZ
* Auto Scaling Group multi AZ

## 70. Elastic Load Balancing (ELB) 
- ELB and Global Accelerator solve the challenge of routing user requests to healthy application endpoints.
-  AWS Global Accelerator relies on ELB to provide the traditional load balancing features such as support for internal and non-AWS endpoints, pre-warming, and Layer 7 routing. 
- Provides load balancing within one Region, AWS Global Accelerator provides traffic management across multiple Regions.
- Include
  - ALB
  - NLB
### Application Load Balancer (ALB)



## 72. ALT

* x-forward-for

## 73. ALB demo

* Create target group
* Practice load balancer

## 74

* Only allow access from ALB
* Define condition rule

## 78

* Sticky cooki

## 79 Cross zone Load Balancing

## 81 SSL Hand on

Add listener

## 83 Auto Scaling Group (ASG)

The goal of an Auto Scaling Group (ASG) is to:
• Scale out (add EC2 instances) to match an increased load
• Scale in (remove EC2 instances) to match a decreased load
• Ensure we have a minimum and a maximum number of EC2 instances running
• Automatically register new instances to a load balancer
• Re-create an EC2 instance in case a previous one is terminated (ex: if unhealthy)

 ![alt text](image-41.png)
Auto Scaling - CloudWatch Alarms & Scaling
• It is possible to scale an ASG based on CloudWatch alarms
• An alarm monitors a metric (such as Average CPU, or a custom metric)
• Metrics such as Average CPU are computed for the overall ASG instances

## 88. Rds red rplicas vs Multiaz

* Network Cost
  * not pay fee for RDS read Rplca winthin in same region
  * \

## 91

Features of Aurora
• Automatic fail-over
• Backup and Recovery
• Isolation and security
• Industry compliance
• Push-button scaling
• Automated Patching with Zero Downtime
• Advanced Monitoring
• Routine Maintenance
• Backtrack: restore data at any point of time without using backups

## 93

Auto

 ![alt tvsext](image-42.png)

## 98. Elastic Cache HandOn

* Security
   ![alt text](image-43.png)
  * Encryption Config
    * Transit
    * At rest
  * Security
* Cluster detail:
   ![alt text](image-44.png)
  * Primary Endpoint
  * Reader Endpoint

## 99. Elastic Cache for SA

*  ![alt text](image-46.png)
*  ![alt text](image-47.png)

## 101. Route 53








1. What is *DNS* and dd
   \[LINK\](This is a link)
   dns

## Question

* Subnet: Span all azs


 ![alt text](image-48.png)

* *DNS Record Time*:
   ![alt text](image-49.png)

   ![alt text](image-50.png)
* *Go to AWS Cloudshell*
  * sudo yum install -y bind-utils
  * nslookup  test.steahan...
  * dig

## 105 EC2 setup

* Create 3 EC2
* Create load balancer

## 106 TTL(Time to live)

* \

## 107. CNam and Alias

 ![alt text](image-51.png)

* Alias: Point hostname to aws resource
* CName not for apex record

## Route 53 
- Amazon Route 53 is a highly available and scalable cloud Domain Name System (DNS) web service. It is designed to give developers and businesses an extremely reliable and cost-effective way to route end users to Internet applications by translating names like www.example.com into the numeric IP addresses like 192.0.2.1 that computers use to connect to each other. Route 53 is ruled out as the company wants to continue using its own custom DNS service.

## 127 S3

* So3 looks like a global service but buckets are created in a region
* *Prefix* = Directory
*  ![alt text](image-52.png)
* Bucket
* Object
  * Metadata
  * Tags
  * Version ID(if enable)
* Default *encrytiokn*
  * SSE-S3
  * KMS

### S3 Security

- User base
  - Which url could use for specific user
- Resource Base
  - Bucket Policies: 
  - Object Access Controler LIst - Finer Grant
  - Bucket(ACL)

## 130 Bucket policy

* Use tool to generate policy

## Amazon S3 Transfer Acceleration(S3TA)
- enables fast, easy, and secure transfers of files over long distances between your client and an S3 bucket. 
- Takes advantage of *Amazon CloudFront’s globally distributed edge locations*.
- As the data arrives at an edge location, data is routed to Amazon S3 over an optimized network path.
- Pay only for transfer that are accelerated
## S3 – Requester Pays

* With Requester Pays buckets, the requester instead of the bucket owner pays the cost of the request and the data download from the bucket

## S3 - Access Point

* VPC Origin - *DNS Name*
* EC2 could create VPC Enpoint(Gateway or Interface Endpoint)


## 163 - S3 - Object Standard



## Cloudfront
- CDN service that securely delivers data, videos, applications, and APIs to customers globally with low latency, high transfer speeds, all within a developer-friendly environment.
- CloudFront points of presence (POPs) (edge locations) make sure popular content can be served quickly to your viewers.
- has regional edge caches that bring more of your content closer to your viewers, even when the content is not popular enough to stay at a POP, to help improve performance for that content.

### Origin failover feature

- support your data resiliency needs.
- If your content is not already cached in an edge location, 
    -> CloudFront retrieves it from an origin that you've identified as the source for the definitive version of the content.
#### 165 Cloudfront with S3

* Origin access
* Distribution

## 170. Global Accelator
- Utilizes the Amazon global network, allowing you to improve the performance of your applications by:
    1. lowering first-byte latency(the round trip time for a packet to go from a client to your endpoint and back again)
    2. jitter (the variation of latency)
    3. increasing throughput (the amount of time it takes to transfer data) as compared to the public internet
- Provides static IP addresses that act as a fixed entry point to your application endpoints in a single or multiple AWS Regions such as ALB, NLB, EC2 instances. 
- Improve wide range of app(TCP, UDP) by proxying packets at the edge to applications running in one or more AWS Regions.
- Global Accelerator is a good fit for non-HTTP use cases, such as gaming (UDP), IoT (MQTT), or Voice over IP, as well as for HTTP use cases that specifically require static IP addresses or deterministic, fast regional failover.
- AWS Global Accelerator and Amazon CloudFront are separate services that use the AWS global network and its edge locations around the world. CloudFront improves performance for both cacheable content (such as images and videos) and dynamic content (such as API acceleration and dynamic site delivery), while Global Accelerator improves performance for a wide range of applications over TCP or UDP.
- not help in accelerating the file transfer speeds into S3 for the given use-case.
- When go public internet - A lot of latency because there many hops
- Unicast IP: 1 server 1 IP
- Any Cast IP: Same Ip, client is routed to near on
- Global Accelator: Talk to closed Edge location -> Public ALP
- Create Private AWS network
- Perform healcheck for your app

# AWS Direct Connect
- Establish a dedicated network connection from your premises to AWS. 
- AWS Direct Connect lets you establish a dedicated network connection between your network and one of the AWS Direct Connect locations.
- With *AWS Direct Connect* plus *VPN*, you can combine one or more AWS Direct Connect dedicated network connections with the *Amazon VPC VPN*. This combination provides an *IPsec-encrypted private connection* that also reduces network costs, increases bandwidth throughput, and provides a more consistent network experience than internet-based VPN connections.
- Involves significant monetary investment and takes at least a month to set up, therefore it's not the correct fit for this use-case.

## AWS Transit Gateway
-  A network transit hub that you can use to interconnect your virtual private clouds (VPC) and on-premises networks. AWS Transit Gateway by itself cannot establish a low latency and high throughput connection between a data center and AWS Cloud.

## AWS site-to-site VPN
- AWS Site-to-Site VPN enables you to securely connect your on-premises network or branch office site to your Amazon Virtual Private Cloud (Amazon VPC). 
- A VPC VPN Connection utilizes IPSec to establish encrypted network connectivity between your intranet and Amazon VPC over the Internet. 
- VPN Connections are a good solution if you have an immediate need, have low to modest bandwidth requirements, and can tolerate the inherent variability in Internet-based connectivity. 
- However, Site-to-site VPN cannot provide low latency and high throughput connection, therefore this option is ruled out.


## AWS Snow Family

* Ops Hub
* Data transfer

- *AWS Snowball Edge Storage Optimized*: It provides up to 80 Terabytes of usable HDD storage, 40 vCPUs, 1 TB of SATA SSD storage, and up to 40 Gigabytes network connectivity to address large scale data transfer and pre-processing use cases.
- Snowmobile: 100 petabyte in one location

## Amazon FSx for Windows File Server
- provides all of the benefits of a native Windows SMB environment that is fully managed and secured and scaled like any other AWS service. You get detailed reporting, replication, backup, failover, and support for native Windows tools like DFS and Active Directory.
;'lopfdpgtikdcxojjgtkfidcncibdcl  support file shares in Amazon FSx for Windows File Server, so this option is incorrect.
- Amazon FSx File Gateway: low-latency, on-premises access to fully managed file shares in Amazon FSx for Windows File Server. For applications deployed on AWS, you may access your file shares directly from Amazon FSx in AWS
## 178 Storage gateway

* Block storage
* Object Storgae
* File gate
* NFS
* Active Story
* iScis
* *Volume Gateway*
  * Cached Volume
  * Stored Volumne:


### File gateway
- https://d1.awsstatic.com/cloud-storage/Amazon%20FSx%20File%20Gateway%20How%20It%20Works%20Diagram.edbf58e4917d47d04e5a5c22132d44bd92733bf5.png

- File Gateway does not support file shares in Amazon FSx for Windows File Server, so this option is incorrect.

## 187 SQS Fifo queue
- Limited throughput : 300 msg/s without batching, max: 10 message per operation = 3000 msg/s

## Kinesis Data Stream
- Ingest real-time data or streaming data at large scales.
- KDS can continuously capture gigabytes of data per second from hundreds of thousands of sources. 
- The data collected is available in milliseconds, enabling real-time analytics. 
- KDS provides ordering of records, as well as the ability to read and/or replay records in the same order to multiple Amazon Kinesis Applications.


## Firehose
- Ingest data and post to another source
  - S3
  - 

!- Delivery Stream:

## Analytics

## 218. Lambda
- run code without provisioning or managing servers. You pay only for the compute time that you consume—there’s no charge when your code isn’t running.
- currently supports 1000 concurrent executions per AWS account per region.
- If your Amazon SNS message deliveries to AWS Lambda contribute to crossing these concurrency quotas, your Amazon SNS message deliveries will be throttled. You need to contact AWS support to raise the account limit
- Integrates natively with Kinesis Data Streams. The polling, checkpointing, and error handling complexities are abstracted when you use this native integration. The processed data can then be configured to be saved in Amazon DynamoDB.
### 219. Lambda SnapStart

* For Java
* Snap start -> Function is preitnitize

## 225. Dynamodb Advanced Features

### DynamoDB Accelerator(DAX)

* *in- memory cache* for *DynamoDB*
* Help solve read congestion by caching
* Microseconds latency for cached data
* Doesn’t require application logic modification (compatible with existing DynamoDB APIs)
* 5 minutes TTL for cache (default)
   ![alt text](image-59.png)


### DynamoDB - Stream Processing

* Same Kinesis


### Global table

* Make a DynamoDB table accessible with low latency in multiple-regions
* Active-Active replication
* Applications can READ and WRITE to the table in any region
* Must enable DynamoDB Streams as a pre-requisite

  \


### TimeTolive

* Automatically delete items after an expiry timestamp
* Use cases: reduce stored data by keeping only current items, adhere to regulatory obligations, web session handling...


## API GATEWAY
- Amazon API Gateway to create, publish, maintain, monitor, and secure APIs at any scale. 
- APIs act as the front door for applications to access data, business logic, or functionality from your backend services. 
- Using API Gateway, you can create RESTful APIs and WebSocket APIs that enable real-time two-way communication applications.
  
* Endpoint Type:
  * Edge-Optimize(default): For global clients
  * Regional:
  * Private:  
* *Security*: 
  * IAM Role
  * Cognito
  * Custom Authorize(Lamda)
* How to API gateway work:
![alt text](image-73.png)


## Choosing right database
- *RDBMS (SQL/OLTP)* - Great for joins
  - RDS
  - Aurora 
- *NoSQL database* - no joins, no SQL
  - DynamoDB(~JSON)
  - ElasticCache(Key/Value Paris)
  - Neptune(graphs)
  - DocumentDB(For MogoDB)
- *Object Store*: 
  - S3(for big objects)
  - Glacier(for backups/chive)
- **Data Warehouse**(SQL Analytics / BI)
  + Reshift(OLAP)
  + Athena
  + EMR
- *Search*: 
  - OpenSearch(Json) - free text, unstructured search
- *Graphs*: Amazone Neptune - displays relationships between data
- *Ledger*: Amazone Quantum Ledger Database
- *Time series:* AmazonTimestream

## RDS 

- Managed Postgres / Mysql / Oracle / SQL Server / DB2 / MariaDB
- Provision
  - Rds Instace Size and EBS VolumneType & size
- Auto-scaling for storage
- Support 
  - Read Replicas
  - Multi AZ
- Security
  - IAM
  - Security Group
  - KMS
  - SSL in transit
- Auotmated Backup with Point in time restore feature(35 days)
- Manual DB Snapshot for longer-term recoverry
- Support IAM Authentication, integration with Secrets Manager

- ![alt text](image-63.png)
## 236 - Aurora 
- 
- Compatilbe API for Post
- Store in 6 replica - 3 AZ
- Cluster: Customer endopint for writer and reader DB instaces
- Aurora Serverless
- Aurora Global: 
- Aurora Machine Learning: Perfrm ML using SageMaker & Comprehend on Aurora
### Aurora Replica
- *Purpose*
  - Scale read operations of your app(reader endpoint) -> Increase avaibility
  - If the writer instance becomes unavailable, automatically promotes one of the reader instances to take its place as the new write 
  - Up to 15 Aurora Replicas xacross the Availability Zones (AZs) tha DB cluster spans within an AWS Region.
## Amazone Elasticache - Summanry

- Managed Redis / Memchaed
- In-memory datastore, sub-milisecond latency
- Support for Clustering(Redis) and Multi Az, 

## Dynamo DB - Summary
- Can replace ElastiCahe as a key/value store
- Highly Available, Multi Az by default
- DAX cluster for reading cache 
- Event Processing: DynamoDB Streaam to integrate with AWS Lamda, or Kinesis Data Streams
- Global Table feature: active-ative setup
- Export to S3

## S3 - Lifecycle transtion
[- ![alt text](image-74.png)](https://docs.aws.amazon.com/images/AmazonS3/latest/userguide/images/lifecycle-transitions-v4.png)
## S3 - Storage Classes
### S3 One Zone-IA
- Amazon S3 One Zone-IA is for 
  - data that is accessed less frequently, 
  - requires rapid access when needed. 
- Other S3 Storage Classes which store data in a minimum of three Availability Zones (AZs), IA stores data in a single Availability Zone (AZ) and costs 20% less than Standard-IA. 
- One Zone-IA is ideal for customers want a lower-cost option for infrequently accessed and re-creatable data but do not require the availability and resilience of Standard or Standard-IA. 
- The minimum storage duration is *30 days* before you can transition objects from Standard to One Zone-IA.

## Amazon Simple Notification Service(SNS)
- A highly available, durable, secure, fully managed pub/sub messaging service.
- Enables you to decouple 
  - microservices
  - distributed systems
  - serverless applications.
- Fully dynamically server - dynamically scale with your application

## S3

- A key/value store for objects
- Great for bigger objects, not so greate for many small object
- Serverless, scale infinitely, max object size if 5 TB, versioning capacity
- Tiers: S3 Standard, S3 Infrequent Access, S3 Intelligent, S3 Galcier + Life Cycle Policty
- Security SSE-S3, SSE-KMS, SSE-C, TLS in trasit, default ecnrtypion
- Batch Operation on objects using S3 Batch, Listing file using S3 repository
- Performanace: Moti-part upload, S3 Tranfer Accelator, S3 Seelct
- Automation: S3 Event Notification(SNS, SQS, Lambda, EventBride)

## DocumentDB
- Aurora is an "AWS-IMplementation" of PostgreSQL/SQL
- DocumentDB is the same for MongoDB(No SQL DB)

- MonggoDB is sued to store, query and index  JSON Data
- Similiar "deployment concepts" as Aurora
- Fully Managed, hightly available with replication aross 3 AZ
- Auto grows of 10 GB
- Automatically scales to workloads 

## Neptune
- Fully managed graph database
- Higly available with repliactions across multiple AZs
- Great for 
  - knowledge graphs(Wikipedia)
  - Fraud detection
  - Recommedation egnines
  
## Keyspace 
- For apache Casandra
- Using 

## Amazon QLDB
- Stand for Quantum Ledger Database
- Ledger is a book recording financial Transactions
- Review history of all chanages made to your app
- Immutable system 
- Difference with Amazone Managed Blockchain: No decentralization component

## 244 Timestream
- Time series database
- Automatically Scales up/down 
- Faster and cheaper


## 245 Amazon athena
- Severless query service to analyze data in S3
- SQL language(Build in Presto)
- Support CSV, Json, ORC, AVRO, Parquet
- 5 USD per TB
- With Amazone Quicksight
- Use case
  - BI
  - Analytic
  - Report & Analytic & Query VPC Flow Logs, ELB Logs, CloudTrail trails,
- Improve performance
  - Column data for cost saving
    - Apache Parquet is recomment
    - Huge Performace Improvement
    - Use glue to convert to Parquet or ORC
- Compress data for retrivil
- Partion datasets in S3
- Use larger file
- *Federated query*:
  - Allow to run query on AWS or on premise
  - Store result back in S3

## REDSHIFT
- Is base on PostgresSQL but not use for Online Tracsactio Processing
- For OLAP(Online Analytic Processing)
- Should load the data(From Kinesis Firehose)
- Ingest data to redshiff
  - Firehose -> Write S3 ->  S3 Copy -> RedShift
- EC2 -> Redshift by JDBC Driver
- *Reshift Spectrum*: Query data is already in S3 without loading it.

## 248 Open Search
- Succesor to Elastic Search
- On DynamoDB, queries only exist by primary key or indexs
- Could search any field
- Two mode: Managed Cluster or Serverless cluster
- *Security*: Cognito, IAM Role
- Have OpenSearch Dashboard
- OpenSearch Patterns DynamoDB
  - DymamoDB Table -> DynamoDB Stream -> Lambda Function -> OpenSearch -> Search for Item Name -> Retrive ID -> Search Full Item in DynamoDB
- ![alt text](image-65.png)

- OpenSearch Patterns Clouwatch Logs
  - ![alt text](image-66.png)

- OpenSearch Pattern Kisesis DataStream and FireHorse
- ![alt text](image-67.png)

## 249 EMR

- Stand for *Elastic MapReduce*
- Create Hadoop cluster(Bigdata) -> analyze & process vast amount data
- The clusters can be made of hundreds of EC2 instances
- takes care of all the provisioning and configuration
- Use cases: data processing, machine learning, web indexing, big data...
- Master Node: Manage the cluster
- Core Node: Run task and store data
- Task Note(optional)
- Purchasing Options
  - On Demand
  - Reserverd
  - Spot Intances
## 250 Quick Sight
- Severless machine learning BI Service create interative Dashboar
- Use cases:
  - Business analytics
  - Building visualizations
  - Perform ad-hoc analysis
  - Get business insights using data
- Integrated with RDS, Aurora, Athena, Redshift, S3...
- In-memory computation using SPICE engine if data is imported into QuickSight
- Enterprise edition: Possibility to setup Column-Level security (CLS)

## 251 Glue
- Serverless ETL service
- Prepare vs Tranform data for analytics
![alt text](image-68.png)
- Convert data into Parquet Format
![alt text](image-69.png)
- Glue Data Catalog:
- Glue Job Bookmarks: prevent re-processing old data
- Glue Elastic Views
  - Combine and replicate data across lultiple data stores using SQL

- Glue DataBew: Clean and nomalize data using prebuild tranformerm
- Glue Studio: new GUI to create, run and monitor ETL jobs in Glue
- Glue Streaming ETL (built on Apache Spark Structured Streaming): compatible with Kinesis Data Streaming, Kafka, MSK (managed Kafka)

## 252 AWS Lake Formation
- Data lake = central palce to have all your data for analytics purpose
- Easy to setup data lake in days
- It automates many complex manual steps(Collecting, cleansing, moveing, catloging data) and de-duplicate
- Combine Structured and untructured data in datalake
- S3, Rds, Relation & NoSql DB.
- Fine-grained access control
- Build on to of AWS Blue
- ![alt text](image-70.png)
- Many place in setup security

## 314 Amazon GuardDuty
- Intelligent Threat discover y to protect your AWS Account
- Uses Machine Learning algorithms, anomaly detection, 3rd party data
- Input data includes:
  - CloudTrail Events Logs – unusual API calls, unauthorized deployments
    - CloudTrailManagementEvents - createVPCsubnet,createtrail,... 
    - CloudTrailS3DataEvents–getobject,listobjects,deleteobject,...
  - VPC Flow Logs – unusual internal traffic, unusual IP address
  - DNS Logs – compromised EC2 instances sending encoded data within DNS queries 
  - Optional Features: EKS Audit Logs, RDS & Aurora, EBS, Lambda, S3 Data Events...
  - Can setup EventBridge rules to be notified in case of findings
  - ![alt text](image-71.png)
  - ![alt text](image-72.png)

  ## Task
  - Review cloudfront, global accelator