# Practice Test 3

## 1 - HPC
A biotechnology company has multiple **High Performance Computing (HPC)** workflows that quickly and accurately process and analyze genomes for hereditary diseases.
The company is looking to *migrate* these workflows from their on-premises infrastructure to AWS Cloud.

As a solutions architect, which of the following networking components would you recommend on the Amazon EC2 instances running these HPC workflows?

**Solution**

4. [EFA](aws-ass-solution-architect.md#elastic-fabric-adapter-efa)

**Wrong**

1.[Elastic_Network_Interface_ENI](aws-ass-solution-architect.md#elastic_network_interface_eni)
2.[Elastic IP Address (EIP)](aws-ass-solution-architect.md#elastic_ip_address_eip)
  - It is not a networking device that can be used to facilitate HPC workflows.
3. [Elastic Network Adapter (ENA)](aws-ass-solution-architect.md#elastic-network-adapter-ena)
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
- An e-commerce company runs its web application on *Amazon EC2 instances* in an *Auto Scaling group* 
- Handle consumer orders in an *Amazon Simple Queue Service (Amazon SQS)* queue for downstream processing. 
- The DevOps team has observed that the performance of the application goes down in case of a sudden spike in orders received.

As a solutions architect, which of the following solutions would you recommend to address this use-case?
**Solution**
- Use a [target tracking scaling](aws-ass-solution-architect.md#target_tracking_scaling_policy) policy based on a custom Amazon SQS queue metric

**Wrong**
- Use a [simple scaling policy](aws-ass-solution-architect.md#simple_scaling_policy) based on a custom Amazon SQS queue metric
- Use a [scheduled scaling policy](aws-ass-solution-architect.md#scheduled_scaling_policy) based on a custom Amazon SQS queue metric
- Use a [step scaling policy](aws-ass-solution-architect.md#step_scaling_policy) based on a custom Amazon SQS queue metric

## 25
The DevOps team at an IT company has recently migrated to AWS and they are configuring security groups for their two-tier application with public web servers and private database servers.
- The team wants to understand the allowed configuration options for an inbound rule for a security group.

As a solutions architect, which of the following would you identify as an INVALID option for setting up such a configuration?

**Solution**
You can use an Internet Gateway ID as the custom source for the inbound rule
  - [security_group](aws-ass-solution-architect.md#security_group)
  - ![](https://assets-pt.media.datacumulus.com/aws-saa-pt/assets/pt4-q65-i1.jpg)
**Wrong**

You can use a security group as the custom source for the inbound rule

You can use an IP address as the custom source for the inbound rule

You can use a range of IP addresses in CIDR block notation as the custom source for the inbound rule

## 26
An IT company hosts windows based applications on its on-premises data center. 
The company is looking at moving the business to the AWS Cloud.
The cloud solution should offer shared storage space that multiple applications can access without a need for replication.
Also, the solution should integrate with the company's self-managed *Active Directory* domain.

Which of the following solutions addresses these requirements with the minimal integration effort?



**Solution**

Use Amazon FSx for Windows File Server as a shared storage solution
  - [](aws-ass-solution-architect.md#amazon_fsx_for_windows_file_server)
**Wrong**
Use Amazon FSx for Lustre as a shared storage solution with millisecond latencies
  - [Fsx for lustre](aws-ass-solution-architect.md#amazon-fsx-for-lustre)

Use Amazon Elastic File System (Amazon EFS) as a shared storage solution
  - [EFS](aws-ass-solution-architect.md#efs)

Use File Gateway of AWS Storage Gateway to create a hybrid storage solution
  - [AWS Storage Gateway](aws-ass-solution-architect.md#aws_storage_gateway)

## 27
- A media streaming company is looking to migrate its on-premises infrastructure into the AWS Cloud. 
- The engineering team is looking for a fully managed NoSQL persistent data store with in-memory caching to maintain low latency that is critical for real-time scenarios such as video streaming and interactive content. 
- The team expects the number of concurrent users to touch up to a million so the database should be able to scale elastically.

As a solutions architect, which of the following AWS services would you recommend for this use-case?

**Solution**
[Amazon DynamoDB](aws-ass-solution-architect.md#dynamodb)

**Wrong**
[Amazon DocumentDB](aws-ass-solution-architect.md#dynamodb)
[Amazon ElastiCache](aws-ass-solution-architect.md#elasticache)
[Amazon RDS](aws-ass-solution-architect.md#rds)

## 28
Question 28
Skipped
The DevOps team at a multi-national company is helping its subsidiaries standardize Amazon EC2 instances by using the same Amazon Machine Image (AMI). Some of these subsidiaries are in the same AWS region but use different AWS accounts whereas others are in different AWS regions but use the same AWS account as the parent company. The DevOps team has hired you as a solutions architect for this project.

Which of the following would you identify as CORRECT regarding the capabilities of an Amazon Machine Image (AMI)? (Select three)

**Solution**
You can share an Amazon Machine Image (AMI) with another AWS account
Copying an Amazon Machine Image (AMI) backed by an encrypted snapshot cannot result in an unencrypted target snapshot
You can copy an Amazon Machine Image (AMI) across AWS Regions
**Wrong**
You cannot copy an Amazon Machine Image (AMI) across AWS Regions

Copying an Amazon Machine Image (AMI) backed by an encrypted snapshot results in an unencrypted target snapshot
You cannot share an Amazon Machine Image (AMI) with another AWS account

## 29
- A company has set up AWS Organizations to manage several departments running their own AWS accounts. 
- The departments operate from different countries and are spread across various AWS Regions. 
- The company wants to set up a consistent resource provisioning process across departments so that each resource follows pre-defined configurations such as using a specific type of Amazon EC2 instances, specific IAM roles for AWS Lambda functions, etc.

As a solutions architect, which of the following options would you recommend for this use-case?

**Solution**
Use AWS CloudFormation StackSets to deploy the same template across AWS accounts and regions
  - [AWS CloudFormation StackSets](aws-ass-solution-architect.md#aws_cloudformation_stacksets)

**Wrong**
Use AWS Resource Access Manager (AWS RAM) to deploy the same template across AWS accounts and regions
  - AWS Resource Access Manager (AWS RAM) is a service that enables you to easily and securely share AWS resources with any AWS account or within your AWS Organization. Resource Access Manager cannot be used to deploy the same template across AWS accounts and regions.
Use AWS CloudFormation templates to deploy the same template across AWS accounts and regions
  - [CloudFormation templates](aws-ass-solution-architect.md#aws_cloudformation_template)
Use AWS CloudFormation stacks to deploy the same template across AWS accounts and regions
  - [AWS CloudFormation stacks](aws-ass-solution-architect.md#aws_cloudformation_stack)

## 30
- A financial services company wants to move the Windows file server clusters out of their datacenters. 
They are looking for cloud file storage offerings that provide full Windows compatibility.
- Can you identify the AWS storage services that provide highly reliable file storage that is accessible over the industry-standard Server Message Block (SMB) protocol compatible with Windows systems? (Select two)

**Solution**
Amazon FSx for Windows File Server
  - [Amazon FSx for Windows File Server](aws-ass-solution-architect.md#amazon_fsx_for_windows_file_server)
File Gateway Configuration of AWS Storage Gateway
  - Depending on the use case, AWS Storage Gateway provides 3 types of storage interfaces for on-premises applications: File, Volume, and Tape. The File Gateway enables you to store and retrieve objects in Amazon S3 using file protocols such as Network File System (NFS) and Server Message Block (SMB).
  - [AWS_Storage_gateway](aws-ass-solution-architect.md#aws_storage_gateway)
**Wrong**
Amazon Elastic File System (Amazon EFS)
  - Amazon EFS is a file storage service for use with Amazon EC2. Amazon EFS provides a file system interface, file system access semantics, and concurrently-accessible storage for up to thousands of Amazon EC2 instances. Amazon EFS uses the Network File System protocol. EFS does not support SMB protocol.
Amazon Simple Storage Service (Amazon S3)
  - Amazon EBS is a block-level storage service for use with Amazon EC2. Amazon EBS can deliver performance for workloads that require the lowest latency access to data from a single EC2 instance. EBS does not support SMB protocol.
Amazon Elastic Block Store (Amazon EBS)
  - Amazon Simple Storage Service (Amazon S3) is an object storage service that offers industry-leading scalability, data availability, security, and performance. Amazon S3 provides a simple, standards-based REST web services interface that is designed to work with any Internet-development toolkit. S3 does not support SMB protocol.

## Question 31
- A video conferencing application is hosted on a fleet of EC2 instances which are part of an Auto Scaling group. 
- The Auto Scaling group uses a Launch Template (LT1) with "dedicated" instance tenancy but the VPC (V1) used by the Launch Template LT1 has the instance tenancy set to default. 
- Later the DevOps team creates a new Launch Template (LT2) with shared (default) instance tenancy but the VPC (V2) used by the Launch Template LT2 has the instance tenancy set to dedicated.

Which of the following is correct regarding the instances launched via Launch Template LT1 and Launch Template LT2?
**Solution**
- The instances launched by both Launch Template LT1 and Launch Template LT2 will have default instance tenancy
  - [Launch Template](aws-ass-solution-architect.md#ec2_launch_template)
**Wrong**
- The instances launched by Launch Template LT1 will have default instance tenancy while the instances launched by the Launch Template LT2 will have dedicated instance tenancy
  - If either Launch Template Tenancy or VPC Tenancy is set to dedicated, then the instance tenancy is also dedicated. Therefore, this option is incorrect.
- The instances launched by both Launch Template LT1 and Launch Template LT2 will have dedicated instance tenancy
  - If either Launch Template Tenancy or VPC Tenancy is set to dedicated, then the instance tenancy is also dedicated. Therefore, this option is incorrect.

- The instances launched by Launch Template LT1 will have dedicated instance tenancy while the instances launched by the Launch Template LT2 will have shared (default) instance tenancy
  - If either Launch Template Tenancy or VPC Tenancy is set to dedicated, then the instance tenancy is also dedicated. Therefore, this option is incorrect.
- https://docs.aws.amazon.com/autoscaling/ec2/userguide/advanced-settings-for-your-launch-template.html

## Question 32
An online gaming application has a large chunk of its traffic coming from users who download static assets such as historic leaderboard reports and the game tactics for various games. 
The current infrastructure and design are unable to cope up with the traffic and application freezes on most of the pages.

Which of the following is a cost-optimal solution that does not need provisioning of infrastructure?

**Solution**
**Wrong**

Configure AWS Lambda with an Amazon RDS database to provide a serverless architecture

Use Amazon CloudFront with Amazon S3 as the storage solution for the static assets

Use AWS Lambda with Amazon ElastiCache and Amazon RDS for serving static assets at high speed and low latency
Question 32
Skipped
An online gaming application has a large chunk of its traffic coming from users who download static assets such as historic leaderboard reports and the game tactics for various games. The current infrastructure and design are unable to cope up with the traffic and application freezes on most of the pages.

Which of the following is a cost-optimal solution that does not need provisioning of infrastructure?

**Solution**

Use Amazon CloudFront with Amazon S3 as the storage solution for the static assets
  - [Amazon CloudFront with s3](aws-ass-solution-architect.md#cloudfront_with_s3)
**Wrong**
Configure AWS Lambda with an Amazon RDS database to provide a serverless architecture

Use AWS Lambda with Amazon ElastiCache and Amazon RDS for serving static assets at high speed and low latency

Use Amazon CloudFront with Amazon DynamoDB for greater speed and low latency access to static assets

## Question 33
A social media startup uses AWS Cloud to manage its IT infrastructure. 
The engineering team at the startup wants to perform weekly database rollovers for a MySQL database server using a *serverless cron job* that typically takes about 5 minutes to execute the database rollover script written in Python. 
The database rollover will archive the past week’s data from the production database to keep the database small while still keeping its data accessible.

As a solutions architect, which of the following would you recommend as the MOST cost-efficient and reliable solution?

**Solution**
Schedule a weekly Amazon EventBridge event cron expression to invoke an AWS Lambda function that runs the database rollover job
  - AWS Lambda lets you run code without provisioning or managing servers. You pay only for the compute time you consume. AWS Lambda supports standard rate and cron expressions for frequencies of up to once per minute.
  - ![](https://assets-pt.media.datacumulus.com/aws-saa-pt/assets/pt4-q30-i1.jpg)
**Wrong**

Provision an Amazon EC2 spot instance to run the database rollover script to be run via an OS-based weekly cron expression

Provision an Amazon EC2 scheduled reserved instance to run the database rollover script to be run via an OS-based weekly cron expression

*Create a time-based schedule option within an AWS Glue job to invoke itself every week and run the database rollover script*
  - AWS Glue job is meant to be used for batch ETL data processing and it's not the right fit for running a database rollover script. Although AWS Glue is also serverless, AWS Lambda is a more cost-effective option compared to AWS Glue.


## Question 34
- An e-commerce company has deployed its application on EC2 that are configured in a **private subnet** using IPv4. 
- These EC2 read and write a huge volume of data to and from Amazon S3 in the same AWS region. 
- The company has set up subnet routing to direct all the internet-bound traffic through a Network Address Translation gateway (NAT gateway). 
- The company wants to build the most cost-optimal solution without impacting the application's ability to communicate with Amazon S3 or the internet.

Which of the following would you recommend?

**Solution**

- Set up a *VPC gateway endpoint* for Amazon S3. Attach an endpoint policy to the endpoint. Update the route table to direct the S3-bound traffic to the VPC endpoint
  - [VPC_Gateway_Endpoint](aws-ass-solution-architect.md#VPC_Gateway_Endpoint)
**Wrong**

- Set up a *Gateway Load Balancer (GWLB)* endpoint for Amazon S3. Update the route table in the private subnet to direct the S3-bound traffic via the Gateway Load Balancer (GWLB) endpoint
  - [VPC_Gateway_Loadbalancer](aws-ass-solution-architect.md#vpc_gateway_loadbalancer)

- Provision an *internet gateway*. Update the route table in the private subnet to route traffic to the internet gateway. Update the network ACL (NACL) to allow the S3-bound traffic
  - If a subnet is associated with a route table that has a route to an internet gateway, it's known as a **public subnet**
  - This option has been added as a distractor as adding a route to the internet gateway in the route table associated with the private subnet would make the subnet public.

- Set up an *egress-only internet gateway* in the public subnet. Update the route table in the private subnet to route traffic to the internet gateway. Update the network ACL to allow the S3-bound traffic
  - Egress use for IP6 -> Wrong 
## Question 35
A startup has created a new web application for users to complete a risk assessment survey for COVID-19 symptoms via a self-administered questionnaire. The startup has purchased the domain covid19survey.com using Amazon Route 53. The web development team would like to create Amazon Route 53 record so that all traffic for covid19survey.com is routed to www.covid19survey.com.

As a solutions architect, which of the following is the MOST cost-effective solution that you would recommend to the web development team?

**Solution**
- Create an alias record for covid19survey.com that routes traffic to www.covid19survey.com
  - [Alias Record](aws-ass-solution-architect.md#dns_alias_records)
    - You can create an alias record at the top node of a DNS namespace, also known as the zone apex, however, you cannot create a CNAME record for the top node of the DNS namespace. So, if you register the DNS name covid19survey.com, the zone apex is covid19survey.com. You can't create a CNAME record for covid19survey.com, but you can create an alias record for covid19survey.com that routes traffic to www.covid19survey.com.

**Wrong**
- Create an MX record for covid19survey.com that routes traffic to www.covid19survey.com
  - An MX record specifies the names of your mail servers and, if you have two or more mail servers, the priority order. It cannot be used to create Amazon Route 53 record to route traffic for the top node of the DNS namespace, so this option is incorrec
- Create an NS record for covid19survey.com that routes traffic to www.covid19survey.com
  - An NS record identifies the name servers for the hosted zone. It cannot be used to create Amazon Route 53 record to route traffic for the top node of the DNS namespace, so this option is incorrect.
- Create a CNAME record for covid19survey.com that routes traffic to www.covid19survey.com
  - [CNAME](##dns)
  - You cannot create a CNAME record for the top node of the DNS namespace, so this option is incorrect.

## Question 36
- A company recently experienced a database outage in its on-premises data center. 
- The company now wants to migrate to a reliable database solution on AWS that minimizes data loss and stores every transaction on at least two nodes.

Which of the following solutions meets these requirements?

**Solution**
- Set up an Amazon RDS MySQL DB instance with **Multi-AZ** functionality enabled to **synchronously replicate** the data
  - [RDS_Multi_AZ](aws-ass-solution-architect.md#rds_multi_az)
**Wrong**
- Set up an Amazon EC2 instance with a MySQL DB engine installed that triggers an AWS Lambda function to *synchronously* replicate the data to an Amazon RDS MySQL DB instance
  - [RDS_Read_Replica](aws-ass-solution-architect.md#rds_read_replicas)
- Set up an Amazon RDS MySQL DB instance and then create a read replica in another Availability Zone that *synchronously* replicates the data
- Set up an Amazon RDS MySQL DB instance and then create a read replica in a separate AWS Region that *synchronously* replicates the data
  - read replica sysnchorouly relicated the data - Trap

## Question 37
- The engineering team at a company wants to use Amazon Simple Queue Service (Amazon SQS) to decouple components of the underlying application architecture.
- However, the team is concerned about the VPC-bound components accessing Amazon Simple Queue Service (Amazon SQS) over the public internet.

As a solutions architect, which of the following solutions would you recommend to address this use-case?

**Solution**

- Use VPC endpoint to access Amazon SQS
  - [VPC Enpoint](aws-ass-solution-architect.md#vpc_endpoint)
**Wrong**
- Use Internet Gateway to access Amazon SQS
  - [Internet Gateway](aws-ass-solution-architect.md#vpc_internet_gateway)
- Use Network Address Translation (NAT) instance to access Amazon SQS
  - [NAT](aws-ass-solution-architect.md#vpc_nat_gateway)
- Use VPN connection to access Amazon SQS
  - [VPC](aws-ass-solution-architect.md#aws_site_to_site_vpn)

## Question 38
A retail company has connected its on-premises data center to the AWS Cloud via AWS Direct Connect.
The company wants to be able to resolve Domain Name System (DNS) queries for any resources in the on-premises network from the AWS VPC and also resolve any DNS queries for resources in the AWS VPC from the on-premises network.

As a solutions architect, which of the following solutions can be combined to address the given use case? (Select two)
**Solution**
- Create an *inbound endpoint* on Amazon Route 53 Resolver and then Amazon Route 53 Resolver can conditionally forward queries to resolvers on the on-premises network via this endpoint
- Create an *outbound endpoint* on Amazon Route 53 Resolver and then Amazon Route 53 Resolver can conditionally forward queries to resolvers on the on-premises network via this endpoint
    - [DNS](aws-ass-solution-architect.md#router_53_resolver) 
**Wrong**
- Create an *outbound endpoint* on Amazon Route 53 Resolver and then DNS resolvers on the on-premises network can forward DNS queries to Amazon Route 53 Resolver via this endpoint


- Create a *universal endpoint* on Amazon Route 53 Resolver and then Amazon Route 53 Resolver can receive and forward queries to resolvers on the on-premises network via this endpoint
- Create an *inbound endpoint* on Amazon Route 53 Resolver and then DNS resolvers on the on-premises network can forward DNS queries to Amazon Route 53 Resolver via this endpoint

## Question 39
Skipped
- A company has hired you to help with redesigning a real-time data processor. 
- The company wants to build custom applications that process and analyze the streaming data for its specialized needs.

Which solution will you recommend to address this use-case?

**Sollution**
- Use [Amazon Kinesis Data Streams](aws-ass-solution-architect.md#kinesis_data_stream) to process the data streams as well as *decouple the producers and consumers for the real-time data processor*

**Wrong**

- Use Amazon Simple Notification Service (Amazon SNS) to process the data streams as well as decouple the producers and consumers for the real-time data processor

- Use Amazon Simple Queue Service (Amazon SQS) to process the data streams as well as decouple the producers and consumers for the real-time data processor

- Use Amazon Kinesis Data Firehose to process the data streams as well as decouple the producers and consumers for the real-time data processor
  - [](aws-ass-solution-architect.md#firehose)
  - Kinesis Firehose cannot be used to process and analyze the streaming data in custom applications. It can capture, transform, and load streaming data into Amazon S3, Amazon Redshift, Amazon Elasticsearch Service, and Splunk, enabling near real-time analytics.

## Question 40
A retail organization is moving some of its on-premises data to AWS Cloud. The DevOps team at the organization has set up an AWS Managed IPSec VPN Connection between their remote on-premises network and their Amazon VPC over the internet.

Which of the following represents the correct configuration for the IPSec VPN Connection?

**Solution**
Create a virtual private gateway (VGW) on the AWS side of the VPN and a Customer Gateway on the on-premises side of the VPN
  - [VPC](aws-ass-solution-architect.md#aws_site_to_site_vpn)
**Wrong**
- Create a virtual private gateway (VGW) on the on-premises side of the VPN and a Customer Gateway on the AWS side of the VPN
- Create a virtual private gateway (VGW) on both the AWS side of the VPN as well as the on-premises side of the VPN
- Create a Customer Gateway on both the AWS side of the VPN as well as the on-premises side of the VPN

## Question 41
- A leading bank has moved its IT infrastructure to AWS Cloud and they have been using **Amazon EC2 Auto Scaling** for their web servers. 
- This has helped them deal with traffic spikes effectively. 
- But Their MySQL relational database has now become a bottleneck and they urgently need a fully managed auto scaling solution for their relational database to address any unpredictable changes in the traffic.

Can you identify the AWS service that is best suited for this use-case?
**Solution**
[Amazon Aurora Serverless](aws-ass-solution-architect.md#Aurora_Serverless)
  
**Wrong**
- [Amazon DynamoDB](aws-ass-solution-architect.md#dynamodb)
  - NoSql
- [Amazon Aurora](aws-ass-solution-architect.md#aurora)
  - But, its not a complete auto scaling solution and neither is it fully managed like Aurora serverless. Hence is not the right fit for the given use-case.
- [Amazon ElastiCache](aws-ass-solution-architect.md#elasticache)
  - Cachinglayer
## Question 42
- A gaming company uses Application Load Balancers in front of Amazon EC2 instances for different services and microservices.
- The architecture has now become complex with too many Application Load Balancers in multiple AWS Regions. Security updates, firewall configurations, and traffic routing logic have become complex with too many IP addresses and configurations.

The company is looking at an easy and effective way to bring down the number of IP addresses allowed by the firewall and easily manage the entire network infrastructure. Which of these options represents an appropriate solution for this requirement?

**Solution**
- Launch AWS Global Accelerator and create endpoints for all the Regions. Register the Application Load Balancers of each Region to the corresponding endpoints
  - [AWS Global Accelerator](aws-ass-solution-architect.md#aws_global_accelerator)
**Wrong**
- Assign an Elastic IP to an Auto Scaling Group (ASG), and set up multiple Amazon EC2 instances to run behind the Auto Scaling Groups, for each of the Regions
  - You cannot assign an *elastic IP address* to an Auto Scaling Group (ASG), since ASG just manages a collection of Amazon EC2 instances.
- Configure Elastic IPs for each of the Application Load Balancers in each Region
  - An Application Load Balancer cannot be assigned *an Elastic IP address (static IP address)*.
- Set up a Network Load Balancer with elastic IP address. Register the private IPs of all the Application Load Balancers as targets of this Network Load Balancer
  - A Network Load Balancer can be configured to take an *Elastic IP address*. However, with hundreds of Application Load Balancers and Network Load Balancers, the solution will be equally cumbersome to manage.

## Question 43
- A developer has configured inbound traffic for the relevant ports in both the *Security Group* of the Amazon EC2 instance as well as the *Network Access Control List (Network ACL)* of the subnet for the Amazon EC2 instance. 
- The developer is, however, unable to connect to the service running on the Amazon EC2 instance.

As a solutions architect, how will you fix this issue?
**Solution**
Security Groups are stateful, so allowing inbound traffic to the necessary ports enables the connection. Network ACLs are , so you must allow both inbound and outbound traffic
  - [Network ACLs](aws-ass-solution-architect.md#network_acl)
**Wrong**
Rules associated with Network ACLs should never be modified from command line. An attempt to modify rules from command line blocks the rule and results in an erratic behavior

IAM Role defined in the Security Group is different from the IAM Role that is given access in the Network ACLs

Network ACLs are stateful, so allowing inbound traffic to the necessary ports enables the connection. Security Groups are 60, so you must allow both inbound and outbound traffic

## Question 44
Skipped
- A media company has its corporate headquarters in `Los Angeles` with an on-premises data center using an *AWS Direct Connect* connection to the AWS VPC. 
The branch offices in San `Francisco` and `Miami` use *AWS Site-to-Site VPN* connections to connect to the AWS VPC. 
The company is looking for a solution to have the branch offices send and receive data with each other as well as with their corporate headquarters.

As a solutions architect, which of the following AWS services would you recommend addressing this use-case?

**Solution**
AWS VPN CloudHub
**Wrong**
- Software VPN
  - Amazon VPC offers you the flexibility to fully manage both sides of your Amazon VPC connectivity by creating a VPN connection between your remote network and a software VPN appliance running in your Amazon VPC network. Since Software VPN just handles connectivity between the remote network and Amazon VPC, therefore it cannot be used to send and receive data between the remote branch offices of the company.

- [VPC Peering connection](aws-ass-solution-architect.md#vpc_peering)
- VPC Endpoint
  - [VPC Endpoint](aws-ass-solution-architect.md#vpc_endpoint)


## Question 45
Skipped
A global pharmaceutical company wants to move most of the on-premises data into Amazon S3, Amazon Elastic File System (Amazon EFS), and Amazon FSx for Windows File Server easily, quickly, and cost-effectively.

As a solutions architect, which of the following solutions would you recommend as the BEST fit to automate and accelerate *online data transfers* to these AWS storage services?

**Solution**
- Use AWS DataSync to automate and accelerate online data transfers to the given AWS storage services
  - [](aws-ass-solution-architect.md#aws_datasync)
- Use AWS Transfer Family to automate and accelerate online data transfers to the given AWS storage services
  -  Amazon S3 and Amazon EFS. Therefore, it cannot support migration into the other AWS storage services mentioned in the given use-case (Amazon FSx for Windows File Server).
- Use AWS Snowball Edge Storage Optimized device to automate and accelerate online data transfers to the given AWS storage services
  - Offline
- Use File Gateway to automate and accelerate online data transfers to the given AWS storage services
  - S3
  - Therefore, it cannot support migration into the other AWS storage services mentioned in the given use-case (Amazon FSx for Windows File Server).

## 46
- A company has a hybrid cloud structure for its on-premises data center and AWS Cloud infrastructure. 
- The company wants to build a web log archival solution such that only the most frequently accessed logs are available as cached data locally while backing up all logs on Amazon S3.

As a solutions architect, which of the following solutions would you recommend for this use-case?

**Solution**
Use AWS Volume Gateway - Cached Volume - to store the most frequently accessed logs locally for low-latency access while storing the full volume with all logs in its Amazon S3 service bucket
  -[Volumne Gate Way](aws-ass-solution-architect.md#Volume_Gateway)

**Wrong**
Use AWS Direct Connect to store the most frequently accessed logs locally for low-latency access while storing the full backup of logs in an Amazon S3 bucket
  - AWS Direct connect cannot be used to store the most frequently accessed logs locally for low-latency access.

- Use AWS Snowball Edge Storage Optimized device to store the most frequently accessed logs locally for low-latency access while storing the full backup of logs in an Amazon S3 bucket
  - Offline

Use AWS Volume Gateway - Stored Volume - to store the most frequently accessed logs locally for low-latency access while storing the full volume with all logs in its Amazon S3 service bucket

## 47
- The engineering team at a company is moving the static content from the company's logistics website hosted on Amazon EC2 instances to an Amazon S3 bucket. 
- The team wants to use an Amazon CloudFront distribution to deliver the static content. The security group used by the Amazon EC2 instances allows the website to be accessed by a limited set of IP ranges from the company's suppliers. 
- Post-migration to Amazon CloudFront, access to the static content should only be allowed from the aforementioned IP addresses.

Which options would you combine to build a solution to meet these requirements? (Select two)
**Solution**
- *Create an AWS WAF ACL and use an IP match condition to allow traffic only from those IPs that are allowed in the Amazon EC2 security group. Associate this new AWS WAF ACL with the Amazon CloudFront distribution*
  - AWS WAF is a web application firewall that lets you monitor the HTTP and HTTPS requests that are forwarded to your protected web application resources. You can protect the following resource types:
    - Amazon CloudFront distribution
    - Amazon API Gateway REST API
    - Application Load Balancer
    - AWS AppSync GraphQL API
    - Amazon Cognito user pool
  - AWS WAF also lets you control access to your content. Based on conditions that you specify, such as the IP addresses that requests originate from or the values of query strings, your protected resource responds to requests either with the requested content, with an HTTP 403 status code (Forbidden), or with a custom response.
  - If you want to allow or block web requests based on the IP addresses that the requests originate from, create one or more IP match conditions via your AWS WAF. An IP match condition lists up to 10,000 IP addresses or IP address ranges that your requests originate from.

For the given use case, you should add those IP addresses that are allowed in the Amazon EC2 security group into the IP match condition.
- *Configure an origin access identity (OAI) and associate it with the Amazon CloudFront distribution. Set up the permissions in the Amazon S3 bucket policy so that only the OAI can read the objects*
  - When you use Amazon CloudFront with an Amazon S3 bucket as the origin, you can configure Amazon CloudFront and Amazon S3 in a way that provides the following benefits:
  - Restricts access to the Amazon S3 bucket so that it's not publicly accessible
  - Makes sure that viewers (users) can access the content in the bucket only through the specified Amazon CloudFront distribution—that is, prevents them from accessing the content directly from the bucket, or through an unintended CloudFront distribution.
  - To do this, configure Amazon CloudFront to send authenticated requests to Amazon S3, and configure Amazon S3 to only allow access to authenticated requests from Amazon CloudFront.
  - Amazon CloudFront provides two ways to send authenticated requests to an Amazon S3 origin: origin access control (OAC) and origin access identity (OAI).
  - Exam Alert:
    - Please note that AWS recommends using OAC because it supports:
    - All Amazon S3 buckets in all AWS Regions, including opt-in Regions launched after December 2022
    - Amazon S3 server-side encryption with AWS KMS (SSE-KMS)
    - Dynamic requests (POST, PUT, etc.) to Amazon S3
    - OAI doesn't work for the scenarios in the preceding list, or it requires extra workarounds in those scenarios. However, you will continue to see answers enlisting OAI as the preferred option in the actual exam as it takes about 6 months/1 year for a new feature to appear in the exam.

**Wrong**
- Create a new NACL that allows traffic from the same IPs as specified in the current Amazon EC2 security group. Associate this new NACL with the Amazon CloudFront distribution
  - NACL is associated with a subnet within a VPC. Amazon CloudFront delivers your content through a worldwide network of data centers called edge locations. So a NACL cannot be associated with a Amazon CloudFront distribution.
- Create an AWS Web Application Firewall (AWS WAF) ACL and use an IP match condition to allow traffic only from those IPs that are allowed in the Amazon EC2 security group. Associate this new AWS WAF ACL with the Amazon S3 bucket policy
  - You cannot associate an AWS WAF ACL with an Amazon S3 bucket policy.
- Create a new security group that allows traffic from the same IPs as specified in the current Amazon EC2 security group. Associate this new security group with the Amazon CloudFront distribution
  - Amazon CloudFront delivers your content through a worldwide network of data centers called edge locations. So a security group cannot be associated with Amazon CloudFront distribution.
## Question 48
- A media startup is looking at hosting their web application on AWS Cloud. 
- The application will be accessed by users from different geographic regions of the world to upload and download video files that can reach a maximum size of 10 gigabytes. 
- The startup wants the solution to be cost-effective and scalable with the lowest possible latency for a great user experience.

As a Solutions Architect, which of the following will you suggest as an optimal solution to meet the given requirements?

**Solution**
- Use Amazon S3 for hosting the web application and use Amazon S3 Transfer Acceleration (Amazon S3TA) to reduce the latency that geographically dispersed users might face
  - [S3TA](aws-ass-solution-architect.md#s3-transfer-accelerations3ta)
**Wrong**
- Use Amazon S3 for hosting the web application and use Amazon CloudFront for faster distribution of content to geographically dispersed users
  - The given use case has data larger than 1GB and hence S3 Transfer Acceleration is a better option.
- Use Amazon EC2 with Amazon ElastiCache for faster distribution of content, while Amazon S3 can be used as a storage service

- Use Amazon EC2 with AWS Global Accelerator for faster distribution of content, while using Amazon S3 as storage service

## 49
Which of the following AWS services provides a highly available and fault-tolerant solution to capture the clickstream events from the source and then provide a concurrent feed of the data stream to the downstream applications?
**Solution**
- [Amazon Kinesis Data Streams](aws-ass-solution-architect.md#kinesis_data_stream)
  
**Wrong**

- [Amazon Simple Queue Service (Amazon SQS)](aws-ass-solution-architect.md#sqs)
- [Amazon Kinesis Data Firehose](aws-ass-solution-architect.md#firehose)
  -  As Kinesis Data Firehose is used to load streaming data into data stores, therefore this option is incorrect.
- [Amazon Kinesis Data Analytics](aws-ass-solution-architect.md#Kinesis_Data_Analytics)
  - As Kinesis Data Analytics is used to build SQL queries and sophisticated Java applications, therefore this option is incorrect.

## 50 
- A company has its application servers in the public subnet that connect to the Amazon RDS instances in the private subnet. 
- For regular maintenance, the Amazon RDS instances need patch fixes that need to be downloaded from the internet.

Considering the company uses only IPv4 addressing and is looking for a fully managed service, which of the following would you suggest as an optimal solution?

**Solution**
- Configure a Network Address Translation gateway (NAT gateway) in the public subnet of the VPC
  - [NAT](aws-ass-solution-architect.md#vpc_nat_gateway)
**Wrong**
- Configure a Network Address Translation instance (NAT instance) in the public subnet of the VPC
  - NAT intance is manage by customer
- Configure an Egress-only internet gateway for the resources in the private subnet of the VPC
  - It is IP4
- Configure the Internet Gateway of the VPC to be accessible to the private subnet resources by changing the route tables
  - Internet Gateway cannot be used directly with a private subnet. It is not possible to set up this configuration, without a NAT instance or a NAT gateway in the public subnet.

## 51
A DevOps engineer at an IT company just upgraded an Amazon EC2 instance type from t2.nano (0.5G of RAM, 1 vCPU) to u-12tb1.metal (12.3 TB of RAM, 448 vCPUs). How would you categorize this upgrade?

**Solution**
This is a scale up example of vertical scalability

**Wrong**
This is an example of high availability
This is a scale out example of vertical scalability
This is a scale up example of horizontal scalability

## 52
- The database backend for a retail company's website is hosted on Amazon RDS for MySQL having a primary instance and three read replicas to support read scalability. 
- The company has mandated that the *read replicas should lag no more than 1 second* behind the primary instance to provide the best possible user experience. 
- The read replicas are falling further behind during periods of peak traffic spikes, resulting in a bad user experience as the searches produce inconsistent results.

How to reduce the replication lag as much as possible with minimal changes to the application code or the effort required to manage the underlying resources.

Which of the following will you recommend?
**Solution**
Set up database migration from Amazon RDS MySQL to Amazon Aurora MySQL. Swap out the MySQL read replicas with Aurora Replicas. Configure Aurora Auto Scaling
  - [Aurora](aws-ass-solution-architect.md#aurora)
  - Since Amazon Aurora Replicas share the same data volume as the primary instance in the same AWS Region, there is virtually no replication lag. The replica lag times are in the 10s of milliseconds (compared to the replication lag of seconds in the case of MySQL read replicas). Therefore, this is the right option to ensure that the read replicas lag no more than 1 second behind the primary instance.
**Wrong**
- Set up database migration from Amazon RDS MySQL to *Amazon DynamoDB*. Provision a large number of read capacity units (RCUs) to support the required throughput and enable Auto-Scaling
  - This is no SQL
- Set up an *Amazon ElastiCache* for Redis cluster in front of the MySQL database. Update the website to check the cache before querying the read replicas
  - Introducing a caching layer would result in significant changes to the application code, so this option is incorrect.
- Host the MySQL primary database on a memory-optimized Amazon EC2 instance. Spin up additional compute-optimized Amazon EC2 instances to host the read replicas
  - Amazon EC2 instances would result in significant overhead to manage the underlying resources such as OS patching, database patching, etc. So this option is incorrect.

## Question 53
- A leading news aggregation company offers hundreds of digital products and services for customers ranging from law firms to banks to consumers. 
- The company bills its clients based on per unit of *clickstream* data provided to the clients. 
- As the company operates in a regulated industry, it needs to have the same ordered clickstream data available for auditing within a window of 7 days.

As a solutions architect, which of the following AWS services provides the ability to run the billing process and auditing process on the given clickstream data in the same order?

**Solution**
- Amazon Kinesis Data Streams
  - [kinesis_data_stream](aws-ass-solution-architect.md#kinesis_data_stream)
**Wrong**
- Amazon Simple Queue Service (SQS)
  - [SQS](aws-ass-solution-architect.md#sqs)
  - For Amazon SQS, you cannot have the same message being consumed by multiple consumers in the same order a few hours later, therefore this option is incorrect.
- [Amazon Kinesis Data Analytics](aws-ass-solution-architect.md#kinesis_data_analytics)
  
- Amazon Kinesis Data Firehose
  - [Firehose](aws-ass-solution-architect.md#firehose)
  - As Amazon Kinesis Data Firehose is used to load streaming data into data stores , therefore this option is incorrect.

## Question 54
- A leading online gaming company is migrating its flagship application to AWS Cloud for delivering its online games to users across the world.
- The company would like to use a Network Load Balancer to handle millions of requests per second. 
- The engineering team has provisioned multiple instances in a *public subnet* and specified these instance IDs as the targets for the NLB.

As a solutions architect, can you help the engineering team understand the correct routing mechanism for these target instances?

**Solution**
- Traffic is routed to instances using the *primary private IP address* specified in the primary network interface for the instance
  - [NLB_Request_Routing_and_IP_Addresses](aws-ass-solution-architect.md#nlb_request_routing_and_ip_addresses)

**Wrong**
- Traffic is routed to instances using the *primary public IP address specified* in the primary network interface for the instance

- Traffic is routed to instances using *the instance ID specified in the primary network interface* for the instance
  -  - You cannot use instance ID to route traffic to the instance. 
- Traffic is routed to instances using the *primary elastic IP address specified* in the primary network interface for the instance

## 55 Question 55
The DevOps team at an IT company is provisioning a two-tier application in a VPC with a public subnet and a private subnet. The team wants to use either a Network Address Translation (NAT) instance or a Network Address Translation (NAT) gateway in the public subnet to enable instances in the private subnet to initiate outbound IPv4 traffic to the internet but needs some technical assistance in terms of the configuration options available for the Network Address Translation (NAT) instance and the Network Address Translation (NAT) gateway.

As a solutions architect, which of the following options would you identify as CORRECT? (Select three)

**Solution**
- NAT instance can be used as a bastion server
- Security Groups can be associated with a NAT gateway
- NAT instance supports port forwarding

**Explain**
- [NAT instance](aws-ass-solution-architect.md#vpc_nat_instance)
- [Nat Gateway]()
- A *NAT instance* or a *NAT Gateway* can be used in a public subnet in your VPC to enable instances in the private subnet to initiate outbound IPv4 traffic to the Internet.
**Wrong**
NAT gateway can be used as a bastion server
NAT gateway supports port forwarding
Security Groups can be associated with a NAT gateway

## Question 56
- An IT training company hosted its website on Amazon S3 a couple of years ago. 
- Due to COVID-19 related travel restrictions, the training website has suddenly gained traction. 
- With an almost 300% increase in the requests served per day, the company's AWS costs have sky-rocketed for just the Amazon S3 outbound data costs.

As a Solutions Architect, can you suggest an alternate method to reduce costs while keeping the latency low?
**Solution**
- Configure Amazon CloudFront to distribute the data hosted on Amazon S3 cost-effectively
  - [CloudFront](aws-ass-solution-architect.md#cloudfront) 
  - By design, delivering data out of Amazon CloudFront can be more cost-effective than delivering it from Amazon S3 directly to your users.
  - Also, data transfer out for content by using CloudFront is often more cost-effective than serving files directly from Amazon S3, and there is no data transfer fee from Amazon S3 to CloudFront. You only pay for what is delivered to the internet from Amazon CloudFront, plus request fees.
**Wrong**

- To reduce Amazon S3 cost, the data can be saved on an Amazon EBS volume connected to an Amazon EC2 instance that can host the application
  - Amazon EBS volumes are fast and are relatively cheap (though Amazon S3 is still a cheaper alternative). But, Amazon EBS volumes are accessible only through Amazon EC2 instances and are bound to a specific region
- Configure Amazon S3 Batch Operations to read data in bulk at one go, to reduce the number of calls made to Amazon S3 buckets
  -  This statement is incorrect and given only as a distractor. You can use Amazon S3 Batch Operations to perform large-scale batch operations on Amazon S3 objects, and it has nothing to do with content distribution.
- Use Amazon EFS service, as it provides a shared, scalable, fully managed elastic NFS file system for storing AWS Cloud or on-premises data
  - Amazon EFS is a shareable file system that can be mounted onto Amazon EC2 instances. Amazon EFS is costlier than Amazon EBS and not a solution if the company is looking at reducing costs.

## 57
The engineering team at an e-commerce company wants to migrate from Amazon Simple Queue Service (Amazon SQS) Standard queues to FIFO (First-In-First-Out) queues with batching.

As a solutions architect, which of the following steps would you have in the migration checklist? (Select three)

**Solution**
- Make sure that the throughput for the target FIFO (First-In-First-Out) queue does not exceed 3,000 messages per second
- Make sure that the name of the FIFO (First-In-First-Out) queue ends with the .fifo suffix
- Delete the existing standard queue and recreate it as a FIFO (First-In-First-Out) queue
  - [SQS](aws-ass-solution-architect.md#sqs)
**Wrong**
- Convert the existing standard queue into a FIFO (First-In-First-Out) queue
- Make sure that the name of the FIFO (First-In-First-Out) queue is the same as the standard queue
- Make sure that the throughput for the target FIFO (First-In-First-Out) queue does not exceed 300 messages per second

## Question 58
A small business has been running its IT systems on the on-premises infrastructure but the business now plans to migrate to AWS Cloud for operational efficiencies.

As a Solutions Architect, can you suggest a cost-effective serverless solution for its flagship application that has both static and dynamic content?

**Solution**
- Host the static content on Amazon S3 and use AWS Lambda with Amazon DynamoDB for the serverless web application that handles dynamic content. Amazon CloudFront will sit in front of AWS Lambda for distribution across diverse regions

**Wrong**
- Host both the static and dynamic content of the web application on Amazon EC2 with Amazon RDS as database. Amazon CloudFront should be configured to distribute the content across geographically disperse regions

- Host the static content on Amazon S3 and use Amazon EC2 with Amazon RDS for generating the dynamic content. Amazon CloudFront can be configured in front of Amazon EC2 instance, to make global distribution easy
- Host both the static and dynamic content of the web application on Amazon S3 and use Amazon CloudFront for distribution across diverse regions/countries

## Question 59
A financial services company is migrating their messaging queues from self-managed message-oriented middleware systems to Amazon Simple Queue Service (Amazon SQS). 
The development team at the company wants to *minimize the costs* of using Amazon SQS.

As a solutions architect, which of the following options would you recommend for the given use-case?
**Solution**
- Use SQS long polling to retrieve messages from your Amazon SQS queues
  - [long polling](aws-ass-solution-architect.md#long_polling)
**Wrong**

- Use SQS short polling to retrieve messages from your Amazon SQS queues
- Use SQS message timer to retrieve messages from your Amazon SQS queues
- Use SQS visibility timeout to retrieve messages from your Amazon SQS queues

## 60 
- A healthcare company has deployed its web application on Amazon Elastic Container Service (Amazon ECS) container instances running behind an Application Load Balancer.
- The website slows down when the traffic spikes and the website availability is also reduced. 
- The development team has configured Amazon CloudWatch alarms to receive notifications whenever there is an availability constraint so the team can scale out resources. 
- The company wants an automated solution to respond to such events.

Which of the following addresses the given use case?

**Solution**
- Configure AWS Auto Scaling to scale out the Amazon ECS cluster when the ECS service's CPU utilization rises above a threshold
  - You use the Amazon ECS first-run wizard to create a cluster and a service that runs behind an Elastic Load Balancing load balancer. Then you can configure a target tracking scaling policy that scales your service automatically based on the current application load as measured by the service's CPU utilization (from the ECS, ClusterName, and ServiceName category in CloudWatch).

  - When the average CPU utilization of your service rises above 75% (meaning that more than 75% of the CPU that is reserved for the service is being used), a scale out alarm triggers Service Auto Scaling to add another task to your service to help out with the increased load. Conversely, when the average CPU utilization of your service drops below the target utilization for a sustained period, a scale-in alarm triggers a decrease in the service's desired count to free up those cluster resources for other tasks and services.
**Wrong**
- Configure AWS Auto Scaling to scale out the Amazon ECS cluster when the Application Load Balancer's CPU utilization rises above a threshold
- Configure AWS Auto Scaling to scale out the Amazon ECS cluster when the CloudWatch alarm's CPU utilization rises above a threshold
- Configure AWS Auto Scaling to scale out the Amazon ECS cluster when the Application Load Balancer's target group's CPU utilization rises above a threshold

## 61
A media company wants a low-latency way to distribute live sports results which are delivered via a proprietary application using UDP protocol.

As a solutions architect, which of the following solutions would you recommend such that it offers the BEST performance for this use case?

**Solution**

Use AWS Global Accelerator to provide a low latency way to distribute live sports results
  - [AWS_Global_Accelerator](aws-ass-solution-architect.md#AWS_Global_Accelerator)
**Wrong**
Use Auto Scaling group to provide a low latency way to distribute live sports results
Use Elastic Load Balancing (ELB) to provide a low latency way to distribute live sports results
Use Amazon CloudFront to provide a low latency way to distribute live sports results

*Please note the differences between the capabilities of AWS Global Accelerator and Amazon CloudFront*
- AWS Global Accelerator and Amazon CloudFront are separate services that use the AWS global network and its edge locations around the world. Amazon CloudFront improves performance for both cacheable content (such as images and videos) and dynamic content (such as API acceleration and dynamic site delivery). AWS Global Accelerator improves performance for a wide range of applications over TCP or UDP by proxying packets at the edge to applications running in one or more AWS Regions.

- AWS Global Accelerator is a good fit for non-HTTP use cases, such as gaming (UDP), IoT (MQTT), or Voice over IP, as well as for HTTP use cases that specifically require static IP addresses or deterministic, fast regional failover. Both services integrate with AWS Shield for DDoS protection.

## 62
An IT company is looking to move its on-premises infrastructure to AWS Cloud. The company has a portfolio of applications with a few of them using server bound licenses that are valid for the next year. To utilize the licenses, the CTO wants to use dedicated hosts for a one year term and then migrate the given instances to default tenancy thereafter.

As a solutions architect, which of the following options would you identify as CORRECT for changing the tenancy of an instance after you have launched it? (Select two)

**Solution**

- You can change the tenancy of an instance from dedicated to host
- You can change the tenancy of an instance from host to dedicated
- [Tenancy_Value](aws-ass-solution-architect.md#tenancy_value)

**Wrong**
- You can change the tenancy of an instance from default to dedicated
- You can change the tenancy of an instance from dedicated to default
- You can change the tenancy of an instance from default to host


## 63
- A legacy application is built using a tightly-coupled monolithic architecture.
- Due to a sharp increase in the number of users, the application performance has degraded.
-  The company now wants to decouple the architecture and adopt AWS microservices architecture. 
-  Some of these microservices need to handle fast running processes whereas other microservices need to handle slower processes.

Which of these options would you identify as the right way of connecting these microservices?

**Solution**
- Configure Amazon Simple Queue Service (Amazon SQS) queue to decouple microservices running faster processes from the microservices running slower ones
**Wrong**
- Use Amazon Simple Notification Service (Amazon SNS) to decouple microservices running faster processes from the microservices running slower ones
- Add Amazon [EventBridge](aws-ass-solution-architect.md#event_bridge) to decouple the complex architecture
- Configure Amazon Kinesis Data Streams to decouple microservices running faster processes from the microservices running slower ones

## 64
The development team at a retail company wants to optimize the cost of Amazon EC2 instances. The team wants to move certain nightly batch jobs to spot instances. The team has hired you as a solutions architect to provide the initial guidance.

Which of the following would you identify as CORRECT regarding the capabilities of spot instances? (Select three)

**Solution**
- If a spot request is persistent, then it is opened again after your Spot Instance is interrupted
  - [Spot Instance](aws-ass-solution-architect.md#ec2_spot_instances)
- Spot Fleets can maintain target capacity by launching replacement instances after Spot Instances in the fleet are terminated
- When you cancel an active spot request, it terminates the associated instance as well
**Wrong**


- Spot Fleets cannot maintain target capacity by launching replacement instances after Spot Instances in the fleet are terminated
- When you cancel an active spot request, it does not terminate the associated instance
- If a spot request is persistent, then it is opened again after you stop the Spot Instance

## 65
A big data analytics company is working on a real-time vehicle tracking solution. The data processing workflow involves both I/O intensive and throughput intensive database workloads. 
The development team needs to store this real-time data in a NoSQL database hosted on an Amazon EC2 instance and needs to support up to 25,000 IOPS per volume.

As a solutions architect, which of the following Amazon Elastic Block Store (Amazon EBS) volume types would you recommend for this use-case?

**Solution**
- Provisioned IOPS SSD (io1)
  - Provisioned IOPS SSD (io1) is backed by solid-state drives (SSDs) and is a high-performance Amazon EBS storage option designed for critical, I/O intensive database and application workloads, as well as throughput-intensive database workloads. io1 is designed to deliver a consistent baseline performance of up to 50 IOPS/GB to a maximum of 64,000 IOPS and provide up to 1,000 MB/s of throughput per volume. Therefore, the io1 volume type would be able to meet the requirement of 25,000 IOPS per volume for the given use-case.
**Faild**

- Cold HDD (sc1)
  -  sc1 is backed by hard disk drives (HDDs). It is ideal for less frequently accessed workloads with large, cold datasets. It supports max IOPS/Volume of 250.
- General Purpose SSD (gp2)
  - gp2 is backed by solid-state drives (SSDs) and is suitable for a broad range of transactional workloads, including dev/test environments, low-latency interactive applications, and boot volumes. It supports max IOPS/Volume of 16,000.
- Throughput Optimized HDD (st1)
  - st1 is backed by hard disk drives (HDDs) and is ideal for frequently accessed, throughput-intensive workloads with large datasets and large I/O sizes, such as MapReduce, Kafka, log processing, data warehouse, and ETL workloads. It supports max IOPS/Volume of 500.