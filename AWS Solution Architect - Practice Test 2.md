# Practice Test 2  
  
## 1  EC2
- A company is looking at storing their *less frequently accessed files on AWS* that can be *concurrently accessed by hundreds of Amazon EC2 instances*.  
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
- The company uses **Amazon RDS MySQL** as the database.  
- The engineering team wants an urgent solution to this issue where the rapidly increasing workload might **exceed the available database storage**.  
  
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
- [Read Replicas](aws-ass-solution-architect.md#Read_Replicas)  
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
- The security team at the company has noticed a surge in **malicious attacks** from a **specific IP address** to **steal sensitive data stored** on the Amazon EC2 instances.


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
    - This will allow all Amazon EC2 instances to be deployed in the same VPC (although from different accounts) and easily communicate with one another.

**Wrong**
- Create a **VPC peering connection** between all virtual private cloud (VPCs)
  - [VPC peering connection](aws-ass-solution-architect.md#vpc_peering)
- Create a **Private Link** between all the Amazon EC2 instances
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
*It allows starting an Amazon EC2 instance only when the IP where the call originates is within the 34.50.31.0/24 CIDR block*
    - AWS evaluates these policies when an IAM principal (user or role) makes a request
    - The `aws:SourceIP` in this condition always represents the IP of the caller of the API. That is very helpful if you want to restrict access to certain AWS API for example from the public IP of your on-premises infrastructure.
    - *IPs Type*
      - **elastic IP address (EIP)** - An elastic IP address (EIP) is a static IPv4 address designed for dynamic cloud computing. An Elastic IP address is associated with your AWS account. With an Elastic IP address, you can mask the failure of an instance or software by rapidly remapping the address to another instance in your account.
      - **Private IP address** - A private IPv4 address is an IP address that's not reachable over the Internet. You can use private IPv4 addresses for communication between instances in the same VPC.
      - **Public IP address** - A public IP address is an IPv4 address that's reachable from the Internet. You can use public addresses for communication between your instances and the Internet.

## 17 - EC2 Hibernate
- Machine Learning research group uses a proprietary computer vision application hosted on an Amazon EC2 instance. 
- Every time the instance needs to be stopped and started again, the application takes about 3 minutes to start as some auxiliary software programs need to be executed so that the application can function. 
- The research group would like to minimize the application boostrap time whenever the system needs to be stopped and then started at a later point in time.
**Solution**
- Use Amazon  [EC2 Instance Hibernate](aws-ass-solution-architect.md#ec2_hibernate)

## 18 - Cert Renew
 - App on EC2 instances. 
 - Application handles sensitive customer data, the security team at the company wants to ensure that any SSL/TLS certificates configured on Amazon EC2 instances via the AWS Certificate Manager (ACM) are renewed before their expiry date. 
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
    [](aws-ass-solution-architect.md#aurora-replica)

**Wrong**
## 21 - Very Hard
