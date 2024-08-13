# Practice Test 2  
  
## 1  EC2
- A company is looking at storing their *less frequently accessed files on AWS* that can be *concurrently accessed by hundreds of EC2s*.  
- The company needs the most **cost-effective file storage service** that provides immediate access to data whenever needed.  
  
~~Solution~~  
- *Amazon Elastic File System (EFS) Standard–IA storage class*  
- [EFS Standard–IA](aws-ass-solution-architect.md#Efs_Standard_Ia)  
~~Wrong~~  
- *Amazon S3 Standard-Infrequent Access (S3 Standard-IA) storage class*  
- ~~Object Storage Service~~  
- *Amazon Elastic Block Store (EBS)*  
- ~~Block-level Storage service~~ use with **EC2**  
- *Amazon Elastic File System (EFS) Standard storage class*  
- ~~For frequently accessed files~~.  
- The company is also looking at cutting costs by optimally storing the infrequently accessed data  
  
## 2 - Practice with IAM Role  
- `s3:ListBucket` is applied to buckets, so the ARN is in the form `"Resource":"arn:aws:s3:::mybucket"`, without a trailing `/`  
- `s3:GetObject` is applied to objects within the bucket, so the ARN is in the form `"Resource":"arn:aws:s3:::mybucket/*"`, with a trailing `/*` to indicate all objects within the bucket mybucket  
  
**Wrong**  
```json  
{  
"Version":"2012-10-17",  
"Statement":[  
{  
"Effect":"Allow",  
"Action":[  
"s3:ListBucket",  
"s3:GetObject"  
],  
"Resource":"arn:aws:s3:::mybucket"  
}  
]  
}  
```  
-> This option is incorrect as it provides read-only access only to the bucket, not its contents.  
  
```json  
{  
"Version":"2012-10-17",  
"Statement":[  
{  
"Effect":"Allow",  
"Action":[  
"s3:ListBucket",  
"s3:GetObject"  
],  
"Resource":"arn:aws:s3:::mybucket/*"  
}  
]  
}  
```  
-> This option is incorrect as it provides read-only access only to the objects within the bucket and it does not provide listBucket permissions to the bucket itself.  
  
```json  
{  
"Version":"2012-10-17",  
"Statement":[  
{  
"Effect":"Allow",  
"Action":[  
"s3:ListBucket"  
],  
"Resource":"arn:aws:s3:::mybucket/*"  
},  
{  
"Effect":"Allow",  
"Action":[  
"s3:GetObject"  
],  
"Resource":"arn:aws:s3:::mybucket"  
}  
]  
}  
```  
This option is incorrect as it provides listing access only to the bucket contents.  
  
- [https://aws.amazon.com/blogs/security/writing-iam-policies-how-to-grant-access-to-an-amazon-s3-bucket/](https://aws.amazon.com/blogs/security/writing-iam-policies-how-to-grant-access-to-an-amazon-s3-bucket/)  
- [https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html)  
  
## 3 - Cognito  
- authentication/authorization mechanisms that AWS offers to authorize an API call within the Amazon API Gateway.  
- The company would prefer a solution that offers built-in user management.  
  
**Solution**  
- [Cognito User Pools](aws-ass-solution-architect.md#Cognito_User_Pools)  
  
**Wrong**  
- [AWS_IAM authorization](aws-ass-solution-architect.md#AWS_IAM_Authorization)  
- *Use AWS Lambda authorizer for Amazon API Gateway*  
- If you have an existing Identity Provider (IdP), you can use an AWS Lambda authorizer for Amazon API Gateway to invoke a Lambda function to authenticate/validate a given user against your Identity Provider. You can use a Lambda authorizer for custom validation logic based on identity metadata.  
- A Lambda authorizer can send additional information derived from a bearer token or request context values to your backend service. For example, the authorizer can return a map containing user IDs, user names, and scope. By using Lambda authorizers, your backend does not need to map authorization tokens to user-centric data, allowing you to limit the exposure of such information to just the authorization function.  
- When using Lambda authorizers, AWS strictly advises against passing credentials or any sort of sensitive data via query string parameters or headers, so this is not as secure as using Amazon Cognito User Pools.  
- *Use Amazon Cognito Identity Pools*  
- identity pools aren't an authentication mechanism in themselves and hence aren't a choice for this use case.  
- [Cognito user identity](aws-ass-solution-architect.md#Cognito_User_Identity)  
  
## 4 - Amazon RDS MySQL  
- A company has recently launched a new mobile gaming application that the users are adopting rapidly.  
- The company uses Amazon RDS MySQL as the database.  
- The engineering team wants an urgent solution to this issue where the rapidly increasing workload might exceed the available database storage.  
  
**Solution**  
- *Enable storage auto-scaling for Amazon RDS MySQL* :  
  
**Wrong**  
*Migrate RDS MySQL database to Amazon Aurora which offers storage auto-scaling*  
- Although Aurora offers automatic storage scaling  
- involves significant systems administration effort to migrate from Amazon RDS MySQL to Aurora.  
  
*Migrate Amazon RDS MySQL database to Amazon DynamoDB*  
- Amazon DynamoDB is a NoSQL database  
  
*Create read replica for Amazon RDS MySQL*  
- Cannot help to automatically scale storage for the primary database.  
  
## 5 - Redshift  
- **Amazon Redshift cluster** writes data to an **Amazon S3 bucket** belonging to a different AWS account.  
- The files created in the Amazon S3 bucket using the UNLOAD command from the Redshift are not even accessible to the Amazon S3 bucket owner.  
**Solution**  
- By default, an Amazon S3 object is owned by the AWS account that uploaded it. So the Amazon S3 bucket owner will not implicitly have access to the objects written by the Amazon Redshift cluster  
- To get access to the data files, an AWS Identity and Access Management (IAM) role with cross-account permissions must run the UNLOAD command again. Follow these steps to set up the Amazon Redshift cluster with cross-account permissions to the bucket:  
1. From the **account of the Amazon S3 bucket**, create an IAM role (Bucket Role) with permissions to the bucket.  
2. From the **account of the Amazon Redshift cluster**, create another IAM role (Cluster Role) with permissions to assume the Bucket Role.  
3. Update the **Bucket Role** to grant bucket access and create a trust relationship with the **Cluster Role**.  
4. From the Amazon Redshift cluster, run the UNLOAD command using the Cluster Role and Bucket Role.  
  
## 6 - Log file  
- single log processing model for all the log files (consisting of system logs, application logs, database logs, etc)  
- can be processed in a serverless fashion and then durably stored for downstream analytics.  
- The company wants to use an AWS managed service that **automatically scales to match the throughput of the log data** and requires **no ongoing administration.**  
**Solution**  
- *Amazon Kinesis Data Firehose*  
- [Firehorse](aws-ass-solution-architect.md#firehose)  
  
**Wrong Answer**  
- *AWS Lambda*:  
- -> It cannot be used for production-grade serverless log analytics.  
- *Amazon EMR* [EMR](aws-ass-solution-architect.md#emr)  
- -> Using an Amazon EMR cluster would imply **managing the underlying infrastructure** so it’s ruled out.  
- *Amazon Kinesis Data Streams*: [Kinesis Data Stream](aws-ass-solution-architect.md#Kinesis_Data_Stream)  
- -> With Amazon Kinesis Data Streams, you can scale up to a sufficient number of **shards** (note, however, that you'll need to provision enough shards ahead of time). As it requires manual administration of shards, it's not the correct choice for the given use-case.  
  
## 7 - EC2 - MSSQL  
- A silicon valley based startup has a two-tier architecture using **Amazon EC2** instances for its flagship application.  
- web servers (**443**) - security group A, are in **public** subnets across two Availability Zones (AZs)  
- MSSQL based database instances (**1433**), - security group B, are in **2 private subnets** across two Availability Zones (AZs).  
  
**Solution**  
- For security group A: Add an inbound rule that allows traffic from all sources on port 443.  
- Add an outbound rule with the destination as security group B on port 1433  
- For security group B: Add an inbound rule that allows traffic only from security group A on port 1433  
  
## 8 - Amazon RDS Read Replicas  
  
**Solution**  
- *If the master database is encrypted, the read replicas are encrypted*  
- Database instance running with RDS encryption, data stored at rest in the underlying storage is encrypted, as are its automated backups, read replicas, and snapshots.  
- [Read Replicas](aws-ass-solution-architect.md#RDS_Read_Replicas)  
**Wrong**  
  
## 9  
- Share **sensitive accounting data** stored in an **Amazon RDS** with an external auditor.  
- The auditor has its own AWS account and needs its own copy of the database.  
  
**Solution**  
- Create an encrypted snapshot of the database, share the snapshot, and allow access **KMS encryption key**  
- You can share the AWS KMS key that was used to encrypt the snapshot with any accounts that you want to be able to access the snapshot.  
- You can share AWS KMS Key with another AWS account by adding the other account to the *AWS KMS key policy*.  
  
**Wrong**  
- Create a snapshot of the database in *Amazon S3* and assign an *IAM role* to the auditor to grant access to bucket  
- Amazon RDS stores the DB snapshots in the Amazon S3 bucket belonging to the same AWS region where the Amazon RDS instance is located  
- Amazon RDS stores these on your behalf and you do not have direct access to these snapshots in Amazon S3  
- -> it's not possible to grant access to the snapshot objects in Amazon S3.  
- *Export the database contents to text files -> Amazon S3, -> new IAM user for the auditor*  
- a lot of unnecessary work and is difficult to audit  
- *Set up a read replica of the database* and configure IAM standard database authentication to grant the auditor access  
- Creating Read Replicas for audit purposes is overkill.  
- The auditor needs to have their own copy of the database, which is not possible with replicas.  
  
## 10 - RDS unencrypted  
- Upon a security review of your AWS account, an AWS consultant has found that a few Amazon RDS databases are unencrypted.  
**Solution**  
- Steps  
1. Take a snapshot of the database  
2. copy it as an encrypted snapshot  
3. estore a database from the encrypted snapshot.  
4. Terminate the previous database  
- You can only enable encryption for an Amazon RDS DB instance when you create it, not after the DB instance is created. However, because you can encrypt a copy of an unencrypted DB snapshot, you can effectively add encryption to an unencrypted DB instance. That is, you can create a snapshot of your DB instance, and then create an encrypted copy of that snapshot. So this is the correct option.  
**Wrong**  
- *Replica* - If the master is not encrypted, the read replicas cannot be encrypted.  
  
- **Enable Multi-AZ for the database**, and make sure the standby instance is encrypted. Stop the main database to that the standby database kicks in, then disable Multi-AZ - Multi-AZ is to help with High Availability, not encryption.  
  
**Enable encryption on the Amazon RDS database using the AWS Console** - *no direct option* to encrypt an RDS DB using the AWS Console.  
  
## 11 - Linux File System
- Mount a *network file system* on *Linux instances*, 
- Files will be stored and accessed frequently -> infrequently. 
- -> What solution is the **MOST cost-effective**

**Solution**
- Amazon EFS Infrequent Access [](aws-ass-solution-architect.md#efs)
**Wrong**
- S3 Glacier Deep Archive
    -  *These are data archiving solutions and hence this option is incorrect.*
- Amazon Fsx for Lustre
    - *Better suited for distributed computing for HPC(expensive)*
- Amazone S3 Intelligent Tiering
    - object storage service,
## 12 - EBS Volumn Termination
Change the default configuration for Amazon EBS volume termination. 
By default, the root volume of EC2 for an EBS-backed AMI is deleted when the instance terminates.

**Solution**
- `DeleteOnTermination` to false
**Wrong**
- `DeleteOnTermination` to true
- `TerminateOnDelete`

## 13
- To improve the *performance* and *security* of the application, 
- CloudFront distribution with an ALB as the custom origin. 
- Also AWS WAFwith Amazon CloudFront distribution. 
- The security team at the company has noticed a surge in **malicious attacks** from a **specific IP address** to **steal sensitive data stored** on the EC2s.


**Solution**
- *Create an IP match condition in the AWS WAF to block the malicious IP address*
  - [WAF](aws-ass-solution-architect.md#WAF)
**Wrong**
- *Network AC*: are not associated with instances
- *Security Group*: only allow not deny
- *Create a ticket with AWS support* : Managing the security of your application is your responsibility, not that of AWS

## 14- Aurora Replica
- Application uses an Amazon Aurora Multi-AZ deploymentd
- Causing *high input/output (I/O)* and *adding latency to the write requests against the database*.

**Solution**
- Set up a read replica and modify the application to use the appropriate endpoint
    - [Aurora](aws-ass-solution-architect.md#aurora)
**Wrong**
- Provision another Amazon Aurora database and link it to the primary database as a read replica
- Activate read-through caching on the Amazon Aurora database
- Read from the Multi-AZ standby instance
  - You create a standby instance while setting up a Multi-AZ deployment for Amazon RDS and NOT for Aurora.

## 15 AWS Organizations 
- You have multiple AWS accounts within a single AWS Region managed by **AWS Organizations** 
- Ensure all EC2 in all these accounts can communicate privately. 
- Which of the following solutions provides the capability at the CHEAPEST cost?

**Solution**
- Create a **VPC** in an account and share one or more of its subnets with the other accounts using *Resource Access Manager*
    - [RAM](aws-ass-solution-architect.md#ram)
    - The correct solution is to share the subnet(s) within a VPC using RAM. 
    - This will allow all EC2s to be deployed in the same VPC (although from different accounts) and easily communicate with one another.

**Wrong**
- Create a **VPC peering connection** between all virtual private cloud (VPCs)
  - [VPC peering connection](aws-ass-solution-architect.md#vpc_peering)
- Create a **Private Link** between all the EC2s
  - [Private Link](aws-ass-solution-architect.md#private_link)
- Create an **AWS Transit Gateway** and link all the virtual private cloud (VPCs) in all the accounts together
    - [AWS Transit Gateway](aws-ass-solution-architect.md#aws_transit_gateway)
    - will work but will be an expensive solution

## 16
What does this IAM policy do?

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Mystery Policy",
      "Action": [
        "ec2:RunInstances"
      ],
      "Effect": "Allow",
      "Resource": "*",
      "Condition": {
        "IpAddress": {
          "aws:SourceIp": "34.50.31.0/24"
        }
      }
    }
  ]
}

```
  
**Answer**
*It allows starting an EC2 only when the IP where the call originates is within the 34.50.31.0/24 CIDR block*
    - AWS evaluates these policies when an IAM principal (user or role) makes a request
    - The `aws:SourceIP` in this condition always represents the IP of the caller of the API. That is very helpful if you want to restrict access to certain AWS API for example from the public IP of your on-premises infrastructure.
    - *IPs Type*
      - **elastic IP address (EIP)** - An elastic IP address (EIP) is a static IPv4 address designed for dynamic cloud computing. An Elastic IP address is associated with your AWS account. With an Elastic IP address, you can mask the failure of an instance or software by rapidly remapping the address to another instance in your account.
      - **Private IP address** - A private IPv4 address is an IP address that's not reachable over the Internet. You can use private IPv4 addresses for communication between instances in the same VPC.
      - **Public IP address** - A public IP address is an IPv4 address that's reachable from the Internet. You can use public addresses for communication between your instances and the Internet.

## 17 - EC2 Hibernate
- Machine Learning research group uses a proprietary computer vision application hosted on an EC2. 
- Every time the instance needs to be stopped and started again, the application takes about 3 minutes to start as some auxiliary software programs need to be executed so that the application can function. 
- The research group would like to minimize the application boostrap time whenever the system needs to be stopped and then started at a later point in time.
**Solution**
- Use Amazon  [EC2 Instance Hibernate](aws-ass-solution-architect.md#ec2_hibernate)

## 18 - Cert Renew
 - App on EC2 instances. 
 - Application handles sensitive customer data, the security team at the company wants to ensure that any SSL/TLS certificates configured on EC2s via the AWS Certificate Manager (ACM) are renewed before their expiry date. 
 - Notifies the security team 30 days before the certificate expiration. 
 - The solution should require the least amount of scripting and maintenance effort.

**Solution**
- Leverage AWS Config managed rule to check if any SSL/TLS certificates created via ACM are marked for expiration within 30 days. Configure the rule to trigger an Amazon SNS notification to the security team if any certificate expires within 30 days
  - [AWS_Certificate_Manager](aws-ass-solution-architect.md#aws_certificate_manager)
  - [AWS_Config](aws-ass-solution-architect.md#aws_config)
  - You can configure AWS Config to stream configuration changes and notifications to an Amazon SNS topic
**Wrong**
- *Monitor the days to expiry Amazon CloudWatch metric for certificates imported into ACM. Create a CloudWatch alarm to monitor such certificates based on the days to expiry metric and then trigger a custom action of notifying the security team*
  - Users can build alarms to monitor certificates based on days to expiry and also trigger custom actions such as calling a Lambda function or paging an administrator.

- Leverage AWS Config managed rule to check if any SSL/TLS certificates created via ACM are marked for expiration within 30 days. Configure the rule to trigger an Amazon SNS notification to the security team if any certificate expires within 30 days

- Monitor the days to expiry Amazon CloudWatch metric for certificates created via ACM. Create a CloudWatch alarm to monitor such certificates based on the days to expiry metric and then trigger a custom action of notifying the security team
**-> Any SSL/TLS certificates created via ACM do not need any monitoring/intervention for expiration. ACM automatically renews such certificates. Hence both these options are incorrect.**

## 19 - RDS For MySQL
- Uses **Amazon RDS for MySQL** but is running into performance issues despite using **Read Replicas**. 
- The company has branch offices across the world, and it needs the solution to work on a global scale.
Which of the following will you recommend as the MOST cost-effective and high-performance solution?

**Solution**
- *Use Amazon Aurora Global Database to enable fast local reads with low latency in each region*
  - You can use Amazon S3 to host a static website. On a static website, individual web pages include static content. They might also contain client-side scripts. To host a static website on Amazon S3, you configure an Amazon S3 bucket for website hosting and then upload your website content to the bucket.

  - You can use Amazon CloudFront to improve the performance of your website. CloudFront makes your website files (such as HTML, images, and video) available from data centers around the world (called edge locations). When a visitor requests a file from your website, CloudFront automatically redirects the request to a copy of the file at the nearest edge location. This results in faster download times than if the visitor had requested the content from a data center that is located farther away. 
 - [CloudFront](aws-ass-solution-architect.md#cloudfront)

**Wrong**
- Dynano DB [Dynano DB](aws-ass-solution-architect.md#dynamodb)
  - [DynamoDB_GlobalTable](aws-ass-solution-architect.md#dynamodb_globaltable)
- Amazon Redshift - Amazon Redshift is not suited to be used as a transactional relational database, so this option is not correct.
- EC2s in each AWS region, install MySQL - nightmare

## 20 - Lambda with S3 different account
AWS Lambda function in AWS account A that accesses an Amazon Simple Storage Service (Amazon S3) bucket in AWS account B.

**Solution**
Create an IAM role for the AWS Lambda function that grants access to the Amazon S3 bucket. Set the IAM role as the AWS Lambda function's execution role. Make sure that the bucket policy also grants access to the AWS Lambda function's execution role
  - ![S3](https://assets-pt.media.datacumulus.com/aws-saa-pt/assets/pt2-q16-i1.jpg)
**Wrong**
Create an IAM role for the AWS Lambda function that grants access to the Amazon S3 bucket. Set the IAM role as the Lambda function's execution role and that would give the AWS Lambda function cross-account access to the Amazon S3 bucket
  - When the execution role of AWS Lambda and Amazon S3 bucket to be accessed are from different accounts, then you need to grant Amazon S3 bucket access permissions to the IAM role and also ensure that the bucket policy grants access to the AWS Lambda function's execution role.
## 21 - Very Hard
- **AWS Direct Connect** for migrating app to the AWS Cloud.
- The on-premises application writes hundreds of video files into a mounted NFS file system daily. 
- Post-migration, the company will host **EC2 instance** with a mounted EFS file system. 
- Before the migration cutover, the company must build a process that will replicate the newly created on-premises video files to the Amazon EFS file system.

**Solution**
- Configure an *AWS DataSync agent* on the *on-premises server*: 
  - access to the NFS file system. 
  - Transfer data over the AWS Direct Connect connection to an AWS PrivateLink interface VPC endpoint for Amazon EFS by using a private VIF. 
- Set up an AWS DataSync scheduled task to send the video files to the Amazon EFS file system every 24 hours
- [AWS DataSync](aws-ass-solution-architect.md#aws_datasync)
- [AWS_Direct_Connect](aws-ass-solution-architect.md#aws_direct_connect)
- To establish a private connection between your **VPC** and the **Amazon EFS API**, you can create an *interface VPC endpoint*. You can also access the interface VPC endpoint from on-premises environments or other VPCs using AWS VPN, AWS Direct Connect, or VPC peering.
**Wrong**

- *Configure an AWS DataSync agent on the on-premises server that has access to the NFS file system. Transfer data over the AWS Direct Connect connection to an AWS VPC peering endpoint for Amazon EFS by using a private VIF. Set up an AWS DataSync scheduled task to send the video files to the Amazon EFS file system every 24 hours*
  - A [VPC peering connection](aws-ass-solution-architect.md#vpc_peering) is a networking connection between two VPCs that enables you to route traffic between them privately.
  - You cannot use VPC peering to transfer data over the Direct Connect connection from the on-premises systems to AWS.
- *Configure an AWS DataSync agent on the on-premises server that has access to the NFS file system. Transfer data over the AWS Direct Connect connection to an Amazon S3 bucket by using public VIF. Set up an AWS Lambda function to process event notifications from Amazon S3 and copy the video files from Amazon S3 to the Amazon EFS file system*
  - You can use a public virtual interface to connect to AWS resources that are reachable by a public IP address such as an Amazon Simple Storage Service (Amazon S3) bucket or AWS public endpoints. Although it is theoretically possible to set up this solution, however, it is not the most operationally efficient solution, since it involves sending data via AWS DataSync to Amazon S3 and then in turn using an AWS Lambda function to finally send data to Amazon EFS.
- *Configure an AWS DataSync agent on the on-premises server that has access to the NFS file system. Transfer data over the AWS Direct Connect connection to an Amazon S3 bucket by using a VPC gateway endpoint for Amazon S3. Set up an AWS Lambda function to process event notifications from Amazon S3 and copy the video files from Amazon S3 to the Amazon EFS file system*
  - You can access Amazon S3 from your VPC using gateway VPC endpoints. You cannot use the Amazon S3 gateway endpoint to transfer data over the AWS Direct Connect connection from the on-premises systems to Amazon S3. So this option is incorrect.

## 22 Data transfer charges for Amazon RDS read replicas
- *Amazon RDS read replicas* to provide enhanced performance and read scalability. 

**Solution**
- *There are data transfer charges for replicating data across AWS Regions* 
  - [Amazon RDS read replicas](aws-ass-solution-architect.md#rds_read_replicas)

## 23 Amazon EC2 placement group
- client engagement ETL workloads are currently handled via a Hadoop cluster deployed in the on-premises data center.
- migrate their ETL workloads to AWS Cloud
- needs to be highly available with about 50 Amazon EC2 AZ.

**Solution**
- *Partition placement group*
  - [EC2_Placement_Group](aws-ass-solution-architect.md#EC2_Placement_Group)
  - This strategy is typically used by large distributed and replicated workloads, such as Hadoop, Cassandra, and Kafka.

**Wrong**
- Cluster placement group
  - This is not suited for distributed and replicated workloads such as Hadoop.
- Spread placement group
  -  This is not suited for distributed and replicated workloads such as Hadoop.
- Both Spread placement group and Partition placement group


## 24 
You have a team of developers in your company, and you would like to ensure they can quickly experiment with `AWS Managed Policies` by attaching them to their accounts
- Prevent them from doing an escalation of privileges, by granting themselves the `AdministratorAccess` managed policy. 
- How should you proceed?

**Solution**
*For each developer, define an IAM permission boundary that will restrict the managed policies they can attach to themselves*
- [IAM_Permissions_Boundaries](aws-ass-solution-architect.md#iam_permissions_boundaries)
**Wrong**
1. *Put the developers into an IAM group, and then define an IAM permission boundary on the group that will restrict the managed policies they can attach to themselves*
   - IAM permission boundary can only be applied to roles or users, not IAM groups
2. *Attach an IAM policy to your developers, that prevents them from attaching the AdministratorAccess policy*
- the developers can remove this policy from themselves and escalate their privileges.
3. *Create a Service Control Policy (SCP) on your AWS account that restricts developers from attaching themselves the AdministratorAccess policy*
   - If you consider this option, since AWS Organizations is not mentioned in this question, so we can't apply an SCP.

## 25 Ec2 Cost
An application runs big data workloads on EC2. The application runs 24x7 all round the year and needs at least 20 instances to maintain a minimum acceptable performance threshold and the application needs 300 instances to handle spikes in the workload. Based on historical workloads processed by the application, it needs 80 instances 80% of the time.

**Solution**
- Purchase 80 reserved instances (RIs). Provision additional on-demand and spot instances per the workload demand (Use Auto Scaling Group with launch template to provision the mix of on-demand and spot instances)

## 26 IAM Group
Consider the following policy associated with an *IAM group* containing several users:

- **Note**: SourceIP = UserIP


## 27 cost optimizations for EC2
- The team wants to manage the workload using a mix of on-demand and spot instances across multiple instance types. 
- They would like to create an Auto Scaling group with a mix of these instances.

**Solution**
-  *You can only use a launch template to provision capacity across multiple instance types using both On-Demand Instances and Spot Instances to achieve the desired scale, performance, and cost*
   - [ec2_launch_template](aws-ass-solution-architect.md#ec2_launch_template) 
Wrong
1. *You can neither use a launch configuration nor a launch template to provision capacity across multiple instance types using both On-Demand Instances and Spot Instances to achieve the desired scale, performance, and cost*
  - You cannot use a launch configuration to provision capacity across multiple instance types using both On-Demand Instances and Spot Instances
  - [ec2_launch_configuration](aws-ass-solution-architect.md#ec2_launch_configuration)
2. *You can use a launch configuration or a launch template to provision capacity across multiple instance types using both On-Demand Instances and Spot Instances to achieve the desired scale, performance, and cost*
3. *You can only use a launch configuration to provision capacity across multiple instance types using both On-Demand Instances and Spot Instances to achieve the desired scale, performance, and cost*

## 28 Hosting
- static website with lots of animations in line with the theme of the movie. **scalable serverless solution.**
- MOST cost-optimal and high-performance solution

**Solution**
*Build the website as a static website hosted on Amazon S3. Create an Amazon CloudFront distribution with Amazon S3 as the origin. Use Amazon Route 53 to create an alias record that points to your Amazon CloudFront distribution*
**Wrong**
1. Host on-premises data center:  Create an Amazon CloudFront distribution with this instance as the custom origin
2. AWS Lambda: Create an Amazon CloudFront distribution with Lambda as the origin
   - Not Hosting service
3. EC2: Create a Amazon CloudFront distribution with the EC2 as the custom origin
  - the studio wants a serverless solution

## 29 Password Rotation
**Solution**
- *AWS Secrets Manager*
  - [aws_secrets_manager](aws-ass-solution-architect.md#aws_secrets_manager)
**Wrong**
1. [KMS](aws-ass-solution-architect.md#kms) 
   - encryption service, not a secrets store
2. [CloudHSM](aws-ass-solution-architect.md#cloudhsm)
   - encryption service, not a secrets store
3. [Systems Manager Parameter Store](aws-ass-solution-architect.md#aws_systems_manager_parameter_store) 


## 30 

Migrating app from *on-premises data center* to *AWS* for:
- read-scaling capability 
- availability. 

- The existing architecture leverages a *Microsoft SQL Server database* that sees a *heavy read load*. 
- The engineering team does a full copy of the **production database** at the start of the business day to populate a **dev database**. During this period, application users face high latency leading to a bad user experience.

--> looking at alternate *database options and migrating database engines* if required. 

**Solution**
*Leverage Amazon Aurora MySQL with Multi-AZ Aurora Replicas and create the dev database by restoring from the automated backups of Amazon Aurora*
- [Aurora](aws-ass-solution-architect.md#aurora)
- [Aurora Backup](aws-ass-solution-architect.md#aurora_back_up)
- ~~For the given use case, you can create the dev database by restoring from the automated backups of Amazon Aurora.~~
**Wrong**
1. *Amazon RDS for MySQL with a Multi-AZ deployment and use the standby instance as the dev database*
  - The standby is there just for handling failover in a Multi-AZ deployment. You cannot access the standby instance and use it as a dev database
2. *Leverage Amazon RDS for SQL server with a Multi-AZ deployment and read replicas. Use the read replica as the dev database*
  - A read replica cannot be used as a dev database because it does not allow any database write operations
3. *Leverage Amazon Aurora MySQL with Multi-AZ Aurora Replicas and restore the dev database via mysqldump*
  - Restoring the dev database via mysqldump would still result in a significant load on the primary DB

## 31
- A social photo-sharing web is hosted on *EC2* behind an *ELB(ALP)*
- The app  for 
  - gives the users the ability to upload their photos in *S3*
  -  also shows a leaderboard on the homepage of the app in *DynamoDB*
- *EC2* need to access both *S3* and *DynamoDB* for these features.

->**MOST secure option**
**Solution**
*Attach the appropriate IAM role to the EC2 profile so that the instance can access Amazon S3 and Amazon DynamoDB*
  - [IAM Role](aws-ass-solution-architect.md#iam_role)
**Wrong**
1. *Encrypt the AWS credentials via a custom encryption library and save it in a secret directory on the EC2s. The application code can then safely decrypt the AWS credentials to make the API calls to Amazon S3 and Amazon DynamoDB*
2. *Configure AWS CLI on the EC2s using a valid IAM user's credentials. The application code can then invoke shell scripts to access Amazon S3 and Amazon DynamoDB via AWS CLI*
3. *Save the AWS credentials (access key Id and secret access token) in a configuration file within the application code on the EC2s. EC2s can use these credentials to access Amazon S3 and Amazon DynamoDB*
-> ~~Keeping the AWS credentials (encrypted or plain text) on the Amazon EC2 instance is a bad security practice, therefore these three options using the AWS credentials are incorrect.~~

## 32 - Dedicated Intance Cost Saving
- Run their applications on single-tenant hardware to meet regulatory guidelines.
- Find the MOST cost-effective way of isolating their EC2 to a single tenant?

**Solution**
- [Dedicated Instances](aws-ass-solution-architect.md#ec2_dedicated_instance)

**Bad**
- [Dedicated Host](aws-ass-solution-architect.md#ec2_dedicated_hosts)
  - This option is costlier than the Dedicated Instance

## 33
- Monitoring solution for desktop systems, that will be sending telemetry data into AWS every 1 minute.
- Data for each system must be processed in order, independently, 
- *Scale the number of consumers to be possibly equal to the number of desktop systems* that are being monitored.
**Solution**
- *Use an Amazon Simple Queue Service (Amazon SQS) FIFO (First-In-First-Out) queue, and make sure the telemetry data is sent with a Group ID attribute representing the value of the Desktop ID*
  - [SQS Fifo Queue with Group Id](aws-ass-solution-architect.md#SQS_Fifo_queue)

**Bad**
- *Use an Amazon Kinesis Data Stream, and send the telemetry data with a Partition ID that uses the value of the Desktop ID*
  - [Kinesis Data Stream](aws-ass-solution-architect.md#kinesis_data_stream)
  - Work and would give us the data for each desktop application within shards, but we can only have as many consumers as shards in Kinesis (which is in practice, much less than the number of producers).
- *Use an Amazon Simple Queue Service (Amazon SQS) FIFO (First-In-First-Out) queue, and send the telemetry data as is*
  - Not scale
- *Use an Amazon Simple Queue Service (Amazon SQS) standard queue, and send the telemetry data as is*
  - Not same order

## 34 ASG not terminating unhealthy EC2

- *Auto Scaling group (ASG)* is not terminating an unhealthy **EC1**.

**Solution**
1. *The instance maybe in Impaired status*
2. *The health check grace period for the instance has not expired*
  - [Auto Scaling](aws-ass-solution-architect.md#83-auto-scaling-group-asg) 

3. *The instance has failed the Elastic Load Balancing (ELB) health check status*
**Bad**
1. *A custom health check might have failed. The Auto Scaling group (ASG) does not terminate instances that are set unhealthy by custom checks*

You can define custom health checks in Amazon EC2 Auto Scaling. When a custom health check determines that an instance is unhealthy, the check manually triggers SetInstanceHealth and then sets the instance's state to Unhealthy. Amazon EC2 Auto Scaling then terminates the unhealthy instance.
2. *A user might have updated the configuration of the Auto Scaling group (ASG) and increased the minimum number of instances forcing ASG to keep all instances alive*

This statement is incorrect. If the configuration is updated and ASG needs more number of instances, ASG will launch new, healthy instances and does not keep unhealthy ones alive.
3. *The Amazon EC2 instance could be a spot instance type, which cannot be terminated by the Auto Scaling group (ASG)*

 Amazon EC2 Auto Scaling terminates Spot instances when capacity is no longer available or the Spot price exceeds your maximum price.

## 35 - User Data EC2
- An engineering team wants to examine the feasibility of the user data feature of Amazon EC2 for an upcoming project.

**Solution**
- By default, scripts entered as user data are executed with root user privileges
  - Scripts entered as user data are executed as the root user, hence do not need the sudo command in the script. Any files you create will be owned by root; if you need non-root users to have file access, you should modify the permissions accordingly in the script.

- By default, user data runs only during the boot cycle when you first launch an instance
  - By default, user data scripts and cloud-init directives run only during the boot cycle when you first launch an instance. You can update your configuration to ensure that your user data scripts and cloud-init directives run every time you restart your instance.

**Wrong**
- By default, scripts entered as user data do not have root user privileges for executing
- By default, user data is executed every time an Amazon EC2 instance is re-started

- When an instance is running, you can update user data by using root user credentials

## 36 Window server
Your company has an on-premises Distributed File System Replication (DFSR) service to keep files synchronized on multiple Windows servers, and would like to migrate to AWS cloud.
**Solution**
*Amazon FSx for Windows File Server*
- [FSx for window file server](aws-ass-solution-architect.md#amazon-fsx-for-windows-file-server)

## 37 S3 Enryption Options
- AWS Cloud with **data security requirements** such that the encryption key must be stored in a custom application running on-premises. 
- The company wants to offload the data storage as well as the encryption process to Amazon S3 but continue to use the existing encryption key.
- Which Amazon S3 encryption options allows the company to leverage Amazon S3 for storing data with given constraints?

**Solution**
- Server-Side Encryption with Customer-Provided Keys (SSE-C)
  - [S3_Enryption_Options](aws-ass-solution-architect.md#s3_enryption_options)
**Wrong**
- *Server-Side Encryption with Amazon S3 managed keys (SSE-S3)*
- *Server-Side Encryption with AWS Key Management Service (AWS KMS) keys (SSE-KMS)*
- *Client-Side Encryption with data encryption is done on the client-side before sending it to Amazon S3*

# 38 AWS KMS multi-region key
- Operated only in the `us-east-1` region and stores encrypted data in Amazon S3 using `SSE-KMS`. 
- As part of enhancing its security posture as well as improving the backup and recovery architecture, the company wants to store the encrypted data in Amazon S3 that is replicated into the `us-west-1`.
- The security policies mandate that the data must be encrypted and decrypted using the same key in both AWS regions.

**Solution**
*Create a new Amazon S3 bucket in the us-east-1 region with replication enabled from this new bucket into another bucket in us-west-1 region. Enable SSE-KMS encryption on the new bucket in us-east-1 region by using an AWS KMS multi-region key. Copy the existing data from the current Amazon S3 bucket in us-east-1 region into this new Amazon S3 bucket in us-east-1 region*
  - Refer to [KMS_MutiRegion_Keys](aws-ass-solution-architect.md#KMS_MutiRegion_Keys)
  - You can use multi-region AWS KMS keys in Amazon S3. However, Amazon S3 currently treats multi-region keys as though they were single-region keys, and does not use the multi-region features of the key.
  - To require server-side encryption of all objects in a particular Amazon S3 bucket, you can use a policy. For example, the following bucket policy denies the upload object (s3:PutObject) permission to everyone if the request does not include the x-amz-server-side-encryption header requesting server-side encryption with SSE-KMS.
**Wrong**
- Cloudwatch and Lambdar: Significant Effrot
- Share KMS Key with another region: Could not
- Could not convert single region to multi-region

## 39 ALB with Cognito User Pools 
A social media application is hosted on an Amazon EC2 fleet running behind an ALB.
- The application traffic is fronted by an Amazon CloudFront distribution. 
- The engineering team wants to *decouple the user authentication process* for the application, so that the application servers can just focus on the business logic.
- Mininal Effort

**Solution**
Use Amazon Cognito Authentication via Cognito User Pools for your Application Load Balancer
  - [Cognito_User_Pools](aws-ass-solution-architect.md#cognito_user_pools)
  - [ALB_with_Cognito_User_Pools](aws-ass-solution-architect.md#alb_with_cognito_user_pools)

**Wrong**
1. Use *Cognito Identity Pools* with ALB: Amazon Cognito identity pools provide temporary AWS credentials for users who are guests (unauthenticated) and for users who have been authenticated and received a token.
2. *CloudFront Distribution* + *Cognito_User_Pools*:  Cognito User Pools with CloudFront distribution as you have to create a separate AWS Lambda@Edge function to accomplish the authentication via Cognito User Pools. This involves additional development effort
3. Amazon Cognito Authentication via Cognito Identity Pools for your Amazon CloudFront distribution - Same As beblow