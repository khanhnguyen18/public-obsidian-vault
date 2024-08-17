# Practice Test 3

## 1 - HPC
A biotechnology company has multiple **High Performance Computing (HPC)** workflows that quickly and accurately process and analyze genomes for hereditary diseases.
The company is looking to *migrate* these workflows from their on-premises infrastructure to AWS Cloud.

As a solutions architect, which of the following networking components would you recommend on the Amazon EC2 instances running these HPC workflows?

**Solution**
4. Elastic Fabric Adapter (EFA)
- [EFA](aws-ass-solution-architect.md#elastic-fabric-adapter-efa)
  **Wrong**
1. Elastic Network Interface (ENI)
- [Elastic_Network_Interface_ENI](##Elastic_Network_Interface_ENI)
- Elastic_Network_Interface_ENI
2. Elastic IP Address (EIP)
- [Elastic IP Address (EIP)](aws-ass-solution-architect.md#elastic_ip_address_eip)
- It is not a networking device that can be used to facilitate HPC workflows.
3. Elastic Network Adapter (ENA)
- [Elastic Network Adapter (ENA)](aws-ass-solution-architect.md#elastic-network-adapter-ena)
- Although enhanced networking provides higher bandwidth, higher packet per second (PPS) performance, and consistently lower inter-instance latencies, still EFA is a better fit for the given use-case because the EFA device provides all the functionality of an ENA device, plus hardware support for applications to communicate directly with the EFA device without involving the instance kernel (OS-bypass communication) using an extended programming interface.

## 2 Config history
- A financial services company has recently migrated from on-premises infrastructure to AWS Cloud.
  The DevOps team wants to implement a solution that allows all resource configurations to be reviewed and make sure that they meet compliance guidelines.
- Also, the solution should be able to offer the capability to look into the resource configuration history across the application stack.

As a solutions architect, which of the following solutions would you recommend to the team?

**Solution**
- *Use AWS Config to review resource configurations to meet compliance guidelines and maintain a history of resource configuration changes*
  - 
**Wrong**
1. *Use Amazon CloudWatch to review resource configurations to meet compliance guidelines and maintain a history of resource configuration changes*
    - AWS CloudWatch provides you with data and actionable insights to monitor your applications, respond to system-wide performance changes, optimize resource utilization, and get a unified view of operational health. You cannot use Amazon CloudWatch to maintain a history of resource configuration changes.

2. *Use AWS CloudTrail to review resource configurations to meet compliance guidelines and maintain a history of resource configuration changes*
- With AWS CloudTrail, you can log, continuously monitor, and retain account activity related to actions across your AWS infrastructure.
- You can use AWS CloudTrail to answer questions such as - “Who made an API call to modify this resource?”.
- AWS CloudTrail provides an event history of your AWS account activity thereby enabling governance, compliance, operational auditing, and risk auditing of your AWS account. You cannot use AWS CloudTrail to maintain a history of resource configuration changes.

3. *Use AWS Systems Manager to review resource configurations to meet compliance guidelines and maintain a history of resource configuration changes*
- Using AWS Systems Manager, you can group resources, like Amazon EC2 instances, Amazon S3 buckets, or Amazon RDS instances, by application, view operational data for monitoring and troubleshooting, and take action on your groups of resources.
- You cannot use AWS Systems Manager to maintain a history of resource configuration changes.

**Note**
You may see scenario-based questions asking you to select one of Amazon CloudWatch vs AWS CloudTrail vs AWS Config. Just remember this thumb rule
1. Think resource performance monitoring, events, and alerts; think Amazon CloudWatch.
2. Think account-specific activity and audit; think AWS CloudTrail.
3. Think resource-specific history, audit, and compliance; think AWS Config.

## 3 Datatabase Migration

The **business analytics team** at a company has been running ad-hoc queries on **Oracle and PostgreSQL services on Amazon RDS** to prepare daily reports for senior management.
To facilitate the business analytics reporting, the engineering team now wants to *continuously replicate this data and consolidate these databases into a petabyte-scale data warehouse by streaming data to Amazon Redshift*.

As a solutions architect, which of the following would you recommend as the MOST resource-efficient solution that requires the LEAST amount of development time without the need to manage the underlying infrastructure?

**Solution**
Use [AWS Database Migration Service (AWS DMS)](aws-ass-solution-architect.md#dms) to replicate the data into Amazon Redshift
- replicate your data with high availability and consolidate databases into a petabyte-scale data warehouse by streaming data to *Amazon Redshift* and *Amazon S3*.
- The Amazon Redshift cluster must be in the same AWS account and the same AWS Region as the replication instance
-  During a database migration to Amazon Redshift, AWS DMS first moves data to an Amazon S3 bucket. When the files reside in an Amazon S3 bucket, AWS DMS then transfers them to the proper tables in the Amazon Redshift data warehouse. AWS DMS creates the S3 bucket in the same AWS Region as the Amazon Redshift database. The AWS DMS replication instance must be located in that same region.

**Wrong**
- Use [Glue](aws-ass-solution-architect.md#glue)
    - Using AWS Glue involves significant development efforts to write custom migration scripts to copy the database data into Redshift.
      Use [AWS EMR](aws-ass-solution-architect.md#emr) to replicate the data into Amazon Redshift
    - Using EMR involves significant infrastructure management efforts to set up and maintain the EMR cluster. Additionally this option involves a major development effort to write custom migration jobs to copy the database data into Redshift.

Use [Amazon Kinesis Data Streams](aws-ass-solution-architect.md#kinesis_data_stream) to replicate  into Amazon Redshift
- However, the user is expected to manually provision an appropriate number of shards to process the expected volume of the incoming data stream

## 4 RDS Read Replica
The application maintenance team at a company has noticed that the production application is very slow when the business reports are run on the Amazon RDS database. These reports fetch a large amount of data and have complex queries with multiple joins, spanning across multiple business-critical core tables.
- *CPU, memory, and storage metrics are around 50% of the total capacity*.

Can you recommend an improved and cost-effective way of generating the business reports while keeping the production application unaffected?



**Solution**
- Create a read replica and connect the report generation tool/application to it
    - [Read Relica](aws-ass-solution-architect.md#rds_read_replicas)

**Wrong**
1. Increase the size of Amazon RDS instance
- *CPU, memory, and storage metrics are around 50% of the total capacity*

2. Migrate from General Purpose SSD to magnetic storage to enhance IOPS
- This is incorrect. Amazon RDS supports magnetic storage for backward compatibility only. AWS recommends that you use General Purpose SSD or Provisioned IOPS for any storage needs.

1. Configure the Amazon RDS instance to be Multi-AZ DB instance, and connect the report generation tool to the DB instance in a different AZ
- Amazon RDS Multi-AZ deployments provide enhanced availability and durability for RDS database (DB) instances, making them a natural fit for production database workloads. When you provision a Multi-AZ DB Instance, Amazon RDS automatically creates a primary DB Instance and synchronously replicates the data to a standby instance in a different Availability Zone (AZ). Each AZ runs on its own physically distinct, independent infrastructure, and is engineered to be highly reliable. However, you cannot read from the standby database, making multi-AZ, an incorrect option for the given scenario.

## 5 Choose DB
- A global manufacturing company with facilities in the US, Europe, and Asia is designing a new distributed application to optimize its procurement workflow.
- The orders booked in one AWS Region should be visible to all AWS Regions in a second or less.
- The database should be able to facilitate failover with a short *Recovery Time Objective (RTO)*. The uptime of the application is critical to ensure that the manufacturing processes are not impacted.

MOST cost-effective solution?

**Solution**
Provision Amazon Aurora Global Database
- [Aurora Global](aws-ass-solution-architect.md#aurora_global_table)
- [Disaster_Recovery](aws-ass-solution-architect.md#aurora_disaster_recovery)

**Wrong**
Provision Amazon RDS for PostgreSQL with a cross-Region read replica
Provision Amazon RDS for MySQL with a cross-Region read replica
-  For a failover, read replicas have to be manually promoted to a standalone database instance since the process is not automatic. Hence, the RTO will be quite high, so both these options are not correct for this use case.

Provision Amazon DynamoDB global tables
-  Aurora Global Database is good for applications that need to support cross-Region reads with low latency updates and the ability to quickly failover between regions.
-  DynamoDB global tables provide cross-region active-active capabilities with high performance, but you lose some of the data access flexibility that comes with SQL-based databases.
-  Due to the active-active configuration of DynamoDB global tables, there is no concept of failover because the application writes to the table in its region, and then the data is replicated to keep the other regions' table in sync. DynamoDB global tables is a much costlier solution than Aurora Global Database for the given requirement.

## 6
- An e-commerce company uses **Microsoft Active Directory** to provide users and groups with access to resources on the on-premises infrastructure.
- The company has extended its IT infrastructure to AWS in the form of a hybrid cloud.
  The engineering team at the company wants to run directory-aware workloads on AWS for a SQL Server-based application.
- The team also wants to configure a trust relationship to enable single sign-on (SSO) for its users to access resources *in either domain*.
  As a solutions architect, which of the following AWS services would you recommend for this use-case?

**Solution**
AWS Directory Service for Microsoft Active Directory (AWS Managed Microsoft AD)
- [AWS_Directory_Service](aws-ass-solution-architect.md#aws_directory_service)

**Wrong**
Simple Active Directory (Simple AD)
- Simple AD does not support features such as trust relationships with other domains. Therefore, this option is not correct.
  Amazon Cloud Directory
- [Cloud_Directory](aws-ass-solution-architect.md#cloud_directory)
  Active Directory Connector
- Use AD Connector if you only need to allow your on-premises users to log in to AWS applications and services with their Active Directory credentials. AD Connector simply connects your existing on-premises Active Directory to AWS. You cannot use it to run directory-aware workloads on AWS, hence this option is not correct.

**Exam Alert:**
You may see questions on choosing "AWS Managed Microsoft AD" vs "AD Connector" vs "Simple AD" on the exam. Just remember that you should use AD Connector if you only need to allow your on-premises users to log in to AWS applications with their Active Directory credentials. AWS Managed Microsoft AD would also allow you to run directory-aware workloads in the AWS Cloud. AWS Managed Microsoft AD is your best choice if you have more than 5,000 users and need a trust relationship set up between an AWS hosted directory and your on-premises directories. Simple AD is the least expensive option and your best choice if you have 5,000 or fewer users and don’t need the more advanced Microsoft Active Directory features such as trust relationships with other domains.

## Question 7
A financial services company wants to identify any sensitive data stored on its Amazon S3 buckets.
The company also wants to monitor and protect all data stored on Amazon S3 against any malicious activity.

As a solutions architect, which of the following solutions would you recommend to help address the given requirements?

**Solution**
- Use Amazon GuardDuty to monitor any malicious activity on data stored in Amazon S3. Use Amazon Macie to identify any sensitive data stored on Amazon S3
    - [GuardDuty](aws-ass-solution-architect.md#guardduty)
    - [Macie](aws-ass-solution-architect.md#macie)



## Question 8
Your application is hosted by a provider on yourapp.provider.com. You would like to have your users access your application using www.your-domain.com, which you own and manage under Amazon Route 53.

Which Amazon Route 53 record should you create?


**Solution**
- Create a CNAME record
    - A CNAME record maps DNS queries for the name of the current record, such as acme.example.com, to another domain (example.com or example.net) or subdomain (acme.example.com or zenith.example.org).

**Wrong**
- Create an Alias Record
    - ![](https://assets-pt.media.datacumulus.com/aws-saa-pt/assets/pt4-q64-i1.jpg)
- Create an A record
    - Used to point a domain or subdomain to an IP address. 'A record' cannot be used to map one domain name to another.
- Create a PTR record
    -  A Pointer (PTR) record resolves an IP address to a fully-qualified domain name (FQDN) as an opposite to what A record does. PTR records are also called Reverse DNS records. 'PTR record' cannot be used to map one domain name to another.

- Create an Alias Record
    - Alias records let you route traffic to selected AWS resources, such as Amazon CloudFront distributions and Amazon S3 buckets. They also let you route traffic from one record in a hosted zone to another record. 3rd party websites do not qualify for these as we have no control over those. 'Alias record' cannot be used to map one domain name to another.



## Question 9
- A data analytics company manages an application that stores user data in a Amazon DynamoDB table.
- The development team has observed that once in a while, the application writes corrupted data in the Amazon DynamoDB table. As soon as the issue is detected, the team needs to remove the corrupted data at the earliest.

What do you recommend?


**Solution**
Use Amazon DynamoDB on-demand backup to restore the table to the state just before corrupted data was written
- Amazon DynamoDB enables you to back up your table data continuously by using point-in-time recovery (PITR). When you enable PITR, DynamoDB backs up your table data automatically with per-second granularity so that you can restore to any given second in the preceding 35 days.

- PITR helps protect you against accidental writes and deletes. For example, if a test script writes accidentally to a production DynamoDB table or someone mistakenly issues a "DeleteItem" call, PITR has you covered.
  **Wrong**
- **Use Amazon DynamoDB on-demand backup to restore the table to the state** just before corrupted data was written - The on-demand backup and restore process scales without degrading the performance or availability of your applications. It uses a new and unique distributed technology that lets you complete backups in seconds regardless of table size. You can create backups that are consistent within seconds across thousands of partitions without worrying about schedules or long-running backup processes. All on-demand backups are cataloged, discoverable, and retained until they are explicitly deleted.
- **Configure the Amazon DynamoDB table as a global table** and point the application to use the table from another AWS region that has no corrupted data - Global tables build on the global Amazon DynamoDB footprint to provide you with a fully managed, multi-Region, and multi-active database that delivers fast, local, read and write performance for massively scaled, global applications.

Global tables eliminate the difficult work of replicating data between Regions and resolving update conflicts, enabling you to focus on your application's business logic. In addition, global tables enable your applications to stay highly available even in the unlikely event of isolation or degradation of an entire Region.

Any changes made to any item in any replica table are replicated to all the other replicas within the same global table. In a global table, a newly written item is usually propagated to all replica tables within a second. With a global table, each replica table stores the same set of data items. Amazon DynamoDB does not support partial replication of only some of the items. If applications update the same item in different Regions at about the same time, conflicts can arise. To help ensure eventual consistency, Amazon DynamoDB global tables use a last-writer-wins reconciliation between concurrent updates, in which DynamoDB makes its best effort to determine the last writer. With this conflict resolution mechanism, all replicas agree on the latest update and converge toward a state in which they all have identical data.

Global tables replicate your Amazon DynamoDB tables automatically across your choice of AWS Regions. This option has been added as a distractor since you cannot point the application to use the table from another AWS region, since there is no "other" table in another region. It's just a single logical Global table.

- *Use Amazon DynamoDB Streams* to restore the table to the state just before corrupted data was written - Amazon DynamoDB Streams captures a time-ordered sequence of item-level modifications in any Amazon DynamoDB table and stores this information in a log for up to 24 hours. Applications can access this log and view the data items as they appeared before and after they were modified, in near-real time. A DynamoDB stream is an ordered flow of information about changes to items in a Amazon DynamoDB table. When you enable a stream on a table, DynamoDB captures information about every modification to data items in the table.

Amazon DynamoDB Streams writes stream records in near-real time so that you can build applications that consume these streams and take action based on the contents. It will take considerable effort and custom coding to reliably rebuild table data to the state just before any corrupted data was written. So this option is not the best fit.

## Question 10

A retail company has its flagship application running on a fleet of Amazon EC2 instances behind Elastic Load Balancing (ELB). The engineering team has been seeing recurrent issues wherein the in-flight requests from the ELB to the Amazon EC2 instances are getting dropped when an instance becomes unhealthy.

Which of the following features can be used to address this issue?

**Solution**
- [ebl_connection_draining](aws-ass-solution-architect.md#ebl_connection_draining)

**Wrong**
- [elb_idle_timeout](aws-ass-solution-architect.md#elb_idle_timeout)
- [ELB_CrossZoneLoadBalancing](aws-ass-solution-architect.md#ELB_CrossZoneLoadBalancing)
- [ELB_Sticky_Sessions](aws-ass-solution-architect.md#elb_sticky_sessions)

## 11
- A health care application processes the real-time health data of the patients into an analytics workflow. - With a sharp increase in the number of users, the system has become slow and sometimes even unresponsive as it does not have a retry mechanism. 
- The startup is looking at a scalable solution that has minimal implementation overhead.

**Correct option:**

*Use Amazon Kinesis Data Streams to ingest the data, process it using AWS Lambda or run analytics using Amazon Kinesis Data Analytics*

- [Amazon Kinesis Data Streams (KDS)](aws-ass-solution-architect.md#kinesis_data_stream) 
- KDS makes sure your streaming data is available to multiple real-time analytics applications, to Amazon S3, or AWS Lambda within 70 milliseconds of the data being collected.
-  Amazon Kinesis data streams scale from megabytes to terabytes per hour and scale from thousands to millions of PUT records per second. 
- You can dynamically adjust the throughput of your stream at any time based on the volume of your input data.

Incorrect options:

*Use Amazon Simple Notification Service (Amazon SNS) for data ingestion and configure AWS Lambda to trigger logic for downstream processing* 
- Amazon Simple Notification Service (Amazon SNS) is a fully managed messaging service for both application-to-application (A2A) and application-to-person (A2P) communication. Amazon SNS is a push mechanism that does not support **robust retry mechanisms**, as is needed in the current use case.

- *Use Amazon Simple Queue Service (Amazon SQS) for data ingestion and configure AWS Lambda to trigger logic for downstream processing* - Amazon Simple Queue Service (Amazon SQS) is a messaging service that helps in decoupling systems and reducing the complexity of architecture. Amazon SQS can still work but Amazon Kinesis Data streams is custom made for streaming real-time data.

- *Use Amazon API Gateway with the existing REST-based interface to create a high performing architecture* - Amazon API Gateway is not meant for handling real-time streaming data.

## 12
- An IT company is using Amazon Simple Queue Service (Amazon SQS) queues for decoupling the various components of application architecture. 
- As the consuming components need additional time to process Amazon Simple Queue Service (Amazon SQS) messages, the company wants to postpone the delivery of new messages to the queue for a few seconds.

As a solutions architect, which of the following solutions would you suggest to the company?

**Solution**
- Use visibility timeout to postpone the delivery of new messages to the queue for a few seconds
  - [Delay queues](aws-ass-solution-architect.md#sqs_delay_queue)
**Wrong**

1. Use dead-letter queues to postpone the delivery of new messages to the queue for a few seconds
  - [dead_letter_queue](aws-ass-solution-architect.md#dead_letter_queue)

2. Use Amazon SQS FIFO queues to postpone the delivery of new messages to the queue for a few seconds
  - [fifo](aws-ass-solution-architect.md#sqs_fifo_queue)

3. Use visibility timeout to postpone the delivery of new messages to the queue for a few seconds
  - [Visibility_timeout](aws-ass-solution-architect.md#visibility_timeout)

## 13
- A company has a license-based, expensive, legacy commercial database solution deployed at its on-premises data center. 
- The company wants to migrate this database to a more efficient, open-source, and cost-effective option on AWS Cloud. The CTO at the company wants a solution that can handle complex database configurations such as secondary indexes, foreign keys, and stored procedures.

As a solutions architect, which of the following AWS services should be combined to handle this use-case? (Select two)

**Solution**

*AWS Database Migration Service (AWS DMS)*
*AWS Schema Conversion Tool (AWS SCT)*


  - [DMS](aws-ass-solution-architect.md#dms)
  - AWS Database Migration Service helps you migrate databases to AWS quickly and securely. The source database remains fully operational during the migration, minimizing downtime to applications that rely on the database. AWS Database Migration Service supports homogeneous migrations such as Oracle to Oracle, as well as heterogeneous migrations between different database platforms, such as Oracle or Microsoft SQL Server to Amazon Aurora.
  - Given the use-case where the CTO at the company wants to move away from license-based, expensive, legacy commercial database solutions deployed at the on-premises data center to more efficient, open-source, and cost-effective options on AWS Cloud, this is an example of heterogeneous database migrations.
  - That makes heterogeneous migrations a two-step process.
    -  First use the *AWS Schema Conversion Tool* to convert the source schema and code to match that of the target database, and then use the AWS Database Migration Service to migrate data from the source database to the target database. 
    -  All the required data type conversions will automatically be done by the *AWS Database Migration Service* during the migration. The source database can be located on your on-premises environment outside of AWS, running on an Amazon EC2 instance, or it can be an Amazon RDS database. The target can be a database in Amazon EC2 or Amazon RDS.
  - [heterogeneous_migrations](aws-ass-solution-architect.md#heterogeneous_migrations)



**Wrong**
*AWS Glue*
- AWS Glue is a fully managed extract, transform, and load (ETL) service that makes it easy for customers to prepare and load their data for analytics. AWS Glue job is meant to be used for batch ETL data processing. Therefore, it cannot be used for database migrations.
*AWS Snowball Edge*
- AWS Snowball Edge
- You may see the Snowball device on the exam, just remember that the original Snowball device had 80TB of storage space. AWS Snowball Edge cannot be used for database migrations.

*Basic Schema Copy*
- To quickly migrate a database schema to your target instance you can rely on the Basic Schema Copy feature of AWS Database Migration Service. Basic Schema Copy will automatically create tables and primary keys in the target instance if the target does not already contain tables with the same names. Basic Schema Copy is great for doing a test migration, or when you are migrating databases heterogeneously e.g. Oracle to MySQL or SQL Server to Oracle. Basic Schema Copy will not migrate secondary indexes, foreign keys or stored procedures. When you need to use a more customizable schema migration process (e.g. when you are migrating your production database and need to move your stored procedures and secondary database objects), you must use the AWS Schema Conversion Tool.

## 14
An engineering lead is designing a VPC with public and private subnets. The VPC and subnets use IPv4 CIDR blocks. 
There is one public subnet and one private subnet in each of three Availability Zones (AZs) for high availability. 
An internet gateway is used to provide internet access for the public subnets. 
The private subnets require access to the internet to allow Amazon EC2 instances to download software updates.

Which of the following options represents the correct solution to set up internet access for the private subnets?

**Solution**
1. Set up three NAT gateways, one in each public subnet in each AZ. Create a custom route table for each AZ that forwards non-local traffic to the NAT gateway in its AZ
   1. [Nat Gateway](aws-ass-solution-architect.md#vpc_nat_gateway)


**Wrong**



2. *Set up three NAT gateways, one in each private subnet in each AZ. Create a custom route table for each AZ that forwards non-local traffic to the NAT gateway in its AZ*
-  NAT gateways need to be set up in public subnets, so this option is incorrect.

3. Set up three egress-only internet gateways, one in each public subnet in each AZ. Create a custom route table for each AZ that forwards non-local traffic to the egress-only internet gateway in its AZ
- An Egress-only Internet gateway is a horizontally scaled, redundant, and highly available VPC component that allows outbound communication over IPv6 from instances in your VPC to the internet, and prevents the internet from initiating an IPv6 connection with your instances. The given use-case is for IPv4 traffic, hence an Egress-only Internet gateway is not an option.

*4. Set up three Internet gateways, one in each private subnet in each AZ. Create a custom route table for each AZ that forwards non-local traffic to the Internet gateway in its AZ*
- Internet gateways cannot be provisioned in private subnets of a VPC.

## 15
The engineering team at a social media company wants to use Amazon CloudWatch alarms to automatically recover Amazon EC2 instances if they become impaired. The team has hired you as a solutions architect to provide subject matter expertise.

As a solutions architect, which of the following statements would you identify as CORRECT regarding this automatic recovery process? (Select two)

**Solution**
- A recovered instance is identical to the original instance, including the instance ID, private IP addresses, Elastic IP addresses, and all instance metadata

- If your instance has a public IPv4 address, it retains the public IPv4 address after recovery

**Wrong**

*Terminated Amazon EC2 instances can be recovered if they are configured at the launch of instance* - This is incorrect as terminated instances cannot be recovered.

*During instance recovery, the instance is migrated during an instance reboot, and any data that is in-memory is retained* - As mentioned above, during instance recovery, the instance is migrated during an instance reboot, and any data that is in-memory is lost.

*If your instance has a public IPv4 address*, it does not retain the public IPv4 address after recovery - As mentioned above, if your instance has a public IPv4 address, it retains the public IPv4 address after recovery.


## Question 16

A financial services company is looking to move its on-premises IT infrastructure to AWS Cloud. The company has multiple long-term server bound licenses across the application stack and the CTO wants to continue to utilize those licenses while moving to AWS.

As a solutions architect, which of the following would you recommend as the MOST cost-effective solution?

**Solution**
- Use [Amazon EC2 dedicated hosts](aws-ass-solution-architect.md#ec2_dedicated_hosts)

  
## Question 17

A retail company uses AWS Cloud to manage its IT infrastructure. 
The company has set up AWS Organizations to manage several departments running their AWS accounts and using resources such as Amazon EC2 instances and Amazon RDS databases. 
The company wants to provide shared and centrally-managed VPCs to all departments using applications that need a high degree of interconnectivity.

As a solutions architect, which of the following options would you choose to facilitate this use-case?

**Solution**
3. Use *VPC sharing* to *share a VPC with other AWS accounts* belonging to the same parent organization from AWS Organizations
  - [VPC Sharing](aws-ass-solution-architect.md#vpc_sharing)
**Wrong**
1. Use *VPC peering* to *share a VPC with other AWS accounts* belonging to the same parent organization from AWS Organizations
- shares one or more subnets, The owner account cannot share the VPC itself.

2. Use *VPC sharing* to *share one or more subnets with other AWS accounts* belonging to the same parent organization from AWS Organizations

4. Use *VPC peering* to *share one or more subnets with other AWS accounts* belonging to the same parent organization from AWS Organizations
   - Instances in either VPC can communicate with each other as if they are within the same network. VPC peering does not facilitate centrally managed VPCs. Therefore this option is incorrect.

## Question 18
A startup has recently moved their monolithic web application to AWS Cloud. The application runs on a single Amazon EC2 instance. Currently, the user base is small and the startup does not want to spend effort on elaborate disaster recovery strategies or Auto Scaling Group. The application can afford a maximum downtime of 10 minutes.

In case of a failure, which of these options would you suggest as a cost-effective and automatic recovery procedure for the instance?

**Solution**
- Configure an *Amazon CloudWatch alarm* that triggers the recovery of the Amazon EC2 instance, in case the instance fails. The instance, however, should only be configured with an Amazon EBS volume
  - [EC2 Instance Recover](aws-ass-solution-architect.md#ec2_instance_recover)
**Wrong**
- Configure *Amazon EventBridge events* that can *trigger the recovery* of the Amazon EC2 instance, in case the instance or the application fails
  - You cannot use Amazon EventBridge events to directly trigger the recovery of the Amazon EC2 instance.

- Configure *AWS Trusted Advisor* to monitor the health check of Amazon EC2 instance and provide a remedial action in case an unhealthy flag is detected
  - You can use Amazon EventBridge events to detect and react to changes in the status of AWS Trusted Advisor checks. This support is only available with AWS Business Support and AWS Enterprise Support. AWS Trusted Advisor by itself does not support health checks of Amazon EC2 instances or their recovery.

- Configure an *Amazon CloudWatch alarm* that triggers the recovery of the Amazon EC2 instance, in case the instance fails. The instance can be configured with Amazon Elastic Block Store (Amazon EBS) or with instance store volumes
  - The recover action is supported only on instances that have Amazon EBS volumes configured on them, instance store volumes are not supported for automatic recovery by Amazon CloudWatch alarms.

## Question 19
- An IT consultant is helping a small business revamp their technology infrastructure on the AWS Cloud. 
- The business has *two AWS accounts* and all resources are provisioned in the `us-west-2` region. 

- The IT consultant is trying to launch an Amazon EC2 instance in each of the two AWS accounts such that the instances are in the same Availability Zone (AZ) of the `us-west-2` region.

- Even after selecting the same default subnet (us-west-2a) while launching the instances in each of the AWS accounts, the IT consultant notices that the Availability Zones (AZs) are still different.

As a solutions architect, which of the following would you suggest resolving this issue?

**Solution**
- Use Availability Zone (AZ) ID to uniquely identify the Availability Zones across the two AWS Accounts
  - An Availability Zone is represented by a region code followed by a letter identifier; for example, us-east-1a. To ensure that resources are distributed across the Availability Zones for a region, AWS maps Availability Zones to names for each AWS account. For example, the Availability Zone us-west-2a for one AWS account might not be the same location as us-west-2a for another AWS account.

  - To coordinate Availability Zones across accounts, you must use the AZ ID, which is a unique and consistent identifier for an Availability Zone. For example, usw2-az2 is an AZ ID for the us-west-2 region and it has the same location in every AWS account.

  - Viewing AZ IDs enables you to determine the location of resources in one account relative to the resources in another account. For example, if you share a subnet in the Availability Zone with the AZ ID usw2-az2 with another account, this subnet is available to that account in the Availability Zone whose AZ ID is also usw2-az2.

  - You can view the AZ IDs by going to the service health section of the Amazon EC2 Dashboard via your AWS Management Console.
**Wrong**
- Reach out to AWS Support for creating the Amazon EC2 instances in the same Availability Zone (AZ) across the two AWS accounts
  - Since the AZ ID is a unique and consistent identifier for an Availability Zone, there is no need to contact AWS Support. Therefore, this option is incorrect.

- Use the default VPC to uniquely identify the Availability Zones across the two AWS Accounts
  - *VPC* is a virtual network dedicated to your AWS account. It is logically isolated from other virtual networks in the AWS Cloud. Since a VPC spans an AWS region, it cannot be used to uniquely identify an Availability Zone. Therefore, this option is incorrect.


- Use the default subnet to uniquely identify the Availability Zones across the two AWS Accounts
  - *A subnet* is a range of IP addresses in your VPC. A subnet spans an Availability Zone of an AWS region. The default subnet representing the Availability Zone us-west-2a for one AWS account might not be the same location as us-west-2a for another AWS account. Therefore, this option is incorrect.

## Question 20

An e-commerce company is using Elastic Load Balancing (ELB) for its fleet of Amazon EC2 instances spread across two Availability Zones (AZs), 
- with 
  - one instance as a target in **Availability Zone A** 
  - four instances as targets in **Availability Zone B**. 
- The company is doing benchmarking for server performance when cross-zone load balancing is enabled compared to the case when cross-zone load balancing is disabled.

**Solution**
With cross-zone load balancing enabled, one instance in Availability Zone A receives 20% traffic and four instances in Availability Zone B receive 20% traffic each. With cross-zone load balancing disabled, one instance in Availability Zone A receives 50% traffic and four instances in Availability Zone B receive 12.5% traffic each
  - [ELB_Crosszone_load_balancing](aws-ass-solution-architect.md#ELB_CrossZoneLoadBalancing)
**Wrong**

With cross-zone load balancing enabled, one instance in Availability Zone A receives no traffic and four instances in Availability Zone B receive 25% traffic each. With cross-zone load balancing disabled, one instance in Availability Zone A receives 50% traffic and four instances in Availability Zone B receive 12.5% traffic each

With cross-zone load balancing enabled, one instance in Availability Zone A receives 50% traffic and four instances in Availability Zone B receive 12.5% traffic each. With cross-zone load balancing disabled, one instance in Availability Zone A receives 20% traffic and four instances in Availability Zone B receive 20% traffic each

With cross-zone load balancing enabled, one instance in Availability Zone A receives 20% traffic and four instances in Availability Zone B receive 20% traffic each. With cross-zone load balancing disabled, one instance in Availability Zone A receives no traffic and four instances in Availability Zone B receive 25% traffic each


## 21
The DevOps has created **a custom VPC (V1)** and attached an **Internet Gateway (I1)** to the VPC. 

The team has also created a **subnet (S1)** in this custom VPC and added a route to this **subnet's route table** (R1) that directs internet-bound traffic to the Internet Gateway. 

Now the team launches an **Amazon EC2 instance (E1)** in the **subnet S1** and assigns **a public IPv4 address to this instance. **
  
Next the team also launches a **Network Address Translation (NAT)** instance (N1) in the **subnet S1**.

Under the given infrastructure setup, which of the following entities is doing the *Network Address Translation* for E1?

**Solution**
[Internet Gateway (I1)](aws-ass-solution-architect.md#vpc_internet_gateway)
**Wrong**
- Subnet (S1) + Route Table (R1)
  - **VPC** is a virtual network dedicated to your AWS account. 
  - **A subnet** is a range of IP addresses in your VPC. 
  - **A route table** contains a set of rules, called routes, that are used to determine where network traffic is directed. 
  - -> ~~Therefore neither Subnet nor Route Table can be used for Network Address Translation.~~

- *Network Address Translation (NAT)* instance (N1)
  - You can use a network address translation (NAT) instance in a public subnet in your VPC to enable instances in *the private subnet* to *initiate outbound* IPv4 traffic to the Internet or other AWS services, but prevent the instances from *receiving inbound traffic* initiated by someone on the Internet. As the instance E1 is in a public subnet, therefore this option is not correct.

References:
- https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Internet_Gateway.html
- https://docs.aws.amazon.com/vpc/latest/userguide/VPC_NAT_Instance.html

## Question 22
An **AWS Organization** is using **Service Control Policies (SCPs)** for central control over the maximum available permissions for all accounts in their organization. 

This allows the organization to ensure that all accounts stay within the organization’s access control guidelines.

Which of the given scenarios are correct regarding the permissions described below? **(Select three)**

**Solution**
If a user or role has an IAM permission policy that grants access to an action that is either not allowed or explicitly denied by the applicable service control policy (SCP), the user or role can't perform that action

Service control policy (SCP) affects all users and roles in the member accounts, including root user of the member accounts

Service control policy (SCP) does not affect service-linked role
**Wrong**
1. Service control policy (SCP) affects all users and roles in the member accounts, excluding root user of the member accounts
4. Service control policy (SCP) affects service-linked roles
5. Service control policy (SCP) affects all users and roles in the member accounts, excluding root user of the member accounts
6. If a user or role has an IAM permission policy that grants access to an action that is either not allowed or explicitly denied by the applicable service control policy (SCP), the user or role can still perform that action


## Question 23
- A company wants to improve its gaming application by adding a leaderboard that uses a complex proprietary algorithm based on the participating user's performance metrics to identify the top users on a real-time basis. 
- The technical requirements mandate high elasticity, low latency, and real-time processing to deliver customizable user data for the community of users. 
- The leaderboard would be accessed by millions of users simultaneously.

Which of the following options support the case for using Amazon ElastiCache to meet the given requirements? (Select two)

**Solution**
- Use Amazon ElastiCache to improve latency and throughput for read-heavy application workloads
- Use Amazon ElastiCache to improve the performance of compute-intensive workloads
- [ElastiCache](aws-ass-solution-architect.md#amazone-elasticache---summanry)
**Wrong**
- Use Amazon ElastiCache to improve the performance of Extract-Transform-Load (ETL) workloads

- Use Amazon ElastiCache to run highly complex JOIN queries
- Use Amazon ElastiCache to improve latency and throughput for write-heavy application workloads

## Question 24