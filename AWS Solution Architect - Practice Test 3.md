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