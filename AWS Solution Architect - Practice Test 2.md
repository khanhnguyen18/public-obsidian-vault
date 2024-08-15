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

## 38 AWS KMS multi-region key
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

## 40 Route 53 Failover
- A manufacturing company area prone to *natural disasters*. 
- The company is *not ready to fully migrate to the AWS Cloud*, but it wants a failover environment on AWS in case the on-premises data center fails. 
- The company runs web servers that connect to external vendors.
- The data available on AWS and on-premises must be uniform.

Which of the following solutions would have the LEAST amount of downtime?

**Solution**
- Set up a Amazon Route 53 failover record. 
  - Run application servers on **EC2** instances behind an **ALB** in an **Auto Scaling group**. 
  - Set up [[AWS Storage Gateway]](aws-ass-solution-architect.md#aws_storage_gateway) with stored volumes to back up data to **Amazon S3**
->
- Storage Gateway also integrates natively with Amazon S3 cloud storage which makes your data available for in-cloud processing.
- 
**Wrong**
1. *Set up a Amazon Route 53 failover record*. 
  - Run an **AWS Lambda** function to execute an **AWS CloudFormation template** to launch 2 Amazon EC2.
  - Set up **AWS Storage Gateway** with stored volumes to back up data to **Amazon S3**. 
  - Set up an **AWS Direct Connect** connection between a VPC and the data center
  
2. *Set up a Amazon Route 53 failover record.*
   1. Set up an **AWS Direct Connect** connection between a VPC and the data center. 
   2. Run application servers on **Amazon EC2** in an **Auto Scaling group**. 
   3. Run an AWS Lambda function to execute an **AWS CloudFormation template** to create an ALB
3. *Set up a Amazon Route 53 failover record*. 
   1. Execute an **AWS CloudFormation template** from a script to provision EC2 behind an ALB. 
   2. Set up **AWS Storage Gateway** with stored volumes to back up data to **Amazon S3**

AWS CloudFormation is a convenient provisioning mechanism for a broad range of AWS and third-party resources. It supports the infrastructure needs of many different types of applications such as existing enterprise applications, legacy applications, applications built using a variety of AWS resources, and container-based solutions.

These three options involve AWS CloudFormation as part of the solution. Now, AWS CloudFormation takes time to provision the resources and hence is not the right solution when LEAST amount of downtime is mandated for the given use case. Therefore, these options are not the right fit for the given requirement.

## 41 VPC Gateway
Many VPC in various account - need to be connected in a star network with one another and connected with on-premises networks through AWS Direct Connect.

**Solution**
- [AWS Transit Gateway](aws-ass-solution-architect.md#AWS_Transit_Gateway)

**Wrong**
- [AWS PrivateLink](aws-ass-solution-architect.md#private_link)

- [VPC Peering](aws-ass-solution-architect.md#vpc_peering)
  - VPC Peering helps connect two VPCs and is not transitive. It would require to create many peering connections between all the VPCs to have them connect This alone wouldn't work, because we would need to also connect the on-premises data center through Direct Connect and Direct Connect Gateway, but that's not mentioned in this answer.
- [Virtual private gateway (VGW)](aws-ass-solution-architect.md#virtual_private_gateway)

## 42 CPU utilization Notification
A cybersecurity company uses a fleet of Amazon EC2 instances to run a proprietary application.
Wants to be notified via an email whenever the **CPU utilization for any of the Amazon EC2 instances breaches a certain threshold.**
Solution with the LEAST amount of development effort? (Select two)

**Solution**
- [Amazon CloudWatch](aws-ass-solution-architect.md#cloudwatch)
  - You can use Amazon CloudWatch Alarms to send an email via Amazon SNS whenever any of the Amazon EC2 instances breaches a certain threshold. Hence both these options are correct.
- [Amazon SNS](aws-ass-solution-architect.md#sns)

**Wrong**
- [Amazon SQS](aws-ass-solution-architect.md#sqs)
- [AWS Lambda](aws-ass-solution-architect.md#lambda)
- [AWS Step Functions](##)
  - You cannot use Step Functions to monitor CPU utilization of Amazon EC2 instances or send notification emails, hence this option is incorrect.

## 43 Route 53 Policy
- Content management application with the web-tier running on **EC2 instances** and the database tier running on **Aurora** in `us-east-1`
- 90% of its customers in the *US* and *Europe*
- Getting reports of deteriorated application performance from customers in Europe with high application load time
**Solution**
- Setup another fleet of EC2 instances for the web tier in the `eu-west-1` region. Enable latency routing policy in Route 53
  - [Route53_Lantency_Routing](aws-ass-solution-architect.md#Route53_Lantency_Routing)
- Create Aurora read replicas in the `eu-west-1` region
  - [Aurora](aws-ass-solution-architect.md#aurora_replica)
  - Aurora read replicas can be used to scale out reads across regions. This will improve the application performance for users in Europe. Therefore, this is also a correct option for the given use-case.
**Wrong**
- Setup another fleet of EC2 instances for the web tier in the `eu-west-1` region. Enable geolocation routing policy in Route 53
  - [Geolocation_Routing](aws-ass-solution-architect.md#geolocation_routing)
  - You cannot use geolocation routing to reduce latency, hence this option is incorrect.

- Create Aurora Multi-AZ standby instance in the `eu-west-1` region
  - Amazon Aurora Multi-AZ enhances the availability and durability for the database, it does not help in read scaling, so it is not a correct option for the given use-case.
  - [](aws-ass-solution-architect.md#aurora_back_up)
- Setup another fleet of xEC2 instances for the web tier in the `eu-west-1` region. Enable failover routing policy in Amazon Route 53
  - [Failover_Routing](aws-ass-solution-architect.md#failover_routing)
  - You cannot use failover routing to reduce latency, hence this option is incorrect.

## 44 Server-side encryption norms
Store confidential data in Amazon S3 and it needs to meet the following data security and compliance norms:
- Encryption key usage must be logged for auditing purposes
- Encryption Keys must be rotated every year
- The data must be encrypted at rest

Which is the MOST operationally efficient solution?
**Solution**
- *Server-side encryption* with AWS KMS keys (SSE-KMS) with automatic key rotation
  - [Server-side encryption](aws-ass-solution-architect.md#s3_security)
  - [Rotating_KMS_Keys](aws-ass-solution-architect.md#rotating_kms_keys)

**Wrong**
1. *Server-side encryption with AWS Key Management Service (AWS KMS) keys (SSE-KMS) with manual key rotation*
  - possible to manually rotate the AWS KMS key, it is not the best fit solution as it is not operationally efficient.
2. *Server-side encryption (SSE-S3) with automatic key rotation*
  - cannot log the usage of the encryption key for auditing purposes
3. *Server-side encryption with customer-provided keys (SSE-C) with automatic key rotation*
  -  It is possible to automatically rotate the customer-provided keys but you will need to develop the underlying solution to automate the key rotation

## 45 Database
- Application that will perform **a lot of overwrites and deletes on data** 
- Require the latest information to be available anytime data is read via queries on database tables.

As a Solutions Architect, which database technology will you recommend?

**Solution**
- *RDS*
  - [RDS](aws-ass-solution-architect.md#rds)
**Wrong**
1. [Amazon ElastiCache](aws-ass-solution-architect.md#amazon_elasticache)
2. [Amazon S3](aws-ass-solution-architect.md#s3)
  - Not DB technology
3. [Amazon Neptune](aws-ass-solution-architect.md#neptune)
  - Amazon Neptune is a graph database so it's not a good fit.
   
## 46 SG Statful And NCL Stateless
- A developer has configured *inbound traffic* for the relevant ports in both 
  1. the Security Group of the Amazon EC2
  2. the network access control list (network ACL) of the subnet for the EC2. 
- But unable to connect to the service running on EC2.

**Solution**
- Security Groups are stateful, so allowing inbound traffic to the necessary ports enables the connection. Network access control list (network ACL) are stateless, so you must allow both inbound and outbound traffic

## 47
- Real-time data analytics tool for IBO
- The IoT data is funneled into *Kinesis Data Streams* which further acts as the source of a delivery stream for *Kinesis Firehose*
- The engineering team has now configured a *Kinesis Agent* to send IoT data from another set of devices to the same *Kinesis Firehose* delivery stream
- They noticed that data is not reaching Kinesis Firehose as expected

**Solution**
- Kinesis Agent cannot write to Amazon Kinesis Firehose for which the delivery stream source is already set as Amazon Kinesis Data Streams
  - [Firehose](aws-ass-solution-architect.md#firehose)
  - Kinesis Data Stream is configured as the source of a Kinesis Firehose delivery stream, Firehose’s `PutRecord` and `PutRecordBatch` operations are disabled and `Kinesis Agent` cannot write to Kinesis Firehose Delivery Stream directly

**Wrong**
1. Kinesis Agent can only write to Amazon Kinesis Data Streams, not to Amazon Kinesis Firehose
-  [Kinesis Agent](aws-ass-solution-architect.md#kinesis_agent) is a stand-alone Java software application that offers an easy way to collect and send data to Amazon Kinesis Data Streams or Amazon Kinesis Firehose. So this option is incorrect.
- Amazon Kinesis Firehose delivery stream has reached its limit and needs to be scaled manually - Amazon Kinesis Firehose is a fully managed service that automatically scales to match the throughput of your data and requires no ongoing administration. Therefore this option is not correct.


## 48 VPC

- Multiple AWS accounts and has interconnected these accounts in a hub-and-spoke style using the *AWS Transit Gateway*. 
- Amazon VPCs have been provisioned across these AWS accounts to facilitate network isolation.

Which of the following solutions would reduce both the administrative overhead and the costs while providing shared access to services required by workloads in each of the VPCs?

**Solution**
- Build a shared services Amazon Virtual Private Cloud (Amazon VPC)
  - [Centralized_VPC_Endpoints](aws-ass-solution-architect.md#centralized_vpc_endpoints)
**Wrong**
- Use [Fully meshed VPC Peering connection](aws-ass-solution-architect.md#fully_meshed_vpc_peering)
- Use VPCs connected with AWS Direct Connect

## 49 
An *HTTP application* is deployed on an *Auto Scaling Group ALB* that provides HTTPS termination,
accesses a PostgreSQL database managed by Amazon RDS.
How should you configure the security groups?

**Solution**
- PostgreSQL port = 5432 HTTP port = 80 HTTPS port = 443
- The traffic goes like this : 
  1. The client sends an *HTTPS request* to ALB on port 443. This is handled by the rule - "*The security group of the ALB should have an inbound rule from anywhere on port 443*"
  2. *ALB* then forwards the request to one of the EC2. This is handled by the rule - "The security group of the Amazon EC2 instances should have an inbound rule from the security group of the Application Load Balancer on port 80"
  3. The Amazon EC2 instance further accesses the PostgreSQL database managed by Amazon RDS on port 5432. This is handled by the rule - "The security group of Amazon RDS should have an inbound rule from the security group of the Amazon EC2 instances in the Auto Scaling group on port 5432"

**Wrong**
- The security group of the Amazon EC2 instances should have an inbound rule from the security group of the Amazon RDS database on port 5432

- The security group of Amazon RDS should have an inbound rule from the security group of the Amazon EC2 instances in the Auto Scaling group on port 80

- The security group of the Application Load Balancer should have an inbound rule from anywhere on port 80

## 50 EC2_Default_Termination_Policy
- Auto Scaling needs to terminate an instance from `us-east-1a` AZ as it has the most number of instances amongst the Availability Zone (AZs) being used currently. 
There are 4 instances in the Availability Zone (AZ) us-east-1a like so: 
1. Instance A has the oldest launch template
2. Instance B has the oldest launch configuration
3. Instance C has the newest launch configuration 
4. Instance D is closest to the next billing hour.

Which of the following instances would be terminated per the default termination policy?
**Solution**
- Instance B
  - [EC2_Default_Termination_Policy](aws-ass-solution-architect.md#ec2_default_termination_policy)

## 51 - AWS Snowball and S3 Glacier
Use AWS Snowball to move *on-premises backups* into a *long term archival tier on AWS*.
Which solution provides the MOST cost savings?

**Solution**
- Create an AWS Snowball job and target an Amazon S3 bucket. Create a lifecycle policy to transition this data to Amazon S3 Glacier Deep Archive on the same day
  - [AWS_Snowball](aws-ass-solution-architect.md#aws_snowball ) + [S3_Glacier](aws-ass-solution-architect.md#s3_glacier)
  - For this scenario, you will want to minimize the time spent in *Amazon S3 Standard* for all files to avoid unintended Amazon S3 Standard storage charges. 
  - AWS recommends using a *zero-day lifecycle policy*. when using it, you are only charged Amazon S3 Glacier Deep Archive rates. 
  - When billed, the lifecycle policy is accounted for first, and if the destination is Amazon S3 Glacier Deep Archive, you are charged Amazon S3 Glacier Deep Archive rates for the transferred files.
- You can't move data directly from AWS Snowball into Amazon S3 Glacier, you need to go through Amazon S3 first, and then use a lifecycle policy. So this option is correct.
- **Wrong**

- Create an AWS Snowball job and target a Amazon S3 Glacier Vault
- Create a AWS Snowball job and target an Amazon S3 Glacier Deep Archive Vault
- Create an AWS Snowball job and target an Amazon S3 bucket. Create a lifecycle policy to transition this data to Amazon S3 Glacier on the same day

## 52
- A weather forecast agency collects key weather metrics across multiple cities in the US and sends this data in the form of *key-value pairs* to AWS Cloud at a *one-minute frequency*.

As a solutions architect, which of the following AWS services would you use to build a solution for processing and then *reliably storing this data* with *high availability*? (Select two)

**Solution**
- [Amazon DynamoDB](aws-ass-solution-architect.md#dynamodb)
- [AWS Lambda](aws-ass-solution-architect.md#lambda)
**Wrong**
- [Amazon RDS](aws-ass-solution-architect.md#rds) - Relation Database
- [Amazon Redshift](aws-ass-solution-architect.md#redshift) 
- [Amazon ElastiCache](aws-ass-solution-architect.md#amazon_elasticache) - Elasticache is used as a caching layer in front of relational databases. It is not a good fit to store data in key-value pairs from the IoT sources, so this option is not correct.

## 53
- A retail company wants to rollout and test a blue-green deployment for its *global application* in the next 48 hours.
- Most of the customers use mobile phones which are prone to DNS caching. The company has only two days left for the annual Thanksgiving sale to commence.

As a Solutions Architect, which of the following options would you recommend to test the deployment on as many users as possible in the given time frame?


**Solution**
- Use AWS Global Accelerator to distribute a portion of traffic to a particular deployment
  - [BlueGreenDeployment](aws-ass-solution-architect.md#bluegreendeployment)
  - [Global Accelerator](aws-ass-solution-architect.md#aws_global_accelerator)
    - AWS Global Accelerator uses endpoint weights to determine the proportion of traffic that is directed to endpoints in an endpoint group, and traffic dials to control the percentage of traffic that is directed to an endpoint group (an AWS region where your application is deployed).

    - While relying on the DNS service is a great option for blue/green deployments, it may not fit use-cases that require a fast and controlled transition of the traffic. Some client devices and internet resolvers cache DNS answers for long periods; this DNS feature improves the efficiency of the DNS service as it reduces the DNS traffic across the Internet, and serves as a resiliency technique by preventing authoritative name-server overloads. The downside of this in blue/green deployments is that you don’t know how long it will take before all of your users receive updated IP addresses when you update a record, change your routing preference or when there is an application failure.
      - https://aws.amazon.com/blogs/networking-and-content-delivery/using-aws-global-accelerator-to-achieve-blue-green-deployments

    - With AWS Global Accelerator, you can shift traffic gradually or all at once between the blue and the green environment and vice-versa without being subject to DNS caching on client devices and internet resolvers, traffic dials and endpoint weights changes are effective within seconds.
**Wrong**
- Use ELB to distribute traffic across deployments
  - ELB can distribute traffic across healthy instances. You can also use the Application Load Balancers weighted target groups feature for blue/green deployments as it does not rely on the DNS service. In addition you don’t need to create new ALBs for the green environment. As the use-case refers to a global application, so this option cannot be used for a multi-Region solution which is needed for the given requirement.
- Use Amazon Route 53 weighted routing to spread traffic across different deployments
  - Weighted routing lets you associate multiple resources with a single domain name (example.com) or subdomain name (acme.example.com) and choose how much traffic is routed to each resource. This can be useful for a variety of purposes, including load balancing and testing new versions of the software. As discussed earlier, DNS caching is a negative behavior for this use case and hence Amazon Route 53 is not a good option.
- Use AWS CodeDeploy deployment options to choose the right deployment
  - [Code deploy](aws-ass-solution-architect.md#code-deploy) 
  - Blue/Green deployment is one of the deployment types that CodeDeploy supports. CodeDeploy is not meant to distribute traffic across instances, so this option is incorrect

## 54 EC2 Pricing
An IT company wants to optimize the costs incurred on its fleet of *100 Amazon EC2 instances* for the next year. 
- Based on historical analyses, the engineering team observed that *70 of these instances handle* the compute services of its flagship application and need to be always available. 
- The other 30 instances are used to handle batch jobs that can afford a delay in processing.

As a solutions architect, which of the following would you recommend as the MOST cost-optimal solution?

**Solution**
Purchase 70 reserved instances (RIs) and 30 spot instances
  - [EC2 Pricing](aws-ass-solution-architect.md#ec2---type-of-instace)
**Wrong**
Purchase 70 on-demand instances and 30 spot instances
Purchase 70 on-demand instances and 30 reserved instances
Purchase 70 reserved instances and 30 on-demand instances

## 55
- A big data consulting firm needs to set up a *data lake* on *Amazon S3* for a Health-Care client. 
- The data lake is split in raw and refined zones. 
- For compliance reasons, the **source data** needs to be kept for a minimum of 5 years. 
- The source data arrives in the **raw zone** and is then processed via an *AWS Glue* into the refined zone. The business analysts run ad-hoc queries only on the data in the refined zone using *Amazon Athena*.
-  The team is concerned about the cost of data storage in both the raw and refined zones as the data is increasing at a rate of 1 terabyte daily in each zone.

**Solution**

1. Use *AWS Glue ETL job* to write the transformed data in the **refined zone** using a compressed file format
  - [AWS Glue ETL job](aws-ass-solution-architect.md#glue)
  - You cannot transition the **refined zone** data into Amazon S3 Glacier Deep Archive because it is used by the business analysts for ad-hoc querying. Therefore, the best optimization is to have the **refined zone**data stored in a compressed format via the Glue job. The compressed data would reduce the storage cost incurred on the data in the refined zone.

2. Setup a lifecycle policy to transition the raw zone data into Amazon S3 Glacier Deep Archive after 1 day of object creation
 - [S3 Lifecycle](aws-ass-solution-architect.md#s3_lifecycle)

**Wrong**
2. Create an AWS Lambda function based job to delete the raw zone data after 1 day
- As mentioned in the use-case, the source data needs to be kept for a minimum of 5 years for compliance reasons. Therefore the data in the raw zone cannot be deleted after 1 day.

3. Setup a lifecycle policy to transition the refined zone data into Amazon S3 Glacier Deep Archive after 1 day of object creation
   - You cannot transition the *refined zone* data into Amazon S3 Glacier Deep Archive because it is used by the business analysts for ad-hoc querying. Hence this option is incorrect.
4. Use *AWS Glue ETL* job to write the transformed data in the refined zone using CSV format
 - It is cost-optimal to write the data in the refined zone using a compressed format instead of CSV format. The compressed data would reduce the storage cost incurred on the data in the refined zone. So, this option is incorrect.

## 56 
- A startup has just developed a video backup service hosted on a fleet of Amazon EC2 instances. 
- The Amazon EC2 instances are behind an ALB and the instances are using EBS Volumes for storage. 
- The service provides authenticated users the ability to upload videos that are then saved on the EBS volume attached to a given instance. 
- On the first day of the beta launch, users start complaining that they can see only some of the videos in their uploaded videos backup. 
- Every time the users log into the website, they claim to see a different subset of their uploaded videos.

Which of the following is the MOST optimal solution to make sure that users can view all the uploaded videos? (Select two)

**Solution**
1. Write a one time job to copy the videos from all [EBS](aws-ass-solution-architect.md#ebs) to Amazon S3 and then modify the application to use Amazon S3 standard for storing the videos
3. Mount Amazon Elastic File System (Amazon EFS) on all Amazon EC2 instances. Write a one time job to copy the videos from all Amazon EBS volumes to Amazon EFS. Modify the application to use Amazon EFS for storing the videos

- *As Amazon EBS volumes are attached locally to the Amazon EC2 instances, therefore the uploaded videos are tied to specific Amazon EC2 instances. Every time the user logs in, they are directed to a different instance and therefore their videos get dispersed across multiple EBS volumes. The correct solution is to use either Amazon S3 or Amazon EFS to store the user videos.*

**Wrong**
1. Write a one time job to copy the videos from all Amazon EBS volumes to Amazon RDS and then modify the application to use Amazon RDS for storing the videos

2. Write a one time job to copy the videos from all Amazon EBS volumes to Amazon DynamoDB and then modify the application to use Amazon DynamoDB for storing the videos
3. Write a one time job to copy the videos from all Amazon EBS volumes to Amazon S3 Glacier Deep Archive and then modify the application to use Amazon S3 Glacier Deep Archive for storing the videos


## 57

- An IT company provides S3 bucket access to specific users within the same account for completing project specific work. 
With changing business requirements, cross-account S3 access requests are also growing every month. 
The company is looking for a solution that can offer user level as well as account-level access permissions for the data stored in Amazon S3 buckets.

As a Solutions Architect, which of the following would you suggest as the MOST optimized way of controlling access for this use-case?

**Solution**
1. Use [S3 Bucket Policies](aws-ass-solution-architect.md#s3_bucket_policy)

**Wrong**

2. Use [Access Control Lists (ACLs)](aws-ass-solution-architect.md#acl)
3. Use [Security Groups](aws-ass-solution-architect.md#security_group)
For EC2, not for S3
4. [Use Identity and Access Management (IAM) policies](aws-ass-solution-architect.md#iam)
- Organizations with many employees to create and manage multiple users under a single AWS account. IAM policies are attached to the users, enabling centralized control of permissions for users under your AWS Account to access buckets or objects. With IAM policies, you can only grant users within your own AWS account permission to access your Amazon S3 resources. So, this is not the right choice for the current requirement.


## 58 
- Private hosted zone and associated it with a Virtual Private Cloud (VPC). 
- However, the Domain Name System (DNS) queries for the private hosted zone remain unresolved.

As a Solutions Architect, can you identify the Amazon VPC options to be configured in order to get the private hosted zone to work?
**Solution**
- Enable DNS hostnames and DNS resolution for private hosted zones
  - DNS hostnames and DNS resolution are required settings for private hosted zones. DNS queries for private hosted zones can be resolved by the Amazon-provided VPC DNS server only. As a result, these options must be enabled for your private hosted zone to work.
  - [DNS](aws-ass-solution-architect.md#dns_hosted_zones)
**Wrong**
- Remove any overlapping namespaces for the private and public hosted zones
- Fix the Name server (NS) record and Start Of Authority (SOA) records that may have been created with wrong configurations
- Fix conflicts between your private hosted zone and any Resolver rule that routes traffic to your network for the same domain name, as it results in ambiguity over the route to be taken


## 59 
You would like to migrate an AWS account from an AWS Organization A to an AWS Organization B. What are the steps dco to it?

### 
- Remove the member account from the old organization. Send an invite to the member account from the new Organization. Accept the invite to the new organization from the member account

Open an AWS Support ticket to ask them to migrate the account

**Solution**
1. Remove the member account from the old organization. Send an invite to the member account from the new Organization. Accept the invite to the new organization from the member account
  - [AWS Organization](aws-ass-solution-architect.md#aws_organization)
  - To migrate accounts from one organization to another, you must have root or IAM access to both the member and master accounts. Here are the steps to follow: 
    - 1. Remove the member account from the old organization 
    - 2. Send an invite to the member account from the new Organization 
    - 3. Accept the invite to the new organization from the member account

**Wrong**
2. Open an AWS Support ticket to ask them to migrate the account


3. Send an invite to the new organization. Remove the member account from the old organization. Accept the invite to the new organization from the member account


4. Send an invite to the new organization. Accept the invite to the new organization from the member account. Remove the member account from the old organization

## 60 

Your company has a monthly big data workload, running for about 2 hours, which can be efficiently distributed across multiple servers of various sizes, with a variable number of CPUs. The solution for the workload should be able to withstand server failures.

**Solution**
3. Run the workload on a Spot Fleet

**Fail***
1. Run the workload on [Dedicated Hosts](aws-ass-solution-architect.md#ec2_dedicated_hosts)
They're not particularly cost-efficient. So this option is not correct.

1. Run the workload on Reserved Instances (RI)

- Reserved Instances are less cost-optimized than Spot Instances, and most efficient when used continuously. Here the workload is once a month, so this is not efficient.
3. Run the workload on Spot Instances

- A Spot Instance is an unused Amazon EC2 instance that is available for less than the On-Demand price. Because Spot Instances enable you to request unused Amazon EC2 instances at steep discounts, you can lower your Amazon EC2 costs significantly. The hourly price for a Spot Instance is called a Spot price. Only spot fleets can maintain target capacity by launching replacement instances after Spot Instances in the fleet are terminated, so spot instances, by themselves, are not the right fit for this use-case.


## 61

- EC2 instances (behind Application Load Balancer) deployed in a single Availability Zone (AZ).
- To maintain an acceptable level of end-user experience, the application needs at least 4 instances to be always available.

As a solutions architect, which of the following would you recommend so that the application achieves high availability with MINIMUM cost?
**Solution**
2. Deploy the instances in three Availability Zones (AZs). Launch two instances in each Availability Zone (AZ)
   1. The correct option is to deploy the instances in three Availability Zones (AZs) and launch two instances in each Availability Zone (AZ). Even if one of the AZs goes out of service, still we shall have 4 instances available and the application can maintain an acceptable level of end-user experience. Therefore, we can achieve high availability with just 6 instances in this case.
**Faild**
1. Deploy the instances in two Availability Zones (AZs). Launch two instances in each Availability Zone (AZ)

3. Deploy the instances in two Availability Zones (AZs). Launch four instances in each Availability Zone (AZ)
4. Deploy the instances in one Availability Zones. Launch two instances in the Availability Zone (AZ)

## 62
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
        "StringEquals": {
          "aws:RequestedRegion": "eu-west-1"
        }
      }
    }
  ]
}
```

**Solution**
2. It allows running Amazon EC2 instances only in the eu-west-1 region, and the API call can be made from anywhere in the world
  - You can use the `aws:RequestedRegion` key to compare the AWS Region that was called in the request with the Region that you specify in the policy. You can use this global condition key to control which Regions can be requested.

  - `aws:RequestedRegion` represents the *target of the API call*. So in this example, we can only launch an Amazon EC2 instance in eu-west-1, and we can do this API call from anywhere.

**Wrongo**
1. It allows running Amazon EC2 instances in any region when the API call is originating from the eu-west-1 region
3. It allows running Amazon EC2 instances anywhere but in the eu-west-1 region
4. It allows running Amazon EC2 instances in the eu-west-1 region, when the API call is made from the eu-west-1 region
    
## 63 - EFS Performance Mode
An analytics company wants to improve the performance of its big data processing workflows running on Amazon Elastic File System (Amazon EFS). Which of the following performance modes should be used for Amazon EFS to address this requirement?
**Solution**
2. Max I/O
  - [EFS](aws-ass-solution-architect.md#efs)
  - *Max I/O performance mode* is used to scale to higher levels of aggregate throughput and operations per second. This scaling is done with a tradeoff of slightly higher latencies for file metadata operations. Highly parallelized applications and workloads, such as big data analysis, media processing, and genomic analysis, can benefit from this mode.
  - [EFS Mode](aws-ass-solution-architect.md#efs_performance_mode)
**Wrong**
1. General Purpose

3. Provisioned Throughput
4. Bursting Throughput
- [EFS Througput Mode](aws-ass-solution-architect.md#efs_throuhput_mode)


## 64 Aurora DB Global

A company is developing a global healthcare application that requires the least possible *latency for database read/write operations* from users in *several geographies across* the world. 
The company has hired you as an AWS Certified Solutions Architect Associate to build a solution using Amazon Aurora that offers an effective recovery point objective (RPO) of seconds and a recovery time objective (RTO) of a minute.

**Solution**
2. Set up an [Amazon Aurora Global Database](aws-ass-solution-architect.md#aurora_global_table) cluster

**Wrong**
1. Set up an Amazon Aurora multi-master Database cluster
3. Set up an Amazon Aurora provisioned Database cluster

==> Both these options work in a single AWS Region, so these options are incorrect.


4. Set up an Amazon Aurora multi-master Database cluster
  - AWS does not offer the multi-master feature in a Aurora database cluster,


## 65
An IT company is working on a client project to build a Supply Chain Management application. 
The web-tier of the application runs on an *Amazon EC2 instance* and the database tier is on *Amazon RDS MySQL*.
- For beta testing, all the resources are currently deployed in *a single Availability Zone (AZ)*. The development team wants to improve application availability before the go-live.

Given that all end users of the web application would be located in the US, which of the following would be the MOST resource-efficient solution?

**Solution**
4. Deploy the web-tier *Amazon EC2 instances* in two Availability Zones (AZs), behind an Elastic Load Balancer. Deploy the *Amazon RDS MySQL* database **in Multi-AZ configuration**
  - Elastic Load Balancing automatically distributes incoming application traffic across multiple targets, such as Amazon EC2 instances, containers, IP addresses, and Lambda functions. It can handle the varying load of your application traffic in a single Availability Zone or across multiple Availability Zones. Therefore, deploying the web-tier Amazon EC2 instances in two Availability Zones (AZs), behind an Elastic Load Balancer would improve the availability of the application.
  - Amazon RDS Multi-AZ deployments provide enhanced availability and durability for RDS database (DB) instances, making them a natural fit for production database workloads. When you provision a Multi-AZ DB Instance, Amazon RDS automatically creates a primary DB Instance and synchronously replicates the data to a standby instance in a different Availability Zone (AZ). Each Availability Zone (AZ) runs on its own physically distinct, independent infrastructure, and is engineered to be highly reliable. Deploying the Amazon RDS MySQL database in Multi-AZ configuration would improve availability and hence this is the correct
[RDS](aws-ass-solution-architect.md#rds)

**Wrong**
1. Deploy the web-tier Amazon EC2 instances in two regions, behind an Elastic Load Balancer. Deploy the Amazon RDS MySQL database in read replica configuration

2. Deploy the web-tier Amazon EC2 instances in two regions, behind an Elastic Load Balancer. Deploy the Amazon RDS MySQL database **in Multi-AZ configuration**

3. Deploy the web-tier Amazon EC2 instances in two Availability Zones (AZs), behind an Elastic Load Balancer. Deploy the Amazon RDS MySQL database in read replica configuration

- Amazon RDS Read Replicas provide enhanced performance and durability for RDS database (DB) instances. They make it easy to elastically scale out beyond the capacity constraints of a single DB instance for read-heavy database workloads. Read replicas are meant to address scalability issues. You cannot use read replicas for improving availability, so both these options are incorrect.