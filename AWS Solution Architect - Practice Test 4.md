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

# Question 9
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
