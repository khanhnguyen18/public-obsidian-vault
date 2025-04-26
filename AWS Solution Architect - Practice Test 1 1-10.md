# Practice Test 1
- https://nab.udemy.com/course/practice-exams-aws-certified-solutions-architect-associate/learn/quiz/4726080/result/1225323700

- https://nab.udemy.com/course/aws-certified-solutions-architect-associate-saa-c03/learn/lecture/34844034


## Question 1
- The DevOps team at an e-commerce company wants to perform some maintenance work on a specific Amazon EC2 instance that is part of an Auto Scaling group using a step scaling policy.
- The team is facing a maintenance challenge - every time the team deploys a maintenance patch, the instance health check status shows as out of service for a few minutes.
- This causes the Auto Scaling group to provision another replacement instance immediately.

As a solutions architect, which are the MOST time/resource efficient steps that you would recommend so that the maintenance work can be completed at the earliest? (Select two)

**Options**
- Suspend the ScheduledActions process type for the Auto Scaling group and apply the maintenance patch to the instance. Once the instance is ready, you can you can manually set the instance's health status back to healthy and activate the ScheduledActions process type again
- Put the instance into the Standby state and then update the instance by applying the maintenance patch. Once the instance is ready, you can exit the Standby state and then return the instance to service
- Your selection is incorrect
- Delete the Auto Scaling group and apply the maintenance fix to the given instance. Create a new Auto Scaling group and add all the instances again using the manual scaling policy
- Your selection is correct
- Suspend the ReplaceUnhealthy process type for the Auto Scaling group and apply the maintenance patch to the instance. Once the instance is ready, you can manually set the instance's health status back to healthy and activate the ReplaceUnhealthy process type again
- Take a snapshot of the instance, create a new Amazon Machine Image (AMI) and then launch a new instance using this AMI. Apply the maintenance patch to this new instance and then add it back to the Auto Scaling Group by using the manual scaling policy. Terminate the earlier instance that had the maintenance issue


**Solution**
- **Put the instance into the Standby state and then update the instance by applying the maintenance patch. Once the instance is ready, you can exit the Standby state and then return the instance to service**. You can put an instance that is in the InService state into the *Standby state*, update some software or troubleshoot the instance, and then return the instance to service. Instances that are on standby are still part of the Auto Scaling group, but they do not actively handle application traffic.
- **Suspend the ReplaceUnhealthy process type for the Auto Scaling group and apply the maintenance patch to the instance. Once the instance is ready, you can manually set the instance's health status back to healthy and activate the ReplaceUnhealthy process type again** - The *ReplaceUnhealthy* process terminates instances that are marked as unhealthy and then creates new instances to replace them. Amazon EC2 Auto Scaling stops replacing instances that are marked as unhealthy. Instances that fail EC2 or Elastic Load Balancing health checks are still marked as unhealthy. As soon as you resume the ReplaceUnhealthly process, Amazon EC2 Auto Scaling replaces instances that were marked unhealthy while this process was suspended.
    - #suspend-resume-processes

**Wrong**
**Take a snapshot of the instance, create a new Amazon Machine Image (AMI) and then launch a new instance using this AMI. Apply the maintenance patch to this new instance and then add it back to the Auto Scaling Group by using the manual scaling policy. Terminate the earlier instance that had the maintenance issue** - Taking the snapshot of the existing instance to create a new AMI and then creating a new instance in order to apply the maintenance patch is not time/resource optimal, hence this option is ruled out.

**Delete the Auto Scaling group and apply the maintenance fix to the given instance. Create a new Auto Scaling group and add all the instances again using the manual scaling policy** - It's not recommended to delete the Auto Scaling group just to apply a maintenance patch on a specific instance.

**Suspend the ScheduledActions process type for the Auto Scaling group and apply the maintenance patch to the instance. Once the instance is ready, you can you can manually set the instance's health status back to healthy and activate the ScheduledActions process type again** - Amazon EC2 Auto Scaling does not execute scaling actions that are scheduled to run during the suspension period. This option is not relevant to the given use-case.

References:
- https://docs.aws.amazon.com/autoscaling/ec2/userguide/as-enter-exit-standby.html
- https://docs.aws.amazon.com/autoscaling/ec2/userguide/as-suspend-resume-processes.html
- https://docs.aws.amazon.com/autoscaling/ec2/userguide/health-checks-overview.html
## Question 2
- A gaming company is looking at improving the availability and performance of its global flagship application which utilizes User Datagram Protocol and needs to support fast regional failover in case an AWS Region goes down.
- The company wants to continue using its own custom Domain Name System (DNS) service.
  Which of the following AWS services represents the best solution for this use-case?
  **Options**
- Amazon CloudFront
- AWS Elastic Load Balancing (ELB)
- Amazon Route 53
- AWS Global Accelerator
  **Solution**
  *AWS Global Accelerator* #global_accelerator
- AWS Global Accelerator utilizes the Amazon global network, allowing you to improve the performance of your applications by lowering first-byte latency (the round trip time for a packet to go from a client to your endpoint and back again) and jitter (the variation of latency), and increasing throughput (the amount of time it takes to transfer data) as compared to the public internet.
- AWS Global Accelerator improves performance for a wide range of applications over TCP or UDP by proxying packets at the edge to applications running in one or more AWS Regions. Global Accelerator is a good fit for non-HTTP use cases, such as gaming (UDP), IoT (MQTT), or Voice over IP, as well as for HTTP use cases that specifically require static IP addresses or deterministic, fast regional failover.
  **Wrong**
  *Amazon CloudFront* - Amazon CloudFront is a fast content delivery network (CDN) service that securely delivers data, videos, applications, and APIs to customers globally with low latency, high transfer speeds, all within a developer-friendly environment. #cloundfront

AWS Global Accelerator and Amazon CloudFront are separate services that use the AWS global network and its edge locations around the world. CloudFront improves performance for both cacheable content (such as images and videos) and dynamic content (such as API acceleration and dynamic site delivery), while Global Accelerator improves performance for a wide range of applications over TCP or UDP. #cloundfront #global_accelerator

*AWS Elastic Load Balancing (ELB)* - Both of the services, ELB and Global Accelerator solve the challenge of routing user requests to healthy application endpoints. AWS Global Accelerator relies on ELB to provide the traditional load balancing features such as support for internal and non-AWS endpoints, pre-warming, and Layer 7 routing. However, while ELB provides load balancing within one Region, AWS Global Accelerator provides traffic management across multiple Regions. #elb

A regional ELB load balancer is an ideal target for AWS Global Accelerator. By using a regional ELB load balancer, you can precisely distribute incoming application traffic across backends, such as Amazon EC2 instances or Amazon ECS tasks, within an AWS Region.

If you have workloads that cater to a global client base, AWS recommends that you use AWS Global Accelerator. If you have workloads hosted in a single AWS Region and used by clients in and around the same Region, you can use an Application Load Balancer or Network Load Balancer to manage your resources.

*Amazon Route 53* - Amazon Route 53 is a highly available and scalable cloud Domain Name System (DNS) web service. It is designed to give developers and businesses an extremely reliable and cost-effective way to route end users to Internet applications by translating names like www.example.com into the numeric IP addresses like 192.0.2.1 that computers use to connect to each other. Route 53 is ruled out as the company wants to continue using its own custom DNS service. #route53

**Reference**:
https://aws.amazon.com/global-accelerator/faqs/

## Question 3
- A new DevOps engineer has just joined a development team and wants to understand the replication capabilities for Amazon RDS Multi-AZ deployment as well as Amazon RDS Read-replicas.
  Which of the following correctly summarizes these capabilities for the given database?


**Options**
- Multi-AZ follows asynchronous replication and spans at least two Availability Zones (AZs) within a single region. Read replicas follow asynchronous replication and can be within an Availability Zone (AZ), Cross-AZ, or Cross-Region.
- Multi-AZ follows asynchronous replication and spans at least two Availability Zones (AZs) within a single region. Read replicas follow asynchronous replication and can be within an Availability Zone (AZ), Cross-AZ, or Cross-Region.
- Multi-AZ follows asynchronous replication and spans one Availability Zone (AZ) within a single region. Read replicas follow synchronous replication and can be within an Availability Zone (AZ), Cross-AZ, or Cross-Region
- Multi-AZ follows asynchronous replication and spans at least two Availability Zones (AZs) within a single region. Read replicas follow synchronous replication and can be within an Availability Zone (AZ), Cross-AZ, or Cross-Region
- Multi-AZ follows synchronous replication and spans at least two Availability Zones (AZs) within a single region. Read replicas follow asynchronous replication and can be within an Availability Zone (AZ), Cross-AZ, or Cross-Region

**Solution**
- Multi-AZ follows synchronous replication and spans at least two Availability Zones (AZs) within a single region. Read replicas follow asynchronous replication and can be within an Availability Zone (AZ), Cross-AZ, or Cross-Region  #multi-az #read-replica

**Wrong**

## Question 4
- A healthcare company uses its on-premises infrastructure to run legacy applications that require specialized customizations to the underlying Oracle database as well as its host operating system (OS).
- The company also wants to improve the availability of the Oracle database layer.
- Meets these requirements while minimizing the underlying infrastructure maintenance effort.

Which of the following options represents the best solution for this use case?


**Options**
- Leverage multi-AZ configuration of Amazon RDS Custom for Oracle that allows the Database Administrator (DBA) to access and customize the database environment and the underlying operating system
- Leverage multi-AZ configuration of Amazon RDS for Oracle that allows the Database Administrator (DBA) to access and customize the database environment and the underlying operating system
- Deploy the Oracle database layer on multiple Amazon EC2 instances spread across two Availability Zones (AZs). This deployment configuration guarantees high availability and also allows the Database Administrator (DBA) to access and customize the database environment and the underlying operating system
- Leverage cross AZ read-replica configuration of Amazon RDS for Oracle that allows the Database Administrator (DBA) to access and customize the database environment and the underlying operating system


**Solution**
- Leverage multi-AZ configuration of **Amazon RDS Custom** for Oracle that allows the Database Administrator (DBA) to access and customize the database environment and the underlying operating system #multi-az #rds-custome
    - For the given use-case, you need to use Amazon RDS Custom for Oracle as it allows you to access and customize your database server host and operating system, for example by applying special patches and changing the database software settings to support third-party applications that require privileged access. Amazon RDS Custom for Oracle facilitates these functionalities with minimum infrastructure maintenance effort. You need to set up the RDS Custom for Oracle in multi-AZ configuration for high availability.

**Wrong**
- Leverage multi-AZ configuration of Amazon RDS for Oracle that allows the Database Administrator (DBA) to access and customize the database environment and the underlying operating system

- Leverage cross AZ read-replica configuration of Amazon RDS for Oracle that allows the Database Administrator (DBA) to access and customize the database environment and the underlying operating system

    - Amazon RDS for Oracle does not allow you to access and customize your database server host and operating system. Therefore, both these options are incorrect.

- **Deploy the Oracle database layer on multiple Amazon EC2 instances spread across two Availability Zones (AZs)**. This deployment configuration guarantees high availability and also allows the Database Administrator (DBA) to access and customize the database environment and the underlying operating system - The use case requires that the best solution should involve minimum infrastructure maintenance effort. When you use Amazon EC2 instances to host the databases, you need to manage the server health, server maintenance, server patching, and database maintenance tasks yourself. In addition, you will also need to manage the multi-AZ configuration by deploying Amazon EC2 instances across two Availability Zones (AZs), perhaps by using an Auto Scaling group. These steps entail significant maintenance effort. Hence this option is incorrect.

## Question 5
- A healthcare startup needs to enforce compliance and regulatory guidelines for objects stored in Amazon S3.
- One of the key requirements is to provide adequate protection against accidental deletion of objects.

As a solutions architect, what are your recommendations to address these guidelines? (Select two) ?

**Options**
- Enable multi-factor authentication (MFA) delete on the Amazon S3 bucket
- Change the configuration on Amazon S3 console so that the user needs to provide additional confirmation while deleting any Amazon S3 object
- Create an event trigger on deleting any Amazon S3 object. The event invokes an Amazon Simple Notification Service (Amazon SNS) notification via email to the IT manager
- Establish a process to get managerial approval for deleting Amazon S3 objects
- Enable versioning on the Amazon S3 bucket

**Solution**
- Enable multi-factor authentication (MFA) delete on the Amazon S3 bucket #s3-mfa
- Enable versioning on the Amazon S3 bucket. #s3-versioning

**Wrong**
**Create an event trigger on deleting any Amazon S3 object**. The event invokes an Amazon SNS notification via email to the IT manager - Sending an event trigger after object deletion does not meet the objective of preventing object deletion by mistake because the object has already been deleted. So, this option is incorrect.

**Establish a process to get managerial approval for deleting Amazon S3 objects** - This option for getting managerial approval is just a distractor.

**Change the configuration on Amazon S3 console so that the user needs to provide additional confirmation while deleting any Amazon S3 object** - There is no provision to set up Amazon S3 configuration to ask for additional confirmation before deleting an object. This option is incorrect.

## Question 6
- A retail company uses **EC2 instances**, **API Gateway**, **RDS**, **Elastic Load Balancer** and **CloudFront.**
- To improve the security, the Risk Advisory group has suggested a feasibility check for using the **GuardDuty** service.

Which of the following would you identify as *data sources* supported by Amazon GuardDuty?

**Options**
- Amazon CloudFront logs, Amazon API Gateway logs, AWS CloudTrail events
- VPC Flow Logs, Amazon API Gateway logs, Amazon S3 access logs
- VPC Flow Logs, Domain Name System (DNS) logs, AWS CloudTrail events
- Elastic Load Balancing logs, Domain Name System (DNS) logs, AWS CloudTrail events

**Solution**
- VPC Flow Logs, Domain Name System (DNS) logs, AWS CloudTrail events
    - #guard-duty

**Wrong**


## Question 7
- An **organization** wants to delegate access to a **set of users** from the **development environment** so that they can access some resources in the **production** environment which is managed under **another AWS account**.

**Options**
- Create a new IAM role with the required permissions to access the resources in the production environment. The users can then assume this IAM role while accessing the resources from the production environment
- It is not possible to access cross-account resources
- Create new IAM user credentials for the production environment and share these credentials with the set of users from the development environment
- Both IAM roles and IAM users can be used interchangeably for cross-account access


**Solution**
- Create a new IAM role with the required permissions to access the resources in the production environment. The users can then assume this IAM role while accessing the resources from the production environment #iam-role


**Wrong**
- *Create new IAM user credentials for the production environment and share these credentials with the set of users from the development environment* - There is no need to create new **IAM user credentials** for the production environment, as you can use IAM roles to access cross-account resources.

- *It is not possible to access cross-account resources* - You can use IAM roles to access cross-account resources.

- *Both IAM roles and IAM users can be used interchangeably for cross-account access* - IAM roles and IAM users are separate IAM entities and should not be mixed. Only IAM roles can be used to access cross-account resources.


## Question 8
#api-gateway
- Both **stateful** and **stateless** client-server communications via the application programming interface (APIs) developed using its platform.
- Build a solution to fulfill this market need using *API Gateway*.

Which of the following would you identify as correct?


**Options**
- Amazon API Gateway creates RESTful APIs that enable stateful client-server communication and Amazon API Gateway also creates WebSocket APIs that adhere to the WebSocket protocol, which enables stateless, full-duplex communication between client and server
- Amazon API Gateway creates RESTful APIs that enable stateful client-server communication and Amazon API Gateway also creates WebSocket APIs that adhere to the WebSocket protocol, which enables stateful, full-duplex communication between client and server
- Amazon API Gateway creates RESTful APIs that enable stateless client-server communication and Amazon API Gateway also creates WebSocket APIs that adhere to the WebSocket protocol, which enables stateful, full-duplex communication between client and server
- Amazon API Gateway creates RESTful APIs that enable stateless client-server communication and Amazon API Gateway also creates WebSocket APIs that adhere to the WebSocket protocol, which enables stateless, full-duplex communication between client and server


**Solution**
- Amazon API Gateway creates RESTful APIs that enable stateful client-server communication and Amazon API Gateway also creates WebSocket APIs that adhere to the WebSocket protocol, which enables stateful, full-duplex communication between client and server

**Wrong**

## Question 9
- Provisioned an **EC2 instance 1A** which is running in *Region A*.
- Later, takes a snapshot of the instance 1A and then creates a new **AMI** in *Region A* from this snapshot.
- This AMI is then copied into another *Region B*.
- The founder provisions an instance 1B in *Region B* using this new AMI in Region B.

At this point in time,   what entities exist in Region B?


**Options**
- 1 Amazon EC2 instance and 1 AMI exist in Region B
- 1 Amazon EC2 instance and 1 snapshot exist in Region B
- 1 Amazon EC2 instance, 1 AMI and 1 snapshot exist in Region B
- 1 Amazon EC2 instance and 2 AMIs exist in Region B


**Solution**
- 1 Amazon EC2 instance, 1 AMI and 1 snapshot exist in Region B #ami
    - When copied from Region A into Region B, it automatically creates a snapshot in Region B because AMIs are **based on the underlying snapshots**. Further, an instance is created from this AMI in Region B.  #ebs-snapshot


**Wrong**


## Question 10
- The blogger has created a test file of size 1 gigabytes with some random data.
- Next he copies this test file into AWS S3 Standard storage class, provisions an Amazon EBS volume (General Purpose SSD (gp2)) with 100 gigabytes of provisioned storage and copies the test file into the Amazon EBS volume, and lastly copies the test file into an Amazon EFS Standard Storage filesystem.
- At the end of the month, he analyses the bill for costs incurred on the respective storage types for the test file.

What is the correct order of the storage charges incurred for the test file on these three storage types?


**Options**
- Cost of test file storage on Amazon EBS < Cost of test file storage on Amazon S3 Standard < Cost of test file storage on Amazon EFS
- Cost of test file storage on Amazon S3 Standard < Cost of test file storage on Amazon EFS < Cost of test file storage on Amazon EBS
- Cost of test file storage on Amazon S3 Standard < Cost of test file storage on Amazon EBS < Cost of test file storage on Amazon EFS
- Cost of test file storage on Amazon EFS < Cost of test file storage on Amazon S3 Standard < Cost of test file storage on Amazon EBS


**Solution**
- Cost of test file storage on Amazon S3 Standard < Cost of test file storage on Amazon EFS < Cost of test file storage on Amazon EBS
    - EFS Standard Storage pricing is $0.30 per GB per month. Therefore the cost for storing the test file on EFS is $0.30 for the month.#efs
    - EBS General Purpose SSD (gp2) volumes, the charges are $0.10 per GB-month of provisioned storage. Therefore, for a provisioned storage of **100GB for this use-case**, the monthly cost on EBS is $0.10*100 = $10. This cost is irrespective of how much storage is actually consumed by the test file. #ebs
    - S3 Standard storage, the pricing is $0.023 per GB per month. Therefore, the monthly storage cost on S3 for the test file is $0.023. #s3

**Wrong**
