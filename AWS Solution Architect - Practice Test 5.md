# Practice Test 5
- https://nab.udemy.com/course/practice-exams-aws-certified-solutions-architect-associate/learn/quiz/5077342/result/1359446051#overview

## 1
A company needs a massive PostgreSQL database and the engineering team would like to retain control over managing the patches, version upgrades for the database, and consistent performance with high IOPS. The team wants to install the database on an Amazon EC2 instance with the optimal storage type on the attached Amazon EBS volume.

As a solutions architect, which of the following configurations would you suggest to the engineering team?

**Options**
- EBS volume of General Purpose SSD (gp2) type
- EBS volume of cold HDD (sc1) type
- EBS volume of Throughput Optimized HDD (st1) type
- EBS volume of Provisioned IOPS SSD (io1) type

**Solution**
- EBS volume of Provisioned IOPS SSD (io1) type
  - [EBS](aws-ass-solution-architect.md#ebs)

## 2
- A pharmaceutical company is considering moving to AWS Cloud to accelerate the research and development process. 
- Most of the daily workflows would be centered around running batch jobs on Amazon EC2 instances with storage on Amazon Elastic Block Store (Amazon EBS) volumes. 
- The CTO is concerned about meeting HIPAA compliance norms for sensitive data stored on Amazon EBS.

Which of the following options outline the correct capabilities of an encrypted Amazon EBS volume? (Select three)

**Options**
- Data at rest inside the volume is NOT encrypted
- Any snapshot created from the volume is encrypted
- Any snapshot created from the volume is NOT encrypted
- Data at rest inside the volume is encrypted
- Data moving between the volume and the instance is NOT encrypted
- Data moving between the volume and the instance is encrypted

**Solution**

- Any snapshot created from the volume is encrypted
- Data at rest inside the volume is encrypted
- Data moving between the volume and the instance is encrypted

* Amazon Elastic Block Store (Amazon EBS) provides block-level storage volumes for use with Amazon EC2 instances. When you create an encrypted Amazon EBS volume and attach it to a supported instance type, data stored at rest on the volume, data moving between the volume and the instance, snapshots created from the volume and volumes created from those snapshots are all encrypted. 
* It uses AWS Key Management Service (AWS KMS) customer master keys (CMK) when creating encrypted volumes and snapshots. Encryption operations occur on the servers that host Amazon EC2 instances, ensuring the security of both data-at-rest and data-in-transit between an instance and its attached Amazon EBS storage.


## 3
A junior developer is learning to build websites using HTML, CSS, and JavaScript. He has created a static website and then deployed it on Amazon S3. Now he can't seem to figure out the endpoint for his super cool website.

As a solutions architect, can you help him figure out the allowed formats for the Amazon S3 website endpoints? (Select two)

**Options**
- http://bucket-name.s3-website-Region.amazonaws.com
- http://bucket-name.Region.s3-website.amazonaws.com
- http://bucket-name.s3-website.Region.amazonaws.com
- http://s3-website-Region.bucket-name.amazonaws.com
- http://s3-website.Region.bucket-name.amazonaws.com


**Soluiton**
When you configure your bucket as a static website, the website is available at the AWS Region-specific website endpoint of the bucket.
Depending on your Region, your Amazon S3 website endpoints follow one of these two formats.
s3-website dash (-) Region ‐ http://bucket-name.s3-website.Region.amazonaws.com
s3-website dot (.) Region ‐ http://bucket-name.s3-website-Region.amazonaws.com
* https://docs.aws.amazon.com/AmazonS3/latest/dev/WebsiteEndpoints.html

## 4
A retail company wants to establish encrypted network connectivity between its on-premises data center and AWS Cloud. The company wants to get the solution up and running in the fastest possible time and it should also support encryption in transit.

As a solutions architect, which of the following solutions would you suggest to the company?

**Option**

- Use AWS Direct Connect to establish encrypted network connectivity between the on-premises data center and AWS Cloud
- Use AWS Secrets Manager to establish encrypted network connectivity between the on-premises data center and AWS Cloud
- Use AWS Site-to-Site VPN to establish encrypted network connectivity between the on-premises data center and AWS Cloud
- Use AWS Data Sync to establish encrypted network connectivity between the on-premises data center and AWS Cloud


**Solution**
- Use AWS Site-to-Site VPN to establish encrypted network connectivity between the on-premises data center and AWS Cloud
* [](../markdown-documents/work/AWS/aws-ass-solution-architect.md#aws-site-to-site-vpn)

**Wrong**
- AWS Direct Connect does not support encrypted network connectivity between an on-premises data center and AWS Cloud, therefore this option is incorrect.
- AWS DataSync makes it simple and fast to move large amounts of data online between on-premises storage and AWS. AWS DataSync eliminates or automatically handles many of these tasks, including scripting copy jobs, scheduling, and monitoring transfers, validating data, and optimizing network utilization

## 5
- The engineering team at an e-commerce company uses an AWS Lambda function to write the order data into a single DB instance Amazon Aurora cluster.
-  The team has noticed that many order- writes to its Aurora cluster are getting missed during peak load times. 
-  The diagnostics data has revealed that the database is experiencing high CPU and memory consumption during traffic spikes. 
-  The team also wants to enhance the availability of the Aurora DB.

Which of the following steps would you combine to address the given scenario? (Select two)

**Options**
- Create a replica Aurora instance in another Availability Zone to improve the availability as the replica can serve as a failover target
- Use Amazon EC2 instances behind an Application Load Balancer to write the order data into Amazon Aurora cluster
- Create a standby Aurora instance in another Availability Zone to improve the availability as the standby can serve as a failover target
- Increase the concurrency of the AWS Lambda function so that the order-writes do not get missed during traffic spikes
- Handle all read operations for your application by connecting to the reader endpoint of the Amazon Aurora cluster so that Aurora can spread the load for read-only connections across the Aurora replica

**Solution**
- Handle all read operations for your application by connecting to the reader endpoint of the Amazon Aurora cluster so that Aurora can spread the load for read-only connections across the Aurora replica
- Create a replica Aurora instance in another Availability Zone to improve the availability as the replica can serve as a failover target
  * If the primary instance in a DB cluster using single-master replication fails, Aurora automatically fails over to a new primary instance in one of two ways:
  * By promoting an existing Aurora Replica to the new primary instance By creating a new primary instance

 
## 6
**Questions**
- An *Internet-of-Things (IoT)* company is planning on distributing a master *sensor* in people's homes to measure the key metrics from its smart devices.
- In order to provide adjustment commands for these devices, the company would like to have a streaming system that supports *ordered data* based on the sensor's key, and also sustains *high throughput messages (thousands of messages per second)*.

As a solutions architect, which of the following AWS services would you recommend for this use-case?
**Option**
- Amazon Simple Queue Service (Amazon SQS)
- Amazon Kinesis Data Streams
- Amazon Simple Notification Service (Amazon SNS)
- AWS Lambda

**Solution**
- Amazon Kinesis Data Streams
  + [Kinesis Data Stream](../markdown-documents/work/AWS/aws-ass-solution-architect.md#kinesis-data-stream)

**Wrong**
- SQS:
  - queues aren't meant for real-time streaming of data.
- SNS
- Lambda

## 7
- A financial services company runs its flagship web application on AWS.
- The application *serves thousands of users during peak hours.* 
- The company needs a **scalable near-real-time** solution to *share hundreds of thousands of financial transactions with multiple internal applications*. 
- The solution should also *remove sensitive details* from the transactions before storing the cleansed transactions in a document database for low-latency retrieval.

As an AWS Certified Solutions Architect Associate, which of the following would you recommend?

**Options**
- Feed the streaming transactions into Amazon Kinesis Data Streams. Leverage AWS Lambda integration to remove sensitive data from every transaction and then store the cleansed transactions in Amazon DynamoDB. The internal applications can consume the raw transactions off the Amazon Kinesis Data Stream
- Persist the raw transactions into Amazon DynamoDB. Configure a rule in Amazon DynamoDB to update the transaction by removing sensitive data whenever any new raw transaction is written. Leverage Amazon DynamoDB Streams to share the transactions data with the internal applications
- Feed the streaming transactions into Amazon Kinesis Data Firehose. Leverage AWS Lambda integration to remove sensitive data from every transaction and then store the cleansed transactions in Amazon DynamoDB. The internal applications can consume the raw transactions off the Amazon Kinesis Data Firehose
- Batch process the raw transactions data into Amazon S3 flat files. Use S3 events to trigger an AWS Lambda function to remove sensitive data from the raw transactions in the flat file and then store the cleansed transactions in Amazon DynamoDB. Leverage DynamoDB Streams to share the transactions data with the internal applications

**Solution**
- Feed the streaming transactions into Amazon Kinesis Data Streams. Leverage AWS Lambda integration to remove sensitive data from every transaction and then store the cleansed transactions in Amazon DynamoDB. The internal applications can consume the raw transactions off the Amazon Kinesis Data Stream
  - [](../markdown-documents/work/AWS/aws-ass-solution-architect.md#kinesis-data-stream)
**Wrong**
- Batch 

## 8
- A gaming company is doing pre-launch testing for its new product. 
- The company runs its production database on an Aurora MySQL DB cluster and the performance testing team wants access to multiple test databases that must be re-created from production data. 
- The company has hired you as an AWS Certified Solutions Architect - Associate to deploy a solution to create these test databases quickly with the LEAST required effort.

**Solution**
- Use database cloning to create multiple clones of the production database and use each clone as a test database
- Set up binlog replication in the Aurora MySQL database instance to create multiple new test database instances
- Enable database Backtracking on the production database and let the testing team use the production database
- Take a backup of the Aurora MySQL database instance using the mysqldump utility, create multiple new test database instances and restore each test database from the backup

**Solution**
- Use database cloning to create multiple clones of the production database and use each clone as a test database
  - [](aws-ass-solution-architect.md#aurora)

**Wrong**

- Set up binlog replication in the Aurora MySQL database instance to create multiple new test database instances
  + Using Backtracking, you can "rewind" the DB cluster to any time you specify. One of the major advantages of backtracking is that it can rewind the DB cluster much faster compared to restoring a DB cluster via point-in-time restore (PITR) or via a manual DB cluster snapshot, which can take hours. Backtracking a DB cluster doesn't require a new DB cluster and rewinds the DB cluster in minutes.
  + However, as the given use-case is around pre-release testing, it does not make sense to use production DB itself for testing even if backtracking is enabled. The right solution is to use clones of the production DB for testing.

- Binglog:
  - binlog replication requires several steps such as creating a snapshot of your replication source, loading the snapshot into your replica target, etc.

## 9
A medium-sized business has a taxi dispatch application deployed on an Amazon EC2 instance. Because of an unknown bug, the application causes the instance to freeze regularly. Then, the instance has to be manually restarted via the AWS management console.

Which of the following is the MOST cost-optimal and resource-efficient way to implement an automated solution until a permanent fix is delivered by the development team?

**Solution**
- Setup an Amazon CloudWatch alarm to monitor the health status of the instance. In case of an Instance Health Check failure, Amazon CloudWatch Alarm can publish to an Amazon Simple Notification Service (Amazon SNS) event which can then trigger an AWS lambda function. The AWS lambda function can use Amazon EC2 API to reboot the instance
- Setup an Amazon CloudWatch alarm to monitor the health status of the instance. In case of an Instance Health Check failure, an EC2 Reboot CloudWatch Alarm Action can be used to reboot the instance
- Use Amazon EventBridge events to trigger an AWS Lambda function to reboot the instance status every 5 minutes
- Use Amazon EventBridge events to trigger an AWS Lambda function to check the instance status every 5 minutes. In the case of Instance Health Check failure, the AWS lambda function can use Amazon EC2 API to reboot the instance

**Solution**
- Setup an Amazon CloudWatch alarm to monitor the health status of the instance. In case of an Instance Health Check failure, Amazon CloudWatch Alarm can publish to an Amazon Simple Notification Service (Amazon SNS) event which can then trigger an AWS lambda function. The AWS lambda function can use Amazon EC2 API to reboot the instance

## 10
The engineering team at a retail company manages 3 Amazon EC2 instances that make read-heavy database requests to the Amazon RDS for the PostgreSQL database instance. As an AWS Certified Solutions Architect - Associate, you have been tasked to make the database instance resilient from a disaster recovery perspective.

Which of the following features will help you in disaster recovery of the database? (Select two)
**Options**
- Use the database cloning feature of the Amazon RDS Database cluster
- Enable the automated backup feature of Amazon RDS in a multi-AZ deployment that creates backups across multiple Regions
- Use cross-Region Read Replicas
- Enable the automated backup feature of Amazon RDS in a multi-AZ deployment that creates backups in a single AWS Region
- Use Amazon RDS Provisioned IOPS (SSD) Storage in place of General Purpose (SSD) Storage

**Solution**
- Use cross-Region Read Replicas
  - In addition to using Read Replicas to reduce the load on your source database instance, you can also use Read Replicas to implement a DR solution for your production DB environment. If the source DB instance fails, you can promote your Read Replica to a standalone source server. Read Replicas can also be created in a different Region than the source database. Using a cross-Region Read Replica can help ensure that you get back up and running if you experience a regional availability issue.

- Enable the automated backup feature of Amazon RDS in a multi-AZ deployment that creates backups across multiple Regions
  - Amazon RDS provides high availability and failover support for database instances using Multi-AZ deployments. Amazon RDS uses several different technologies to provide failover support. Multi-AZ deployments for MariaDB, MySQL, Oracle, and PostgreSQL DB instances use Amazon's failover technology.
  - The automated backup feature of Amazon RDS enables point-in-time recovery for your database instance. Amazon RDS will back up your database and transaction logs and store both for a user-specified retention period. If it’s a Multi-AZ configuration, backups occur on standby to reduce the I/O impact on the primary. Amazon RDS supports Cross-Region Automated Backups. Manual snapshots and Read Replicas are also supported across multiple Regions.

## 11
Your company is evolving towards a microservice approach for their website. The company plans to expose the website from the same load balancer, linked to different target groups with different URLs, that are similar to these - checkout.mycorp.com, www.mycorp.com, mycorp.com/profile, and mycorp.com/search.

As a Solutions Architect, which Load Balancer type do you recommend to achieve this routing feature with MINIMUM configuration and development effort?

**Option**
- Create an NGINX based load balancer on an Amazon EC2 instance to have advanced routing capabilities
- Create a Network Load Balancer
- Create a Classic Load Balancer
- Create an Application Load Balancer

**Solution**
- Create an Application Load Balancer
  - [ALB](aws-ass-solution-architect.md#alb)
  - Application Load Balancer can automatically distribute incoming application traffic across multiple targets, such as Amazon EC2 instances, containers, IP addresses, and Lambda functions. It can handle the varying load of your application traffic in a single Availability Zone or across multiple Availability Zones.
  - If your application is composed of several individual services, an Application Load Balancer can route a request to a service based on the content of the request.

## 12
A medical devices company uses Amazon S3 buckets to store critical data. Hundreds of buckets are used to keep the data segregated and well organized. Recently, the development team noticed that the lifecycle policies on the Amazon S3 buckets have not been applied optimally, resulting in higher costs.

As a Solutions Architect, can you recommend a solution to reduce storage costs on Amazon S3 while keeping the IT team's involvement to a minimum?

**Options**
- Use Amazon S3 Intelligent-Tiering storage class to optimize the Amazon S3 storage costs
- Use Amazon S3 Outposts storage class to reduce the costs on Amazon S3 storage by storing the data on-premises
- Use Amazon S3 One Zone-Infrequent Access, to reduce the costs on Amazon S3 storage
- Configure Amazon EFS to provide a fast, cost-effective and sharable storage service
**Solutions**
- Use Amazon S3 Intelligent-Tiering storage class to optimize the Amazon S3 storage costs
  - [S3_Intelligent_Tiering](aws-ass-solution-architect.md#s3_intelligent_tiering)

**Wrong**

## 13
- A DevOps engineer at an organization is debugging issues related to an Amazon EC2 instance. 
- The engineer has SSH'ed into the instance and he needs to retrieve the instance public IP from within a shell script running on the instance command line.

Can you identify the correct URL path to get the instance public IP?

**Options**
- http://169.254.169.254/latest/user-data/public-ipv4
- http://254.169.254.169/latest/meta-data/public-ipv4
- http://254.169.254.169/latest/user-data/public-ipv4
- http://169.254.169.254/latest/meta-data/public-ipv4
**Solution**
- http://**169.254.169.254**/latest/meta-data/public-ipv4
  - *Instance metadata* is the data about your instance that you can use to configure or manage the running instance.
  - *Instance user data* is the data that you specified in the form of a configuration script while launching your instance.

## 14
- A leading video streaming provider is migrating to AWS Cloud infrastructure for delivering its content to users across the world. 
- The company wants to make sure that the solution supports at least a million requests per second for its Amazon EC2 server farm.

As a solutions architect, which type of Elastic Load Balancing would you recommend as part of the solution stack?
**Options**
- Application Load Balancer
- Network Load Balancer
- Infrastructure Load Balancer
- Classic Load Balancer
**Solution**
- [Network Load Balancer](aws-ass-solution-architect.md#nlb)

## 15
A company wants to publish an event into an Amazon Simple Queue Service (Amazon SQS) queue whenever a new object is uploaded on Amazon S3.

Which of the following statements are true regarding this functionality?

**Options**
- Both Standard Amazon SQS queue and FIFO SQS queue are allowed as an Amazon S3 event notification destination
- Only Standard Amazon SQS queue is allowed as an Amazon S3 event notification destination, whereas FIFO SQS queue is not allowed
- Only FIFO Amazon SQS queue is allowed as an Amazon S3 event notification destination, whereas Standard SQS queue is not allowed
- Neither Standard Amazon SQS queue nor FIFO SQS queue are allowed as an Amazon S3 event notification destination
**Solution**
- Only Standard Amazon SQS queue is allowed as an Amazon S3 event notification destination, whereas FIFO SQS queue is not allowed
  - The Amazon S3 notification feature enables you to receive notifications when certain events happen in your bucket. To enable notifications, you must first add a notification configuration that identifies the events you want Amazon S3 to publish and the destinations where you want Amazon S3 to send the notifications.
  - Amazon S3 supports the following destinations where it can publish events:
    - SNS topic
    - Amazon SQS queue
    - AWS Lambda
    - Currently, the Standard Amazon SQS queue is only allowed as an Amazon S3 event notification destination, whereas the FIFO SQS queue is not allowed.

## 16
- A company's cloud architect has set up a solution that uses *Amazon Route 53* to configure the DNS records for the primary website with the domain pointing to the *Application Load Balancer (ALB).* 
- The company wants a solution where users will be directed to a static error page, configured as a backup, in case of unavailability of the primary website.

Which configuration will meet the company's requirements, while keeping the changes to a bare minimum?

**Options**
- Use Amazon Route 53 Latency-based routing. Create a latency record to point to the Amazon S3 bucket that holds the error page to be displayed
- Set up Amazon Route 53 active-passive type of failover routing policy. If Amazon Route 53 health check determines the Application Load Balancer endpoint as unhealthy, the traffic will be diverted to a static error page, hosted on Amazon S3 bucket
- Set up Amazon Route 53 active-active type of failover routing policy. If Amazon Route 53 health check determines the Application Load Balancer endpoint as unhealthy, the traffic will be diverted to a static error page, hosted on Amazon S3 bucket
- Use Amazon Route 53 Weighted routing to give minimum weight to Amazon S3 bucket that holds the error page to be displayed. In case of primary failure, the requests get routed to the error page

  
**Solution**
- Set up Amazon Route 53 active-passive type of failover routing policy. If Amazon Route 53 health check determines the Application Load Balancer endpoint as unhealthy, the traffic will be diverted to a static error page, hosted on Amazon S3 bucket
  - [](aws-ass-solution-architect.md#failover_routing)

## 17
- A media company is evaluating the possibility of moving its IT infrastructure to the AWS Cloud.
- The company needs at least 10 terabytes of storage with the maximum possible I/O performance for processing certain files which are mostly large videos.
- The company also needs close to 450 terabytes of very durable storage for storing media content and almost double of it, i.e. 900 terabytes for archival of legacy data.
As a Solutions Architect, which set of services will you recommend to meet these requirements?

**Options**
- Amazon EC2 instance store for maximum performance, AWS Storage Gateway for on-premises durable data access and Amazon S3 Glacier Deep Archive for archival storage
- Amazon S3 standard storage for maximum performance, Amazon S3 Intelligent-Tiering for intelligent, durable storage, and Amazon S3 Glacier Deep Archive for archival storage
- Amazon EBS for maximum performance, Amazon S3 for durable data storage, and Amazon S3 Glacier for archival storage
- Amazon EC2 instance store for maximum performance, Amazon S3 for durable data storage, and Amazon S3 Glacier for archival storage
- Amazon EC2 instance store for maximum performance, Amazon S3 for durable data storage, and Amazon S3 Glacier for archival storage

**Solution**
- Amazon EC2 instance store for maximum performance, Amazon S3 for durable data storage, and Amazon S3 Glacier for archival storage

## 18

- A global media company uses a fleet of *Amazon EC2 instances* (behind an *Application Load Balancer*) to power its video streaming application. 
- To improve the performance of the application, the engineering team has also created an Amazon CloudFront distribution with the Application Load Balancer as the custom origin. 
- The security team at the company has noticed a spike in the number and types of SQL injection and cross-site scripting attack vectors on the application.

As a solutions architect, which of the following solutions would you recommend as the MOST effective in countering these malicious attacks?

**Options**
- Use AWS Web Application Firewall (AWS WAF) with Amazon CloudFront distribution
- Use Amazon Route 53 with Amazon CloudFront distribution
- Use AWS Security Hub with Amazon CloudFront distribution
- Use AWS Firewall Manager with CloudFront distribution
**Solution**
- Use AWS Web Application Firewall (AWS WAF) with Amazon CloudFront distribution
  - [WAF](aws-ass-solution-architect.md#waf)
**Wrong**
- [AWS Security Hub](aws-ass-solution-architect.md#aws_security_hub)
- [AWS_Firewall_Manager](aws-ass-solution-architect.md#aws_firewall_manager)

## 19
- A startup has created a cost-effective backup solution in another AWS Region. 
- The application is running in warm standby mode and has Application Load Balancer (ALB) to support it from the front.
- The current failover process is manual and requires updating the DNS alias record to point to the secondary Application Load Balancer in another Region in case of failure of the primary Application Load Balancer.

As a Solutions Architect, what will you recommend to automate the failover process?

**Options**
- Enable an Amazon Route 53 health check
- Configure AWS Trusted Advisor to check on unhealthy instances
- Enable an Amazon EC2 instance health check
- Enable an ALB health check

**Solution**
- Enable an Amazon Route 53 health check

Determining the health of an ELB endpoint is more complex than health checking a single IP address. For example, what if your application is running fine on Amazon EC2, but the load balancer itself isn't reachable? Or if your load balancer and your Amazon EC2 instances are working correctly, but a bug in your code causes your application to crash? Or how about if the Amazon EC2 instances in one Availability Zone of a multi-AZ ELB are experiencing problems?

Amazon Route 53 DNS Failover handles all of these failure scenarios by integrating with ELB behind the scenes. Once enabled, Route 53 automatically configures and manages health checks for individual ELB nodes. Amazon Route 53 also takes advantage of the Amazon EC2 instance health checking that ELB performs (information on configuring your ELB health checks is available here). By combining the results of health checks of your Amazon EC2 instances and your ELBs, Amazon Route 53 DNS Failover can evaluate the health of the load balancer and the health of the application running on the Amazon EC2 instances behind it. In other words, if any part of the stack goes down, Amazon Route 53 detects the failure and routes traffic away from the failed endpoint.

Using Amazon Route 53 DNS Failover, you can run your primary application simultaneously in multiple AWS regions around the world and failover across regions. Your end-users will be routed to the closest (by latency), healthy region for your application. Amazon Route 53 automatically removes from service any region where your application is unavailable - it will pull an endpoint out of service if there is region-wide connectivity or operational issue, if your application goes down in that region, or if your ELB or Amazon EC2 instances go down in that region.

**Wrong**
**Enable an ALB health check** - ELB health check verifies that a specified TCP port on an instance is accepting connections or a specified page has returned an error code of 200. It is not useful for the given failover scenario.

**Enable an Amazon EC2 instance health check** - Instance status checks monitor the software and network configuration of your instance. It is not intelligent enough to understand if the application on the instance is working correctly. Hence, this is not the right choice for the given use-case.

**Configure AWS Trusted Advisor to check on unhealthy instances** - AWS Trusted Advisor examines the health check configuration for Auto Scaling groups. If Elastic Load Balancing is being used for an Auto Scaling group, the recommended configuration is to enable an Elastic Load Balancing health check. AWS Trusted Advisor recommends certain configuration changes by comparing your system configurations to AWS Best practices. It cannot handle a failover the way Amazon Route 53 does.

## 20 
- Your firm has implemented a multi-tiered networking structure within the VPC - with two public and two private subnets.
- The public subnets are used to deploy the Application Load Balancers, while the two private subnets are used to deploy the application on Amazon EC2 instances.
- The development team wants the Amazon EC2 instances to have access to the internet.
- The solution has to be fully managed by AWS and needs to work over IPv4.

What will you recommend?

**Options**
- NAT Instances deployed in your public subnet
- Egress-Only Internet Gateways deployed in your private subnet
- Internet Gateways deployed in your private subnet
- NAT Gateways deployed in your public subnet

**Solution**
- [NAT Gateways](aws-ass-solution-architect.md#vpc_nat_gateway) deployed in your public subnet

**Wrong**
- NAT Instances deployed in your public subnet 
  - You can use a network address translation (NAT) instance in a public subnet in your VPC to enable instances in the private subnet to initiate outbound IPv4 traffic to the Internet or other AWS services, but prevent the instances from receiving inbound traffic initiated by someone on the Internet.
  - Amazon provides Amazon Linux AMIs that are configured to run as NAT instances.
  - These AMIs include the s
  - tring amzn-ami-vpc-nat in their names, so you can search for them in the Amazon EC2 console.
  - NAT Instances would work but won't scale and you would have to manage them (as they're nothing but Amazon EC2 instances).

- Internet Gateways deployed in your private subnet 
  - An internet gateway is a horizontally scaled, redundant, and highly available VPC component that allows communication between instances in your VPC and the internet. 
  - It, therefore, imposes no availability risks or bandwidth constraints on your network traffic. 
  - *Internet Gateways must be deployed in a public subnet*, hence not an option here.
  - Egress-Only Internet Gateways deployed in your private subnet: IP6

## 21

A financial services company is moving its IT infrastructure to AWS Cloud and wants to enforce adequate data protection mechanisms on Amazon Simple Storage Service (Amazon S3) to meet compliance guidelines.
The engineering team has hired you as a solutions architect to build a solution for this requirement.

Can you help the team identify the INCORRECT option from the choices below?

**Options**
- Amazon S3 can encrypt data in transit using HTTPS (TLS)
- Amazon S3 can encrypt object metadata by using Server-Side Encryption
- Amazon S3 can protect data at rest using Client-Side Encryption
- Amazon S3 can protect data at rest using Server-Side Encryption

**Wrong**
- Amazon S3 can encrypt object metadata by using Server-Side Encryption
  - Metadata, which can be included with the object, is not encrypted while being stored on Amazon S3. Therefore, AWS recommends that customers not place sensitive information in Amazon S3 metadata.

## 22
A solutions architect has been tasked to design a *low-latency solution* for a static, single-page application, *accessed by users through a custom domain name*. The solution must be **serverless**, provide *in-transit data encryption* and needs to be *cost-effective*.

Which AWS services can be combined to build the simplest possible solution for the company's requirement?

**Options**
- Host the application on AWS Fargate and front it with Elastic Load Balancing for an improved performance
- Host the application on Amazon EC2 instance with instance store volume for high performance and low latency access to users
- Configure Amazon S3 to store the static data and use AWS Fargate for hosting the application
- Use Amazon S3 to host the static website and Amazon CloudFront to distribute the content for low latency access

**Solution**
- Use Amazon S3 to host the static website and Amazon CloudFront to distribute the content for low latency access

- To host a static website on Amazon S3, you configure an Amazon S3 bucket for website hosting and then upload your website content to the bucket. When you configure a bucket as a static website, you must enable website hosting, set permissions, and create and add an index document. Depending on your website requirements, you can also configure redirects, web traffic logging, and a custom error document.

- After you configure your bucket as a static website, you can access the bucket through the AWS Region-specific Amazon S3 website endpoints for your bucket. Website endpoints are different from the endpoints where you send REST API requests. Amazon S3 doesn't support HTTPS access for website endpoints. If you want to use HTTPS, you can use CloudFront to serve a static website hosted on Amazon S3.

- You can use Amazon CloudFront to improve the performance of your website. CloudFront makes your website files (such as HTML, images, and video) available from data centers around the world (called edge locations). When a visitor requests a file from your website, Amazon CloudFront automatically redirects the request to a copy of the file at the nearest edge location. This results in faster download times than if the visitor had requested the content from a data center that is located farther away.

- Amazon CloudFront caches content at edge locations for a period of time that you specify. If a visitor requests content that has been cached for longer than the expiration date, Amazon CloudFront checks the origin server to see if a newer version of the content is available. If a newer version is available, Amazon CloudFront copies the new version to the edge location. Changes that you make to the original content are replicated to edge locations as visitors request the content.

## 23
- A mobile chat application uses Amazon DynamoDB as its database service to provide low latency chat updates.
- A new developer has joined the team and is reviewing the configuration settings for Amazon DynamoDB which have been tweaked for certain technical requirements.
- AWS CloudTrail service has been enabled on all the resources used for the project.
- Yet, Amazon DynamoDB encryption details are nowhere to be found.
Which of the following options can explain the root cause for the given issue?

**Options**
- By default, all Amazon DynamoDB tables are encrypted under AWS managed Keys, which do not write to AWS CloudTrail logs
- By default, all Amazon DynamoDB tables are encrypted using AWS owned keys, which do not write to AWS CloudTrail logs
- By default, all Amazon DynamoDB tables are encrypted under Customer managed keys, which do not write to AWS CloudTrail logs
- By default, all Amazon DynamoDB tables are encrypted using Data keys, which do not write to AWS CloudTrail logs

**Solution**
- By default, all Amazon DynamoDB tables are encrypted using AWS owned keys, which do not write to AWS CloudTrail logs
  - AWS owned keys are not stored in your AWS account. They are part of a collection of KMS keys that AWS owns and manages for use in multiple AWS accounts. AWS services can use AWS owned keys to protect your data. AWS owned keys used by DynamoDB are rotated every year (approximately 365 days).
  - You cannot view, manage, or use AWS owned keys, or audit their use. However, you do not need to do any work or change any programs to protect the keys that encrypt your data. You are not charged a monthly fee or a usage fee for use of AWS owned keys, and they do not count against AWS KMS quotas for your account.
  - All DynamoDB tables are encrypted. There is no option to enable or disable encryption for new or existing tables. By default, all tables are encrypted under an AWS owned key in the DynamoDB service account. However, you can select an option to encrypt some or all of your tables under a customer managed key or the AWS managed key for DynamoDB in your account.

## 24
- A silicon valley based healthcare startup uses AWS Cloud for its IT infrastructure.
- The startup stores patient health records on Amazon Simple Storage Service (Amazon S3).
- The engineering team needs to implement an archival solution based on Amazon S3 Glacier to enforce regulatory and compliance controls on data access.

As a solutions architect, which of the following solutions would you recommend?

**Options**
- Use Amazon S3 Glacier vault to store the sensitive archived data and then use an Amazon S3 Access Control List to enforce compliance controls
- Use Amazon S3 Glacier to store the sensitive archived data and then use an Amazon S3 lifecycle policy to enforce compliance controls
- Use Amazon S3 Glacier vault to store the sensitive archived data and then use a vault lock policy to enforce compliance controls
- Use Amazon S3 Glacier to store the sensitive archived data and then use an Amazon S3 Access Control List to enforce compliance controls

**Solution**
- Use *Amazon S3 Glacier vault* to store the sensitive archived data and then use a vault lock policy to enforce compliance controls
  - An Amazon S3 Glacier vault is a container for storing archives. When you create a vault, you specify a vault name and the AWS Region in which you want to create the vault. Amazon S3 Glacier Vault Lock allows you to easily deploy and enforce compliance controls for individual Amazon S3 Glacier vaults with a vault lock policy. You can specify controls such as “write once read many” (WORM) in a vault lock policy and lock the policy from future edits. Therefore, this is the correct option.

  - Amazon S3 access control lists (ACLs) enable you to manage access to buckets and objects. It cannot be used to enforce compliance controls

## 25
A cyber security company is running a mission critical application using a single Spread placement group of Amazon EC2 instances. The company needs 15 Amazon EC2 instances for optimal performance.

How many Availability Zones (AZs) will the company need to deploy these Amazon EC2 instances per the given use-case?

**Options**
- 3
- 15
- 14
- 7

**Solution**
- 3
  - A [spread placement group](aws-ass-solution-architect.md#ec2_placement_group) can span multiple Availability Zones in the same Region. You can have a maximum of **seven running instances per Availability Zone per group**. Therefore, to deploy 15 Amazon EC2 instances in a single Spread placement group, the company needs to use 3 Availability Zones.

## 26
- An application with global users across AWS Regions had suffered an issue when the Elastic Load Balancing (ELB) in a Region malfunctioned thereby taking down the traffic with it. 
- The manual intervention cost the company significant time and resulted in major revenue loss.

What should a solutions architect recommend to reduce internet latency and add automatic failover across AWS Regions?

**Option**
- Set up an Amazon Route 53 geoproximity routing policy to route traffic
- Set up AWS Direct Connect as the backbone for each of the AWS Regions where the application is deployed
- Set up AWS Global Accelerator and add endpoints to cater to users in different geographic locations
- Create Amazon S3 buckets in different AWS Regions and configure Amazon CloudFront to pick the nearest edge location to the user

**Solution**
- Set up AWS Global Accelerator and add endpoints to cater to users in different geographic locations
  - As your application architecture grows, so does the complexity, with longer user-facing IP lists and more nuanced traffic routing logic. AWS Global Accelerator solves this by providing you with two static IPs that are anycast from our globally distributed edge locations, giving you a single entry point to your application, regardless of how many AWS Regions it’s deployed in. This allows you to add or remove origins, Availability Zones or Regions without reducing your application availability. Your traffic routing is managed manually, or in console with endpoint traffic dials and weights. If your application endpoint has a failure or availability issue, AWS Global Accelerator will automatically redirect your new connections to a healthy endpoint within seconds.

**Wrong**
- *AWS Direct Coonect*:  It cannot be used to serve users directly.
- *S3*: If most of the content is static,
- *Amazon Route 53 geoproximity*: Geoproximity routing lets Amazon Route 53 route traffic to your resources based on the geographic location of your users and your resources. Unlike AWS Global Accelerator, managing and routing to different instances, ELBs and other AWS resources will become an operational overhead as the resource count reaches into the hundreds. With inbuilt features like Static anycast IP addresses, fault tolerance using network zones, Global performance-based routing, TCP Termination at the Edge - AWS Global Accelerator is the right choice for multi-region, low latency use cases.

## 27
- An application hosted on Amazon EC2 contains *sensitive personal information* about all its customers and needs to be protected from all types of cyber-attacks. 
- The company is considering using the AWS Web Application Firewall (AWS WAF) to handle this requirement.

Can you identify the correct solution leveraging the capabilities of AWS WAF?

**Options**
- Create Amazon CloudFront distribution for the application on Amazon EC2 instances. Deploy AWS WAF on Amazon CloudFront to provide the necessary safety measures
- AWS WAF can be directly configured on Amazon EC2 instances for ensuring the security of the underlying application data
- Configure an Application Load Balancer (ALB) to balance the workload for all the Amazon EC2 instances. Configure Amazon CloudFront to distribute from an Application Load Balancer since AWS WAF cannot be directly configured on ALB. This configuration not only provides necessary safety but is scalable too
- AWS WAF can be directly configured only on an Application Load Balancer or an Amazon API Gateway. One of these two services can then be configured with Amazon EC2 to build the needed secure architecture

**Solution**
- Create Amazon CloudFront distribution for the application on Amazon EC2 instances. Deploy AWS WAF on Amazon CloudFront to provide the necessary safety measures

**Wrong**
- EC2: - AWS WAF can be deployed on Amazon CloudFront, the Application Load Balancer (ALB), and Amazon API Gateway. It cannot be configured directly on an Amazon EC2 instance.


## 28
An e-commerce company uses Amazon Simple Queue Service (Amazon SQS) queues to decouple their application architecture. The engineering team has observed message processing failures for some customer orders.

As a solutions architect, which of the following solutions would you recommend for handling such message failures?

**Options**
- Use a temporary queue to handle message processing failures
- Use short polling to handle message processing failures
- Use long polling to handle message processing failures
- Use a dead-letter queue to handle message processing failures

**Solution**
- Use a dead-letter queue to handle message processing failures
  - Dead-letter queues can be used by other queues (source queues) as a target for messages that can't be processed (consumed) successfully. Dead-letter queues are useful for debugging your application or messaging system because they let you isolate problematic messages to determine why their processing doesn't succeed. Sometimes, messages can’t be processed because of a variety of possible issues, such as when a user comments on a story but it remains unprocessed because the original story itself is deleted by the author while the comments were being posted. In such a case, the dead-letter queue can be used to handle message processing failures.


## 29
- A development team has deployed a microservice to the Amazon Elastic Container Service (Amazon ECS).
-  The application layer is in a Docker container that provides both static and dynamic content through an Application Load Balancer.
-  With increasing load, the Amazon ECS cluster is experiencing higher network usage. The development team has looked into the network usage and found that 90% of it is due to distributing static content of the application.

As a Solutions Architect, what do you recommend to improve the application's network usage and decrease costs?

**Options**
- Distribute the dynamic content through Amazon S3
- Distribute the static content through Amazon S3
- Distribute the dynamic content through Amazon EFS
- Distribute the static content through Amazon EFS

**Solution**
- Distribute the static content through Amazon S3

## 30
A DevOps engineer at an IT company was recently added to the admin group of the company's AWS account. The AdministratorAccess managed policy is attached to this group.

Can you identify the AWS tasks that the DevOps engineer CANNOT perform even though he has full Administrator privileges (Select two)?

**Options**
- Delete the IAM user for his manager
- Delete an Amazon S3 bucket from the production environment
- Close the company's AWS account
- Change the password for his own IAM user account
- Configure an Amazon S3 bucket to enable AWS Multi-Factor Authentication (AWS MFA) delete

**Solution**
- Close the company's AWS account
- Configure an Amazon S3 bucket to enable AWS Multi-Factor Authentication (AWS MFA) delete

## 31
Question 31
- A silicon valley based startup helps its users legally sign highly confidential contracts.
- To meet the compliance guidelines, the startup must ensure that the signed contracts are encrypted using the AES-256 algorithm via an encryption key that is generated as well as managed internally.
- The startup is now migrating to AWS Cloud and would like the data to be encrypted on AWS.
- The startup wants to continue using their existing encryption key generation as well as key management mechanism.

What do you recommend?


**Options**
- SSE-KMS
- Client-Side Encryption
- SSE-C
- SSE-S3


**Solution**
- SSE-C


**Wrong**

## 32
Question 32
- A company hires experienced specialists to analyze the customer service calls attended by its call center representatives.
- Now, the company wants to move to AWS Cloud and is looking at an automated solution to analyze customer service calls for sentiment analysis via ad-hoc SQL queries.

As a Solutions Architect, which of the following solutions would you recommend?


**Options**
- Use Amazon Kinesis Data Streams to read the audio files and machine learning (ML) algorithms to convert the audio files into text and run customer sentiment analysis
- Use Amazon Kinesis Data Streams to read the audio files and Amazon Alexa to convert them into text.
- Amazon Kinesis Data Analytics can be used to analyze these files and Amazon Quicksight can be used to visualize and display the output.
- Use Amazon Transcribe to convert audio files to text and Amazon Athena to perform SQL based analysis to understand the underlying customer sentiments
- Use Amazon Transcribe to convert audio files to text and Amazon Quicksight to perform SQL based analysis on these text files to understand the underlying patterns.
- Visualize and display them onto user Dashboards for reporting purposes.


**Solution**
- Use Amazon Transcribe to convert audio files to text and Amazon Athena to perform SQL based analysis to understand the underlying customer sentiments
  + [Amazon Transcribe](##)


**Wrong**

## Question 33
- A leading media company wants to do an accelerated online migration of hundreds of terabytes of files from their on-premises data center to Amazon S3 and then establish a mechanism to access the migrated data for ongoing updates from the on-premises applications.

As a solutions architect, which of the following would you select as the MOST performant solution for the given use-case?


**Options**
- Use AWS DataSync to migrate existing data to Amazon S3 as well as access the Amazon S3 data for ongoing updates
- Use File Gateway configuration of AWS Storage Gateway to migrate data to Amazon S3 and then use Amazon S3 Transfer Acceleration (Amazon S3TA) for ongoing updates from the on-premises applications
- Use Amazon S3 Transfer Acceleration (Amazon S3TA) to migrate existing data to Amazon S3 and then use AWS DataSync for ongoing updates from the on-premises applications
- Use AWS DataSync to migrate existing data to Amazon S3 and then use File Gateway to retain access to the migrated data for ongoing updates from the on-premises applications


**Solution**
- Use [AWS DataSync](aws-ass-solution-architect.md#aws_datasync) to migrate existing data to Amazon S3 and then use [File Gateway](aws-ass-solution-architect.md#file_gateway) to retain access to the migrated data for ongoing updates from the on-premises applications


**Wrong**


## Question 34
- While troubleshooting, a cloud architect realized that the Amazon EC2 instance is unable to connect to the internet using the Internet Gateway.

Which conditions should be met for internet connectivity to be established? (Select two)


**Options**
- The subnet has been configured to be public and has no access to the internet
- The network access control list (network ACL) associated with the subnet must have rules to allow inbound and outbound traffic
- The instance's subnet is associated with multiple route tables with conflicting configurations
- The route table in the instance’s subnet should have a route to an Internet Gateway
- The instance's subnet is not associated with any route table


**Solution**
- The network access control list (network ACL) associated with the subnet must have rules to allow inbound and outbound traffic
  - The [network access control](aws-ass-solution-architect.md#network_acl) list that is associated with the subnet must have rules to allow inbound and outbound traffic on port 80 (for HTTP traffic) and port 443 (for HTTPs traffic). This is a necessary condition for Internet Gateway connectivity.


- The route table in the instance’s subnet should have a route to an Internet Gateway
  - A route table contains a set of rules, called routes, that are used to determine where network traffic from your subnet or gateway is directed. The route table in the instance’s subnet should have a route defined to the Internet Gateway.
**Wrong**




## Question 35
- A financial services firm uses a high-frequency trading system and wants to write the log files into Amazon S3.
- The system will also read these log files in parallel on a near real-time basis.
- The engineering team wants to address any data discrepancies that might arise when the trading system overwrites an existing log file and then tries to read that specific log file.

Which of the following options BEST describes the capabilities of Amazon S3 relevant to this scenario?


**Options**
- A process replaces an existing object and immediately tries to read it.
Until the change is fully propagated, Amazon S3 might return the new data.
- A process replaces an existing object and immediately tries to read it.
Until the change is fully propagated, Amazon S3 might return the previous data.
- A process replaces an existing object and immediately tries to read it.
 Until the change is fully propagated, Amazon S3 does not return any data.
- A process replaces an existing object and immediately tries to read it.
 Amazon S3 always returns the latest version of the object.


**Solution**

 - Amazon S3 always returns the latest version of the object.
Amazon S3 delivers strong read-after-write consistency automatically, without changes to performance or availability, without sacrificing regional isolation for applications, and at no additional cost.

After a successful write of a new object or an overwrite of an existing object, any subsequent read request immediately receives the latest version of the object. Amazon S3 also provides strong consistency for list operations, so after a write, you can immediately perform a listing of the objects in a bucket with any changes reflected.

Strong read-after-write consistency helps when you need to immediately read an object after a write. For example, strong read-after-write consistency when you often read and list immediately after writing objects.

To summarize, all Amazon S3 GET, PUT, and LIST operations, as well as operations that change object tags, ACLs, or metadata, are strongly consistent. What you write is what you will read, and the results of a LIST will be an accurate reflection of what’s in the bucket.

**Wrong**

## Question 36
- A health-care company manages its web application on Amazon EC2 instances running behind Auto Scaling group (ASG).
- The company provides ambulances for critical patients and needs the application to be reliable.
- The workload of the company can be managed on 2 Amazon EC2 instances and can peak up to 6 instances when traffic increases.

As a Solutions Architect, which of the following configurations would you select as the best fit for these requirements?


**Options**
- The Auto Scaling group should be configured with the minimum capacity set to 4, with 2 instances each in two different Availability Zones. The maximum capacity of the Auto Scaling group should be set to 6.
- The Auto Scaling group should be configured with the minimum capacity set to 4, with 2 instances each in two different AWS Regions.The maximum capacity of the Auto Scaling group should be set to 6.
- The Auto Scaling group should be configured with the minimum capacity set to 2 and the maximum capacity set to 6 in a single Availability Zone
- The Auto Scaling group should be configured with the minimum capacity set to 2, with 1 instance each in two different Availability Zones. The maximum capacity of the Auto Scaling group should be set to 6.


**Solution**
- The Auto Scaling group should be configured with the minimum capacity set to 4, with 2 instances each in two different Availability Zones. The maximum capacity of the Auto Scaling group should be set to 6.
  - Amazon EC2 Auto Scaling attempts to distribute instances evenly between the Availability Zones that are enabled for your Auto Scaling group. This is why the minimum capacity should be 4 instances and not 2. Auto Scaling group will launch 2 instances each in both the AZs and this redundancy is needed to keep the service available always.
  - Amazon EC2 Auto Scaling enables you to take advantage of the safety and reliability of geographic redundancy by spanning Auto Scaling groups across multiple Availability Zones within a Region. When one Availability Zone becomes unhealthy or unavailable, Auto Scaling launches new instances in an unaffected Availability Zone. When the unhealthy Availability Zone returns to a healthy state, Auto Scaling automatically redistributes the application instances evenly across all of the designated Availability Zones. Since the application is extremely critical and needs to have a reliable architecture to support it, the Amazon EC2 instances should be maintained in at least two Availability Zones (AZs) for uninterrupted service.

**Wrong**

Which of the following is true regarding cross-zone load balancing as seen in Application Load Balancer versus Network Load Balancer?


**Options**
- By default, cross-zone load balancing is enabled for Application Load Balancer and disabled for Network Load Balancer
- By default, cross-zone load balancing is enabled for both Application Load Balancer and Network Load Balancer
- By default, cross-zone load balancing is disabled for Application Load Balancer and enabled for Network Load Balancer
- By default, cross-zone load balancing is disabled for both Application Load Balancer and Network Load Balancer


**Solution**


**Wrong**

## Question 37
Which of the following is true regarding cross-zone load balancing as seen in Application Load Balancer versus Network Load Balancer?


**Options**
- By default, cross-zone load balancing is enabled for Application Load Balancer and disabled for Network Load Balancer
- By default, cross-zone load balancing is enabled for both Application Load Balancer and Network Load Balancer
- By default, cross-zone load balancing is disabled for Application Load Balancer and enabled for Network Load Balancer
- By default, cross-zone load balancing is disabled for both Application Load Balancer and Network Load Balancer


**Solution**
- By default, cross-zone load balancing is enabled for Application Load Balancer and disabled for Network Load Balancer

**Wrong**


## Question 38
- A financial services company has to retain the activity logs for each of their customers to meet compliance guidelines.
- Depending on the business line, the company wants to retain the logs for 5-10 years in highly available and durable storage on AWS.
- The overall data size is expected to be in Petabytes.
- In case of an audit, the data would need to be accessible within a timeframe of up to 48 hours.

Which AWS storage option is the MOST cost-effective for the given compliance requirements?


**Options**
- Amazon S3 Standard storage
- Third party tape storage
- Amazon S3 Glacier Deep Archive
- Amazon S3 Glacier


**Solution**
- Amazon S3 Glacier Deep Archive
  - ![](https://assets-pt.media.datacumulus.com/aws-saa-pt/assets/pt5-q24-i1.jpg)


**Wrong**

Amazon S3 Glacier - As mentioned earlier, Amazon S3 Glacier Deep Archive is up to 75% less expensive than Amazon S3 Glacier and provides retrieval within 12 hours. So using Amazon S3 Glacier is not the correct choice.

## Question 39
- You have built an application that is deployed with Elastic Load Balancing and an Auto Scaling Group.
- As a Solutions Architect, you have configured aggressive Amazon CloudWatch alarms, making your Auto Scaling Group (ASG) scale in and out very quickly, renewing your fleet of Amazon EC2 instances on a daily basis.
- A production bug appeared two days ago, but the team is unable to SSH into the instance to debug the issue, because the instance has already been terminated by the Auto Scaling Group.
- The log files are saved on the Amazon EC2 instance.

How will you resolve the issue and make sure it doesn't happen again?


**Options**
- Use AWS Lambda to regularly SSH into the Amazon EC2 instances and copy the log files to Amazon S3
- Make a snapshot of the Amazon EC2 instance just before it gets terminated
- Install an Amazon CloudWatch Logs agents on the Amazon EC2 instances to send logs to Amazon CloudWatch
- Disable the Termination from the Auto Scaling Group any time a user reports an issue


**Solution**
- Install an Amazon CloudWatch Logs agents on the Amazon EC2 instances to send logs to Amazon CloudWatch
  - You can use the Amazon CloudWatch Logs agent installer on an existing Amazon EC2 instance to install and configure the Amazon CloudWatch Logs agent. After installation is complete, logs automatically flow from the instance to the log stream you create while installing the agent. The agent confirms that it has started and it stays running until you disable it.

**Wrong**

## Question 40
- An Internet-of-Things (IoT) company is looking for a database solution on AWS Cloud that has Auto Scaling capabilities and is highly available.
- The database should be able to handle any changes in data attributes over time, in case the company updates the data feed from its IoT devices.
- The database must provide the capability to output a continuous stream with details of any changes to the underlying data.

As a Solutions Architect, which database will you recommend?


**Options**
- Amazon Redshift
- Amazon Relational Database Service (Amazon RDS)
- Amazon DynamoDB
- Amazon Aurora

**Solution**
- Amazon DynamoDB
  - Whenever an application creates, updates, or deletes items in the table, DynamoDB Streams writes a stream record with the primary key attributes of the items that were modified. A stream record contains information about a data modification to a single item in a DynamoDB table. You can configure the stream so that the stream records capture additional information, such as the "before" and "after" images of modified items.

**Wrong**
