# Practice Test 4

## Question 1
A small rental company had 5 employees, all working under the same AWS cloud account. 
These employees deployed their applications built for various functions- including billing, operations, finance, etc. Each of these employees has been operating in their own VPC.
 Now, there is a need to connect these VPCs so that the applications can communicate with each other.

Which of the following is the MOST cost-effective solution for this use-case?

**Solution**
- Use a VPC peering connection
  - [vpc_peering](aws-ass-solution-architect.md#vpc_peering)
**Wrong**

- Use an [AWS Direct Connect connection](aws-ass-solution-architect.md#aws_direct_connect)
  
- Use a [Network Address Translation gateway](aws-ass-solution-architect.md#vpc_nat_gateway) (NAT gateway)

- [Use an Internet Gateway](aws-ass-solution-architect.md#vpc_internet_gateway)

## Question 2
- As a solutions architect, you have created a solution that utilizes an Application Load Balancer with stickiness and an Auto Scaling Group (ASG). 
- The Auto Scaling Group spans across 2 Availability Zones (AZs). 
  - AZ-A has 3 Amazon EC2 instances 
  - AZ-B has 4 Amazon EC2 instances. 
- The Auto Scaling Group is about to go into a scale-in event due to the triggering of a Amazon CloudWatch alarm.

What will happen under the default Auto Scaling Group configuration?

**Solution**
- The instance with the oldest launch template or launch configuration will be terminated in AZ-B
  - [EC2_Default_Termination_Policy](aws-ass-solution-architect.md#EC2_Default_Termination_Policy)

**Wrong**
- A random instance will be terminated in AZ-B
- An instance in the AZ-A will be created
- A random instance in the AZ-A will be terminated

## Question 3
Amazon Route 53 is configured to route traffic to two Network Load Balancer nodes belonging to two Availability Zones (AZs): AZ-A and AZ-B. 
Cross-zone load balancing is disabled. 
AZ-A has four targets and AZ-B has six targets.

Which of the below statements is true about traffic distribution to the target instances from Amazon Route 53?

**Solution**
- Each of the four targets in AZ-A receives 12.5% of the traffic
  - [elb_crosszoneloadbalancing](aws-ass-solution-architect.md#elb_crosszoneloadbalancing)
**Wrong**
- Each of the six targets in AZ-B receives 10% of the traffic
- Each of the four targets in AZ-A receives 10% of the traffic
- Each of the four targets in AZ-A receives 8% of the traffic

## Question 4
A media company uses Amazon ElastiCache Redis to enhance the performance of its Amazon RDS database layer. The company wants a robust disaster recovery strategy for its caching layer that guarantees minimal downtime as well as minimal data loss while ensuring good application performance.

Which of the following solutions will you recommend to address the given use-case?

**Solution**
- Opt for Multi-AZ configuration with automatic failover functionality to help mitigate failure
  - [rds_multi_az](aws-ass-solution-architect.md#rds_multi_az)
  - 
**Wrong**
- Schedule daily automatic backups at a time when you expect low resource utilization for your cluster
- Schedule manual backups using Redis append-only file (AOF)
  - Manual backups using AOF are retained indefinitely and are useful for testing and archiving. You can schedule manual backups to occur up to 20 times per node within any 24-hour period. Although AOF provides a measure of fault tolerance, it can't protect your data from a hardware-related cache node failure, so there is a risk of data loss.
- Add read-replicas across multiple availability zones (AZs) to reduce the risk of potential data loss because of failure
  - To scale read capacity, Amazon ElastiCache allows you to add up to five read replicas across multiple availability zones. Read replicas are used to ease out read traffic from the primary database and cannot be used as a complete fault-tolerant solution in itself.

## Question 5
A retail company uses AWS Cloud to manage its technology infrastructure. The company has deployed its consumer-focused web application on Amazon EC2-based web servers and uses Amazon RDS PostgreSQL database as the data store. The PostgreSQL database is set up in a private subnet that allows inbound traffic from selected Amazon EC2 instances. The database also uses AWS Key Management Service (AWS KMS) for encrypting data at rest.

Which of the following steps would you recommend to facilitate end-to-end security for the data-in-transit while accessing the database?

**Solution**
- Configure Amazon RDS to use SSL for data in transit
  - [](aws-ass-solution-architect.md#rds_ssl)
**Wrong**
- Create a new network access control list (network ACL) that blocks SSH from the entire Amazon EC2 subnet into the database
  - You cannot SSH into an Amazon RDS database instance.
- Create a new security group that blocks SSH from the selected Amazon EC2 instances into the database
  - You cannot SSH into an Amazon RDS database instance.
- Use IAM authentication to access the database instead of the database user's access credentials
  - You can authenticate to your database instance using AWS Identity and Access Management (IAM) database authentication. IAM database authentication works with MySQL and PostgreSQL. With this authentication method, you don't need to use a password when you connect to a database instance. Instead, you use an authentication token.
  - IAM authentication is just another way to authenticate the user's credentials while accessing the database. It would not significantly enhance the security in a way that enabling SSL does by facilitating the in-transit encryption for the database.


## Question 6
A financial services firm has traditionally operated with an on-premise data center and would like to create a disaster recovery strategy leveraging the AWS Cloud.

As a Solutions Architect, you would like to ensure that a scaled-down version of a fully functional environment is always running in the AWS cloud, and in case of a disaster, the recovery time is kept to a minimum. Which disaster recovery strategy is that?

**Solution**
- Warm Standby
  - [](aws-ass-solution-architect.md#disaster_recovery_strategy)
**Wrong**
- Pilot Light
- Backup and Restore
- Multi Site

## Question 7
- A developer in your company has set up a classic 2 tier architecture consisting of an Application Load Balancer and an Auto Scaling group (ASG) managing a fleet of Amazon EC2 instances. 
- The Application Load Balancer is deployed in a subnet of size 10.0.1.0/24 
- The Auto Scaling group is deployed in a subnet of size 10.0.4.0/22.

As a solutions architect, you would like to adhere to the security pillar of the well-architected framework. How do you configure the security group of the Amazon EC2 instances to only allow traffic coming from the Application Load Balancer?

**Solution**
- Add a rule to authorize the security group of the Application Load Balancer
  - [Security Group](aws-ass-solution-architect.md#security_group)
  - [ALB](aws-ass-solution-architect.md#alb)
**Wrong**

- Add a rule to authorize the CIDR 10.0.1.0/24
- Add a rule to authorize the security group of the Auto Scaling group
- Add a rule to authorize the CIDR 10.0.4.0/22
- Adding the entire CIDR of the Application Load Balancer would work, but wouldn't guarantee that only the Auto Scaling group can access the Amazon EC2 instances that are part of the Auto Scaling group. Here, the right solution is to add a rule on the Auto Scaling group security group to allow incoming traffic only from the security group configured for the Application Load Balancer.

## Question 8
- A CRM company has a software as a service (SaaS) application that feeds updates to other in-house and third-party applications. 
- The SaaS application and the in-house applications are being migrated to use AWS services for this inter-application communication.

As a Solutions Architect, which of the following would you suggest to asynchronously decouple the architecture?

**Solution**
- Use Amazon EventBridge to decouple the system architecture
  - [EventBridge](aws-ass-solution-architect.md#event_bridge)
  - Both Amazon EventBridge and Amazon SNS can be used to develop event-driven applications, but for this use case, EventBridge is the right fit.
**Wrong**
- Use Amazon EventBridge to decouple the system architecture
  - Both Amazon EventBridge and Amazon SNS can be used to develop event-driven applications, but for this use case, EventBridge is the right fit.
- Use Elastic Load Balancing (ELB) for effective decoupling of system architecture
- Use Amazon Simple Notification Service (Amazon SNS) to communicate between systems and decouple the architecture
  - Amazon SNS does not support third-party services integration.

## Question 9
- The engineering team at a global e-commerce company is currently reviewing their disaster recovery strategy. 
- The team has outlined that they need to be able to quickly recover their application stack with a Recovery Time Objective (RTO) of 5 minutes, in all of the AWS Regions that the application runs. 
- The application stack currently takes over 45 minutes to install on a Linux system.

As a Solutions architect, which of the following options would you recommend as the disaster recovery strategy?
**Solution**
- Create an Amazon Machine Image (AMI) after installing the software and copy the AMI across all Regions. Use this Region-specific AMI to run the recovery process in the respective Regions
  - [AMI](aws-ass-solution-architect.md#ami)
  - [AMI Cross-Region Copying](aws-ass-solution-architect.md#ami_cross_region_copying)
**Wrong**
- Store the installation files in Amazon S3 for quicker retrieval
- Use Amazon EC2 user data to speed up the installation process
- Create an Amazon Machine Image (AMI) after installing the software and use this AMI to run the recovery process in other Regions

## Question 10
- A music-sharing company uses a Network Load Balancer to direct traffic to 5 Amazon EC2 instances managed by an Auto Scaling group. 
- When a very popular song is released, the Auto Scaling Group scales to 100 instances and the company incurs high network and compute fees.

The company wants a solution to reduce the costs without changing any of the application code. What do you recommend?

**Solution**
- Use an Amazon CloudFront distribution
  - [Amazon CloudFront distribution](aws-ass-solution-architect.md#cloudfront)
  - Amazon CloudFront is the right answer because we can put it in front of our *Auto Scaling group* and leverage a Global Caching feature that will help us distribute the content reliably with dramatically reduced costs (the ASG won't need to scale as much).
**Wrong**
- Leverage [AWS Storage Gateway](aws-ass-solution-architect.md#aws_storage_gateway)
- Move the songs to Amazon S3
- Move the songs to Amazon S3 Glacier

## Question 11

- A ride-sharing company wants to improve the ride-tracking system that stores GPS coordinates for all rides. - The engineering team at the company is looking for a *NoSQL database* that has single-digit millisecond latency, can scale horizontally, and is serverless, so that they can perform high-frequency lookups reliably.

As a Solutions Architect, which database do you recommend for their requirements?

**Solution**
- [Amazon DynamoDB](aws-ass-solution-architect.md#dynamodb)
**Wrong**

- [Amazon ElastiCache](aws-ass-solution-architect.md#elasticache)
- [Amazon Relational Database Service (Amazon RDS)](aws-ass-solution-architect.md#rds)
- [Amazon Neptune](aws-ass-solution-architect.md#neptune)

## Question 12
- Your company runs a web portal to match developers to clients who need their help. 
- As a solutions architect, you've designed the architecture of the website to be fully serverless with **Amazon API Gateway** and **AWS Lambda**.
- The backend uses **Amazon DynamoDB** table. 
- You would like to automatically congratulate your developers on important milestones, such as - their first paid contract. All the contracts are stored in Amazon DynamoDB.

Which Amazon DynamoDB feature can you use to implement this functionality such that there is LEAST delay in sending automatic notifications?

**Solution**

- [Amazon DynamoDB Streams + AWS Lambda](aws-ass-solution-architect.md#dynamodb)
  - [DynamoDB_Streams](aws-ass-solution-architect.md#dynamodb_streams)
  - [AWS Lambda](aws-ass-solution-architect.md#lambda)
  - Amazon DynamoDB Streams will contain a stream of all the changes that happen to an Amazon DynamoDB table. It can be chained with an AWS Lambda function that will be triggered to react to these changes, one of which is the developer's milestone. Therefore, this is the correct

**Wrong**

- Amazon EventBridge events + AWS Lambda
- Amazon Simple Queue Service (Amazon SQS) + AWS Lambda
- Amazon DynamoDB DAX + Amazon API Gateway
  -[DAX](aws-ass-solution-architect.md#dynamodb-acceleratordax)
  - DAX is a caching layer and Amazon API Gateway is used to deploy APIs at scale, so this won't help


## 13
The development team at a social media company wants to handle some complicated queries such as "What are the number of likes on the videos that have been posted by friends of a user A?".

As a solutions architect, which of the following AWS database services would you suggest as the BEST fit to handle such use cases?


**Solution**

- Amazon Neptune
  - [Neptune](aws-ass-solution-architect.md#neptune)

**Wrong**

- Amazon Redshift
  - [Redshift](aws-ass-solution-architect.md#redshift)
- Amazon OpenSearch Service
  - [OpenSearch](aws-ass-solution-architect.md#Open_Search)
- Amazon Aurora
  - [Aurora](aws-ass-solution-architect.md#aurora)


## Question 14
- A company has noticed that its *Amazon EBS Elastic Volume (io1)* accounts for 90% of the cost and the remaining 10% cost can be attributed to the Amazon EC2 instance. 
- The *Amazon CloudWatch metrics* report that both the Amazon EC2 instance and the Amazon EBS volume are under-utilized.
- The Amazon CloudWatch metrics also show that the Amazon EBS volume has occasional I/O bursts. 
- The entire infrastructure is managed by AWS CloudFormation.

As a Solutions Architect, what do you propose to reduce the costs?

**Solution**
- Convert the Amazon EC2 instance EBS volume to gp2
  - [EBS](aws-ass-solution-architect.md#ebs)
  - *General Purpose SSD (gp2)* volumes offer cost-effective storage that is ideal for a broad range of workloads. These volumes deliver single-digit millisecond latencies and the ability to burst to 3,000 IOPS for an extended duration. 
  - Between a minimum of 100 IOPS (at 33.33 GiB and below) and a maximum of 16,000 IOPS (at 5,334 GiB and above), baseline performance scales linearly at 3 IOPS per GiB of volume size. 
  - AWS designs gp2 volumes to deliver a provisioned performance of 99% uptime. A gp2 volume can range in size from 1 GiB to 16 TiB.

**Wrong**

- Don't use a AWS CloudFormation template to create the database as the AWS CloudFormation service incurs greater service charges
  - This statement is incorrect as AWS CloudFormation is a free service to use
- Change the Amazon EC2 instance type to something much smaller
- Keep the Amazon EBS volume to io1 and reduce the IOPS
  - Keeping the Amazon EBS volume to io1 and reducing the IOPS may interfere with the burst of performance we need

## 15 Question 15
- You have developed a new REST API leveraging the Amazon API Gateway, AWS Lambda and Amazon Aurora database services. 
- Most of the workload on the website is read-heavy. 
- The data rarely changes and it is acceptable to serve users outdated data for about 24 hours.
- Recently, the website has been experiencing high load and the costs incurred on the Aurora database have been very high.

How can you easily reduce the costs while improving performance, with minimal changes?

**Solution**

Enable Amazon API Gateway Caching
  - [Api_Gateway_Caching](aws-ass-solution-architect.md#Api_Gateway_Cachingy)

**Wrong**
- Enable AWS Lambda In Memory Caching
  - Labmda don't have
- Switch to using an [Application Load Balancer](aws-ass-solution-architect.md#alb)
  - Switching to a Load Balancer would not improve the current status as we need a caching mechanism.
- Add Amazon Aurora Read Replicas
  - Adding Aurora Read Replicas would greatly increase the cost, therefore this option is ruled out.

## Question 16
- A company has developed a popular photo-sharing website using a serverless pattern on the AWS Cloud using Amazon API Gateway and AWS Lambda. The backend uses an Amazon RDS PostgreSQL database. 
- The website is experiencing high read traffic and the AWS Lambda functions are putting an increased read load on the Amazon RDS database.

The architecture team is planning to increase the read throughput of the database, without changing the application's core logic. As a Solutions Architect, what do you recommend?

**Solution**
- Use [Amazon RDS Read Replicas](aws-ass-solution-architect.md#rds_read_replicas)

**Wrong**
- Use Amazon DynamoDB
- Use Amazon ElastiCache
- Use Amazon RDS Multi-AZ feature

## Question 17
- A Big Data processing company has created a distributed data processing framework that performs best if the network performance between the processing machines is high. 
- The application has to be deployed on AWS, and the company is only looking at performance as the key measure.
- As a Solutions Architect, which deployment do you recommend?

**Solution**

- Use a [Cluster placement group](aws-ass-solution-architect.md#ec2_placement_group)

**Wrong**
- Use Spot Instances
  - Spot Instances are a cost-effective choice if you can be flexible about when your applications run and if your applications can be interrupted. Since performance is the key criteria, this is not the right choice.
- Use a Spread placement group
  - A spread placement group can span multiple Availability Zones (AZs) in the same Region
- Optimize the Amazon EC2 kernel using EC2 User Data
  - Optimizing the Amazon EC2 kernel won't help with network performance 

## Question 18
- An Internet of Things (IoT) company would like to have a streaming system that performs real-time analytics on the ingested IoT data. 
- Once the analytics is done, the company would like to send notifications back to the mobile applications of the IoT device owners.
- As a solutions architect, which of the following AWS technologies would you recommend to send these notifications to the mobile applications?

**Solution**
- Amazon Kinesis with Amazon Simple Notification Service (Amazon SNS)
  - Amazon Kinesis makes it easy to collect, process, and analyze real-time, streaming data so you can get timely insights and react quickly to new information. Amazon Kinesis offers key capabilities to cost-effectively process streaming data at any scale, along with the flexibility to choose the tools that best suit the requirements of your application.
  - With Amazon Kinesis, you can ingest real-time data such as video, audio, application logs, website clickstreams, and IoT telemetry data for machine learning, analytics, and other applications. Amazon Kinesis enables you to process and analyze data as it arrives and respond instantly instead of having to wait until all your data is collected before the processing can begin
  - Amazon Kinesis will be great for event streaming from the IoT devices
  - [Amazon Kinesis](aws-ass-solution-architect.md#kinesis_data_stream)
  - [SNS](aws-ass-solution-architect.md#sns)

**Wrong**
- Amazon Kinesis with Amazon Simple Email Service (Amazon SES)
- Amazon Simple Queue Service (Amazon SQS) with Amazon Simple Notification Service (Amazon SNS)
- Amazon Kinesis with Amazon Simple Queue Service (Amazon SQS)
  

## Question 19
- An e-commerce company tracks user clicks on its flagship website and performs analytics to provide *near-real-time product recommendations*. 
- An Amazon EC2 instance receives data from the website and sends the data to an Amazon Aurora Database instance.
- Another Amazon EC2 instance continuously checks the changes in the database and executes SQL queries to provide recommendations. 
- Now, the company wants a redesign to decouple and scale the infrastructure. The solution must ensure that data can be analyzed in real-time without any data loss even when the company sees huge traffic spikes.

What would you recommend as an AWS Certified Solutions Architect - Associate?

**Solution**
- Leverage Amazon Kinesis Data Streams to capture the data from the website and feed it into Amazon Kinesis Data Analytics which can query the data in real time. Lastly, the analyzed feed is output into Amazon Kinesis Data Firehose to persist the data on Amazon S3
  - You can use [Amazon Kinesis Data Streams](aws-ass-solution-architect.md#kinesis_data_stream) to build custom applications that process or analyze streaming data for specialized needs. Amazon Kinesis Data Streams manages the infrastructure, storage, networking, and configuration needed to stream your data at the level of your data throughput. You don't have to worry about provisioning, deployment, or ongoing maintenance of hardware, software, or other services for your data streams.
  - For the given use case, you can use [Amazon Kinesis Data Analytics](aws-ass-solution-architect.md#kinesis_data_analytics) to transform and analyze incoming streaming data from Kinesis Data Streams in real time. Kinesis Data Analytics takes care of everything required to run streaming applications continuously, and scales automatically to match the volume and throughput of your incoming data. With Amazon Kinesis Data Analytics, there are no servers to manage, no minimum fee or setup cost, and you only pay for the resources your streaming applications consume.
  - For the given use case, post the real-time analysis, the output feed from Kinesis Data Analytics is output into [Kinesis Data Firehose](aws-ass-solution-architect.md#firehose) which dumps the data into Amazon S3 without any data loss.


**Wrong**
- Leverage Amazon Kinesis Data Streams to capture the data from the website and feed it into Amazon [QuickSight](aws-ass-solution-architect.md#QuickSight) which can query the data in real time. Lastly, the analyzed feed is output into Kinesis Data Firehose to persist the data on Amazon S3
- Leverage Amazon SQS to capture the data from the website. Configure a fleet of Amazon EC2 instances under an Auto scaling group to process messages from the Amazon SQS queue and trigger the scaling policy based on the number of pending messages in the queue. Perform real-time analytics using a third-party library on the Amazon EC2 instances
- Leverage Amazon Kinesis Data Streams to capture the data from the website and feed it into Amazon Kinesis Data Firehose to persist the data on Amazon S3. Lastly, use Amazon Athena to analyze the data in real time

## Question 20
- An e-commerce company has copied 1 petabyte of data from its on-premises data center to an Amazon S3 bucket in `the us-west-1` Region using an `AWS Direct Connect` link. 
- The company now wants to set up a one-time copy of the data to another Amazon S3 bucket in the `us-east-1` Region. 
- The on-premises data center does not allow the use of AWS Snowball.

As a Solutions Architect, which of the following options can be used to accomplish this goal? (Select two)

**Solution**
- Set up Amazon S3 batch replication to copy objects across Amazon S3 buckets in another Region using S3 console and then delete the replication configuration
  - [](aws-ass-solution-architect.md#s3_batch_replication)

- Copy data from the source bucket to the destination bucket using the aws S3 sync command
  - [S3_Sync_command](aws-ass-solution-architect.md#s3_sync_command)

**Wrong**

- Use AWS Snowball Edge device to copy the data from one Region to another Region

- Copy data from the source Amazon S3 bucket to a target Amazon S3 bucket using the S3 console
- Set up Amazon S3 Transfer Acceleration (Amazon S3TA) to copy objects across Amazon S3 buckets in different Regions using S3 console