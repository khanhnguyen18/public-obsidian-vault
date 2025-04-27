# Practice Test 1
- https://nab.udemy.com/course/practice-exams-aws-certified-solutions-architect-associate/learn/quiz/4726080/result/1225323700
- https://nab.udemy.com/course/aws-certified-solutions-architect-associate-saa-c03/learn/lecture/34844034

# Question 11

- A **video analytics organization** has been acquired by a leading media company.
- The analytics organization has **10 independent applications** with an on-premises data footprint of about *70 Terabytes* for each application.
- Timeline of *two weeks* to carry out the data migration from on-premises data center to AWS Cloud and establish connectivity.
  Which of the following are the MOST **cost-effective** options for completing the data transfer and establishing connectivity? (*Select two*)

**Options**
- Order 70 AWS Snowball Edge Storage Optimized devices to complete the one-time data transfer
- Setup AWS Direct Connect to establish connectivity between the on-premises data center and AWS Cloud
- Setup AWS Site-to-Site VPN to establish on-going connectivity between the on-premises data center and AWS Cloud
- Order 10 AWS Snowball Edge Storage Optimized devices to complete the one-time data transfer
- Order 1 AWS Snowmobile to complete the one-time data transfer

**Solution**
- Setup AWS Site-to-Site VPN to establish on-going connectivity between the on-premises data center and AWS Cloud
    - VPN Connections can be configured in minutes and are a good solution if you have an immediate need, have low to modest bandwidth requirements, and can tolerate the inherent variability in Internet-based connectivity.
    - Therefore this option is the right fit for the given use-case as the connectivity can be easily established within the given timeframe. #vpn
- Order 10 AWS Snowball Edge Storage Optimized devices to complete the one-time data transfer #snowball
  **Wrong**
- Setup AWS Direct Connect to establish connectivity between the on-premises data center and AWS Cloud
    - Involves significant monetary investment and takes at least a month to set up, therefore it's not the correct fit for this use-case. #direct-connect
- 1 AWS Snowmobile #snowmobile

## Question 12
- A news network uses **Amazon S3** to aggregate the raw video footage from its reporting teams across the US.
- The news network has recently expanded into *new geographies in Europe and Asia*.
- The technical teams at the overseas branch offices have reported huge delays in uploading large video files to the destination Amazon S3 bucket.

Which of the following are the *MOST cost-effective* options to improve the file upload speed into Amazon S3 (Select two)

- Use AWS Global Accelerator for faster file uploads into the destination Amazon S3 bucket
- Use Amazon S3 Transfer Acceleration (Amazon S3TA) to enable faster file uploads into the destination S3 bucket
- Use multipart uploads for faster file uploads into the destination Amazon S3 bucket
- Create multiple AWS Direct Connect connections between the AWS Cloud and branch offices in Europe and Asia. #direct-connect
- Use the direct connect connections for faster file uploads into Amazon S3.
- Create multiple AWS Site-to-Site VPN connections between the AWS Cloud and branch offices in Europe and Asia. Use these VPN connections for faster file uploads into Amazon S3. #vpn


**Solution**
- Use Amazon S3 Transfer Acceleration (Amazon S3TA) to enable faster file uploads into the destination S3 bucket #sthree-ta
- Use multipart uploads for faster file uploads into the destination Amazon S3 bucket #sthree-multi-upload


**Wrong**

## Question 13
- The sourcing team at the **US headquarters** of a global e-commerce company is preparing a **spreadsheet** of the new product catalog.
- The spreadsheet is saved on an Amazon EFS created in us-east-1 region.
- The sourcing team counterparts from other AWS regions such as *Asia Pacific* and *Europe* also want to collaborate on this spreadsheet.

As a solutions architect, what is your recommendation to enable this collaboration with the LEAST amount of operational overhead?

**Options**
- The spreadsheet on the EFS can be accessed in other AWS regions by using an inter-region VPC peering connection
- The spreadsheet will have to be copied into Amazon EFS file systems of other AWS regions as Amazon EFS is a regional service and it does not allow access from other AWS regions
- The spreadsheet will have to be copied in Amazon S3 which can then be accessed from any AWS region
- The spreadsheet data will have to be moved into an Amazon RDS for MySQL database which can then be accessed from any AWS region


**Solution**
- The spreadsheet on the EFS can be accessed in other AWS regions by using an inter-region VPC peering connection #efs

**Wrong**

## Question 14
- re-creatable assets on S3 buckets.
- The assets are accessed by a large number of users for the first few days and the frequency of access falls down drastically after a week.
- Although the assets would be accessed occasionally after the first week, *but they must continue to be immediately accessible when required*.
- The cost of maintaining all the assets on Amazon S3 storage is turning out to be very expensive and the agency is looking at reducing costs as much as possible.

Suggest a way to lower the storage costs while fulfilling the business requirements?

**Options**
- Configure a lifecycle policy to transition the objects to S3 Standard-Infrequent Access (S3 Standard-IA) after 7 days
- Configure a lifecycle policy to transition the objects to S3 Standard-Infrequent Access (S3 Standard-IA) after 30 days
- Configure a lifecycle policy to transition the objects to S3 One Zone-Infrequent Access (S3 One Zone-IA) after 7 days
- Configure a lifecycle policy to transition the objects to S3 One Zone-Infrequent Access (S3 One Zone-IA) after 30 days

**Solution**
- Configure a lifecycle policy to transition the objects to Amazon S3 One Zone-Infrequent Access (S3 One Zone-IA) after **30** days #sthre-one-zone-ia


**Wrong**


## Question 15
- A company manages a multi-tier social media application that runs on **EC2** instances behind an **ALB.**
- The instances run in an **Auto Scaling group** across multiple **AZs** and use an **Amazon Aurora DB**.
- Make the application more resilient to periodic spikes in request rates.

Which of the following solutions would you recommend for the given use-case? (Select two)


**Options**
- Use Amazon Aurora Replica
- Use AWS Shield #shield
- Use AWS Direct Connect #direct-connect
- Use Amazon CloudFront distribution in front of the Application Load Balancer
- Use AWS Global Accelerator #global-accelerator

**Solution**
1. Use *CloudFront* distribution in front of the **Application Load Balancer** #cloudfront-origin-failover
2. Use *Amazon Aurora Replica* #aurora-replica

