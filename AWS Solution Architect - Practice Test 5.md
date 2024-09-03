# Practice Test 5

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

Question 19
- A startup has created a cost-effective backup solution in another AWS Region. 
- The application is running in warm standby mode and has Application Load Balancer (ALB) to support it from the front.
- The current failover process is manual and requires updating the DNS alias record to point to the secondary Application Load Balancer in another Region in case of failure of the primary Application Load Balancer.

As a Solutions Architect, what will you recommend to automate the failover process?

**Options**
Enable an Amazon Route 53 health check
Configure AWS Trusted Advisor to check on unhealthy instances
Enable an Amazon EC2 instance health check
Enable an ALB health check
**Solution**
Enable an Amazon Route 53 health check

Determining the health of an ELB endpoint is more complex than health checking a single IP address. For example, what if your application is running fine on Amazon EC2, but the load balancer itself isn't reachable? Or if your load balancer and your Amazon EC2 instances are working correctly, but a bug in your code causes your application to crash? Or how about if the Amazon EC2 instances in one Availability Zone of a multi-AZ ELB are experiencing problems?

Amazon Route 53 DNS Failover handles all of these failure scenarios by integrating with ELB behind the scenes. Once enabled, Route 53 automatically configures and manages health checks for individual ELB nodes. Amazon Route 53 also takes advantage of the Amazon EC2 instance health checking that ELB performs (information on configuring your ELB health checks is available here). By combining the results of health checks of your Amazon EC2 instances and your ELBs, Amazon Route 53 DNS Failover can evaluate the health of the load balancer and the health of the application running on the Amazon EC2 instances behind it. In other words, if any part of the stack goes down, Amazon Route 53 detects the failure and routes traffic away from the failed endpoint.

Using Amazon Route 53 DNS Failover, you can run your primary application simultaneously in multiple AWS regions around the world and failover across regions. Your end-users will be routed to the closest (by latency), healthy region for your application. Amazon Route 53 automatically removes from service any region where your application is unavailable - it will pull an endpoint out of service if there is region-wide connectivity or operational issue, if your application goes down in that region, or if your ELB or Amazon EC2 instances go down in that region.

**Wrong**
*Enable an ALB health check* - ELB health check verifies that a specified TCP port on an instance is accepting connections or a specified page has returned an error code of 200. It is not useful for the given failover scenario.

**Enable an Amazon EC2 instance health check** - Instance status checks monitor the software and network configuration of your instance. It is not intelligent enough to understand if the application on the instance is working correctly. Hence, this is not the right choice for the given use-case.

**Configure AWS Trusted Advisor to check on unhealthy instances** - AWS Trusted Advisor examines the health check configuration for Auto Scaling groups. If Elastic Load Balancing is being used for an Auto Scaling group, the recommended configuration is to enable an Elastic Load Balancing health check. AWS Trusted Advisor recommends certain configuration changes by comparing your system configurations to AWS Best practices. It cannot handle a failover the way Amazon Route 53 does.

