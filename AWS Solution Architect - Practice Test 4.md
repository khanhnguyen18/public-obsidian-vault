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


## 21
- A company has recently created a new department to handle their services workload. 
- An IT team has been asked to create a custom VPC to isolate the resources created in this new department. 
- They have set up the public subnet and [internet gateway (IGW)](aws-ass-solution-architect.md#vpc_internet_gateway). 
- However, they are not able to ping the Amazon EC2 instances with elastic IP address (EIP) launched in the newly created VPC.

As a Solutions Architect, the team has requested your help. How will you troubleshoot this scenario? (Select two)

**Solution**
- Check if the security groups allow ping from the source
  - [security_group](aws-ass-solution-architect.md#security_group)
- Check if the route table is configured with internet gateway
**Wrong**
- Contact AWS support to map your VPC with subnet
- Create a secondary internet gateway to attach with public subnet and move the current internet gateway to private and write route tables
- Disable Source / Destination check on the Amazon EC2 instance
  - The Source/Destination Check attribute controls whether source/destination checking is enabled on the instance. Disabling this attribute enables an instance to handle network traffic that isn't specifically destined for the instance. For example, instances running services such as network address translation, routing, or a firewall should set this value to disabled. The default value is enabled. Source/Destination Check is not relevant to the question and it has been added as a distractor.


## Question 22
- The engineering team at a company is running batch workloads on AWS Cloud. 
- The team has embedded Amazon RDS database connection strings within each web server hosting the flagship application. 
- After failing a security audit, the team is looking at a different approach to store the database secrets securely and automatically rotate the database credentials.

Which of the following solutions would you recommend to meet this requirement?

**Solution**
- AWS Secrets Manager

**Wrong**
Question 22
Skipped
The engineering team at a company is running batch workloads on AWS Cloud. The team has embedded Amazon RDS database connection strings within each web server hosting the flagship application. After failing a security audit, the team is looking at a different approach to store the database secrets securely and automatically rotate the database credentials.

Which of the following solutions would you recommend to meet this requirement?

**Solution**
- AWS Secrets Manager
  - [AWS_Secrets_Manager](aws-ass-solution-architect.md#aws_secrets_manager)

**Wrong**
- [AWS Systems Manager Parameter Store](aws-ass-solution-architect.md#aws_systems_manager_parameter_store)
  - Not support automatically rotate DB Credential
- AWS Key Management Service (KMS)
  - Cannot store secrets
- [AWS Systems Manager](aws-ass-solution-architect.md#aws_system_manager)
  - AWS Systems Manager cannot be used to store your secrets securely and automatically rotate the database credentials.

## 23
A startup's cloud infrastructure consists of a few *Amazon EC2 instances*, *Amazon RDS instances* and *Amazon S3 storage*. A year into their business operations, the startup is incurring costs that seem too high for their business requirements.

Which of the following options represents a valid cost-optimization solution?

**Solution**
- Use [AWS Cost Explorer](aws-ass-solution-architect.md#aws_cost_explorer) Resource Optimization to get a report of Amazon EC2 instances that are either idle or have low utilization and use [AWS Compute Optimizer](aws-ass-solution-architect.md#aws_compute_optimizer) to look at instance type recommendations

**Wrong**
- Use [Amazon S3 Storage class analysis](aws-ass-solution-architect.md#s3_analytics_storage_class_analysis) to get recommendations for transitions of objects to Amazon S3 Glacier storage classes to reduce storage costs. You can also automate moving these objects into lower-cost storage tier using Lifecycle Policies
  -By using Amazon S3 Analytics Storage Class analysis you can analyze storage access patterns to help you decide when to transition the right data to the right storage class 
  - Help you determine when to transition less frequently accessed STANDARD storage to the STANDARD_IA (IA, for infrequent access) storage class. 
  - Storage class analysis does not give recommendations for transitions to the ONEZONE_IA or S3 Glacier storage classes.
- Use AWS Compute Optimizer recommendations to help you choose the optimal Amazon EC2 purchasing options and help reserve your instance capacities at reduced costs
  - AWS Compute Optimizer recommends optimal AWS Compute resources for your workloads to reduce costs and improve performance by using machine learning to analyze historical utilization metrics. Over-provisioning compute can lead to unnecessary infrastructure cost and under-provisioning compute can lead to poor application performance. Compute Optimizer helps you choose the optimal Amazon EC2 instance types, including those that are part of an Amazon EC2 Auto Scaling group, based on your utilization data. It does not recommend instance purchase options.
- Use [AWS Trusted Advisor](aws-ass-solution-architect.md#aws_trust_advisor) checks on Amazon EC2 Reserved Instances to automatically renew reserved instances (RI). AWS Trusted advisor also suggests Amazon RDS idle database instances
  - AWS Trusted advisor does not have a feature to auto-renew Reserved Instances.

## 24
- A ride-sharing company wants to use an Amazon DynamoDB table for data storage. 
- The table will not be used during the night hours whereas the read and write traffic will often be unpredictable during day hours. 
- When traffic spikes occur they will happen very quickly.

Which of the following will you recommend as the best-fit solution?

**Solution**
- Set up Amazon DynamoDB table in the on-demand capacity mode
  - [DynamoDB_Capacity_Mode](aws-ass-solution-architect.md#dynamodb_capacity_mode)
  - The given use case clearly states that when the traffic spikes occur they happen very quickly, thereby implying an unpredictable traffic pattern, therefore the on-demand capacity mode is the correct option for the given use case.

**Wrong**
- Set up A[mazon DynamoDB global table](aws-ass-solution-architect.md#dynamodb_globaltable) in the provisioned capacity mode
  - Amazon DynamoDB global table cannot be used to handle an unpredictable load on a Amazon DynamoDB table.
- Set up Amazon DynamoDB table in the provisioned capacity mode with auto-scaling enabled
- Set up Amazon DynamoDB table with a [global secondary index](aws-ass-solution-architect.md#dynamodb_global_secondary_index)
     - GSI cannot be used to handle an unpredictable load on a DynamoDB table.

## 25
- An e-commerce company wants to migrate its on-premises application to AWS. 
- The application consists of application servers and a Microsoft SQL Server database. 
- The solution should result in the maximum possible availability for the database layer while minimizing operational and management overhead.

As a solutions architect, which of the following would you recommend to meet the given requirements?

**Solution**
- Migrate the data to Amazon RDS for SQL Server database in a Multi-AZ deployment
  - [RDS_Multi_AZ](aws-ass-solution-architect.md#rds_multi_az)
  - This option provides the maximum possible availability for the database layer while minimizing operational and management overhead.

**Wrong**
- Migrate the data to Amazon RDS for SQL Server database in a cross-region read-replica configuration
  - Amazon RDS Read Replicas enable you to create one or more read-only copies of your database instance within the same AWS Region or in a different AWS Region. Read replicas are used to enhance the read scalability of a database. You cannot use read replicas to improve the availability of a database. Therefore this option is incorrect.
- Migrate the data to Amazon RDS for SQL Server database in a cross-region Multi-AZ deployment
  - Amazon RDS Multi-AZ deployments provide enhanced availability for database instances within a single AWS Region
- Migrate the data to Amazon EC2 instance hosted SQL Server database. Deploy the Amazon EC2 instances in a Multi-AZ configuration


## 26
- A company wants to grant access to an Amazon S3 bucket to users in its own AWS account as well as to users in another AWS account. 
- Which of the following options can be used to meet this requirement?

**Solution**
- Use a bucket policy to grant permission to users in its account as well as to users in another account
  - [S3_Bucket_Policy](aws-ass-solution-architect.md#s3_bucket_policy)
  - [IAM_Policy_type](aws-ass-solution-architect.md#iam_policy_types)
**Wrong**
- Use either a bucket policy or a user policy to grant permission to users in its account as well as to users in another account
  - If an AWS account that owns a bucket wants to grant permission to users in its own AWS account, it can use either a bucket policy or a user policy. The user policies are for managing permissions for users in their own AWS account and NOT for users in other AWS accounts. Therefore both these options are incorrect.
- Use permissions boundary to grant permission to users in its account as well as to users in another account
- Use a user policy to grant permission to users in its account as well as to users in another account
  - If an AWS account that owns a bucket wants to grant permission to users in its own AWS account, it can use either a bucket policy or a user policy. The user policies are for managing permissions for users in their own AWS account and NOT for users in other AWS accounts. Therefore both these options are incorrect.


## 27
- A company uses Application Load Balancers in multiple AWS Regions. 
- The Application Load Balancers receive inconsistent traffic that varies throughout the year.
- The engineering team at the company needs to allow the IP addresses of the Application Load Balancers in the on-premises firewall to enable connectivity.

Which of the following represents the MOST scalable solution with minimal configuration changes?

**Solution**
- Set up AWS Global Accelerator. Register the Application Load Balancers in different Regions to the AWS Global Accelerator. Configure the on-premises firewall's rule to allow static IP addresses associated with the AWS Global Accelerator
  - [AWS Global Accelerator](aws-ass-solution-architect.md#aws_global_accelerator)
  - It provides static IP addresses that provide a fixed entry point to your applications and eliminate the complexity of managing specific IP addresses for different AWS Regions and Availability Zones.
  - Associate the static IP addresses provided by AWS Global Accelerator to regional AWS resources or endpoints, such as Network Load Balancers, Application Load Balancers, Amazon EC2 Instances, and Elastic IP addresses. The IP addresses are anycast from AWS edge locations so they provide onboarding to the AWS global network close to your users.

**Wrong**
- Set up a Network Load Balancer in one Region. Register the private IP addresses of the Application Load Balancers in different Regions with the Network Load Balancer. Configure the on-premises firewall's rule to allow the Elastic IP address attached to the Network Load Balancer
  - Using a single Network Load Balancer is not possible across AWS regions since an Network Load Balancer is Region bound. Multiple Network Load Balancers have to be registered for the on-premises firewall.
- Migrate all Application Load Balancers in different Regions to the [Network Load Balancers](aws-ass-solution-architect.md#NLB). Configure the on-premises firewall's rule to allow the Elastic IP addresses of all the Network Load Balancers
  - Although you could potentially migrate the Application Load Balancers to Network Load Balancers, this option requires changes to the on-premises firewall's configuration rules, hence this is not the right fit for the given use-case. It is more optimal to manage the two static IPs provided by the AWS Global Accelerator for configuring the firewall.
- Develop an AWS Lambda script to get the IP addresses of the Application Load Balancers in different Regions. Configure the on-premises firewall's rule to allow the IP addresses of the Application Load Balancers
  -  This option requires on-going changes to the on-premises firewall's configuration rules because the IP addresses of the Application Load Balancers would keep changing. Hence this is not the right fit for the given use-case. It is more optimal to configure the firewall with a one-time change for the two static IPs provided by the AWS Global Accelerator.
## 28
A company wants to adopt a hybrid cloud infrastructure where it uses some AWS services such as Amazon S3 alongside its on-premises data center. 
The company wants a dedicated private connection between the on-premise data center and AWS. 
In case of failures though, the company needs to guarantee uptime and is willing to use the public internet for an encrypted connection.

What do you recommend? (Select two)

**Solution**

- Use [AWS Direct Connect connection](aws-ass-solution-architect.md#aws_direct_connect) as a primary connection
  - AWS Direct Connect does not involve the Internet; instead, it uses dedicated, private network connections between your intranet and Amazon VPC.
  - AWS Direct Connect as a primary connection guarantees great performance and security (as the connection is private)
- Use [AWS Site-to-Site VPN](aws-ass-solution-architect.md#aws_site_to_site_vpn) as a backup connection
  - As we don't mind going over the public internet (which is reliable, but less secure as connections are going over the public route), we should use a Site to Site VPN which offers an encrypted connection to handle failover scenarios.

**Wrong**

- Use AWS Site-to-Site VPN as a primary connection
- Use [Egress Only Internet Gateway](aws-ass-solution-architect.md#vpc_egress_only_internet_gateway) as a backup connection
  - Egress-Only Internet Gateway cannot be used to connect on-premises data centers to AWS Cloud.
- Use AWS Direct Connect connection as a backup connection

## 29

A Pharmaceuticals company is looking for a simple solution to connect its VPCs and on-premises networks through a central hub.
As a Solutions Architect, which of the following would you suggest as the solution that requires the LEAST operational overhead?

**Solution**
- Use AWS Transit Gateway to connect the Amazon VPCs to the on-premises networks
  - [](aws-ass-solution-architect.md#aws_transit_gateway)
**Wronf**
- Use Transit VPC Solution to connect the Amazon VPCs to the on-premises networks
  - [Transit VPC Solution](aws-ass-solution-architect.md#transit_vpc)
  - Transit VPC is not the right solution for this use-case as Transit Gateway provides several advantages over Transit VPC:
    - 1. Transit Gateway abstracts away the complexity of maintaining VPN connections with hundreds of VPCs.
    - 2. Transit Gateway removes the need to manage and scale Amazon EC2 based software appliances. AWS is responsible for managing all resources needed to route traffic. 
    - 3. Transit Gateway removes the need to manage high availability by providing a highly available and redundant Multi-AZ infrastructure. 
    - 4. Transit Gateway improves bandwidth for inter-VPC communication to burst speeds of 50 Gbps per Availability Zone (AZ). 
    - 5. Transit Gateway streamlines user costs to a simple per hour per/GB transferred model.
    - 6. Transit Gateway decreases latency by removing Amazon EC2 proxies and the need for VPN encapsulation.
- [Fully meshed VPC peering](aws-ass-solution-architect.md#fully_meshed_vpc_peering) can be used to connect the Amazon VPCs to the on-premises networks
- Partially meshed VPC peering can be used to connect the Amazon VPCs to the on-premises networks

## 30
- A company's business logic is built on several microservices that are running in the on-premises data center. 
- They currently communicate using a message broker that supports the MQTT protocol. 
- The company is looking at migrating these applications and the message broker to AWS Cloud without changing the application logic.

Which technology allows you to get a managed message broker that supports the MQTT protocol?

**Solution**
- [Amazon MQ](aws-ass-solution-architect.md#aws_mq)

**Wrong**
- Amazon Simple Queue Service (Amazon SQS)
- Amazon Simple Notification Service (Amazon SNS)
- Amazon Kinesis Data Streams

## 31
- A systems administrator is creating IAM policies and attaching them to IAM identities. 
- After creating the necessary identity-based policies, the administrator is now creating resource-based policies.

Which is the only resource-based policy that the IAM service supports?

**Solution**

- Trust policy
  - [iam_trust_policy](aws-ass-solution-architect.md#iam_trust_policy)
**Wrong**

- Permissions boundary
  - [iam_permissions_boundaries](aws-ass-solution-architect.md#iam_permissions_boundaries)
- Access control list (ACL)
- AWS Organizations Service Control Policies (SCP)

## Question 32
- For security purposes, a development team has decided to deploy the Amazon EC2 instances in a private subnet. 
- The team plans to use VPC endpoints so that the instances can access some AWS services securely. 
- The members of the team would like to know about the two AWS services that support Gateway Endpoints.

As a solutions architect, which of the following services would you suggest for this requirement? (Select two)

**Solution**

- Amazon DynamoDB
- Amazon S3
  - [Gateway Endpoint](aws-ass-solution-architect.md#vpc_gateway_endpoint)


**Wrong**
- Amazon Simple Queue Service (Amazon SQS)
- Amazon Simple Notification Service (Amazon SNS)
- Amazon Kinesis

## Question 33

Question 33
- As a Solutions Architect, you are tasked to design a distributed application that will run on various Amazon EC2 instances. 
- This application needs to have the highest performance local disk to cache data.
- Also, data is copied through an Amazon EC2 to EC2 replication mechanism. 
- It is acceptable if the instance loses its data when stopped or terminated.

Which storage solution do you recommend?

**Solution**
- [Instance Store](aws-ass-solution-architect.md#EC2_Intance_store)

**Wrong**
- Amazon Simple Storage Service (Amazon S3)
- Amazon Elastic File System (Amazon EFS)
- Amazon Elastic Block Store (EBS)


## Question 34
- A healthcare company is evaluating storage options on Amazon S3 to meet regulatory guidelines. 
- The data should be stored in such a way on Amazon S3 that it cannot be deleted until the regulatory time period has expired.
As a solutions architect, which of the following would you recommend for the given requirement?


**Solution**
- Use Amazon S3 Object Lock
**Wrong**
- Activate AWS Multi-Factor Authentication (AWS MFA) delete on the Amazon S3 bucket
- Use Amazon S3 Glacier Vault Lock
  - A vault is a container for storing archives on Glacier. When you create a vault, you specify a vault name and the AWS Region in which you want to create the vault. Since Vault Lock is only for Glacier and not for Amazon S3, so it cannot be used for the given use-case.
- Use Amazon S3 cross-region replication (S3 CRR)
  - Only the root account can enable MFA delete. MFA delete cannot be used for the given use case because it just represents an additional security layer and can be disabled by anyone having access to the root account credentials.

## Question 35
- An Elastic Load Balancer has marked all the Amazon EC2 instances in the target group as unhealthy.
- Surprisingly, when a developer enters the IP address of the Amazon EC2 instances in the web browser, he can access the website.

What could be the reason the instances are being marked as unhealthy? (Select two)

**Solution**
- The route for the health check is misconfigured
- The security group of the Amazon EC2 instance does not allow for traffic from the security group of the Application Load Balancer
  - [ALB_Security_Group_Vs_Health_Check](aws-ass-solution-architect.md#alb_security_group_vs_health_check)

**Wrong**
- The Amazon Elastic Block Store (Amazon EBS) volumes have been improperly mounted
  - You can access the website using the IP address which means there is no issue with the Amazon EBS volumes. So this option is not correct.
- Your web-app has a runtime that is not supported by the Application Load Balancer
  - There is no connection between a web app runtime and the application load balancer.
- You need to attach elastic IP address (EIP) to the Amazon EC2 instances
  - This option is a distractor as Elastic IPs do not need to be assigned to Amazon EC2 instances while using an Application Load Balancer.

## Question 36
- You are working for a software as a service (SaaS) company as a solutions architect and help design solutions for the company's customers.
- One of the customers is a bank and has a requirement to *whitelist a public IP* when the bank is accessing external services across the internet.

Which architectural choice do you recommend to maintain high availability, support scaling-up to 10 instances and comply with the bank's requirements?

**Solution**
- Use a [Network Load Balancer](aws-ass-solution-architect.md#nlb) with an Auto Scaling Group
  - Classic Load Balancers and Application Load Balancers use the private IP addresses associated with their Elastic network interfaces as the source IP address for requests forwarded to your web servers.

  - These IP addresses can be used for various purposes, such as allowing the load balancer traffic on the web servers and for request processing. It's a best practice to use security group referencing on the web servers for whitelisting load balancer traffic from Classic Load Balancers or Application Load Balancers.

  - However, because Network Load Balancers don't support security groups, based on the target group configurations, the IP addresses of the clients or the private IP addresses associated with the Network Load Balancers must be allowed on the web server's security group.

**Wrong**

- Use an Application Load Balancer with an Auto Scaling Group
  - Application and Classic Load Balancers expose a fixed DNS (=URL) rather than the IP address. So these are incorrect options for the given use-case.
- Use an Auto Scaling Group with Dynamic Elastic IPs attachment
  - ASG does not have a dynamic Elastic IPs attachment feature.
- Use a Classic Load Balancer with an Auto Scaling Group
  - Classic Load Balancer provides basic load balancing across multiple Amazon EC2 instances and operates at both the request level and connection level. Classic Load Balancer is intended for applications that were built within the Amazon EC2-Classic network.

## 37 
The engineering team at a leading e-commerce company is anticipating a surge in the traffic because of a flash sale planned for the weekend. 
- You have estimated the web traffic to be 10x. 
- The content of your website is highly *dynamic* and changes very often.

As a Solutions Architect, which of the following options would you recommend to make sure your infrastructure scales for that day?

**Solution**

Use an [Auto Scaling Group](../markdown-documents/work/AWS/aws.md#asg)

**Wrong**
- Use an Amazon CloudFront distribution in front of your website
  - dymamic above
- Use an [Amazon Route 53](aws-ass-solution-architect.md#route_53) Multi Value record
  - Use Multi Value answer routing policy when you want Route 53 to respond to DNS queries with up to eight healthy records selected at random. Amazon Route 53 does not help in scaling your application. This option has been added as a distractor.
- Deploy the website on Amazon S3

## 38
The engineering team at an e-commerce company has been tasked with migrating to a *serverless architecture*. The team wants to focus on the key points of consideration when using AWS Lambda as a backbone for this architecture.

As a Solutions Architect, which of the following options would you identify as correct for the given requirement? (Select three)

**Solution**

- By default, AWS Lambda functions always operate from an AWS-owned VPC and hence have access to any public internet address or public AWS APIs. Once an AWS Lambda function is VPC-enabled, it will need a route through a Network Address Translation gateway (NAT gateway) in a public subnet to access public resources
  - [Lambda_VPC_Enable](aws-ass-solution-architect.md#lambda_vpc_enable)
- Since AWS Lambda functions can scale extremely quickly, it's a good idea to deploy a Amazon CloudWatch Alarm that notifies your team when function metrics such as ConcurrentExecutions or Invocations exceeds the expected threshold
- If you intend to reuse code in more than one AWS Lambda function, you should consider creating an AWS Lambda Layer for the reusable code
  - [Lambda_Layer](aws-ass-solution-architect.md#lambda_layer)

**Wrong**

- AWS Lambda allocates compute power in proportion to the memory you allocate to your function. AWS, thus recommends to over provision your function time out settings for the proper performance of AWS Lambda functions
- Serverless architecture and containers complement each other but you cannot package and deploy AWS Lambda functions as container images
- If you intend to reuse code in more than one AWS Lambda function, you should consider creating an AWS Lambda Layer for the reusable code
- The bigger your deployment package, the slower your AWS Lambda function will cold-start. Hence, AWS suggests packaging dependencies as a separate package from the actual AWS Lambda package


## 39
A Big Data analytics company writes data and log files in *Amazon S3 buckets*. 
- The company now wants to stream the existing data files as well as any ongoing file updates from Amazon S3 to Amazon Kinesis Data Streams.

As a Solutions Architect, which of the following would you suggest as the fastest possible way of building a solution for this requirement?

**Solution**
- Leverage AWS Database Migration Service (AWS DMS) as a bridge between Amazon S3 and Amazon Kinesis Data Streams
  - [DMS](aws-ass-solution-architect.md#dms)
  - [DMS_S3](aws-ass-solution-architect.md#dms_s3)

**Wrong**
- Configure Amazon EventBridge events for the bucket actions on Amazon S3. An AWS Lambda function can then be triggered from the Amazon EventBridge event that will send the necessary data to Amazon Kinesis Data Streams
  - Enable AWS Cloudtrail trail to use object-level actions as a trigger for Amazon EventBridge events 
  - Also, using AWS Lambda functions would require significant custom development to write the data into Amazon Kinesis Data Streams, so this option is not the right fit.
- Leverage Amazon S3 event notification to trigger an AWS Lambda function for the file create event. The AWS Lambda function will then send the necessary data to Amazon Kinesis Data Streams
  - Using AWS Lambda functions would require significant custom development to write the data into Amazon Kinesis Data Streams, so this option is not the right fit.
- Amazon S3 bucket actions can be directly configured to write data into Amazon Simple Notification Service (Amazon SNS). Amazon SNS can then be used to send the updates to Amazon Kinesis Data Streams
  - Amazon S3 cannot directly write data into *Amazon SNS*, although it can certainly use *Amazon S3 event notifications* to send an event to Amazon SNS.

## 40
- Your company is deploying a website running on *AWS Elastic Beanstalk*. 
- The website takes over 45 minutes for the installation and contains both static as well as dynamic files that must be generated during the installation process.

As a Solutions Architect, you would like to bring the time to create a new instance in your AWS Elastic Beanstalk deployment to be less than 2 minutes. Which of the following options should be combined to build a solution for this requirement? (Select two)

**Options**
- Use AWS Elastic Beanstalk deployment caching feature
- Use Amazon EC2 user data to install the application at boot time
- Store the installation files in Amazon S3 so they can be quickly retrieved
- Create a Golden Amazon Machine Image (AMI) with the static installation components already setup
- Use Amazon EC2 user data to customize the dynamic installation parts at boot time
**Solution**
- Create a Golden Amazon Machine Image (AMI) with the static installation components already setup
  - [](aws-ass-solution-architect.md#aws_beanstalk)
  - A custom AMI can improve provisioning times when instances are launched in your environment if you need to install a lot of software that isn't included in the standard AMIs.
  - A Golden AMI is an AMI that you standardize through configuration, consistent security patching, and hardening. It also contains agents you approve for logging, security, performance monitoring, etc. For the given use-case, you can have the static installation components already setup via the golden AMI.
- Use Amazon EC2 user data to customize the dynamic installation parts at boot time
  - Amazon EC2 instance user data is the data that you specified in the form of a configuration script while launching your instance. You can use Amazon EC2 user data to customize the dynamic installation parts at boot time, rather than installing the application itself at boot time.
**Wrong**
- Use AWS Elastic Beanstalk deployment caching feature
- Use Amazon EC2 user data to install the application at boot time
- Create a Golden Amazon Machine Image (AMI) with the static installation components already setup
- Store the installation files in Amazon S3 so they can be quickly retrieved
  - It cannot be used to run or generate dynamic files since Amazon S3 is not an environment but a storage service.
- Use Amazon EC2 user data to customize the dynamic installation parts at boot time
  - User data of an instance can be used to perform common automated configuration tasks or run scripts after the instance starts. User data, cannot, however, be used to install the application since it takes over 45 minutes for the installation which contains static as well as dynamic files that must be generated during the installation process.

## 41
- A mobile gaming company is experiencing heavy read traffic to its Amazon Relational Database Service (Amazon RDS) database that retrieves player’s scores and stats. 
- The company is using an Amazon RDS database instance type that is not cost-effective for their budget. 
- The company would like to implement a strategy to deal with the high volume of read traffic, reduce latency, and also downsize the *instance size to cut costs*.

Which of the following solutions do you recommend?

**Option**
- Amazon RDS Read Replicas
- Move to Amazon Redshift
- Switch application code to AWS Lambda for better performance
- Setup Amazon ElastiCache in front of Amazon RDS

**Solution**
- Setup [Amazon ElastiCache](aws-ass-solution-architect.md#elasticache) in front of Amazon RDS

**Wrong**
- Setup [Amazon RDS Read Replicas](aws-ass-solution-architect.md#rds_read_replicas)
  - Adding read replicas would further add to the database costs and will not help in reducing latency when compared to a caching solution. So this option is ruled out.
- Move to Amazon Redshift
  - Amazon Redshift is optimized for datasets ranging from a few hundred gigabytes to a petabyte or more. If the company is looking at cost-cutting, moving to Amazon Redshift from Amazon RDS is not an option.
- Switch application code to AWS Lambda for better performance

## 42
A company runs a popular dating website on the AWS Cloud. 
- As a Solutions Architect, you've designed the architecture of the website to follow a serverless pattern on the AWS Cloud using Amazon API Gateway and AWS Lambda. 
- The backend uses an Amazon RDS PostgreSQL database. 
- Currently, the application uses a username and password combination to connect the AWS Lambda function to the Amazon RDS database.

You would like to improve the security at the authentication level by leveraging short-lived credentials. What will you choose? (Select two)

**Options**
- Embed a credential rotation logic in the AWS Lambda, retrieving them from SSM
- Restrict the Amazon RDS database security group to the AWS Lambda's security group
- Attach an AWS Identity and Access Management (IAM) role to AWS Lambda
- Deploy AWS Lambda in a VPC
- Use *IAM authentication* from AWS Lambda to Amazon RDS PostgreSQL
**Solution**
- Use *IAM authentication* from AWS Lambda to Amazon RDS PostgreSQL
  - [AWS_IAM_Authorization](aws-ass-solution-architect.md#AWS_IAM_Authorization)
- Attach an *AWS Identity and Access Management (IAM)* role to AWS Lambda
- You can authenticate to your database instance using AWS Identity and Access Management (IAM) database authentication. IAM database authentication works with MySQL and PostgreSQL. With this authentication method, you don't need to use a password when you connect to a database instance. Instead, you use an authentication token.

- An authentication token is a unique string of characters that Amazon RDS generates on request. Authentication tokens are generated using AWS Signature Version 4. Each token has a lifetime of 15 minutes. You don't need to store user credentials in the database, because authentication is managed externally using IAM. You can also still use standard database authentication.

- IAM database authentication provides the following benefits: 1. Network traffic to and from the database is encrypted using Secure Sockets Layer (SSL). 2. You can use IAM to centrally manage access to your database resources, instead of managing access individually on each DB instance. 3. For applications running on Amazon EC2, you can use profile credentials specific to your Amazon EC2 instance to access your database instead of a password, for greater security.
**Wrong**
- Embed a credential rotation logic in the AWS Lambda, retrieving them from SSM 
  - AWS Systems Manager Parameter Store (aka SSM Parameter Store) provides secure, hierarchical storage for configuration data management and secrets management. You can store data such as passwords, database strings, Amazon EC2 instance IDs, Amazon Machine Image (AMI) IDs, and license codes as parameter values. You can store values as plain text or encrypted data.
  - Retrieving credentials from SSM is overkill for the expected solution and hence this is not a correct option.
- Deploy AWS Lambda in a VPC
- Restrict the Amazon RDS database security group to the AWS Lambda's security group
  - This question is very tricky because all answers do indeed increase security. But the question is related to authentication mechanisms, and as such, deploying an AWS Lambda in a VPC or tightening security groups does not change the authentication layer. IAM authentication to Amazon RDS is supported, which must be achieved by attaching an IAM role the AWS Lambda function

## 43
- You started a new job as a solutions architect at a company that has both AWS experts and people learning AWS.
- Recently, a developer misconfigured a newly created Amazon RDS database which resulted in a production outage.
How can you ensure that Amazon RDS specific best practices are incorporated into a reusable infrastructure template to be used by all your AWS users?

**Options**
- Attach an IAM policy to interns preventing them from creating an Amazon RDS database
- Create an AWS Lambda function which sends emails when it finds misconfigured Amazon RDS databases
- Use AWS CloudFormation to manage Amazon RDS databases
- Store your recommendations in a custom AWS Trusted Advisor rule
**Solution**
- Use [AWS CloudFormation](aws-ass-solution-architect.md#cloudformation) to manage Amazon RDS databases

**Wrong**
- Attach an IAM policy to interns preventing them from creating an Amazon RDS database
  - Does not solve the problem of allowing any user to create resources by leveraging reusable infrastructure templates. So, this option is ruled out.
- Create an AWS Lambda function which sends emails when it finds misconfigured Amazon RDS databases
  - Using an AWS Lambda function to scan for a misconfigured Amazon RDS database is a reactive mechanism. It does not help in creating reusable infrastructure templates.

- Store your recommendations in a custom AWS Trusted Advisor rule
  - AWS Trusted Advisor just provides recommendations rather than creating reusable infrastructure templates.

## Question 44
- A niche social media application allows users to connect with sports athletes.
-  As a solutions architect, you've designed the architecture of the application to be fully serverless using Amazon API Gateway and AWS Lambda. T
-  he backend uses an Amazon DynamoDB table. Some of the star athletes using the application are highly popular, and therefore Amazon DynamoDB has increased the read capacity units (RCUs). 
-  Still, the application is experiencing a hot partition problem.

What can you do to improve the performance of Amazon DynamoDB and eliminate the hot partition problem without a lot of application refactoring?

**Correct answer**
- Use Amazon DynamoDB DAX
  - [DynamoDB Accelerator(DAX)](aws-ass-solution-architect.md#dynamodb-acceleratordax)

**Wrong**
- Use Amazon ElastiCache
  - ElastiCache could also be a solution, but it will require a lot of refactoring work on the AWS Lambda side.
- Use Amazon DynamoDB Streams
- Use Amazon DynamoDB Global Tables

## Question 45
Skipped
A company has migrated its application from a monolith architecture to a microservices based architecture. The development team has updated the Amazon Route 53 simple record to point "myapp.mydomain.com" from the old Load Balancer to the new one.

The users are still not redirected to the new Load Balancer. What has gone wrong in the configuration?

**Options**
- The Alias Record is misconfigured
  - [](aws-ass-solution-architect.md#route_53)
- The CNAME Record is misconfigured
- The Time To Live (TTL) is still in effect
- The health checks are failing
  - Simple Records do not have health checks, so this option is incorrect.

**Solution**
- The Time To Live (TTL) is still in effect

## Question 46
- An IT company runs a high-performance computing (HPC) workload on AWS. 
The workload requires high network throughput and low-latency network performance along with tightly coupled node-to-node communications. 
- The Amazon EC2 instances are properly sized for compute and storage capacity and are launched using default options.

Which of the following solutions can be used to improve the performance of the workload?

**Option**
- Select dedicated instance tenancy while launching Amazon EC2 instances
- Select a cluster placement group while launching Amazon EC2 instances
- Select the appropriate capacity reservation while launching Amazon EC2 instances
- Select an Elastic Inference accelerator while launching Amazon EC2 instances

**Solution**
- Select the appropriate capacity reservation while launching Amazon EC2 instances
  - [ec2_placement_group](aws-ass-solution-architect.md#ec2_placement_group)

**Wrong**
- Select dedicated instance tenancy while launching Amazon EC2 instances
- Select the appropriate capacity reservation while launching Amazon EC2 instances
- Select an Elastic Inference accelerator while launching Amazon EC2 instances
  - [Elastic Inference accelerator](aws-ass-solution-architect.md#elastic-inference-accelerator) 



## 47
A social media company wants the capability to dynamically alter the size of a geographic area from which traffic is routed to a specific server resource.

Which feature of Amazon Route 53 can help achieve this functionality?

**Options**
Weighted routing
Geolocation routing
Geoproximity routing
Latency-based routing

**Solution**
- []

**Wrong**

## 48

- You have an Amazon S3 bucket that contains files in two different folders - s3://my-bucket/images and s3://my-bucket/thumbnails. 
- When an image is first uploaded and new, it is viewed several times. 
- But after 45 days, analytics prove that image files are on average rarely requested, but the thumbnails still are. 
- After 180 days, you would like to archive the image files and the thumbnails.
- Overall you would like the solution to remain highly available to prevent disasters happening against a whole Availability Zone (AZ).

How can you implement an efficient cost strategy for your Amazon S3 bucket? (Select two)

**Option**
Create a Lifecycle Policy to transition objects to Amazon S3 Standard IA using a prefix after 45 days
Create a Lifecycle Policy to transition objects to [Amazon S3 One Zone IA](aws-ass-solution-architect.md#s3_ia_onezone) using a prefix after 45 days
Create a Lifecycle Policy to transition all objects to Amazon S3 Glacier after 180 days
Create a Lifecycle Policy to transition all objects to Amazon S3 Standard IA after 45 days
Create a Lifecycle Policy to transition objects to Amazon S3 Glacier using a prefix after 180 days
**Solution**
Create a Lifecycle Policy to transition objects to Amazon S3 One Zone IA using a prefix after 45 days
  - As discussed above, you need to use a prefix while configuring the Lifecycle Policy so that only objects in the *s3://my-bucket/images* are transitioned to Amazon S3 Standard IA and not all the objects in the bucket

**Wrong**
Create a Lifecycle Policy to transition objects to Amazon S3 Glacier using a prefix after 180 days
  - Glacier doesn't need prefixes for the given use-case.
Create a Lifecycle Policy to transition objects to Amazon S3 One Zone IA using a prefix after 45 days
  - Amazon S3 One Zone IA will not achieve the necessary availability in case an Availability Zone (AZ) goes down.

## 49
- A retail company is using [AWS Site-to-Site VPN](aws-ass-solution-architect.md#aws_site_to_site_vpn) connections for secure connectivity to its AWS cloud resources from its on-premises data center.
- Due to a surge in traffic across the VPN connections to the AWS cloud, users are experiencing slower VPN connectivity.

Which of the following options will maximize the VPN throughput? 

**Options**
Create a virtual private gateway with equal cost multipath routing and multiple channels
Use AWS Global Accelerator for the VPN connection to maximize the throughput
Create an AWS Transit Gateway with equal cost multipath routing and add additional VPN tunnels
Use Transfer Acceleration for the VPN connection to maximize the throughput

**Correct**
- Create an AWS Transit Gateway with equal cost multipath routing and add additional VPN tunnels
  - [VPN](aws-ass-solution-architect.md#aws_site_to_site_vpn)
  - With AWS Transit Gateway, you can simplify the connectivity between multiple VPCs and also connect to any VPC attached to AWS Transit Gateway with a single VPN connection. AWS Transit Gateway also enables you to scale the IPsec VPN throughput with equal cost multi-path (ECMP) routing support over multiple VPN tunnels. A single VPN tunnel still has a maximum throughput of 1.25 Gbps. If you establish multiple VPN tunnels to an ECMP-enabled transit gateway, it can scale beyond the default maximum limit of 1.25 Gbps. You also must enable the dynamic routing option on your transit gateway to be able to take advantage of ECMP for scalability.
  - ![](https://assets-pt.media.datacumulus.com/aws-saa-pt/assets/pt3-q18-i1.jpg)
**Wrong**

## 50
- A company has built a serverless application using *Amazon API Gateway* and *AWS Lambda*. 
- The backend is leveraging an *Amazon Aurora MySQL* database. 
- The web application was initially launched in the Americas and the company would now like to expand it to Europe, where a read-only version will be available to improve latency. 
- You plan on deploying the Amazon API Gateway and AWS Lambda using AWS CloudFormation, but would like to have a read-only copy of your data in Europe as well.

As a Solutions Architect, what do you recommend?
**Options**
- Use Amazon DynamoDB Streams
- Use Amazon Aurora Read Replicas
- Create an AWS Lambda function to periodically back up and restore the Amazon Aurora database in another region
- Use Amazon Aurora Multi-AZ
**Solution**
- Use Amazon Aurora Read Replicas
  - [](../markdown-documents/work/AWS/aws-ass-solution-architect.md#aurora-replica)
**Wrong**


## 51

- A development team has configured Elastic Load Balancing for host-based routing. 
- The idea is to support multiple subdomains and different top-level domains.

The rule *.example.com matches which of the following?

**Options**
- test.example.com
- example.test.com
- example.com
- EXAMPLE.COM

**Solution**
example.test.com

**Wrong**

## 52 
- As an e-sport tournament hosting company, you have servers that need to scale and be highly available. 
- Therefore you have deployed an Elastic Load Balancing (ELB) with an Auto Scaling group (ASG) across 3 Availability Zones (AZs). 
- When e-sport tournaments are running, the servers need to scale quickly. 
- And when tournaments are done, the servers can be idle. As a general rule, you would like to be highly available, have the capacity to scale and optimize your costs.

What do you recommend? (Select two)

**Options(2)**
- Use Dedicated hosts for the minimum capacity
- Set the minimum capacity to 1
- Set the minimum capacity to 3
- Use Reserved Instances (RIs) for the minimum capacity
- Set the minimum capacity to 2

**Solution**
- Use Reserved Instances (RIs) for the minimum capacity
- Set the minimum capacity to 2
**Wrong**

## 53
- The engineering team at a social media company has recently migrated to AWS Cloud from its on-premises data center.
- The team is evaluating *Amazon CloudFront* to be used as a CDN for its flagship application. 
- The team has hired you as an AWS Certified Solutions Architect – Associate to advise on Amazon CloudFront capabilities on routing, security, and high availability.

Which of the following would you identify as correct regarding Amazon CloudFront? (Select three)

- Use geo restriction to configure Amazon CloudFront for high-availability and failover
- Use field level encryption in Amazon CloudFront to protect sensitive data for specific content
- Amazon CloudFront can route to multiple origins based on the price class
- Use AWS Key Management Service (AWS KMS) encryption in Amazon CloudFront to protect sensitive data for specific content
- Amazon CloudFront can route to multiple origins based on the content type
- Use an origin group with primary and secondary origins to configure Amazon CloudFront for high-availability and failover

**Solution**
- Use field level encryption in Amazon CloudFront to protect sensitive data for specific content
  - [Cloudfront_field_level_encryption](aws-ass-solution-architect.md#cloudfront_field_level_encryption)

- Amazon CloudFront can route to multiple origins based on the content type
  - [Cloudfront_route_mulitple_origin](aws-ass-solution-architect.md#cloudfront_route_mulitple_origin)
- Use an origin group with primary and secondary origins to configure Amazon CloudFront for high-availability and failover
  - [Cloudfront_secondary_origin](aws-ass-solution-architect.md#cloudfront_route_mulitple_origin)
**Wrong**
- Use AWS Key Management Service (AWS KMS) encryption in Amazon CloudFront to protect sensitive data for specific content

## 54

- A leading e-commerce company runs its IT infrastructure on AWS Cloud. 
- The company has a batch job running at 7AM daily on an *Amazon RDS database*. 
- It processes shipping orders for the past day, and usually gets around 2000 records that need to be processed sequentially in a batch job via a **shell script**. The processing of each record takes about 3 seconds.

What platform do you recommend to run this batch job?

**Options**
- AWS Glue
- AWS Lambda
- Amazon Kinesis Data Streams
- Amazon Elastic Compute Cloud (Amazon EC2)

**Solutions**
- EC2
  - AWS Batch can be used to plan, schedule, and execute your batch computing workloads on Amazon EC2 Instances. Amazon EC2 is the right choice as it can accommodate batch processing and run customized scripts, as is the needed requirement.
- Glue
  -  but cannot run custom shell scripts and hence not the right choice here.
-  KDS
   - However, Kinesis works great with real-time data, we are looking at batch processing, so Kinesis is not an option.
- **AWS Lambda** - AWS Lambda lets you run code without provisioning or managing servers. AWS Lambda functions can be configured to run up to 15 minutes per execution. You can set the timeout to any value between 1 second and 15 minutes. The total runtime for the given use-case is 100 minutes (2000*3=6000 seconds = 100 minutes) but the Lambda would time out after 15 minutes, so this option is incorrect.

## 55
Question 55
- An IT company has a large number of clients opting to build their application programming interface (API) using Docker containers.
- To facilitate the hosting of these containers, the company is looking at various orchestration services available with AWS.

As a Solutions Architect, which of the following solutions will you suggest? (Select two)

**Options**
- Use Amazon EMR for serverless orchestration of the containerized services
- Use Amazon Elastic Container Service (Amazon ECS) with AWS Fargate for serverless orchestration of the containerized services
- Use Amazon Elastic Container Service (Amazon ECS) with Amazon EC2 for serverless orchestration of the containerized services
- Use Amazon Elastic Kubernetes Service (Amazon EKS) with AWS Fargate for serverless orchestration of the containerized services
- Use Amazon SageMaker for serverless orchestration of the containerized services

**Solution**
- Use Amazon Elastic Container Service (Amazon ECS) with AWS Fargate for serverless orchestration of the containerized services
- Use Amazon Elastic Kubernetes Service (Amazon EKS) with AWS Fargate for serverless orchestration of the containerized services
**Wrong**
- [EMR](aws-ass-solution-architect.md#emr)
- [SageMarket](#)

## 56
- A CRM web application was written as a monolith in PHP and is facing scaling issues because of performance bottlenecks. 
- The CTO wants to re-engineer towards microservices architecture and expose their application from the same load balancer, linked to different target groups with different URLs: checkout.mycorp.com, www.mycorp.com, yourcorp.com/profile and yourcorp.com/search. The CTO would like to expose all these URLs as HTTPS endpoints for security purposes.

As a solutions architect, which of the following would you recommend as a solution that requires MINIMAL configuration effort?

**Options**

**Option**
- Change the Elastic Load Balancing (ELB) SSL Security Policy
- Use an HTTP to HTTPS redirect
- Use Secure Sockets Layer certificate (SSL certificate) with SNI
- Use a wildcard Secure Sockets Layer certificate (SSL certificate)

**Solution**
- Use Secure Sockets Layer certificate (SSL certificate) with SNI
  - You can host multiple TLS secured applications, each with its own TLS certificate, behind a single load balancer. To use SNI, all you need to do is bind multiple certificates to the same secure listener on your load balancer. ALB will automatically choose the optimal TLS certificate for each client.

  - ALB’s smart certificate selection goes beyond SNI. In addition to containing a list of valid domain names, certificates also describe the type of key exchange and cryptography that the server supports, as well as the signature algorithm (SHA2, SHA1, MD5) used to sign the certificate.

With SNI support AWS makes it easy to use more than one certificate with the same ALB. The most common reason you might want to use multiple certificates is to handle different domains with the same load balancer. It’s always been possible to use wildcard and subject-alternate-name (SAN) certificates with ALB, but these come with limitations. Wildcard certificates only work for related subdomains that match a simple pattern and while SAN certificates can support many different domains, the same certificate authority has to authenticate each one. That means you have to reauthenticate and reprovision your certificate every time you add a new domain.

**Wrong**
- **Use a wildcard Secure Sockets Layer certificate** (SSL certificate)
  - As the use case requires different domain names, so you cannot use a wildcard SSL certificate.
- **Use an HTTP to HTTPS redirect** - This will not provide multiple secure endpoints for different URLs such as checkout.mycorp.com or www.mycorp.com, therefore it is incorrect for the given use-case.
- **Change the Elastic Load Balancing (ELB) SSL Security Policy** - Elastic Load Balancing (ELB) SSL Security Policy will not provide multiple secure endpoints for different URLs such as checkout.mycorp.com or www.mycorp.com, therefore it is incorrect for the given use-case.

## 57

- A photo hosting service publishes a collection of beautiful mountain images, every month, that aggregate over 50 gigabytes in size and downloaded all around the world. 
- The content is currently hosted on **Amazon EFS** and distributed by **Elastic Load Balancing (ELB)** and **Amazon EC2 instances**. 
- The website is experiencing high load each month and very high network costs.

As a Solutions Architect, what can you recommend that won't force an application refactor and reduce network costs and Amazon EC2 load drastically?

**Optional**
- Host the master pack onto Amazon S3 for faster access
- Upgrade the Amazon EC2 instances
- Enable Elastic Load Balancing (ELB) caching
-Create an Amazon CloudFront distribution
**Solution**
-Create an Amazon CloudFront distribution
**Wrong**
- Host the master pack onto Amazon S3 for faster access
- Upgrade the Amazon EC2 instances
- Enable Elastic Load Balancing (ELB) caching
  - ELB does not have any caching capability.

## 58
- You are working as an AWS architect for a weather tracking facility. 
- You are asked to set up a Disaster Recovery (DR) mechanism with minimum costs. 
- In case of failure, the facility can only bear data loss of approximately 15 minutes without jeopardizing the forecasting models.

As a Solutions Architect, which DR method will you suggest?

**Options**
- Multi-Site
- Backup and Restore
- Warm Standby
- Pilot Light

**Solution**
- [](aws-ass-solution-architect.md#disaster_recovery_strategy)

**Wrong**

 - **Pilot Light:** The term pilot light is often used to describe a DR scenario in which a minimal version of an environment is always running in the cloud. The idea of the pilot light is an analogy that comes from the gas heater. In a gas heater, a small flame that’s always on can quickly ignite the entire furnace to heat up a house. This scenario is similar to a backup-and-restore scenario. For example, with AWS you can maintain a pilot light by configuring and running the most critical core elements of your system in AWS. For the given use-case, a small part of the backup infrastructure is always running simultaneously syncing mutable data (such as databases or documents) so that there is no loss of critical data. When the time comes for recovery, you can rapidly provision a full-scale production environment around the critical core. For Pilot light, RPO/RTO is in 10s of minutes, so this is the correct solution.
 - *Backup and Restore* - In most traditional environments, data is backed up to tape and sent off-site regularly. If you use this method, it can take a long time to restore your system in the event of a disruption or disaster. Amazon S3 is an ideal destination for backup data that might be needed quickly to perform a restore. Transferring data to and from Amazon S3 is typically done through the network and is therefore accessible from any location. There are many commercial and open-source backup solutions that integrate with Amazon S3. You can use AWS Import/Export to transfer very large data sets by shipping storage devices directly to AWS. For longer-term data storage where retrieval times of several hours are adequate, there is Amazon Glacier, which has the same durability model as Amazon S3. Amazon Glacier is a low-cost alternative starting from $0.01/GB per month. Amazon Glacier and Amazon S3 can be used in conjunction to produce a tiered backup solution. Even though Backup and Restore method is cheaper, it has an RPO in hours, so this option is not the right fit.
 - Warm Standby - The term warm standby is used to describe a DR scenario in which a scaled-down version of a fully functional environment is always running in the cloud. A warm standby solution extends the pilot light elements and preparation. It further decreases the recovery time because some services are always running. By identifying your business-critical systems, you can fully duplicate these systems on AWS and have them always on. This option is costlier compared to Pilot Light.
 - Multi-Site - A multi-site solution runs on AWS as well as on your existing on-site infrastructure in an active-active configuration. The data replication method that you employ will be determined by the recovery point that you choose, either Recovery Time Objective (the maximum allowable downtime before degraded operations are restored) or Recovery Point Objective (the maximum allowable time window whereby you will accept the loss of transactions during the DR process). This option is more costly compared to Pilot Light.



## 59
A junior developer has downloaded a sample Amazon S3 bucket policy to make changes to it based on new company-wide access policies. He has requested your help in understanding this bucket policy.

As a Solutions Architect, which of the following would you identify as the correct description for the given policy?
```json
{
 "Version": "2012-10-17",
 "Id": "S3PolicyId1",
 "Statement": [
   {
     "Sid": "IPAllow",
     "Effect": "Allow",
     "Principal": "*",
     "Action": "s3:*",
     "Resource": "arn:aws:s3:::examplebucket/*",
     "Condition": {
        "IpAddress": {"aws:SourceIp": "54.240.143.0/24"},
        "NotIpAddress": {"aws:SourceIp": "54.240.143.188/32"}
     }
   }
 ]
}
```

**Option**
- It ensures the Amazon S3 bucket is exposing an external IP within the Classless Inter-Domain Routing (CIDR) range specified, except one IP
- It authorizes an IP address and a Classless Inter-Domain Routing (CIDR) to access the S3 bucket
- It authorizes an entire Classless Inter-Domain Routing (CIDR) except one IP address to access the Amazon S3 bucket
- It ensures Amazon EC2 instances that have inherited a security group can access the bucket

**Solution**
- It authorizes an entire Classless Inter-Domain Routing (CIDR) except one IP address to access the Amazon S3 bucket
  - 

## 60
An enterprise has decided to move its secondary workloads such as backups and archives to AWS cloud. The CTO wishes to move the data stored on physical tapes to Cloud, without changing their current tape backup workflows. The company holds petabytes of data on tapes and needs a cost-optimized solution to move this data to cloud.

What is an optimal solution that meets these requirements while keeping the costs to a minimum?

**Option**
- Use AWS Direct Connect, a cloud service solution that makes it easy to establish a dedicated network connection from on-premises to AWS to transfer data. Once this is done, Amazon S3 can be used to store data at lesser costs
- Use AWS DataSync, which makes it simple and fast to move large amounts of data online between on-premises storage and AWS Cloud. Data moved to Cloud can then be stored cost-effectively in Amazon S3 archiving storage classes
- Use AWS VPN connection between the on-premises datacenter and your Amazon VPC. Once this is established, you can use Amazon Elastic File System (Amazon EFS) to get a scalable, fully managed elastic NFS file system for use with AWS Cloud services and on-premises resources
- Use Tape Gateway, which can be used to move on-premises tape data onto AWS Cloud. Then, Amazon S3 archiving storage classes can be used to store data cost-effectively for years

**Solution**
- Use Tape Gateway, which can be used to move on-premises tape data onto AWS Cloud. Then, Amazon S3 archiving storage classes can be used to store data cost-effectively for years
  - [Tape Gateway](##tab-grade)
**Wrong**
- Use AWS DataSync, which makes it simple and fast to move large amounts of data online between on-premises storage and AWS Cloud. Data moved to Cloud can then be stored cost-effectively in Amazon S3 archiving storage classes
  - Only support NFS, SMB

- Use AWS VPN connection between the on-premises datacenter and your Amazon VPC. Once this is established, you can use Amazon Elastic File System (Amazon EFS) to get a scalable, fully managed elastic NFS file system for use with AWS Cloud services and on-premises resources  

- VPN: VPN connection is used when businesses have an on-going requirement for connectivity from the on-premises data center to AWS Cloud. Amazon EFS is a managed file system by AWS and cannot be used for archiving on-premises tape data onto AWS Cloud.
- Dirrect connect: irect Connect is used when customers need to retain on-premises structure because of compliance reasons and have moved the rest of the architecture to AWS Cloud. These businesses generally have an on-going requirement for low latency access to AWS Cloud and hence are willing to spend on installing the physical lines needed for this connection. The given use-case needs a cost-optimized solution and they do not have an ongoing requirement for high availability bandwidth.

## 61


You are working as a Solutions Architect for a photo processing company that has a proprietary algorithm to compress an image without any loss in quality. 
- Because of the efficiency of the algorithm, your clients are willing to wait for a response that carries their compressed images back. You also want to process these jobs asynchronously and scale quickly, to cater to the high demand. Additionally, you also want the job to be retried in case of failures.

Which combination of choices do you recommend to minimize cost and comply with the requirements? (Select two)

**Options**
- Amazon Simple Notification Service (Amazon SNS)
- Amazon Simple Queue Service (Amazon SQS)
- Amazon EC2 Reserved Instances (RIs)
- Amazon EC2 On-Demand Instances
- Amazon EC2 Spot Instances

**Solution**
- **Spot instance**
  - To process these jobs, due to the unpredictable nature of their volume, and the desire to save on costs, spot Instances are recommended as compared to on-demand instances. As spot instances are cheaper than reserved instances and do not require long term commitment, spot instances are a better fit for the given use-case
- SQS
  - Amazon SQS will allow you to buffer the image compression requests and process them asynchronously. It also has a direct built-in mechanism for retries and scales seamlessly.

Incorrect options:
- Amazon Simple Notification Service (Amazon SNS) - Amazon Simple Notification Service (Amazon SNS) is a highly available, durable, secure, fully managed pub/sub messaging service that enables you to decouple microservices, distributed systems, and serverless applications. Amazon SNS provides topics for high-throughput, push-based, many-to-many messaging. SNS is not the right fit for this use-case, since its not a queuing mechanism.


## 62
A digital media company needs to manage uploads of around *1 terabyte each* from an application being used by a partner company.

As a Solutions Architect, how will you handle the upload of these files to Amazon S3?

**Solution**
Use multi-part upload feature of Amazon S3
**Wrong**
Use AWS Direct Connect to provide extra bandwidth
Use AWS Snowball
Use Amazon S3 Versioning

## 63
As part of the on-premises data center migration to AWS Cloud, a company is looking at using multiple AWS Snow Family devices to move their on-premises data.

Which AWS Snow Family service offers the feature of storage clustering?

**Solution**
AWS Snowball Edge Compute Optimized
  [](aws-ass-solution-architect.md#aws-snow-family)
**Wrong**
AWS Snowmobile
AWS Snowmobile Storage Compute
AWS Snowcone

## 64

What does this AWS CloudFormation snippet do? (Select three)
```yaml
SecurityGroupIngress:
     - IpProtocol: tcp
       FromPort: 80
       ToPort: 80
       CidrIp: 0.0.0.0/0
     - IpProtocol: tcp
       FromPort: 22
       ToPort: 22
       CidrIp: 192.168.1.1/32
```
**Solution**
- It configures a security group's inbound rules
- It allows any IP to pass through on the HTTP port
- It configures a security group's inbound rules
  - [Security_Group](aws-ass-solution-architect.md#security_group)
**Wrong**
- It only allows the IP 0.0.0.0 to reach HTTP
- It prevents traffic from reaching on HTTP unless from the IP 192.168.1.1
- It configures the inbound rules of a network access control list (network ACL)
- It configures a security group's outbound rules




## 65
- A company has grown from a small startup to an enterprise employing over 1000 people. As the team size has grown, the company has recently observed some strange behavior, with Amazon S3 buckets settings being changed regularly.

How can you figure out what's happening without restricting the rights of the users?

- Use [Amazon S3 access logs](aws-ass-solution-architect.md#s3) to analyze user access using Athena 
- Implement a bucket policy requiring AWS Multi-Factor Authentication (AWS MFA) for all operations 
- Implement an [IAM policy](aws-ass-solution-architect.md#iam_policy_types) to forbid users to change Amazon S3 bucket settings
- Use AWS CloudTrail to analyze API calls

**Solution**
- Use [AWS CloudTrail](aws-ass-solution-architect.md#Cloudtrail) to analyze API calls(read)



