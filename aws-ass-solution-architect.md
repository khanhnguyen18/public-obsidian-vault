# AWS Solution Architect

## Link

```shell
open "/Users/P836088/project/markdown-documents/work/AWS/AWS-Certified-Solutions-Architect-Slides-v37.pdf"
```

## 11. IAM

- Global service
- Root account use
- Policies is define permission of user
- Apply least previledge principle


## 13. IAM Role
- AWS supports six types of policies: 
  1. identity-based policies
  2. resource-based policies,
  3. permissions boundaries, 
  4. service control policy (SCP)of AWS Organizations,
  5. access control list (ACL), 
  6. session policies.


### AWS_IAM_Authorization
 - For consumers who currently are located within your AWS environment or have the means to retrieve (IAM) temporary credentials to access your environment, you can use AWS_IAM authorization and add least-privileged permissions to the respective IAM role to securely invoke your API.
 - API Gateway API Keys is not a security mechanism and should not be used for authorization unless it’s a public API. 
 - It should be used primarily to track a consumer’s usage across your API.

## Section 5

### 30. AWS Budget setup


## ECS
- fully managed container orchestration service. ECS allows you to easily run, scale, and secure Docker container applications on AWS.
  ![](https://d1.awsstatic.com/Product-Page-Diagram_Amazon-Elastic-Container-Service%20march%202023.6ee17a3146661f893bf1ee674aceb65efdf864bd.png)
- With the Fargate launch type, you pay for the amount of vCPU and memory resources that your containerized application requests. vCPU and memory resources are calculated from the time your container images are pulled until the Amazon ECS Task terminates, rounded up to the nearest second.
- With the EC2 launch type, there is no additional charge for the EC2 launch type. You pay for AWS resources (e.g. EC2 instances or EBS volumes) you create to store and run your application.

## Amazon Inspector
- security assessments help you check for unintended network accessibility of your Amazon EC2 instances and for vulnerabilities on those EC2 instances.
-  Amazon Inspector assessments are offered to you as pre-defined rules packages mapped to common security best practices and vulnerability definitions.

## WAF
![](https://d1.awsstatic.com/products/WAF/product-page-diagram_AWS-WAF_How-it-Works@2x.452efa12b06cb5c87f07550286a771e20ca430b9.png)
- a web application firewall service that lets you monitor web requests and protect your web applications from malicious requests.
- Use AWS WAF to block or allow requests based on conditions that you specify, such as the IP addresses.
- You can also use AWS WAF preconfigured protections to block common attacks like SQL injection or cross-site scripting.
- You can use AWS WAF with your Application Load Balancer to allow or block requests based on the rules in a web access control list (web ACL). Geographic (Geo) Match Conditions in AWS WAF allows you to use AWS WAF to restrict application access based on the geographic location of your viewers. With geo match conditions you can choose the countries from which AWS WAF should allow access.
- Geo match conditions are important for many customers. For example, legal and licensing requirements restrict some customers from delivering their applications outside certain countries. These customers can configure a whitelist that allows only viewers in those countries. Other customers need to prevent the downloading of their encrypted software by users in certain countries. These customers can configure a blacklist so that end-users from those countries are blocked from downloading their software.
## 31. EC2
### EC2_Hibernate
- When you hibernate an instance, AWS signals the operating system to perform hibernation (suspend-to-disk).
-  Hibernation saves the contents from 
   -  the instance memory (RAM) to your Amazon EBS root volume. 
-  AWS then persists the instance's Amazon EBS root volume and any attached Amazon EBS data volumes.
- When you start your instance:
  - The Amazon EBS root volume is restored to its previous state
  - The RAM contents are reloaded
  - The processes that were previously running on the instance are resumed

Previously attached data volumes are reattached and the instance retains its instance ID

![Link](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/images/hibernation-flow.png)
### EC2 - Placement Group
- Depending on the type of workload, you can create a placement group using one of the following placement strategies:
  - Cluster - Packs instances close together inside an Availability Zone. This strategy enables workloads to achieve the low-latency network performance necessary for tightly-coupled node-to-node communication that is typical of high-performance computing (HPC) applications.
  - Partition:
    - do not share underlying harware with groups intance(Kafka, Hadoop , Cassandra)
    - A partition placement group can have a maximum of seven partitions per Availability Zone
  - Spead: Strictly place small group of intances accross distince underlying harware to reduce correlated failures.
- More information: https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/placement-groups.html

  ### EC2 - Intance store
- Provides temporary block-level storage for your instance.
- This storage is located on disks that are physically attached to the host instance.
- Instance store is ideal for the temporary storage of information that changes frequently such as buffers, caches, scratch data, and other temporary content, or for data that is replicated across a fleet of instances, such as a load-balanced pool of web servers.
- Instance store volumes are included as part of the instance's usage cost.

As Instance Store based volumes provide high random I/O performance at low cost (as the storage is part of the instance's usage cost) and the resilient architecture can adjust for the loss of any instance, therefore you should use Instance Store based Amazon EC2 instances for this use-case.
- Instance store is ideal for the temporary storage of information that changes frequently such as buffers, caches, scratch data, and other temporary content, or for data that is replicated across a fleet of instances, such as a load-balanced pool of web servers
### EC2 - Pricing
- https://aws.amazon.com/ec2/pricing/


### EC2 - Type of instace
1. Dedicated Hosts
  - A Dedicated Host is a physical EC2 server fully dedicated for your use. Dedicated Hosts can help you reduce costs by allowing you to use your existing server-bound software licenses, including Windows Server, SQL Server, and SUSE Linux Enterprise Server (subject to your license terms). Dedicated Hosts can be purchased On-Demand (hourly) or can be purchased as part of Savings Plans.
2. On-Demand
3. Dedicated Intance 
Physical server that's dedicated to a single customer account.
4. Reserve intance
  
### 32.

## 57

* EBS snapshot archive: 75% cheaper

## EBS
- Amazon EBS volume types fall into two categories:
  1. Solid state drive (SSD) backed volumes optimized for transactional workloads involving frequent read/write operations with small I/O size, where the dominant performance attribute is IOPS.
  2. Hard disk drive (HDD) backed volumes optimized for large streaming workloads where throughput (measured in MiB/s) is a better performance measure than IOPS.
- You can't use st1 or sc1 EBS volumes as root volumes.
## EFS
![](https://d1.awsstatic.com/r2018/b/EFS/product-page-diagram-Amazon-EFS-Launch_How-It-Works.cf947858f0ef3557b9fc14077bdf3f65b3f9ff43.png)
- Provides a simple, scalable, fully managed *Elastic NFS file system* for use with
  -  AWS Cloud services
  -  On-premises resources.
  
- EFS is a **file storage service** for use 
  - Amazon compute (EC2, containers, serverless) 
  - on-premises servers. 
- Amazon EFS provides:
  - a file system interface
  - file system access semantics (such as strong consistency and file locking), 
  - concurrently accessible storage for up to thousands of Amazon EC2 instances.

- Storing data within and across multiple Availability Zones (AZs) for high availability and durability
- EC2 instances can access your file system across AZs, regions, and VPCs
- On-premises servers can access using AWS Direct Connect or AWS VPN.

### Efs_Standard_Ia
- Standard–IA storage class reduces storage costs for files that are not accessed every day.
- It does this without sacrificing the high availability, high durability, elasticity, and POSIX file system access that Amazon EFS provides. 
- AWS recommends Standard-IA storage if you need your full dataset to be readily accessible and want to automatically save on storage costs for files that are less frequently accessed.

### Efs_Infrequent_Access
- Storage class that provides price/performance that is cost-optimized for files, not accessed every day, with storage prices up to **92% lower compared to Amazon EFS Standard**
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
- The Application Load Balancer (ALB) is best suited for load balancing HTTP and HTTPS traffic and provides advanced request routing targeted at the delivery of modern application architectures, including microservices and containers. Operating at the individual request level (Layer 7), the Application Load Balancer routes traffic to targets within Amazon Virtual Private Cloud (Amazon VPC) based on the content of the request.
- This is the correct option since the question has a specific requirement for content-based routing which can be configured via the Application Load Balancer. Different Availability Zones (AZs) provide high availability to the overall architecture and Auto Scaling group will help mask any instance failures.

#### Content-Based Routing
- ALB has access to HTTP headers and allows you to route requests to different backend services accordingly.
- For example, you might want to send requests that include /api in the URL path to one group of servers (we call these target groups) and requests that include /mobile to another.
- Routing requests in this fashion allows you to build applications that are composed of multiple microservices that can run and be scaled independently.
- As you will see in a moment, each Application Load Balancer allows you to define up to 10 URL-based rules to route requests to target groups. Over time, we plan to give you access to other routing methods.


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
## Private_Link
- Simplifies the security of data shared with cloud-based applications by eliminating the exposure of data to the public Internet. 
- Provides private connectivity between VPCs, AWS services, and on-premises applications, securely on the Amazon network. Private Link is a distractor in this question. 
- Private Link is leveraged to create a private connection between an application that is fronted by an NLB in an account, and ENI in another account, without the need of VPC peering and allowing the connections between the two to remain within the AWS network.

## AWS_Config
- ![AWS_Config](https://assets-pt.media.datacumulus.com/aws-saa-pt/assets/pt2-q9-i2.jpg)
- provides a detailed view of the configuration of AWS resources in your AWS account. This includes how the resources are related to one another and how they were configured in the past so that you can see how the configurations and relationships change over time.
- AWS Config provides AWS-managed rules, which are predefined, customizable rules that AWS Config uses to evaluate whether your AWS resources comply with common best practices. You can leverage an AWS Config managed rule to check if any ACM certificates in your account are marked for expiration within the specified number of days. Certificates provided by ACM are automatically renewed. ACM does not automatically renew the certificates that you import. The rule is NON_COMPLIANT if your certificates are about to expire.
## AWS_Certificate_Manager
- service that lets you easily provision, manage, and deploy public and private SSL/TLS certificates for use with AWS services and your internal connected resources. 
- SSL/TLS certificates are used to secure network communications and establish the identity of websites over the Internet as well as resources on private networks.

## AWS_Transit_Gateway
Is a service that enables customers to connect their Amazon Virtual Private Clouds (VPCs) and their on-premises networks to a single gateway

## VPC_Peering
A VPC peering connection is a networking connection between two VPCs that enables you to route traffic between them using private IPv4 addresses or IPv6 addresses. Instances in either VPC can communicate with each other as if they are within the same network. You can create a VPC peering connection between your VPCs, or with a VPC in another AWS account. The VPCs can be in different regions (also known as an inter-region VPC peering connection). VPC peering connections will work, but won't efficiently scale if you add more accounts (you'll have to create many connections).
## RAM
![RAM](https://d1.awsstatic.com/products/RAM/product-page-diagram_AWS-Resource-Access-Manager(1).379df75d48a8e2cc6160859b7ca3626a9b9be0c1.png)
- AWS Resource Access Manager (RAM) is a service that enables share AWS resources with 
  - any AWS account 
  - within your AWS Organization. 
- You can share:
  - AWS Transit Gateways
  - Subnets
  - AWS License Manager configurations
  - Amazon Route 53 Resolver rules resources with RAM. 
- RAM eliminates the need to create duplicate resources in multiple accounts, reducing the operational overhead of managing those resources in every single account you own.
-  You can create resources centrally in a multi-account environment, and use RAM to share those resources across accounts in three simple steps: 
   -  create a Resource Share
   -  Specify resources
   -  Specify accounts. 
-  RAM is available to you at no additional charge.
## 83 Auto Scaling Group (ASG)

The goal of an Auto Scaling Group (ASG) is to:
• Scale out (add EC2 instances) to match an increased load
• Scale in (remove EC2 instances) to match a decreased load
• Ensure we have a minimum and a maximum number of EC2 instances running
• Automatically register new instances to a load balancer
• Re-create an EC2 instance in case a previous one is terminated (ex: if unhealthy)

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

## 98. Elastic Cache HandOn

* Security
  * Encryption Config
    * Transit
    * At rest
  * Security
* Cluster detail:
  * Primary Endpoint
  * Reader Endpoint

## 99. Elastic Cache for SA


## 101. Route 53








1. What is DNS and dd
   \[LINK\](This is a link)
   dns

## Question

* Subnet: Span all azs



* DNS Record Time:

* Go to AWS Cloudshell
  * sudo yum install -y bind-utils
  * nslookup  test.steahan...
  * dig

## 105 EC2 setup

* Create 3 EC2
* Create load balancer

## 106 TTL(Time to live)

## 107. CNam and Alias

* Alias: Point hostname to aws resource
* CName not for apex record

## Route 53
- Amazon Route 53 is a highly available and scalable cloud Domain Name System (DNS) web service. It is designed to give developers and businesses an extremely reliable and cost-effective way to route end users to Internet applications by translating names like www.example.com into the numeric IP addresses like 192.0.2.1 that computers use to connect to each other. Route 53 is ruled out as the company wants to continue using its own custom DNS service.
### Routing Policy
#### Lantency Routing 
#### Failover Routing
#### Geolocation Routing


## Security Group
- A security group acts as a virtual firewall that controls the traffic for one or more instances. 
- When you launch an instance, you can specify one or more security groups; otherwise -> default security group.
- Add rules to each security group that allows traffic to or from its associated instances.
- Modify the rules for a security group at any time; the new rules -> applied to all instances that are associated with the security group. 
*The following are the characteristics of security group rules*:
- By default, security groups allow all outbound traffic.
- Security group rules are always permissive; you can't create rules that deny access.
- Security groups are stateful

- [ec2-security-groups](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-security-groups.html)




## 127 S3

* So3 looks like a global service but buckets are created in a region
* Prefix = Directory
* Bucket
* Object
  * Metadata
  * Tags
  * Version ID(if enable)
* Default encrytiokn
  * SSE-S3
  * KMS

### S3 Security

- User base
  - Which url could use for specific user
- Resource Base
  - Bucket Policies:
  - Object Access Controler LIst - Finer Grant
  - Bucket(ACL)

## KMS
- AWS Key Management Service (AWS KMS) is a service that combines secure, highly available hardware and software to provide a key management system scaled for the cloud. When you use server-side encryption with AWS KMS (SSE-KMS), you can specify a customer-managed CMK that you have already created. SSE-KMS provides you with an audit trail that shows when your CMK was used and by whom. Therefore SSE-KMS is the correct solution for this use-case.
- AWS Key Management Service (KMS) makes it easy for you to create and manage cryptographic keys and control their use across a wide range of AWS services and in your applications. AWS KMS is a secure and resilient service that uses hardware security modules that have been validated under FIPS 140-2.
- Deleting an AWS KMS key in AWS Key Management Service (AWS KMS) is destructive and potentially dangerous. Therefore, AWS KMS enforces a waiting period. To delete a KMS key in AWS KMS you schedule key deletion. You can set the waiting period from a minimum of 7 days up to a maximum of 30 days. The default waiting period is 30 days. During the waiting period, the KMS key status and key state is Pending deletion. To recover the KMS key, you can cancel key deletion before the waiting period ends. After the waiting period ends you cannot cancel key deletion, and AWS KMS deletes the KMS key.
- KMS is global or not?

### Automatic key rotation 

## Cognito
### Cognito_User_Pools
- A user pool is a `user directory` in Amazon Cognito. You can leverage Amazon Cognito User Pools to either provide built-in user management or integrate with external identity providers, such as Facebook, Twitter, Google+, and Amazon. 
- Whether your users sign-in directly or through a third party, all members of the user pool have a directory profile that you can access through a Software Development Kit (SDK).

User pools provide: 
1. Sign-up and sign-in services. 
2. A built-in, customizable web UI to sign in users. 
3. Social sign-in with Facebook, Google, Login with Amazon, and Sign in with Apple, as well as sign-in with SAML identity providers from your user pool. 
4. User directory management and user profiles. 5
5. Security features such as multi-factor authentication (MFA), checks for compromised credentials, account takeover protection, and phone and email verification. 
6. Customized workflows and user migration through AWS Lambda triggers.

After creating an Amazon Cognito user pool, in API Gateway, you must then create a COGNITO_USER_POOLS authorizer that uses the user pool.
![Identity](https://assets-pt.media.datacumulus.com/aws-saa-pt/assets/pt2-q24-i1.jpg
)

### Cognito_User_Identity
- Identity pools provide AWS credentials to grant your users access to other AWS services.
- To enable users in your user pool to access AWS resources, you can configure an identity pool to exchange user pool tokens for AWS credentials.

## 130 Bucket policy

* Use tool to generate policy

## S3 Transfer Acceleration(S3TA)
- enables fast, easy, and secure transfers of files over long distances between your client and an S3 bucket.
- Takes advantage of Amazon CloudFront’s globally distributed edge locations.
- As the data arrives at an edge location, data is routed to Amazon S3 over an optimized network path.
- Pay only for transfer that are accelerated
## S3 - Multipart Upload
- Multipart upload allows you to upload a single object as a set of parts.
- Each part is a contiguous portion of the object's data. You can upload these object parts independently and in any order.
-  If transmission of any part fails, you can retransmit that part without affecting other parts.
-  After all parts of your object are uploaded, Amazon S3 assembles these parts and creates the object.
-   If you're uploading large objects over a stable high-bandwidth network, use multipart uploading to maximize the use of your available bandwidth by uploading object parts in parallel for multi-threaded performance.
-  If you're uploading over a spotty network, use multipart uploading to increase resiliency to network errors by avoiding upload restarts.
## S3 – Requester Pays

* With Requester Pays buckets, the requester instead of the bucket owner pays the cost of the request and the data download from the bucket

## S3 - Access Point

* VPC Origin - DNS Name
* EC2 could create VPC Enpoint(Gateway or Interface Endpoint)


## 163 - S3 - Object Standard



## Cloudfront
- CDN service that securely delivers data, videos, applications, and APIs to customers globally with low latency, high transfer speeds, all within a developer-friendly environment.
- CloudFront points of presence (POPs) (edge locations) make sure popular content can be served quickly to your viewers.
- has regional edge caches that bring more of your content closer to your viewers, even when the content is not popular enough to stay at a POP, to help improve performance for that content.
- You can use different origins for different types of content on a single site – e.g. Amazon S3 for static objects, Amazon EC2 for dynamic content, and custom origins for third-party content.


### Origin failover feature

- support your data resiliency needs.
- If your content is not already cached in an edge location,
  -> CloudFront retrieves it from an origin that you've identified as the source for the definitive version of the content.
#### 165 Cloudfront with S3

* Origin access
* Distribution

## 170. Global Accelerator
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
- Global Accelerator: Talk to closed Edge location -> Public ALP
- Create Private AWS network
- Perform healcheck for your app

## AWS Direct Connect
- Establish a dedicated network connection from your premises to AWS.
- AWS Direct Connect lets you establish a dedicated network connection between your network and one of the AWS Direct Connect locations.
- With AWS Direct Connect plus VPN, you can combine one or more AWS Direct Connect dedicated network connections with the Amazon VPC VPN. This combination provides an IPsec-encrypted private connection that also reduces network costs, increases bandwidth throughput, and provides a more consistent network experience than internet-based VPN connections.
- Involves significant monetary investment and takes at least a month to set up, therefore it's not the correct fit for this use-case.

## AWS Transit Gateway
-  A network transit hub that you can use to interconnect your virtual private clouds (VPC) and on-premises networks. AWS Transit Gateway by itself cannot establish a low latency and high throughput connection between a data center and AWS Cloud.

## AWS site-to-site VPN
- Enables you to securely connect your ~on-premises~ network or branch office site to your Amazon VPC.
- Utilizes protocol security(IPSec) to establish encrypted network connectivity between your intranet and Amazon VPC over the Internet.
- VPN Connections are a good solution if you have an immediate need, have low to modest bandwidth requirements, and can tolerate the inherent variability in Internet-based connectivity.
- However, Site-to-site VPN cannot provide low latency and high throughput connection, therefore this option is ruled out.
## AWS Snow Family
* Ops Hub
* Data transfer

- AWS Snowball Edge Storage Optimized: It provides up to 80 Terabytes of usable HDD storage, 40 vCPUs, 1 TB of SATA SSD storage, and up to 40 Gigabytes network connectivity to address large scale data transfer and pre-processing use cases.
- Snowmobile: 100 petabyte in one location
## AWS Directory Service for Microsoft Active Directory (AWS Managed Microsoft AD)
AWS Directory Service for Microsoft Active Directory, also known as AWS Managed Microsoft AD, enables your directory-aware workloads and AWS resources to use managed Active Directory in the AWS Cloud.
## Amazon FSx for Lustre
Makes it easy and cost-effective to launch and run the world’s most popular high-performance file system.
- It is used for workloads such as machine learning, high-performance computing (HPC), video processing, and financial modeling.
- The open-source Lustre file system is designed for applications that require fast storage – where you want your storage to keep up with your compute.
- FSx for Lustre integrates with Amazon S3, making it easy to process data sets with the Lustre file system. When linked to an S3 bucket, an FSx for Lustre file system transparently presents S3 objects as files and allows you to write changed data back to S3.

## Amazon FSx for Windows File Server
- Amazon FSx for Windows File Server provides fully managed, highly reliable file storage that is accessible over the industry-standard Service Message Block (SMB) protocol. It is built on Windows Server, delivering a wide range of administrative features such as user quotas, end-user file restore, and Microsoft Active Directory (AD) integration. FSx for Windows does not allow you to present S3 objects as files and does not allow you to write changed data back to S3. Therefore you cannot reference the "cold data" with quick access for reads and updates at low cost. Hence this option is not correct.
-
- provides all of the benefits of a native Windows SMB environment that is fully managed and secured and scaled like any other AWS service. You get detailed reporting, replication, backup, failover, and support for native Windows tools like DFS and Active Directory.
- support file shares in Amazon FSx for Windows File Server, so this option is incorrect.
- Amazon FSx File Gateway: low-latency, on-premises access to fully managed file shares in Amazon FSx for Windows File Server. For applications deployed on AWS, you may access your file shares directly from Amazon FSx in AWS
- ![](https://d1.awsstatic.com/r2018/b/FSx-Windows/FSx_Windows_File_Server_How-it-Works.9396055e727c3903de991e7f3052ec295c86f274.png)
## 178 Storage gateway
- A hybrid cloud storage service that gives you on-premises access to virtually unlimited cloud storage.
- types of gateways
  - Tape Gateway
    - allows moving tape backups to the cloud.
  - File Gateway
    - offer ~SMB~ or ~NFs~ in S3 with local catching
  - Volume Gateway
    - Present cloud-based iSCSI block storage volumes to your on-premises applications.
- that seamlessly connect on-premises applications to cloud storage, caching data locally for low-latency access.
- ~Ref~
  - [Link](https://docs.aws.amazon.com/storagegateway/latest/userguide/StorageGatewayConcepts.html)

### File gateway
- https://d1.awsstatic.com/cloud-storage/Amazon%20FSx%20File%20Gateway%20How%20It%20Works%20Diagram.edbf58e4917d47d04e5a5c22132d44bd92733bf5.png

- File Gateway does not support file shares in Amazon FSx for Windows File Server, so this option is incorrect.

## 187 SQS Fifo queue
- Limited throughput : 300 msg/s without batching, max: 10 message per operation = 3000 msg/s

## Kinesis_Data_Stream
-  Amazon Kinesis Data Streams (KDS) is a massively scalable and durable real-time data streaming service. 
-  The throughput of an Amazon Kinesis data stream is designed to scale without limits via increasing the number of shards within a data stream. 

- Enables real-time processing of streaming big data.
- It provides ordering of records, as well as the ability to read and/or replay records in the same order to multiple Amazon Kinesis Applications.
- The Amazon Kinesis Client Library (KCL) delivers all records for a given partition key to the same record processor, making it easier to build multiple applications reading from the same Amazon Kinesis data stream (for example, to perform counting, aggregation, and filtering).
- ~Recomment~
  1. *Routing related records to the same record processor* (as in streaming MapReduce). For example, counting and aggregation are simpler when all records for a given key are routed to the same record processor.
  2. *Ordering of records*. For example, you want to transfer log data from the application host to the processing/archival host while maintaining the order of log statements.
  3. *Ability for multiple applications to consume the same stream concurrently*. For example, you have one application that updates a real-time dashboard and another that archives data to Amazon Redshift. You want both applications to consume data from the same stream concurrently and independently.
  4. *Ability to consume records in the same order a few hours later*. For example, you have a billing application and an audit application that runs a few hours behind the billing application. Because Amazon Kinesis Data Streams stores data for up to 365 days, you can run the audit application up to 365 days behind the billing application.

- Kinesis Data Streams cannot directly write the output to Amazon S3. Unlike Amazon Kinesis Data Firehose, KDS does not offer a ready-made integration via an intermediary AWS Lambda function to reliably dump data into Amazon S3

- Ingest real-time data or streaming data at large scales.
- KDS can continuously capture gigabytes of data per second from hundreds of thousands of sources.
- The data collected is available in milliseconds, enabling real-time analytics.
- KDS provides ordering of records, as well as the ability to read and/or replay records in the same order to multiple Amazon Kinesis Applications.

- Only Cloudwatch and S3 buck could ingest data(not AWS CloudTrail)

## Firehose
- the easiest way to **load streaming data** into 
  - data stores 
  - analytics tools
  - data lakes
- It can capture, transform, and load streaming data into:
  -  Amazon S3
  -  Amazon Redshift
  -  Amazon OpenSearch Service
  -  Splunk
- Enabling near real-time analytics
- It is a fully managed service that automatically scales to match the throughput of your data and requires no ongoing administration.
- It can also batch, compress, and encrypt the data before loading it
  - -> minimizing the amount of storage used at the destination and increasing security.
- ![Overview](https://d1.awsstatic.com/pdp-how-it-works-assets/product-page-diagram_Amazon-KDF_HIW-V2-Updated-Diagram@2x.6e531854393eabf782f5a6d6d3b63f2e74de0db4.png)
## Analytics
- Amazon Kinesis Data Analytics is the easiest way to analyze streaming data in real-time. Kinesis Data Analytics enables you to easily and quickly build queries and sophisticated streaming applications in three simple steps:
- setup your streaming data sources
- write your queries or streaming applications
- set up your destination for processed data.
- Kinesis Data Analytics cannot directly ingest data from the source as it ingests data either from
  - Kinesis Data Streams
  - Kinesis Data Firehose


## 218. Lambda
- run code without provisioning or managing servers. You pay only for the compute time that you consume—there’s no charge when your code isn’t running.
- currently supports 1000 concurrent executions per AWS account per region.
- If your Amazon SNS message deliveries to AWS Lambda contribute to crossing these concurrency quotas, your Amazon SNS message deliveries will be throttled. You need to contact AWS support to raise the account limit
- Integrates natively with Kinesis Data Streams. The polling, checkpointing, and error handling complexities are abstracted when you use this native integration. The processed data can then be configured to be saved in Amazon DynamoDB.
### 219. Lambda SnapStart

* For Java
* Snap start -> Function is preitnitize

## Amazon ElastiCache
Amazon ElastiCache for Memcached is an ideal front-end for data stores like Amazon RDS or Amazon DynamoDB, providing a high-performance middle tier for applications with extremely high request rates and/or low latency requirements


## 225. Dynamodb Advanced Features

### DynamoDB Accelerator(DAX)
- Amazon DynamoDB Accelerator (DAX) is a fully managed, highly available, in-memory cache for DynamoDB that delivers up to a 10x performance improvement – from milliseconds to microseconds – even at millions of requests per second.
- DAX does all the heavy lifting required to add in-memory acceleration to your DynamoDB tables, without requiring developers to manage cache invalidation, data population, or cluster management. Therefore, this is a correct option.
  ![](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/images/dax_high_level.png)

* in- memory cache for DynamoDB
* Help solve read congestion by caching
* Microseconds latency for cached data
* Doesn’t require application logic modification (compatible with existing DynamoDB APIs)
* 5 minutes TTL for cache (default)


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
* Security:
  * IAM Role
  * Cognito
  * Custom Authorize(Lamda)
* How to API gateway work:

## Choosing right database
- RDBMS (SQL/OLTP) - Great for joins
  - RDS
  - Aurora
- NoSQL database - no joins, no SQL
  - DynamoDB(~JSON)
  - ElasticCache(Key/Value Paris)
  - Neptune(graphs)
  - DocumentDB(For MogoDB)
- Object Store:
  - S3(for big objects)
  - Glacier(for backups/chive)
- **Data Warehouse**(SQL Analytics / BI)
  + Reshift(OLAP)
  + Athena
  + EMR
- Search:
  - OpenSearch(Json) - free text, unstructured search
- Graphs: Amazone Neptune - displays relationships between data
- Ledger: Amazone Quantum Ledger Database
- Time series: AmazonTimestream

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
### Read_Replicas
- Amazon RDS Read Replicas provide enhanced performance and durability for RDS database (DB) instances.
- Easy to elastically scale out beyond the capacity constraints of a single DB instance for read-heavy database workloads.
- For the MySQL, MariaDB, PostgreSQL, Oracle, and SQL Server database engines, RDS creates a second DB instance using a snapshot of DB. 
- It then uses the engines native asynchronous replication to update the read replica whenever there is a change to the source DB instance. 
- Can be within an Availability Zone, Cross-AZ, or Cross-Region.
- [Read Replicas Link](https://assets-pt.media.datacumulus.com/aws-saa-pt/assets/pt2-q44-i1.jpg)

### storage auto-scaling
- If your workload is unpredictable, you can enable storage autoscaling for an Amazon RDS DB instance. 
- When Amazon RDS detects that you are running out of free database space it automatically scales up your storage. 
- Amazon RDS starts a storage modification for an autoscaling-enabled DB instance when these factors apply:
  - Free available space is less than 10 percent of the allocated storage.
  - The low-storage condition lasts at least five minutes.
  - At least six hours have passed since the last storage modification.
  - The maximum storage threshold is the limit that you set for autoscaling the DB instance. You can't set the maximum storage threshold for autoscaling-enabled instances to a value greater than the maximum allocated storage.

## Aurora
- Amazon Aurora is a MySQL and PostgreSQL-compatible relational database built for the cloud, that combines the performance and availability of traditional enterprise databases with the simplicity and cost-effectiveness of open source databases. Amazon Aurora features a distributed, fault-tolerant, self-healing storage system that auto-scales up to 128TB per database instance. Aurora is not an in-memory database.
- Amazon Aurora Global Database is designed for globally distributed applications, allowing a single Amazon Aurora database to span multiple AWS regions. It replicates your data with no impact on database performance, enables fast local reads with low latency in each region, and provides disaster recovery from region-wide outages. Amazon Aurora Global Database is the correct choice for the given use-case.

![](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/images/AuroraArch001.png)
- **Cluster** consists of one or more DB instances and a cluster volume that manages the data for those DB instances. 
- An Aurora cluster volume is a virtual database storage volume that spans multiple Availability Zones (AZs), with each Availability Zone (AZ) having a copy of the DB cluster data. 
- Two types of DB instances make up an Aurora DB cluster:
  - **Primary DB instance** 
    - Supports read and write operations, and performs all of the data modifications to the cluster volume. 
    - Each Aurora DB cluster has one primary DB instance.
  - **Aurora Replica**
    - Connects to the same storage volume as the primary DB instance and supports only read operations. 
    - Each Aurora DB cluster can have up to 15 Aurora Replicas in addition to the primary DB instance.
-  Aurora automatically fails over to an Aurora Replica in case the primary DB instance becomes unavailable. 
-  You can specify the failover priority for Aurora Replicas.
-  Aurora Replicas can also offload read workloads from the primary DB instance.
-  You use the reader endpoint for read-only connections for your Aurora cluster. 
-  This endpoint uses a load-balancing mechanism to help your cluster handle a query-intensive workload. 
-  The reader endpoint is the endpoint that you supply to applications that do reporting or other read-only operations on the cluster. 
-  The reader endpoint load-balances connections to available Aurora Replicas in an Aurora DB cluster.

- Compatilbe API for Post
- Store in 6 replica - 3 AZ
- Cluster: Customer endopint for writer and reader DB instaces
- Aurora Serverless
- Aurora Global:
- Aurora Machine Learning: Perfrm ML using SageMaker & Comprehend on Aurora

### Aurora
### Aurora_Global_Table
![Aurora_Global_Table](https://assets-pt.media.datacumulus.com/aws-saa-pt/assets/pt2-q5-i1.jpg)
- Amazon Aurora Global Database is designed for globally distributed applications, allowing a single Amazon Aurora database to span multiple AWS regions.
- It replicates your data with no impact on database performance, enables fast local reads with low latency in each region, and provides disaster recovery from region-wide outages.
- https://aws.amazon.com/rds/aurora/global-database/
### Aurora_Replica
- Purpose
  - Scale read operations of your app(reader endpoint) -> Increase avaibility
  - If the writer instance becomes unavailable, automatically promotes one of the reader instances to take its place as the new write
  - Up to 15 Aurora Replicas xacross the Availability Zones (AZs) tha DB cluster spans within an AWS Region.
## Amazone Elasticache - Summanry

- Managed Redis / Memchaed
- In-memory datastore, sub-milisecond latency
- Support for Clustering(Redis) and Multi Az,

## DynamoDB
- A key-value and document database that delivers single-digit millisecond performance at any scale.
-  It's a fully managed, multi-region, multi-master, durable database with built-in security, backup and restore, and in-memory caching for internet-scale applications.
- Can replace ElastiCahe as a key/value store
- Highly Available, Multi Az by default
- DAX cluster for reading cache
- Event Processing: DynamoDB Streaam to integrate with AWS Lamda, or Kinesis Data Streams
- Global Table feature: active-ative setup
- Export to S3
## DynamoDB_GlobalTable
![DynamoDB_GlobalTable](https://assets-pt.media.datacumulus.com/aws-saa-pt/assets/pt2-q5-i2.jpg)
- Global Tables builds upon DynamoDB’s global footprint to provide you with a fully managed, multi-region, and multi-master database that provides fast, local, read, and write performance for massively scaled, global applications. 
- Global Tables replicates your Amazon DynamoDB tables automatically across your choice of AWS region

## S3 - Lifecycle transtion
[- ![alt text](image-74.png)](https://docs.aws.amazon.com/images/AmazonS3/latest/userguide/images/lifecycle-transitions-v4.png)
## S3 - Storage Classes
[Link](https://aws.amazon.com/s3/storage-classes/)
### S3 One Zone-IA
- Amazon S3 One Zone-IA is for
  - data that is accessed less frequently,
  - requires rapid access when needed.
- Other S3 Storage Classes which store data in a minimum of three Availability Zones (AZs), IA stores data in a single Availability Zone (AZ) and costs 20% less than Standard-IA.
- One Zone-IA is ideal for customers want a lower-cost option for infrequently accessed and re-creatable data but do not require the availability and resilience of Standard or Standard-IA.
- The minimum storage duration is 30 days before you can transition objects from Standard to One Zone-IA.

## Amazon Simple Notification Service(SNS)
- A highly available, durable, secure, fully managed pub/sub messaging service.
- Enables you to decouple
  - microservices
  - distributed systems
  - serverless applications.
- Fully dynamically server - dynamically scale with your application

## S3
- an object storage service that offers industry-leading scalability, data availability, security, and performance.
- Your applications can easily achieve thousands of transactions per second in request performance when uploading and retrieving storage from Amazon S3.
- Amazon S3 automatically scales to high request rates. For example, your application can achieve at least
  - 3,500 PUT/COPY/POST/DELETE or 5,500 GET/HEAD requests per second per prefix in a bucket.
- There are no limits to the number of prefixes in a bucket. For example, if you create 10 prefixes in an Amazon S3 bucket to parallelize reads, you could scale your read performance to 55,000 read requests per second.

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
- Federated query:
  - Allow to run query on AWS or on premise
  - Store result back in S3

## REDSHIFT
- Is base on PostgresSQL but not use for Online Tracsactio Processing
- For OLAP(Online Analytic Processing)
- Should load the data(From Kinesis Firehose)
- Ingest data to redshiff
  - Firehose -> Write S3 ->  S3 Copy -> RedShift
- EC2 -> Redshift by JDBC Driver
- Reshift Spectrum: Query data is already in S3 without loading it.

## 248 Open Search
- Amazon OpenSearch Service is a managed service that makes it easy for you to perform interactive log analytics, real-time application monitoring, website search, and more. OpenSearch is an open source, distributed search and analytics suite derived from Elasticsearch. It cannot be used as a caching layer for Amazon DynamoDB.
-
- Succesor to Elastic Search
- On DynamoDB, queries only exist by primary key or indexs
- Could search any field
- Two mode: Managed Cluster or Serverless cluster
- Security: Cognito, IAM Role
- Have OpenSearch Dashboard
- OpenSearch Patterns DynamoDB
  - DymamoDB Table -> DynamoDB Stream -> Lambda Function -> OpenSearch -> Search for Item Name -> Retrive ID -> Search Full Item in DynamoDB

- OpenSearch Patterns Clouwatch Logs

- OpenSearch Pattern Kisesis DataStream and FireHorse

## EMR
-  Amazon EMR is the industry-leading cloud big data platform for processing vast amounts of data
-  Using open source tools such as 
   -  Apache Spark
   -  Apache Hive
   -  Apache HBase
   -  Apache Flink
   -  Apache Hudi
   -  and Presto. 
- Amazon EMR uses Hadoop, an open-source framework, to distribute your data and processing across a resizable cluster of Amazon EC2 instances
  
- Stand for Elastic MapReduce
- Create Hadoop cluster(Bigdata) -> analyze & process vast amount data

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
- Convert data into Parquet Format
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
- Many place in setup security

## 314 Amazon GuardDuty
-- Offers threat detection that enables you to continuously monitor and protect your AWS accounts, workloads, and data stored in Amazon S3. - GuardDuty analyzes continuous streams of meta-data generated from your account and network activity found in AWS CloudTrail Events, Amazon VPC Flow Logs, and DNS Logs.
- It also uses integrated threat intelligence such as known malicious IP addresses, anomaly detection, and machine learning to identify threats more accurately.
  ![](https://d1.awsstatic.com/product-marketing/Amazon%20GuardDuty/product-page-diagram-Amazon-GuardDuty_how-it-works.a4daf7e3aaf3532623a3797dd3af606a85fc2e7b.png)


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

  ## Task
  - Review cloudfront, Global Accelerator
