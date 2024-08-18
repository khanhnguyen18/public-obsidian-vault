# AWS Solution Architect

## Link

```shell
open "/Users/P836088/project/markdown-documents/work/AWS/AWS-Certified-Solutions-Architect-Slides-v37.pdf"
```

## AWS_Organization
- AWS Organizations helps you centrally govern your environment as you grow and scale your workloads on AWS. 
- You can automate account creation, create groups of accounts to reflect your business needs, and apply policies for these groups for governance. You can also simplify billing by setting up a single payment method for all of your AWS accounts. 
- Through integrations with other AWS services, you can use Organizations to define central configurations and resource sharing across accounts in your organization.
### AWS_Organization_SCP
- One type of policy that you can use to manage your organization. 
- SCPs offer central control over the maximum available permissions for all accounts in your organization, allowing you to ensure your accounts stay within your organization’s access control guidelines. 
- SCPs are available only in an organization that has all features enabled. 
- SCPs aren't available if your organization has enabled only the consolidated billing features. 
- Attaching an SCP to an AWS Organizations entity (root, OU, or account) defines a guardrail for what actions the principals can perform. 

- In service control policy (SCP), you can restrict which AWS services, resources, and individual API actions the users and roles in each member account can access. You can also define conditions for when to restrict access to AWS services, resources, and API actions. *These restrictions even override the administrators of member accounts in the organization.*

*Please note the following effects on permissions vis-a-vis the service control policy (SCP)*:
  - If a user or role has an IAM permission policy that grants access to an action that is either not allowed or explicitly denied by the applicable service control policy (SCP), the user or role can't perform that action.
  - Service control policy (SCP) affects all users and roles in the member accounts, including root user of the member accounts.
  - Service control policy (SCP) does not affect any service-linked role.



## IAM

- Global service
- Root account use
- Policies is define permission of user
- Apply least previledge principle

### IAM_Permissions_Boundaries
- AWS supports permissions boundaries for IAM entities (users or roles). A permissions boundary is an advanced feature for using a managed policy to set the maximum permissions that an identity-based policy can grant to an IAM entity. An entity's permissions boundary allows it to perform only the actions that are allowed by both its identity-based policies and its permissions boundaries. Here we have to use an IAM permission boundary. They can only be applied to roles or users, not IAM groups.
- ![](https://assets-pt.media.datacumulus.com/aws-saa-pt/assets/pt2-q39-i1.jpg)

### IAM_Role
![](https://assets-pt.media.datacumulus.com/aws-saa-pt/assets/pt2-q3-i1.jpg)

- Applications that run on an EC2 must include AWS credentials in their AWS API requests.
  - Could store AWS credentials directly within the EC2 and allow applications in that instance to use those credentials.
  -  But have to manage the credentials and ensure that they securely pass the credentials to each instance and update each EC2 when it's time to rotate the credentials.

-> *IAM role to manage temporary credentials for applications that run on an EC2*.
  - When you use a role, you don't have to distribute long-term credentials (such as a username and password or access keys) to an EC2. 
  - The role supplies temporary permissions that applications can use when they make calls to other AWS resources. When you launch an EC2, you specify an IAM role to associate with the instance. 
  - Applications that run on the instance can then use the role-supplied temporary credentials to sign API requests. 

- AWS supports six types of policies: 
  1. identity-based policies
  2. resource-based policies,
  3. permissions boundaries, 
  4. service control policy (SCP)of AWS Organizations,
  5. access control list (ACL), 
  6. session policies.


### AWS_IAM_Authorization
 - For consumers who currently are located within your AWS environment or have the means to retrieve (IAM) temporary credentials to access your environment, you can use AWS_IAM authorization and add least-privileged permissions to the respective IAM role to securely invoke your API.
 - API Gateway API Keys is not a security mechanism and should not be used for authorization unless it’s a public API. 
 - It should be used primarily to track a consumer’s usage across your API.

## Section 5

### 30. AWS Budget setup


## ECS
- fully managed container orchestration service. ECS allows you to easily run, scale, and secure Docker container applications on AWS.
  ![](https://d1.awsstatic.com/Product-Page-Diagram_Amazon-Elastic-Container-Service%20march%202023.6ee17a3146661f893bf1ee674aceb65efdf864bd.png)
- With the Fargate launch type, you pay for the amount of vCPU and memory resources that your containerized application requests. vCPU and memory resources are calculated from the time your container images are pulled until the Amazon ECS Task terminates, rounded up to the nearest second.
- With the EC2 launch type, there is no additional charge for the EC2 launch type. You pay for AWS resources (e.g. EC2 instances or EBS volumes) you create to store and run your application.

## Amazon Inspector
- security assessments help you check for unintended network accessibility of your EC2s and for vulnerabilities on those EC2 instances.
-  Amazon Inspector assessments are offered to you as pre-defined rules packages mapped to common security best practices and vulnerability definitions.

## WAF
![](https://d1.awsstatic.com/products/WAF/product-page-diagram_AWS-WAF_How-it-Works@2x.452efa12b06cb5c87f07550286a771e20ca430b9.png)
- a web application firewall service that lets you monitor web requests and protect your web applications from malicious requests.
- Use AWS WAF to block or allow requests based on conditions that you specify, such as the IP addresses.
- You can also use AWS WAF preconfigured protections to block common attacks like SQL injection or cross-site scripting.
- You can use AWS WAF with your Application Load Balancer to allow or block requests based on the rules in a web access control list (web ACL). Geographic (Geo) Match Conditions in AWS WAF allows you to use AWS WAF to restrict application access based on the geographic location of your viewers. With geo match conditions you can choose the countries from which AWS WAF should allow access.
- Geo match conditions are important for many customers. For example, legal and licensing requirements restrict some customers from delivering their applications outside certain countries. These customers can configure a whitelist that allows only viewers in those countries. Other customers need to prevent the downloading of their encrypted software by users in certain countries. These customers can configure a blacklist so that end-users from those countries are blocked from downloading their software.
## Event_Bridge
- This event-based service is extremely useful for connecting non-AWS SaaS (Software as a Service) services to AWS services. 
- With Amazon Eventbridge, the downstream application would need to immediately process the events whenever they arrive, thereby making it a tightly coupled scenario.

## EC2
### elastic-fabric-adapter-efa
![](https://d1.awsstatic.com/Product-Page-Diagram_Elastic-Fabric-Adapter_How-it-Works_updated.2a51303e17a203eb094ab098ebc31a61dab66365.png)
- **A network device** that you can attach to your Amazon EC2 instance to accelerate High Performance Computing (HPC) and machine learning applications. 
- It enhances the performance of inter-instance communication that is critical for scaling HPC and machine learning applications. 
- EFA devices provide all *Elastic Network Adapter (ENA)* devices functionalities plus a new OS bypass hardware interface that allows user-space applications to communicate directly with the hardware-provided reliable transport functionality.


### EC2_instance_recover
-https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-instance-recover.htmld

You can create an Amazon CloudWatch alarm to automatically recover the Amazon EC2 instance if it becomes impaired due to an underlying hardware failure or a problem that requires AWS involvement to repair. 
- Terminated instances cannot be recovered. 
- A recovered instance is identical to the original instance, including the instance ID, private IP addresses, Elastic IP addresses, and all instance metadata. 
- If the impaired instance is in a placement group, the recovered instance runs in the placement group. 
- If your instance has a public IPv4 address, it retains the public IPv4 address after recovery. 
- During instance recovery, the instance is migrated during an instance reboot, and any data that is in-memory is lost.

- If your instance fails a system status check, you can use *Amazon CloudWatch alarm* actions to automatically recover it. The recover option is available for over 90% of deployed customer Amazon EC2 instances.
- The Amazon CloudWatch recovery option works only for system check failures, not for instance status check failures. Also, if you terminate your instance, then it can't be recovered.
- You can create an *Amazon CloudWatch alarm* that monitors an Amazon EC2 instance and automatically recovers the instance if it becomes impaired due to an underlying hardware failure or a problem that requires AWS involvement to repair. 
- Terminated instances cannot be recovered. d
- The automatic recovery process attempts to recover your instance for up to three separate failures per day. 
- Your instance may subsequently be retired if automatic recovery fails and a hardware degradation is determined to be the root cause for the original system status check failure.




### EC2_Default_Termination_Policy
![](https://assets-pt.media.datacumulus.com/aws-saa-pt/assets/pt2-q65-i1.jpg)
Following the order:
1. On-Demand vs Spot instances. 
2. instance with the oldest launch template unless there is an instance that uses a launch configuration(A)
3. Next, you need to consider any instance which has the oldest launch configuration.(B) 
4. Closest to the next billing hour(D)
### EC2_Hibernate
- When you hibernate an instance, AWS signals the operating system to perform hibernation (suspend-to-disk).
-  Hibernation saves the contents from 
   -  the instance memory (RAM) to your Amazon EBS root volume. 
-  AWS then persists the instance's Amazon EBS root volume and any attached Amazon EBS data volumes.
- When you start your instance:
  - The Amazon EBS root volume is restored to its previous state
  - The RAM contents are reloaded
  - The processes that were previously running on the instance are resumed

Previously attached data volumes are reattached and the instance retains its instance ID

![Link](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/images/hibernation-flow.png)
### EC2_Launch_Configuration
- Instance configuration template that an *Auto Scaling group* uses to launch EC2 instances. 
- When you create a launch configuration, you specify information for the instances such as the ID of the Amazon Machine Image (AMI), the instance type, a key pair, one or more security groups, and a block device mapping.


### EC2_Launch_Template
- A launch template is similar to a launch configuration, in that it specifies instance configuration information such as the ID of the Amazon Machine Image (AMI), the instance type, a key pair, security groups, and the other parameters that you use to launch EC2 instances. 

- Also, defining a launch template instead of a launch configuration allows you to have multiple versions of a template.

- With launch templates, you can provision capacity across multiple instance types using both On-Demand Instances and Spot Instances to achieve the desired scale, performance, and cost. 

- When you create a Launch Template, the default value for the instance tenancy is shared and the instance tenancy is controlled by the tenancy attribute of the VPC. If you set the Launch Template Tenancy to shared (default) and the VPC Tenancy is set to dedicated, then the instances have dedicated tenancy. If you set the Launch Template Tenancy to dedicated and the VPC Tenancy is set to default, then again the instances have dedicated tenancy.

Amazon EC2 provides three options for the tenancy of your EC2 instances:
  1. *Shared (Shared)* – Multiple AWS accounts may share the same physical hardware. This is the default tenancy option when launching an instance.
  2. *Dedicated instances (Dedicated)* – Your instance runs on single-tenant hardware. No other AWS customer shares the same physical server.
  3. *Dedicated Hosts (Dedicated host)* – The instance runs on a physical server that is dedicated to your use. Using Dedicated Hosts makes it easier to bring your own licenses (BYOL) that have dedicated hardware requirements to EC2 and meet compliance use cases. If you choose this option, you must provide a host resource group for Tenancy host resource group.

### EC2_Placement_Group
- Depending on the type of workload, you can create a placement group using one of the following placement strategies:
  - Cluster 
    - Packs instances close together inside an AZ. ![](https://assets-pt.media.datacumulus.com/aws-saa-pt/assets/pt2-q12-i1.jpg)
    - This strategy enables workloads to achieve the low-latency network performance necessary for tightly-coupled node-to-node communication that is typical of high-performance computing (HPC) applications.
  - Partition:
    - do not share underlying harware with groups instances(Kafka, Hadoop , Cassandra)
    - A partition placement group can have a maximum of seven partitions per AZ
    ![Partition](https://assets-pt.media.datacumulus.com/aws-saa-pt/assets/pt2-q12-i2.jpg)
  - Spead: 
    - Strictly place small group of intances accross distince underlying harware to reduce correlated failures.
  ![](https://assets-pt.media.datacumulus.com/aws-saa-pt/assets/pt2-q12-i3.jpg)
- More information: https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/placement-groups.html

  ### EC2 - Intance store
- Provides temporary block-level storage for your instance.
- This storage is located on disks that are physically attached to the host instance.
- Instance store is ideal for the temporary storage of information that changes frequently such as buffers, caches, scratch data, and other temporary content, or for data that is replicated across a fleet of instances, such as a load-balanced pool of web servers.
- Instance store volumes are included as part of the instance's usage cost.

As Instance Store based volumes provide high random I/O performance at low cost (as the storage is part of the instance's usage cost) and the resilient architecture can adjust for the loss of any instance, therefore you should use Instance Store based EC2s for this use-case.
- Instance store is ideal for the temporary storage of information that changes frequently such as buffers, caches, scratch data, and other temporary content, or for data that is replicated across a fleet of instances, such as a load-balanced pool of web servers


## Tenancy_Value
![](https://assets-pt.media.datacumulus.com/aws-saa-pt/assets/pt4-q16-i1.jpg)
By default, Amazon EC2 instances run on a shared-tenancy basis.
- Dedicated Instances are Amazon EC2 instances that run in a virtual private cloud (VPC) on hardware that's dedicated to a single customer. Dedicated Instances that belong to different AWS accounts are physically isolated at the hardware level. However, Dedicated Instances may share hardware with other instances from the same AWS account that is not Dedicated Instances.

- A Dedicated Host is also a physical server that's dedicated to your use. With a Dedicated Host, you have visibility and control over how instances are placed on the server.
- You can only change the tenancy of an instance from dedicated to host, or from host to dedicated after you've launched 


### EC2-Intancetype



![](https://assets-pt.media.datacumulus.com/aws-saa-pt/assets/pt2-q35-i1.jpg)

- https://aws.amazon.com/ec2/pricing/

#### EC2_Dedicated_Hosts
- A Dedicated Host is a physical EC2 server fully dedicated for your use. Dedicated Hosts can help you reduce costs by allowing you to use your existing server-bound software licenses, including Windows Server, SQL Server, and SUSE Linux Enterprise Server (subject to your license terms). Dedicated Hosts can be purchased On-Demand (hourly) or can be purchased as part of Savings Plans.
- A Dedicated Host is also a physical server that's dedicated for your use. With a Dedicated Host, you have visibility and control over how instances are placed on the server.
#### EC2_Dedicated_Instance 
![](https://assets-pt.media.datacumulus.com/aws-saa-pt/assets/pt2-q23-i1.jpg)
- Run in a virtual private cloud (VPC) on hardware that's dedicated to a single customer. 
- Dedicated Instances that belong to different AWS accounts are physically isolated at a hardware level, even if those accounts are linked to a single-payer account. 
- However, Dedicated Instances may share hardware with other instances from the same AWS account that are not Dedicated Instances.
- Could share with instance in same account

#### EC2_On_Demand

#### EC2_Reserve_Instances

#### EC2_Spot_Instances
![](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/images/spot_lifecycle.png)
- A Spot Instance is an unused Amazon EC2 instance that is available for less than the On-Demand price.
-  Your Spot Instance runs whenever capacity is available and the maximum price per hour for your request exceeds the Spot price. 
-  Any instance present with unused capacity will be allocated. Even though this is cost-effective, it does not fulfill the single-tenant hardware requirement of the client and hence is not the correct option.
-  Because Spot Instances enable you to request unused Amazon EC2 instances at steep discounts, you can lower your Amazon EC2 costs significantly.
-  The hourly price for a Spot Instance is called a Spot price
- A Spot Instance request is either one-time or persistent. If the spot request is persistent, the request is opened again after your Spot Instance is interrupted. If the request is persistent and you stop your Spot Instance, the request only opens after you start your Spot Instance.
 

#### EC2_Spot_Fleet
![](https://assets-pt.media.datacumulus.com/aws-saa-pt/assets/pt2-q49-i1.jpg)
- *Spot Fleets can maintain target capacity by launching replacement instances after Spot Instances in the fleet are terminated*
  - A Spot Fleet is a set of Spot Instances and optionally On-Demand Instances that is launched based on criteria that you specify. T
  - The Spot Fleet selects the Spot capacity pools that meet your needs and launches Spot Instances to meet the target capacity for the fleet. 
  - By default, Spot Fleets are set to maintain target capacity by launching replacement instances after Spot Instances in the fleet are terminated. 
  - You can submit a Spot Fleet as a one-time request, which does not persist after the instances have been terminated. You can include On-Demand Instance requests in a Spot Fleet request.
- *When you cancel an active spot request, it does not terminate the associated instance*
  - If your Spot Instance request is active and has an associated running Spot Instance, or your Spot Instance request is disabled and has an associated stopped Spot Instance, canceling the request does not terminate the instance; you must terminate the running Spot Instance manually. Moreover, to cancel a persistent Spot request and terminate its Spot Instances, you must cancel the Spot request first and then terminate the Spot Instances.
- *If a spot request is persistent, then it is opened again after your Spot Instance is interrupted*
  - A Spot Instance request is either one-time or persistent. If the spot request is persistent, the request is opened again after your Spot Instance is *interrupted*. If the request is persistent and you stop your Spot Instance, the request only opens after you start your Spot Instance.


The Spot Fleet selects the Spot Instance pools that meet your needs and launches Spot Instances to meet the target capacity for the fleet. By default, Spot Fleets are set to maintain target capacity by launching replacement instances after Spot Instances in the fleet are terminated.

A Spot Instance is an unused Amazon EC2 instance that is available for less than the On-Demand price. Spot Instances provide great cost efficiency, but we need to select an instance type in advance. In this case, we want to use the most cost-optimal option and leave the selection of the cheapest spot instance to a Spot Fleet request, which can be optimized with the lowestPrice strategy. So this is the correct option

## EBS
- An easy to use, high-performance block storage service designed for use with Amazon Elastic Compute Cloud (EC2) for both throughput and transaction-intensive workloads at any scale.
- Amazon EBS volume types fall into two categories:
  1. Solid state drive (SSD) backed volumes optimized for transactional workloads involving frequent read/write operations with small I/O size, where the dominant performance attribute is IOPS.
  2. Hard disk drive (HDD) backed volumes optimized for large streaming workloads where throughput (measured in MiB/s) is a better performance measure than IOPS.
- You can't use st1 or sc1 EBS volumes as root volumes.
## EFS
![](https://d1.awsstatic.com/r2018/b/EFS/product-page-diagram-Amazon-EFS-Launch_How-It-Works.cf947858f0ef3557b9fc14077bdf3f65b3f9ff43.png)
- Provides a simple, scalable, fully managed *Elastic NFS file system* for use with
  -  AWS Cloud services
  -  On-premises resources.
  
- EFS is a **file storage service** for use 
  - Amazon compute (EC2, containers, serverless) 
  - on-premises servers. 
- Amazon EFS provides:
  - a file system interface
  - file system access semantics (such as strong consistency and file locking), 
  - concurrently accessible storage for up to thousands of EC2s.

- Storing data within and across AZs for high availability and durability
- EC2 instances can access your file system across AZs, regions, and VPCs
- On-premises servers can access using AWS Direct Connect or AWS VPN.

### EFS_Throuhput_Mode
- *With Bursting Throughput mode*, throughput on Amazon EFS scales as the size of your file system in the standard storage class grow
- *With Provisioned Throughput mode*, you can instantly provision the throughput of your file system (in MiB/s) independent of the amount of data stored.
### EFS_Performance_Mode
![](https://assets-pt.media.datacumulus.com/aws-saa-pt/assets/pt2-q64-i1.jpg)
- *General Purpose performance mode* is ideal for latency-sensitive use cases, like web serving environments, content management systems, home directories, and general file serving. If you don't choose a performance mode when you create your file system, Amazon EFS selects the General Purpose mode for you by default.
-*Max I/O performance mode* is used to scale to higher levels of aggregate throughput and operations per second. This scaling is done with a tradeoff of slightly higher latencies for file metadata operations. Highly parallelized applications and workloads, such as big data analysis, media processing, and genomic analysis, can benefit from this mode.


### Efs_Standard_Ia
- Standard–IA storage class reduces storage costs for files that are not accessed every day.
- It does this without sacrificing the high availability, high durability, elasticity, and POSIX file system access that Amazon EFS provides. 
- AWS recommends Standard-IA storage if you need your full dataset to be readily accessible and want to automatically save on storage costs for files that are less frequently accessed.

### Efs_Infrequent_Access
- Storage class that provides price/performance that is cost-optimized for files, not accessed every day, with storage prices up to **92% lower compared to Amazon EFS Standard**
## 69. High Availability and Scalability

* High Avallability usually goes hand in hand with horizontal
* High availability means running your application / system in at least 2 data centers == AZ)

• Horizontal Scaling: Increase number of instances 😊 scale out / in)

* Auto Scaling Group
* Load Balancer

• High Availability:

* Run instances for the same application across multi AZ
* Auto Scaling Group multi AZ

## ELB
- ELB and Global Accelerator solve the challenge of routing user requests to healthy application endpoints.
-  AWS Global Accelerator relies on ELB to provide the traditional load balancing features such as support for internal and non-AWS endpoints, pre-warming, and Layer 7 routing.
- Provides load balancing within one Region, AWS Global Accelerator provides traffic management across multiple Regions.
- Include
  - ALB
  - NLB
### ELB_Idle_Timeout
  - For each request that a client makes through Elastic Load Balancing, the load balancer maintains two connections. 
  - The front-end connection is between the client and the load balancer. 
  - The back-end connection is between the load balancer and a registered Amazon EC2 instance. 
  - The load balancer has a configured "idle timeout" period that applies to its connections. If no data has been sent or received by the time that the "idle timeout" period elapses, the load balancer closes the connection. 
### ELB_Sticky_Sessions
  - You can use the sticky session feature (also known as session affinity) to enable the load balancer to bind a user's session to a specific instance. 
  - This ensures that all requests from the user during the session are sent to the same instance. 
### ELB_CrossZoneLoadBalancing
![](https://docs.aws.amazon.com/elasticloadbalancing/latest/userguide/images/cross_zone_load_balancing_enabled.png)
- If cross-zone load balancing is disabled:
  + Each of the two targets in Availability Zone A receives 25% of the traffic.
  + Each of the eight targets in Availability Zone B receives 6.25% of the traffic.
This is because each load balancer node can route its 50% of the client traffic only to targets in its Availability Zone

  - The nodes for your load balancer distribute requests from clients to registered targets.
  -  When cross-zone load balancing is enabled, each load balancer node distributes traffic across the registered targets in all enabled Availability Zones (AZs). 
### EBL_Connection_Draining
- To ensure that Elastic Load Balancing stops sending requests to instances that are de-registering or unhealthy while keeping the existing connections open, use connection draining. 
- This enables the load balancer to complete in-flight requests made to instances that are de-registering or unhealthy. 
- The maximum timeout value can be set between 1 and 3,600 seconds (the default is 300 seconds). When the maximum time limit is reached, the load balancer forcibly closes connections to the de-registering instance.

### NLB
- A Network Load Balancer functions at the fourth layer of the Open Systems Interconnection (OSI) model. 
- It can handle millions of requests per second. After the load balancer receives a connection request, it selects a target from the target group for the default rule. 
- It attempts to open a TCP connection to the selected target on the port specified in the listener configuration.
#### NLB_Request_Routing_and_IP_Addresses:
  - If you specify targets using an instance ID, traffic is routed to instances using the *primary private IP* address specified in the *primary network interface* for the instance. The load balancer rewrites the destination IP address from the data packet before forwarding it to the target instance.
  - If you specify targets using *IP addresses*, you can route traffic to an instance using any *private IP address* from one or more network interfaces. This enables multiple applications on an instance to use the same port. Note that each network interface can have its security group. The load balancer rewrites the destination IP address before forwarding it to the target.
### ALB

- The Application Load Balancer (ALB) is best suited for load balancing HTTP and HTTPS traffic and provides advanced request routing targeted at the delivery of modern application architectures, including microservices and containers. Operating at the individual request level (Layer 7), the Application Load Balancer routes traffic to targets within Amazon Virtual Private Cloud (Amazon VPC) based on the content of the request.
- This is the correct option since the question has a specific requirement for content-based routing which can be configured via the Application Load Balancer. Different Availability Zones (AZs) provide high availability to the overall architecture and Auto Scaling group will help mask any instance failures.


#### ALB_with_Cognito_User_Pools
![](https://assets-pt.media.datacumulus.com/aws-saa-pt/assets/pt2-q17-i1.jpg)
- Application Load Balancer can be used to securely authenticate users for accessing your applications. This enables you to offload the work of authenticating users to your load balancer so that your applications can focus on their business logic. You can use Cognito User Pools to authenticate users through well-known social IdPs, such as Amazon, Facebook, or Google, through the user pools supported by Amazon Cognito or through corporate identities, using SAML, LDAP, or Microsoft AD, through the user pools supported by Amazon Cognito

#### Content-Based Routing
- ALB has access to HTTP headers and allows you to route requests to different backend services accordingly.
- For example, you might want to send requests that include /api in the URL path to one group of servers (we call these target groups) and requests that include /mobile to another.
- Routing requests in this fashion allows you to build applications that are composed of multiple microservices that can run and be scaled independently.
- As you will see in a moment, each Application Load Balancer allows you to define up to 10 URL-based rules to route requests to target groups. Over time, we plan to give you access to other routing methods.


## Private_Link
- Simplifies the security of data shared with cloud-based applications by eliminating the exposure of data to the public Internet. 
- Provides private connectivity between VPCs, AWS services, and on-premises applications, securely on the Amazon network. 
- Private Link is utilized to create a private connection between an application that is fronted by an NLB in an account, and an Elastic Network Interface (ENI) in another account, without the need of VPC peering, and allowing the connections between the two to remain within the AWS network.
- Private Link is leveraged to create a private connection between an application that is fronted by an NLB in an account, and ENI in another account, without the need of VPC peering and allowing the connections between the two to remain within the AWS network.

### VPC_Endpoint
- VPC endpoints for Amazon SQS are powered by AWS PrivateLink, a highly available, scalable technology that enables you to privately connect your VPC to supported AWS services.
- AWS customers can access Amazon Simple Queue Service (Amazon SQS) from their Amazon Virtual Private Cloud (Amazon VPC) using VPC endpoints, without using public IPs, and without needing to traverse the public internet
- Amazon VPC endpoints are easy to configure. They also provide reliable connectivity to Amazon SQS without requiring an internet gateway, Network Address Translation (NAT) instance, VPN connection, or AWS Direct Connect connection. With VPC endpoints, the data between your Amazon VPC and Amazon SQS queue is transferred within the Amazon network, helping protect your instances from internet traffic.
- AWS PrivateLink simplifies the security of data shared with cloud-based applications by eliminating the exposure of data to the public Internet. AWS PrivateLink provides private connectivity between VPCs, AWS services, and on-premises applications, securely on the Amazon network. AWS PrivateLink makes it easy to connect services across different accounts and VPCs to significantly simplify the network architecture.
  


## AWS_Config
- ![AWS_Config](https://assets-pt.media.datacumulus.com/aws-saa-pt/assets/pt2-q9-i2.jpg)
- provides a detailed view of the configuration of AWS resources in your AWS account. This includes how the resources are related to one another and how they were configured in the past so that you can see how the configurations and relationships change over time.
- AWS Config provides AWS-managed rules, which are predefined, customizable rules that AWS Config uses to evaluate whether your AWS resources comply with common best practices. You can leverage an AWS Config managed rule to check if any ACM certificates in your account are marked for expiration within the specified number of days. Certificates provided by ACM are automatically renewed. ACM does not automatically renew the certificates that you import. The rule is NON_COMPLIANT if your certificates are about to expire.
## AWS_Certificate_Manager
- service that lets you easily provision, manage, and deploy public and private SSL/TLS certificates for use with AWS services and your internal connected resources. 
- SSL/TLS certificates are used to secure network communications and establish the identity of websites over the Internet as well as resources on private networks.

## AWS_Transit_Gateway

- Is a service that enables customers to connect their Amazon Virtual Private Clouds (VPCs) and their on-premises networks to a single gateway


- Without AWS Transit Gateway 
![](https://d1.awsstatic.com/product-marketing/transit-gateway/tgw-before.7f287b3bf00bbc4fbdeadef3c8d5910374aec963.png)
- With AWS Transit Gateway:
  ![](https://d1.awsstatic.com/product-marketing/transit-gateway/tgw-after.d85d3e2cb67fd2ed1a3be645d443e9f5910409fd.png)

- Cannot establish a low latency and high throughput connection between a data center and AWS Cloud.

## VPC_Peering
- A networking connection between two VPCs that enables you to route traffic between them using private IPv4 addresses or IPv6 addresses. 
- Instances in either VPC can communicate with each other as if they are within the same network. 
- You can create a VPC peering connection between your VPCs, or with a VPC in another AWS account. 
- The VPCs can be in different regions (also known as an inter-region VPC peering connection). VPC peering connections will work, but won't efficiently scale if you add more accounts (you'll have to create many connections).
- VPC could can be in different regions
## RAM
![RAM](https://d1.awsstatic.com/products/RAM/product-page-diagram_AWS-Resource-Access-Manager(1).379df75d48a8e2cc6160859b7ca3626a9b9be0c1.png)
- AWS Resource Access Manager (RAM) is a service that enables share AWS resources with 
  - any AWS account 
  - within your AWS Organization. 
- You can share:
  - AWS Transit Gateways
  - Subnets
  - AWS License Manager configurations
  - Amazon Route 53 Resolver rules resources with RAM. 
- RAM eliminates the need to create duplicate resources in multiple accounts, reducing the operational overhead of managing those resources in every single account you own.
-  You can create resources centrally in a multi-account environment, and use RAM to share those resources across accounts in three simple steps: 
   -  create a Resource Share
   -  Specify resources
   -  Specify accounts. 
-  RAM is available to you at no additional charge.
### VPC_Sharing
- VPC sharing (part of Resource Access Manager) allows multiple AWS accounts to create their application resources such as Amazon EC2 instances, Amazon RDS databases, Amazon Redshift clusters, and AWS Lambda functions, into shared and centrally-managed Amazon Virtual Private Clouds (VPCs). 
- To set this up, the account that owns the VPC (owner) shares one or more subnets with other accounts (participants) that belong to the same organization from AWS Organizations. A
- fter a subnet is shared, the participants can view, create, modify, and delete their application resources in the subnets shared with them. Participants cannot view, modify, or delete resources that belong to other participants or the VPC owner.

You can share Amazon VPCs to leverage the implicit routing within a VPC for applications that require a high degree of interconnectivity and are within the same trust boundaries. This reduces the number of VPCs that you create and manage while using separate accounts for billing and access control.

## AWS_DataSync
![DataSync](https://d1.awsstatic.com/Digital%20Marketing/House/Editorial/products/DataSync/Product-Page-Diagram_AWS-DataSync_On-Premises-to-AWS%402x.8769b9dea1615c18ee0597b236946cbe0103b2da.png)
- Online data transfer service that simplifies, automates, and accelerates copying large amounts of data between:
  - on-premises storage systems and AWS Storage services
  - AWS Storage services.
- You can use AWS DataSync to migrate data located on-premises, at the edge, or in other clouds to Amazon S3, Amazon EFS, Amazon FSx for Windows File Server, Amazon FSx for Lustre, Amazon FSx for OpenZFS, and Amazon FSx for NetApp ONTAP.

- Using task scheduling in AWS DataSync, you can periodically execute a transfer task from your source storage system to the destination. You can use the DataSync scheduled task to send the video files to the Amazon EFS file system every 24 hours.
- AWS DataSync fully automates the data transfer. It comes with retry and network resiliency mechanisms, network optimizations, built-in task scheduling, monitoring via the DataSync API and Console, and Amazon CloudWatch metrics, events, and logs that provide granular visibility into the transfer process. AWS DataSync performs data integrity verification both during the transfer and at the end of the transfer.
- 
## Auto_Scaling_Group




The goal of an Auto Scaling Group (ASG) is to:
• Scale out (add EC2 instances) to match an increased load
• Scale in (remove EC2 instances) to match a decreased load
• Ensure we have a minimum and a maximum number of EC2 instances running
• Automatically register new instances to a load balancer
• Re-create an EC2 instance in case a previous one is terminated (ex: if unhealthy)

Auto Scaling - CloudWatch Alarms & Scaling
• It is possible to scale an ASG based on CloudWatch alarms
• An alarm monitors a metric (such as Average CPU, or a custom metric)
• Metrics such as Average CPU are computed for the overall ASG instances

### ASG_Not_terminate
- *ASG* doesn't terminate an instance that came into service based on *EC2* and *ELB* health checks until the health check grace period expires.
- immediately terminate instances with an *Impaired status*. Instead, Amazon EC2 Auto Scaling waits a few minutes for the instance to recover. Amazon EC2 Auto Scaling might also delay or not terminate instances that fail to report data for status checks. This usually happens when there is insufficient data for the status check metrics in Amazon CloudWatch.
- By default, ASG doesn't use the results of ELB health checks to determine an instance's health status when the group's health check configuration is set to EC2. As a result, Amazon EC2 Auto Scaling doesn't terminate instances that fail ELB health checks. If an instance's status is OutofService on the ELB console, but the instance's status is Healthy on the Amazon EC2 Auto Scaling console, confirm that the health check type is set to ELB.


## 88. Rds red rplicas vs Multiaz

* Network Cost
  * not pay fee for RDS read Rplca winthin in same region

## 91

Features of Aurora
• Automatic fail-over
• Backup and Recovery
• Isolation and security
• Industry compliance
• Push-button scaling
• Automated Patching with Zero Downtime
• Advanced Monitoring
• Routine Maintenance
• Backtrack: restore data at any point of time without using backups

## 93

## 98. Elastic Cache HandOn

* Security
  * Encryption Config
    * Transit
    * At rest
  * Security
* Cluster detail:
  * Primary Endpoint
  * Reader Endpoint

## 99. Elastic Cache for SA


## 101. Route 53








1. What is DNS and dd
   \[LINK\](This is a link)
   dns

## Question

* Subnet: Span all azs



* DNS Record  Time:

* Go to AWS Cloudshell
  * sudo yum install -y bind-utils
  * nslookup  test.steahan...
  * dig

## 105 EC2 setup

* Create 3 EC2
* Create load balancer

## 106 TTL(Time to live)

## 107. CNam and Alias

* Alias: Point hostname to aws resource
* CName not for apex record

## Route_53
- H highly available and scalable cloud Domain Name System (DNS) web service. 
- It is designed to give developers and businesses an extremely reliable and cost-effective way to route end users to Internet applications by translating names like www.example.com into the numeric IP addresses like 192.0.2.1 that computers use to connect to each other. 
### Router_53_Resolver
- By default, Amazon Route 53 Resolver automatically answers DNS queries for local VPC domain names for Amazon EC2 instances. You can integrate DNS resolution between Resolver and DNS resolvers on your on-premises network by configuring forwarding rules.
#### Router_53_Resolver_Inbound_Endpoint
![](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/images/Resolver-inbound-endpoint.png)
- To resolve any DNS queries for resources in the AWS VPC from the on-premises network, you can create an inbound endpoint on Amazon Route 53 Resolver and then DNS resolvers on the on-premises network can forward DNS queries to Amazon Route 53 Resolver via this endpoint.
#### Router_53_Resolver_Outbound_Endpoint
![](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/images/Resolver-outbound-endpoint.png)
- To resolve DNS queries for any resources in the on-premises network from the AWS VPC, you can create an outbound endpoint on Amazon Route 53 Resolver and then Amazon Route 53 Resolver can conditionally forward queries to resolvers on the on-premises network via this endpoint. To conditionally forward queries, you need to create Resolver rules that specify the domain names for the DNS queries that you want to forward (such as example.com) and the IP addresses of the DNS resolvers on the on-premises network that you want to forward the queries to.

### Record Type
#### DNS_Alias_Records
- **Alias** records provide Amazon Route 53–specific extension to DNS functionality. Alias records let you route traffic to selected AWS resources, such as Amazon CloudFront distributions and Amazon S3 buckets.
- You can create an alias record at the top node of a DNS namespace, also known as the zone apex, however, you cannot create a CNAME record for the top node of the DNS namespace. So, if you register the DNS name covid19survey.com, the zone apex is covid19survey.com. You can't create a CNAME record for covid19survey.com, but you can create an alias record for covid19survey.com that routes traffic to www.covid19survey.com.
- You should also note that Amazon Route 53 doesn't charge for alias queries to AWS resources but Route 53 does charge for CNAME queries. Additionally, an alias record can only redirect queries to selected AWS resources such as Amazon S3 buckets, Amazon CloudFront distributions, and another record in the same Amazon Route 53 hosted zone; however a CNAME record can redirect DNS queries to any DNS record. So, you can create a CNAME record that redirects queries from app.covid19survey.com to app.covid19survey.net.
### Routing_Policy
![](https://assets-pt.media.datacumulus.com/aws-saa-pt/assets/pt2-q6-i1.jpg)
#### Route53_Lantency_Routing
- Use latency based routing when you have resources in multiple AWS Regions and you want to route traffic to the region that provides the lowest latency
- To use latency-based routing, you create latency records for your resources in multiple AWS Region
- When Amazon Route 53 receives a DNS query for your domain or subdomain (example.com or acme.example.com), it determines which AWS Regions you've created latency records for, determines which region gives the user the lowest latency, and then selects a latency record for that region.
- Route 53 responds with the value from the selected record, such as the IP address for a web server.
#### Failover_Routing
- Failover routing lets you route traffic to a resource when the resource is healthy or to a different resource when the first resource is unhealthy. 
- The primary and secondary records can route traffic to anything from an Amazon S3 bucket that is configured as a website to a complex tree of records. 
#### Geolocation_Routing
- Geolocation routing lets you choose the resources that serve your traffic based on the geographic location of your users, meaning the location that DNS queries originate from. 
- For example, you might want all queries from Europe to be routed to an ELB load balancer in the Frankfurt region. 
- You can also use geolocation routing to restrict the distribution of content to only the locations in which you have distribution rights. 
- You cannot use geolocation routing to reduce latency, hence this option is incorrect.

## Network_ACL
- To enable the connection to a service running on an instance, the associated network ACL *must allow both inbound traffic on the port* that the service is listening on as well as allow outbound traffic from ephemeral ports. When a client connects to a server, a random port from the ephemeral port range (1024-65535) becomes the client's source port.
- By default, network ACLs allow all inbound and outbound traffic. If your network ACL is more restrictive, then you need to explicitly allow traffic from the ephemeral port range
- If you accept traffic from the internet, then you also must establish a route through an internet gateway. If you accept traffic over VPN or AWS Direct Connect, then you must establish a route through a virtual private gateway.

## DNS_Hosted_Zones
- DNS **hostnames** and **DNS resolution** are required settings for private hosted zones. DNS queries for private hosted zones can be resolved by the Amazon-provided VPC DNS server only. As a result, these options must be enabled for your private hosted zone to work.
- DNS hostnames: For non-default virtual private clouds that aren't created using the Amazon VPC wizard, this option is disabled by default. If you create a private hosted zone for a domain and create records in the zone without enabling DNS hostnames, private hosted zones aren't enabled. To use a private hosted zone, this option must be enabled.
  DNS resolution: Private hosted zones accept DNS queries only from a VPC DNS server. The IP address of the VPC DNS server is the reserved IP address at the base of the VPC IPv4 network range plus two. Enabling DNS resolution allows you to use the VPC DNS server as a Resolver for performing DNS resolution. Keep this option disabled if you're using a custom DNS server in the DHCP Options set, and you're not using a private hosted zone.
## Security_Group
- A security group acts as a virtual firewall that controls the traffic for one or more instances. 
- When you launch an instance, you can specify one or more security groups; otherwise -> default security group.
- Add rules to each security group that allows traffic to or from its associated instances.
- Modify the rules for a security group at any time; the new rules -> applied to all instances that are associated with the security group. 
*The following are the characteristics of security group rules*:
- By default, security groups allow all outbound traffic.
- Security group rules are always permissive; you can't create rules that deny access.
- Security groups are stateful

- [ec2-security-groups](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-security-groups.html)

## S3
- It is an object storage service that offers industry-leading scalability, data availability, security, and performance.
-  Your applications can easily achieve thousands of transactions per second in request performance when uploading and retrieving storage from Amazon S3.

* So3 looks like a global service but buckets are created in a region
* Prefix = Directory
* Bucket
* Object
  * Metadata
  * Tags
  * Version ID(if enable)
* Default encrytiokn
  * SSE-S3
  * KMS
### S3_LifeCycle
![](https://assets-pt.media.datacumulus.com/aws-saa-pt/assets/pt2-q34-i1.jpg)

### S3_Glacier
- **Amazon S3 Glacier and S3 Glacier Deep Archive** are a secure, durable, and extremely low-cost Amazon S3 cloud storage classes for data archiving and long-term backup. They are designed to deliver 99.999999999% durability and provide comprehensive security and compliance capabilities that can help meet even the most stringent regulatory requirements. Finally, Amazon S3 Glacier Deep Archive provides more cost savings than Amazon S3 Glacier.

- You can't move data directly from AWS Snowball into Amazon S3 Glacier, you need to go through Amazon S3 first, and then use a lifecycle policy. So this option is correct.
- https://aws.amazon.com/glacier/
### S3_Security
- User base
  - Which url could use for specific user
- Resource Base
  - Bucket Policies:
  - Object Access Controler LIst - Finer Grant
  - Bucket(ACL)

### S3_Enryption_Options
![](https://assets-pt.media.datacumulus.com/aws-saa-pt/assets/pt2-q10-i1.jpg)
- Options for protecting data at rest in Amazon S3:
  1. Server-Side Encryption
  2. Client-Side Encryption – Encrypt data client-side and upload the encrypted data to Amazon S3. In this case, you manage the encryption process, the encryption keys, and related tools.

#### Server_Side_Encryption
![Server_Side_Encryption](https://assets-pt.media.datacumulus.com/aws-saa-pt/assets/pt2-q50-i1.jpg)
 – The encryption of data at its destination by the application or service that receives it. Amazon S3 encrypts your data at the object level as it writes it to disks in its data centers and decrypts it for you when you access it.
###### Server_Side_Encryption_with_Customer_Provided_Keys 
- You manage the enrtyption Key
- S3 will encrypt

###### *Server-Side Encryption with Amazon S3 managed keys*(**Default**)
- Each object is encrypted with a unique key. 
- As an additional safeguard, it encrypts the key itself with a master key that it regularly rotates. So this option is incorrect.

###### SSE-KMS
- Amazon S3 SSE-KMS to encrypt your S3 object data. 
- Also, when SSE-KMS is requested for the object, the S3 checksum as part of the object's metadata, is stored in encrypted form.
- KMS key could rotate rotate automatically
 

4. *Client-Side Encryption with data encryption* 
- Done on the client-side before sending it to Amazon S3. You can encrypt the data client-side and upload the encrypted data to Amazon S3. 
- In this case, you manage the encryption process, the encryption keys, and related tools.


## Auto_scale_group_ags
#### Target_tracking_scaling_policy
![](https://assets-pt.media.datacumulus.com/aws-saa-pt/assets/pt4-q15-i2.jpg)
![](https://docs.aws.amazon.com/autoscaling/ec2/userguide/images/sqs-as-custom-metric-diagram.png)
- If you use a target tracking scaling policy based on a custom Amazon SQS queue metric, dynamic scaling can adjust to the demand curve of your application more effectively. 
- You may use an existing *CloudWatch Amazon SQS metric* like `ApproximateNumberOfMessagesVisible` for target tracking but you could still face an issue so that the number of messages in the queue might not change proportionally to the size of the Auto Scaling group that processes messages from the queue. The solution is to use a backlog per instance metric with the target value being the acceptable backlog per instance to maintain.

To calculate your backlog per instance, divide the ApproximateNumberOfMessages queue attribute by the number of instances in the InService state for the Auto Scaling group. Then set a target value for the Acceptable backlog per instance.

To illustrate with an example, let's say that the current ApproximateNumberOfMessages is 1500 and the fleet's running capacity is 10. If the average processing time is 0.1 seconds for each message and the longest acceptable latency is 10 seconds, then the acceptable backlog per instance is 10 / 0.1, which equals 100. This means that 100 is the target value for your target tracking policy. If the backlog per instance is currently at 150 (1500 / 10), your fleet scales out, and it scales out by five instances to maintain proportion to the target value.

#### Simple_Scaling_Policy 
- With simple scaling, you choose scaling metrics and threshold values for the *Amazon CloudWatch alarms* that trigger the scaling process. 
- The main issue with simple scaling is that after a scaling activity is started, the policy must wait for the scaling activity or health check replacement to complete and the cooldown period to expire before responding to additional alarms. 
- This implies that the application would not be able to react quickly to sudden spikes in orders.

#### Step_Scaling_Policy
- With step scaling, you choose scaling metrics and threshold values for the *Amazon CloudWatch alarms* that trigger the scaling process. 
- When step adjustments are applied, they increase or decrease the current capacity of your Auto Scaling group, and the adjustments vary based on the size of the alarm breach. For the given use-case, step scaling would try to approximate the correct number of instances by increasing/decreasing the steps as per the policy. 
- This is not as efficient as the target tracking policy where you can calculate the exact number of instances required to handle the spike in orders.

#### scheduled_scaling_policy
- Scheduled scaling allows you to set your scaling schedule.
- For example, let's say that every week the traffic to your web application starts to increase on Wednesday, remains high on Thursday, and starts to decrease on Friday. 
- You can plan your scaling actions based on the predictable traffic patterns of your web application. Scaling actions are performed automatically as a function of time and date. 
- You cannot use scheduled scaling policies to address the sudden spike in orders.



## AWS_Systems_Manager_Parameter_Store
- Provides secure, hierarchical storage for configuration data management and secrets management. 
- You can store data such as passwords, database strings, EC2 IDs, Amazon Machine Image (AMI) IDs, and license codes as parameter values. 
- You can store values as plain text or encrypted data. You can reference Systems Manager parameters in your scripts, commands, SSM documents, and configuration and automation workflows by using the unique name that you specified when you created the parameter.


## CloudHSM
- Acloud-based hardware security module (HSM) that enables you to easily generate and use your encryption keys on the AWS Cloud. 
- With AWS CloudHSM, you can manage your encryption keys using FIPS 140-2 Level 3 validated HSMs. AWS CloudHSM is standards-compliant and enables you to export all of your keys to most other commercially-available HSMs, subject to your configurations. 
- It is a fully-managed service that automates time-consuming administrative tasks for you, such as hardware provisioning, software patching, high-availability, and backups.


## KMS
- Service that combines secure, highly available hardware and software to provide a key management system scaled for the cloud. 
- When you use server-side encryption with AWS KMS (SSE-KMS), you can specify a customer-managed CMK that you have already created. SSE-KMS provides you with an audit trail that shows when your CMK was used and by whom. 
- AWS Key Management Service (KMS) makes it easy for you to create and manage cryptographic keys and control their use across a wide range of AWS services and in your applications. AWS KMS is a secure and resilient service that uses hardware security modules that have been validated under FIPS 140-2.
- *KMS is an encryption service*, it's not a secrets store

- If you use KMS keys, you can use AWS KMS through the AWS Management Console or the AWS KMS API to do the following:
  1. Centrally create, view, edit, monitor, enable or disable, rotate, and schedule deletion of KMS keys.
  2. Define the policies that control how and by whom KMS keys can be used.
  3. Audit their usage to prove that they are being used correctly. Auditing is supported by the AWS KMS API, but not by the AWS KMSAWS Management Console.
### Rotating_KMS_Keys
![](https://assets-pt.media.datacumulus.com/aws-saa-pt/assets/pt2-q50-i2.jpg)
- When you enable automatic key rotation for a KMS key, AWS KMS generates new cryptographic material for the KMS key every year.
### KMS_MutiRegion_Keys
![](https://assets-pt.media.datacumulus.com/aws-saa-pt/assets/pt2-q46-i1.jpg)

AWS KMS supports multi-region keys, which are AWS KMS keys in different AWS regions that can be used interchangeably – as though you had the same key in multiple regions. 
- Each set of related multi-region keys has the same key material and key ID, so you can encrypt data in one AWS region and decrypt it in a different AWS region without re-encrypting or making a cross-region call to AWS KMS.

### Deleting an AWS KMS key
- Destructive and potentially dangerous. Therefore, AWS KMS enforces a waiting period. To delete a KMS key in AWS KMS you schedule key deletion. You can set the waiting period from a minimum of 7 days up to a maximum of 30 days. The default waiting period is 30 days. During the waiting period, the KMS key status and key state is Pending deletion. To recover the KMS key, you can cancel key deletion before the waiting period ends. After the waiting period ends you cannot cancel key deletion, and AWS KMS deletes the KMS key.


### Automatic key rotation 

## Cognito
### Cognito_User_Pools
- A user pool is a `user directory` in Amazon Cognito. You can leverage Amazon Cognito User Pools to either provide built-in user management or integrate with external identity providers, such as Facebook, Twitter, Google+, and Amazon. 
- Whether your users sign-in directly or through a third party, all members of the user pool have a directory profile that you can access through a Software Development Kit (SDK).

User pools provide: 
1. Sign-up and sign-in services. 
2. A built-in, customizable web UI to sign in users. 
3. Social sign-in with Facebook, Google, Login with Amazon, and Sign in with Apple, as well as sign-in with SAML identity providers from your user pool. 
4. User directory management and user profiles. 5
5. Security features such as multi-factor authentication (MFA), checks for compromised credentials, account takeover protection, and phone and email verification. 
6. Customized workflows and user migration through AWS Lambda triggers.

After creating an Amazon Cognito user pool, in API Gateway, you must then create a COGNITO_USER_POOLS authorizer that uses the user pool.
![Identity](https://assets-pt.media.datacumulus.com/aws-saa-pt/assets/pt2-q24-i1.jpg
)

### Cognito_User_Identity
- Identity pools provide AWS credentials to grant your users access to other AWS services.
- To enable users in your user pool to access AWS resources, you can configure an identity pool to exchange user pool tokens for AWS credentials.


## ACL
- Within Amazon S3, you can use ACLs to give read or write access on buckets or objects to groups of users. With ACLs, you can only grant other AWS accounts (not specific users) access to your Amazon S3 resources. So, this is not the right choice for the current requirement.
## S3_Bucket_Policy
![](https://assets-pt.media.datacumulus.com/aws-saa-pt/assets/pt2-q14-i1.jpg)
- Bucket policies in Amazon S3 can be used to add or deny permissions across some or all of the objects within a single bucket. 
- Policies can be attached to users, groups, or Amazon S3 buckets, enabling centralized management of permissions. 
- With bucket policies, you can grant users within your AWS Account or other AWS Accounts access to your Amazon S3 resources.

- You can further restrict access to specific resources based on certain conditions. For example, you can restrict access based on request time (Date Condition), whether the request was sent using SSL (Boolean Conditions), a requester’s IP address (IP Address Condition), or based on the requester's client application (String Conditions). To identify these conditions, you use policy keys.



## S3TA
- enables fast, easy, and secure transfers of files over long distances between your client and an S3 bucket.
- Takes advantage of Amazon CloudFront’s globally distributed edge locations.
- As the data arrives at an edge location, data is routed to Amazon S3 over an optimized network path.
- Pay only for transfer that are accelerated
## S3 - Multipart Upload
- Multipart upload allows you to upload a single object as a set of parts.
- Each part is a contiguous portion of the object's data. You can upload these object parts independently and in any order.
-  If transmission of any part fails, you can retransmit that part without affecting other parts.
-  After all parts of your object are uploaded, Amazon S3 assembles these parts and creates the object.
-   If you're uploading large objects over a stable high-bandwidth network, use multipart uploading to maximize the use of your available bandwidth by uploading object parts in parallel for multi-threaded performance.
-  If you're uploading over a spotty network, use multipart uploading to increase resiliency to network errors by avoiding upload restarts.
## S3 – Requester Pays

* With Requester Pays buckets, the requester instead of the bucket owner pays the cost of the request and the data download from the bucket

## S3 - Access Point

* VPC Origin - DNS Name
* EC2 could create VPC Enpoint(Gateway or Interface Endpoint)


## 163 - S3 - Object Standard


## AWS_Secrets_Manager
- Helps you protect secrets needed to access your applications, services, and IT resources. 
- The service enables you to easily rotate, manage, and retrieve database credentials, API keys, and other secrets throughout their lifecycle. 
- Users and applications retrieve secrets with a call to Secrets Manager APIs, eliminating the need to hardcode sensitive information in plain text. 
- Secrets Manager offers secret rotation with built-in integration for Amazon RDS, Amazon Redshift, and Amazon DocumentDB.

## Cloudfront
- CDN service that securely delivers data, videos, applications, and APIs to customers globally with low latency, high transfer speeds, all within a developer-friendly environment.
- CloudFront points of presence (POPs) (edge locations) make sure popular content can be served quickly to your viewers.
- has regional edge caches that bring more of your content closer to your viewers, even when the content is not popular enough to stay at a POP, to help improve performance for that content.
- You can use different origins for different types of content on a single site – e.g. Amazon S3 for static objects, Amazon EC2 for dynamic content, and custom origins for third-party content.
### cloudfront_with_s3
- A- mazon CloudFront is a content delivery network (CDN) service that delivers static and dynamic web content, video streams, and APIs around the world, securely and at scale. 
- By design, delivering data out of Amazon CloudFront can be more cost-effective than delivering it from Amazon S3 directly to your users. 
- Amazon CloudFront serves content through a worldwide network of data centers called Edge Locations. 
- Using edge servers to cache and serve content improves performance by providing content closer to where viewers are located.

- When you put your content in an Amazon S3 bucket in the cloud, a lot of things become much easier. 
- First, you don’t need to plan for and allocate a specific amount of storage space because Amazon S3 buckets scale automatically. 
- As Amazon S3 is a serverless service, you don’t need to manage or patch servers that store files yourself; you just put and get your content. 
- Finally, even if you require a server for your application (for example, because you have a dynamic application), the server can be smaller because it doesn’t have to handle requests for static content.

- When a user requests content that you serve with Amazon CloudFront, their request is routed to a nearby Edge Location. If Amazon CloudFront has a cached copy of the requested file, CloudFront delivers it to the user, providing a fast (low-latency) response. If the file they’ve requested isn’t yet cached, CloudFront retrieves it from your origin – for example, the Amazon S3 bucket where you’ve stored your content. Then, for the next local request for the same content, it’s already cached nearby and can be served immediately.

By caching your content in Edge Locations, Amazon CloudFront reduces the load on your Amazon S3 bucket and helps ensure a faster response for your users when they request content. Also, data transfer out for content by using Amazon CloudFront is often more cost-effective than serving files directly from Amazon S3, and there is no data transfer fee from Amazon S3 to Amazon CloudFront. You only pay for what is delivered to the internet from Amazon CloudFront, plus request fees.

### Origin failover feature

- support your data resiliency needs.
- If your content is not already cached in an edge location,
  -> CloudFront retrieves it from an origin that you've identified as the source for the definitive version of the content.
#### 165 Cloudfront with S3

* Origin access
* Distribution

## AWS_Global_Accelerator
![](https://d1.awsstatic.com/r2018/b/ubiquity/global-accelerator-how-it-works.feb297eb78d8cc55205874a1691e0ea2bc8bdbf1.png)
![](https://assets-pt.media.datacumulus.com/aws-saa-pt/assets/pt4-q45-i1.jpg)
- AWS Global Accelerator is a networking service that sends your user’s traffic through Amazon Web Service’s global network infrastructure, improving your internet user performance by up to 60%. When the internet is congested, Global Accelerator’s automatic routing optimizations will help keep your packet loss, jitter, and latency consistently low.

- With AWS Global Accelerator, you are provided two global static customer-facing IPs to simplify traffic management. On the back end, add or remove your AWS application origins, such as Network Load Balancers, Application Load Balancers, elastic IP address (EIP), and Amazon EC2 Instances, without making user-facing changes. To mitigate endpoint failure, AWS Global Accelerator automatically re-routes your traffic to your nearest healthy available endpoint.

- AWS Global Accelerator is a **network layer service** that directs traffic to optimal endpoints over the AWS global network, this improves *the availability and performance of your internet applications*. 
- It provides *two static anycast IP addresse*s that act as a fixed entry point to your application endpoints in a single or multiple AWS Regions, such as your ALB, NLB, EIP or EC2, in a single or in multiple AWS regions.

- Utilizes the Amazon global network, allowing you to improve the performance of your applications by:
  1. lowering first-byte latency(the round trip time for a packet to go from a client to your endpoint and back again)
  2. jitter (the variation of latency)
  3. increasing throughput (the amount of time it takes to transfer data) as compared to the public internet
- Provides static IP addresses that act as a fixed entry point to your application endpoints in a single or multiple AWS Regions such as ALB, NLB, EC2 instances.
- Improve wide range of app(TCP, UDP) by proxying packets at the edge to applications running in one or more AWS Regions.
- Global Accelerator is a good fit for non-HTTP use cases, such as gaming (UDP), IoT (MQTT), or Voice over IP, as well as for HTTP use cases that specifically require static IP addresses or deterministic, fast regional failover.
- AWS Global Accelerator and Amazon CloudFront are separate services that use the AWS global network and its edge locations around the world. CloudFront improves performance for both cacheable content (such as images and videos) and dynamic content (such as API acceleration and dynamic site delivery), while Global Accelerator improves performance for a wide range of applications over TCP or UDP.
- not help in accelerating the file transfer speeds into S3 for the given use-case.
- When go public internet - A lot of latency because there many hops
- Unicast IP: 1 server 1 IP
- Any Cast IP: Same Ip, client is routed to near on
- Global Accelerator: Talk to closed Edge location -> Public ALP
- Create Private AWS network
- Perform healcheck for your app

## Code deploy
- In AWS CodeDeploy, a deployment is the process, and the components involved in the process, of installing content on one or more instances. This content can consist of code, web and configuration files, executables, packages, scripts, and so on.
- AWS CodeDeploy deploys content that is stored in a source repository, according to the configuration rules you specify.
## Virtual_private_gateway
- A virtual private gateway (VGW), also known as a VPN Gateway, 
- is the endpoint on the VPC side of your VPN connection. 
- You can create a virtual private gateway before creating the VPC itself. 
## AWS_Direct_Connect
- Establish a dedicated network connection from your premises to AWS.
- AWS Direct Connect lets you establish a dedicated network connection between your network and one of the AWS Direct Connect locations.
- With AWS Direct Connect plus VPN, you can combine one or more AWS Direct Connect dedicated network connections with the Amazon VPC VPN. This combination provides an IPsec-encrypted private connection that also reduces network costs, increases bandwidth throughput, and provides a more consistent network experience than internet-based VPN connections.
- Involves significant monetary investment and takes at least a month to set up, therefore it's not the correct fit for this use-case.

### AWS_Direct_Connect_VIFs: 
![AWS_Direct_Connect_VIFs](https://assets-pt.media.datacumulus.com/aws-saa-pt/assets/pt2-q11-i1.jpg)

## AMI
- An Amazon Machine Image (AMI) provides the information required to launch an instance. 
- An AMI includes the following:

  + One or more Amazon EBS snapshots
  + for instance-store-backed AMIs
  + a template for the root volume of the instance.

- Launch permissions that control which AWS accounts can use the AMI to launch instances.

- A block device mapping that specifies the volumes to attach to the instance when it's launched.

- You can copy an AMI within or across AWS Regions using the AWS Management Console, the AWS Command Line Interface or SDKs, or the Amazon EC2 API, all of which support the CopyImage action. 
- You can copy both Amazon EBS-backed AMIs and instance-store-backed AMIs. 
- You can copy AMIs with encrypted snapshots and also change encryption status during the copy process. Therefore, the option - "You can copy an AMI across AWS Regions" - is correct.

- The following table shows encryption support for various AMI-copying scenarios. While it is possible to copy an unencrypted snapshot to yield an encrypted snapshot, you cannot copy an encrypted snapshot to yield an unencrypted one. Therefore, the option - "Copying an AMI backed by an encrypted snapshot cannot result in an unencrypted target snapshot" is correct.
![](https://assets-pt.media.datacumulus.com/aws-saa-pt/assets/pt4-q55-i1.jpg)

## CloudFormation

### AWS_CloudFormation_Stack
- AWS CloudFormation stack is a set of AWS resources that are created and managed as a single unit when AWS CloudFormation instantiates a template. A stack cannot be used to deploy the same template across AWS accounts and regions.

### AWS_CloudFormation_Template
-  AWS Cloudformation template is a JSON or YAML-format, text-based file that describes all the AWS resources you need to deploy to run your application. 
-  A template acts as a blueprint for a stack. AWS CloudFormation templates cannot be used to deploy the same template across AWS accounts and regions.

### AWS_CloudFormation_StackSets
![](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/images/stack_set_conceptual_sv.png)
AWS CloudFormation StackSet extends the functionality of stacks by enabling you to create, update, or delete stacks across multiple accounts and regions with a single operation. A stack set lets you create stacks in AWS accounts across regions by using a single AWS CloudFormation template. Using an administrator account of an "AWS Organization", you define and manage an AWS CloudFormation template, and use the template as the basis for provisioning stacks into selected target accounts of an "AWS Organization" across specified regions.

## AWS_Site_To_Site_VPN
![](https://docs.aws.amazon.com/whitepapers/latest/aws-vpc-connectivity-options/images/aws-managed-vpn.png)
- Enables you to securely connect your **on-premises** network or branch office site to your Amazon VPC.
- Utilizes protocol security(IPSec) to establish encrypted network connectivity between your intranet and Amazon VPC over the Internet.
- VPN Connections are a good solution if you have an immediate need, have low to modest bandwidth requirements, and can tolerate the inherent variability in Internet-based connectivity.
- However, Site-to-site VPN cannot provide low latency and high throughput connection, therefore this option is ruled out.
- The following are the key concepts for a site-to-site VPN:
  - Virtual private gateway: A virtual private gateway (VGW), also known as a VPN Gateway is the endpoint on the AWS VPC side of your VPN connection.
  - VPN connection: A secure connection between your on-premises equipment and your VPCs.
  - VPN tunnel: An encrypted link where data can pass from the customer network to or from AWS.
  - Customer Gateway: An AWS resource that provides information to AWS about your Customer Gateway device.
  - Customer Gateway device: A physical device or software application on the customer side of the Site-to-Site VPN connection.
### VPN_CloudPub
- If you have multiple AWS Site-to-Site VPN connections, you can provide secure communication between sites using the AWS VPN CloudHub. This enables your remote sites to communicate with each other, and not just with the VPC. Sites that use AWS Direct Connect connections to the virtual private gateway can also be part of the AWS VPN CloudHub. The VPN CloudHub operates on a simple hub-and-spoke model that you can use with or without a VPC. This design is suitable if you have multiple branch offices and existing internet connections and would like to implement a convenient, potentially low-cost hub-and-spoke model for primary or backup connectivity between these remote office
- Per the given use-case, the corporate headquarters has an AWS Direct Connect connection to the VPC and the branch offices have Site-to-Site VPN connections to the VPC. Therefore using the AWS VPN CloudHub, branch offices can send and receive data with each other as well as with their corporate headquarters.
![](https://docs.aws.amazon.com/vpn/latest/s2svpn/images/AWS_VPN_CloudHub-diagram.png)
## AWS Snow Family

### AWS_Snowball
- A data migration and edge computing device that comes in two options. 
  1. **Snowball Edge Storage Optimized**:
    - Devices provide both block storage and Amazon S3-compatible object storage
    - Up to:
      - 40 vCPUs
      - 80 Terabytes of usable HDD storage
      - 1 TB of SATA SSD storage
      - up to 40 Gigabytes network connectivity to address large scale data transfer and pre-processing use cases. 
    - *-> suited for local storage and large scale data transfer*
  2. **AWS Snowball Edge Compute Optimized** devices provide 52 vCPUs, block and object storage, and an optional GPU for use cases like advanced machine learning and full-motion video analysis in disconnected environments.

### AWS_Snowmobile
- 100 petabyte in one location

## AWS Directory Service for Microsoft Active Directory (AWS Managed Microsoft AD)
AWS Directory Service for Microsoft Active Directory, also known as AWS Managed Microsoft AD, enables your directory-aware workloads and AWS resources to use managed Active Directory in the AWS Cloud.
## Amazon FSx for Lustre
Makes it easy and cost-effective to launch and run the world’s most popular high-performance file system.
- It is used for workloads such as machine learning, high-performance computing (HPC), video processing, and financial modeling.
- The open-source Lustre file system is designed for applications that require fast storage – where you want your storage to keep up with your compute.
- FSx for Lustre integrates with Amazon S3, making it easy to process data sets with the Lustre file system. When linked to an S3 bucket, an FSx for Lustre file system transparently presents S3 objects as files and allows you to write changed data back to S3.

## Amazon_FSx_for_Windows_File_Server
![](https://assets-pt.media.datacumulus.com/aws-saa-pt/assets/pt4-q43-i1.jpg)
- Provides fully managed, highly reliable file storage that is accessible over the industry-standard Service Message Block (SMB) protocol. 
- It is built on Windows Server, delivering a wide range of administrative features such as user quotas, end-user file restore, and Microsoft Active Directory (AD) integration. 
- The Distributed File System Replication (DFSR) service is a new multi-master replication engine that is used to keep folders synchronized on multiple servers. Amazon FSx supports the use of Microsoft’s Distributed File System (DFS) to organize shares into a single folder structure up to hundreds of PB in size.
- Amazon FSx for Windows is a perfect distributed file system, with replication capability, and can be mounted on Windows.
- FSx for Windows does not allow you to present S3 objects as files and does not allow you to write changed data back to S3. Therefore you cannot reference the "cold data" with quick access for reads and updates at low cost. Hence this option is not correct.
- provides all of the benefits of a native Windows SMB environment that is fully managed and secured and scaled like any other AWS service. You get detailed reporting, replication, backup, failover, and support for native Windows tools like DFS and Active Directory.
- support file shares in Amazon FSx for Windows File Server, so this option is incorrect.
- Amazon FSx File Gateway: low-latency, on-premises access to fully managed file shares in Amazon FSx for Windows File Server. For applications deployed on AWS, you may access your file shares directly from Amazon FSx in AWS
- ![](https://d1.awsstatic.com/r2018/b/FSx-Windows/FSx_Windows_File_Server_How-it-Works.9396055e727c3903de991e7f3052ec295c86f274.png)
## AWS_Storage_gateway
- A hybrid cloud storage service that gives you on-premises access to virtually unlimited cloud storage.
- types of gateways
  - Tape Gateway
    - allows moving tape backups to the cloud.
  - File Gateway
    - offer ~~SMB~~ or ~~NFs~~ in S3 with local catching
  - Volume Gateway
    - Present cloud-based iSCSI block storage volumes to your on-premises applications.
- that seamlessly connect on-premises applications to cloud storage, caching data locally for low-latency access.
- ~Ref~
  - [Link](https://docs.aws.amazon.com/storagegateway/latest/userguide/StorageGatewayConcepts.html)

- It is not suited to be used as a shared storage space that multiple applications can access in parallel.
### Volume_Gateway
- *With cached volumes*, the AWS Volume Gateway stores the full volume in its Amazon S3 service bucket, and just the recently accessed data is retained in the gateway’s local cache for low-latency access.
- *With stored volumes*, your entire data volume is available locally in the gateway, for fast read access. Volume Gateway also maintains an asynchronous copy of your stored volume in the service’s Amazon S3 bucket. This does not fit the requirements per the given use-case, hence this option is not correct.
### File_gateway
![](https://d1.awsstatic.com/cloud-storage/Amazon%20FSx%20File%20Gateway%20How%20It%20Works%20Diagram.edbf58e4917d47d04e5a5c22132d44bd92733bf5.png)

- File Gateway does not support file shares in Amazon FSx for Windows File Server, so this option is incorrect.

## Step_Functions
- Lets you *coordinate multiple AWS services* into *serverless workflows* so you can build and update apps quickly. 
- Using Step Functions, you can design and run workflows that stitch together services, such as AWS Lambda, AWS Fargate, and Amazon SageMaker, into feature-rich applications. 

## SQS
- Fully managed message queuing service that enables decouple and scale microservices, distributed systems, and serverless applications. 
- SQS offers two types of message queues. 
  1. *Standard queues* offer maximum throughput, best-effort ordering, and at-least-once delivery. 
  2. *FIFO queues* are designed to guarantee that messages are processed exactly once, in the exact order that they are sent.
- By default, FIFO queues support up to 3,000 messages per second with batching, or up to 300 messages per second (300 send, receive, or delete operations per second) without batching. Therefore, using batching you can meet a throughput requirement of upto 3,000 messages per second.
- The name of a FIFO queue must end with the .fifo suffix. The suffix counts towards the 80-character queue name limit. To determine whether a queue is FIFO, you can check whether the queue name ends with the suffix.
- **Message Timer**: - You can use message timers to set an initial invisibility period for a message added to a queue. So, if you send a message with a 60-second timer, the message isn't visible to consumers for its first 60 seconds in the queue. The default (minimum) delay for a message is 0 seconds. The maximum is 15 minutes. You cannot use message timer to retrieve messages from your Amazon SQS queues. This option has been added as a distractor.
### Short_Polling
![](https://assets-pt.media.datacumulus.com/aws-saa-pt/assets/pt4-q34-i1.jpg)
- Amazon SQS provides short polling and long polling to receive messages from a queue. By default, queues use short polling. With short polling, Amazon SQS sends the response right away, even if the query found no messages
### Long_Polling
- With long polling, Amazon SQS sends a response after it collects at least one available message, up to the maximum number of messages specified in the request.
### Message_Timemer
### Visibility_timeout
- Visibility timeout is a period during which Amazon SQS prevents other consumers from receiving and processing a given message. The default visibility timeout for a message is 30 seconds. The minimum is 0 seconds. The maximum is 12 hours. You cannot use visibility timeout to postpone the delivery of new messages to the queue for a few seconds.
### dead_letter_queue
 Dead-letter queues can be used by other queues (source queues) as a target for messages that can't be processed (consumed) successfully. Dead-letter queues are useful for debugging your application or messaging system because they let you isolate problematic messages to determine why their processing doesn't succeed. You cannot use dead-letter queues to postpone the delivery of new messages to the queue for a few seconds
### SQS_Delay_queue
-[](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/images/sqs-delay-queues-diagram.png)
- Delay queues let you postpone the delivery of new messages to a queue for several seconds, for example, when your consumer application needs additional time to process messages. If you create a delay queue, any messages that you send to the queue remain invisible to consumers for the duration of the delay period. The default (minimum) delay for a queue is 0 seconds. The maximum is 15 minutes.


### SQS_Fifo_queue
- Limited throughput : 300 msg/s without batching, max: 10 message per operation = 3000 msg/s
- If we don't specify a **GroupID**, then all the messages are in absolute order, but we can only have 1 consumer at most.
- To allow for multiple consumers to read data for each Desktop application, and to scale the number of consumers, we should use the "Group ID" attribute. So this is the correct option.


## Kinesis_Agent
- a stand-alone Java software application that offers an easy way to collect and send data to Amazon Kinesis Data Streams or Amazon Kinesis Firehose.
## Kinesis_Data_Stream
![](https://assets-pt.media.datacumulus.com/aws-saa-pt/assets/pt4-q46-i1.jpg)
-  Is a massively scalable and durable real-time data streaming service. 
-  The throughput of an Amazon Kinesis data stream is designed to scale without limits via increasing the number of shards within a data stream.
-  KDS can continuously capture gigabytes of data per second from hundreds of thousands of sources such as website clickstreams, database event streams, financial transactions, social media feeds, IT logs, and location-tracking events. 
- The throughput of an Amazon Kinesis data stream is designed to scale without limits via increasing the number of shards within a data stream
- Enables real-time processing of streaming big data.
- It provides ordering of records, as well as the ability to read and/or replay records in the same order to multiple Amazon Kinesis Applications.
- The Amazon Kinesis Client Library (KCL) delivers all records for a given partition key to the same record processor, making it easier to build multiple applications reading from the same Amazon Kinesis data stream (for example, to perform counting, aggregation, and filtering).
- **Recomment**
  1. *Routing related records to the same record processor* (as in streaming MapReduce). For example, counting and aggregation are simpler when all records for a given key are routed to the same record processor.
  2. *Ordering of records*. For example, you want to transfer log data from the application host to the processing/archival host while maintaining the order of log statements.
  3. *Ability for multiple applications to consume the same stream concurrently*. For example, you have one application that updates a real-time dashboard and another that archives data to Amazon Redshift. You want both applications to consume data from the same stream concurrently and independently.
  4. *Ability to consume records in the same order a few hours later*. For example, you have a billing application and an audit application that runs a few hours behind the billing application. Because Amazon Kinesis Data Streams stores data for up to 365 days, you can run the audit application up to 365 days behind the billing application.

- Kinesis Data Streams cannot directly write the output to Amazon S3. Unlike Amazon Kinesis Data Firehose, KDS does not offer a ready-made integration via an intermediary AWS Lambda function to reliably dump data into Amazon S3

- Only Cloudwatch and S3 bucket could ingest data(not AWS CloudTrail)

## Firehose
- the easiest way to **load streaming data** into 
  - data stores 
  - analytics tools
  - data lakes
- It can capture, transform, and load streaming data into:
  -  Amazon S3
  -  Amazon Redshift
  -  Amazon OpenSearch Service
  -  Splunk
- Enabling near real-time analytics
- It is a fully managed service that automatically scales to match the throughput of your data and requires no ongoing administration.
- It can also batch, compress, and encrypt the data before loading it -> minimizing the amount of storage used at the destination and increasing security.

- When an Amazon Kinesis Data Stream is configured as the source of a Kinesis Firehose delivery stream, Firehose’s PutRecord and PutRecordBatch operations are disabled and Kinesis Agent cannot write to Kinesis Firehose Delivery Stream directly
  
- ![Overview](https://d1.awsstatic.com/pdp-how-it-works-assets/product-page-diagram_Amazon-KDF_HIW-V2-Updated-Diagram@2x.6e531854393eabf782f5a6d6d3b63f2e74de0db4.png)
## Kinesis_Data_Analytics
- Amazon Kinesis Data Analytics is the easiest way to analyze streaming data in real-time.
-  Kinesis Data Analytics enables you to easily and quickly build queries and sophisticated streaming applications in three simple steps:
   1. setup your streaming data sources
   2. write your queries or streaming applications
   3. set up your destination for processed data.
- Kinesis Data Analytics cannot directly ingest data from the source as it ingests data either from
  - Kinesis Data Streams
  - Kinesis Data Firehose

## AWS Config
![](https://d1.awsstatic.com/Products/product-name/diagrams/product-page-diagram-Config_how-it-works.bd28728a9066c55d7ee69c0a655109001462e25b.png)
AWS Config is a service that enables you to assess, audit, and evaluate the configurations of your AWS resources. With Config, you can review changes in configurations and relationships between AWS resources, dive into detailed resource configuration histories, and determine your overall compliance against the configurations specified in your internal guidelines. You can use Config to answer questions such as - “What did my AWS resource look like at xyz point in time?”

## VPC
### VPC_Gateway_Loadbalancer
- **Gateway Load Balancers** use *Gateway Load Balancer endpoints* to securely exchange traffic across VPC boundaries. A Gateway Load Balancer endpoint is a VPC endpoint that provides private connectivity between virtual appliances in the service provider VPC and application servers in the service consumer VPC. You cannot set up a gateway load balancer endpoint to access Amazon S3

### VPC_Gateway_Endpoint
![](https://assets-pt.media.datacumulus.com/aws-saa-pt/assets/pt4-q47-i1.jpg)
- **Gateway endpoints** provide reliable connectivity to Amazon S3 without requiring an internet gateway or a NAT device for your VPC. 
- After you create the gateway endpoint, you can add it as a target in your route table for traffic destined from your VPC to Amazon S3. 
- There is no additional charge for using gateway endpoints.
- The **VPC endpoint policy** for the **gateway endpoint** controls access to Amazon S3 from the VPC through the endpoint. The default policy allows full access.
- Using the VPC gateway endpoint allows the Amazon EC2 instances to reach Amazon S3 without using the public internet. Since the data transfer remains within the same AWS region, so there is no data transfer costs for ingress as well as egress traffic. Hence this is the most cost-optimal solution.

### vpc_internet_gateway
- *An Internet Gateway* is a horizontally scaled, redundant, and highly available VPC component that allows communication between your VPC and the internet.
- *An Internet Gateway serves two purposes*: 
  - to provide a target in your VPC route tables for internet-routable traffic 
  - perform network address translation (NAT) for instances that have been assigned public IPv4 addresses.
- Additionally, an Internet Gateway supports IPv4 and IPv6 traffic. It does not cause availability risks or bandwidth constraints on your network traffic
- *Attach an Internet gateway to your VPC*.
  - Add a route to your subnet's route table that directs internet-bound traffic to the internet gateway. If a subnet is associated with a route table that has a route to an internet gateway, it's known as a public subnet. If a subnet is associated with a route table that does not have a route to an internet gateway, it's known as a private subnet.
  - Ensure that instances in your subnet have a globally unique IP address (public IPv4 address, Elastic IP address, or IPv6 address).
  - Ensure that your network access control lists and security group rules allow the relevant traffic to flow to and from your instance.
### vpc_nat_instance
- Differenen NAT Gateway NAT instance
  - ![](https://assets-pt.media.datacumulus.com/aws-saa-pt/assets/pt4-q12-i1.jpg)
  -  https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-comparison.html
- You can use a network address translation (NAT) instance in a public subnet in your VPC to enable instances in *the private subnet* to initiate outbound IPv4 traffic to *the internet or other AWS services*, but prevent the instances from receiving inbound traffic initiated by someone on the internet.
- NAT instances are not a managed service, it has to be managed and maintained by the customer.
### vpc_nat_gateway
![](https://assets-pt.media.datacumulus.com/aws-saa-pt/assets/pt4-q44-i1.jpg)

- You can use a NAT gateway to enable instances in a private subnet to connect to the internet or other AWS services, but prevent the internet from initiating a connection with those instances.

- To create a NAT gateway, you must specify the public subnet in which the NAT gateway should reside. 
- You must also specify an Elastic IP address to associate with the NAT gateway when you create it.
-  The Elastic IP address cannot be changed after you associate it with the NAT Gateway. 
-  After you've created a NAT gateway, you must update the route table associated with one or more of your private subnets to point internet-bound traffic to the NAT gateway. 
-  This enables instances in your private subnets to communicate with the internet.

Each NAT gateway is created in a specific Availability Zone and implemented with redundancy in that zone.

If you have resources in multiple Availability Zones and they share one NAT gateway, and if the NAT gateway’s Availability Zone is down, resources in the other Availability Zones lose internet access. To create an Availability Zone-independent architecture, create a NAT gateway in each Availability Zone and configure your routing to ensure that resources use the NAT gateway in the same Availability Zone.

### Elastic Network Adapter (ENA)
- Elastic Network Adapter (ENA) devices support enhanced networking via single root I/O virtualization (SR-IOV) to provide high-performance networking capabilities. 

### Elastic_Ip_Address_EIP
-  - An Elastic IP address (EIP) is a static IPv4 address associated with your AWS account. An Elastic IP address is a public IPv4 address, which is reachable from the internet. 
### Elastic_Network_Interface_ENI
- Is a Logical networking component in a VPC that represents a virtual network card. 
- You can create a network interface, attach it to an instance, detach it from an instance, and attach it to another instance. 
### Fully_meshed_VPC_Peering
- -This approach creates multiple peering connections to facilitate the sharing of information between resources in different VPCs. This design connects multiple VPCs in a fully meshed configuration, with peering connections between each pair of VPCs. With this configuration, each VPC has access to the resources in all other VPCs. Each peering connection requires modifications to all the other VPCs’ route tables and, as the number of VPCs grows, this can be difficult to maintain. And keep in mind that AWS recommends a maximum of 125 peering connections per VPC. It's complex to manage and isn't a right fit for the current scenario.
### Transit_VPC
![](https://assets-pt.media.datacumulus.com/aws-saa-pt/assets/pt2-q21-i2.jpg)
- Transit VPC uses customer-managed Amazon EC2 VPN instances in a dedicated transit VPC with an Internet gateway. 
- This design requires the customer to deploy, configure, and manage EC2-based VPN appliances, which will result in additional EC2, and potentially third-party product and licensing charges.
-  Note that this design will generate additional data transfer charges for traffic traversing the transit VPC: data is charged when it is sent from a spoke VPC to the transit VPC, and again from the transit VPC to the on-premises network or a different AWS Region. Transit VPC is not the right choice here.
### Centralized_VPC_Endpoints 
![](https://assets-pt.media.datacumulus.com/aws-saa-pt/assets/pt2-q21-i1.jpg)
- Consider an organization that has built a hub-and-spoke network with AWS Transit Gateway. VPCs have been provisioned into multiple AWS accounts, perhaps to facilitate network isolation or to enable delegated network administration. When deploying distributed architectures such as this, a popular approach is to build a "shared services VPC, which provides access to services required by workloads in each of the VPCs. This might include directory services or VPC endpoints. Sharing resources from a central location instead of building them in each VPC may reduce administrative overhead and cost.
- A VPC endpoint allows you to privately connect your VPC to supported AWS services without requiring an Internet gateway, NAT device, VPN connection, or AWS Direct Connect connection. Endpoints are virtual devices that are horizontally scaled, redundant, and highly available VPC components. They allow communication between instances in your VPC and services without imposing availability risks or bandwidth constraints on your network traffic.

- VPC endpoints enable you to reduce data transfer charges resulting from network communication between private VPC resources (such as Amazon Elastic Cloud Compute—or EC2—instances) and AWS Services (such as Amazon Quantum Ledger Database, or QLDB). Without VPC endpoints configured, communications that originate from within a VPC destined for public AWS services must egress AWS to the public Internet in order to access AWS services. This network path incurs outbound data transfer charges. Data transfer charges for traffic egressing from Amazon EC2 to the Internet vary based on volume. With VPC endpoints configured, communication between your VPC and the associated AWS service does not leave the Amazon network. If your workload requires you to transfer significant volumes of data between your VPC and AWS, you can reduce costs by leveraging VPC endpoints.

## BlueGreenDeployment
- Blue/green deployment is a technique for releasing applications by shifting traffic between two identical environments running different versions of the application:
  - "Blue" is the currently running version
  - "green" the new version.
- This type of deployment allows you to test features in the green environment without impacting the currently running version of your application. When you’re satisfied that the green version is working properly, you can gradually reroute the traffic from the old blue environment to the new green environment. Blue/green deployments can mitigate common risks associated with deploying software, such as downtime and rollback capability.
## Lambda
- Run code without provisioning or managing servers. 
- You pay only for the compute time that you consume—there’s no charge when your code isn’t running.
- Currently supports *1000 concurrent executions* per **AWS account** per region.

- If your Amazon SNS message deliveries to AWS Lambda contribute to crossing these concurrency quotas, your Amazon SNS message deliveries will be throttled. You need to contact AWS support to raise the account limit
- Integrates natively with Kinesis Data Streams. The polling, checkpointing, and error handling complexities are abstracted when you use this native integration. The processed data can then be configured to be saved in Amazon DynamoDB.

### 219. Lambda SnapStart

* For Java
* Snap start -> Function is preitnitize

## Amazon_ElastiCache
- ElastiCache allows you to seamlessly set up, run, and scale popular open-source compatible in-memory data stores in the cloud. 
- Build data-intensive apps or boost the performance of your existing databases by retrieving data from high throughput and low latency in-memory data stores. 
- Amazon ElastiCache is a popular choice for real-time use cases like Caching, Session Stores, Gaming, Geospatial Services, Real-Time Analytics, and Queuing. ElastiCache could work but it's a better fit as a caching technology to enhance reads
  
- Amazon ElastiCache for Memcached is an ideal front-end for data stores like Amazon RDS or Amazon DynamoDB, providing a high-performance middle tier for applications with extremely high request rates and/or low latency requirements


## 225. Dynamodb Advanced Features

### DynamoDB Accelerator(DAX)
- Amazon DynamoDB Accelerator (DAX) is a fully managed, highly available, in-memory cache for DynamoDB that delivers up to a 10x performance improvement – from milliseconds to microseconds – even at millions of requests per second.
- DAX does all the heavy lifting required to add in-memory acceleration to your DynamoDB tables, without requiring developers to manage cache invalidation, data population, or cluster management. Therefore, this is a correct option.
  ![](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/images/dax_high_level.png)

* in- memory cache for DynamoDB
* Help solve read congestion by caching
* Microseconds latency for cached data
* Doesn’t require application logic modification (compatible with existing DynamoDB APIs)
* 5 minutes TTL for cache (default)


### DynamoDB - Stream Processing

* Same Kinesis


### Global table

* Make a DynamoDB table accessible with low latency in multiple-regions
* Active-Active replication
* Applications can READ and WRITE to the table in any region
* Must enable DynamoDB Streams as a pre-requisite

  \


### TimeTolive

* Automatically delete items after an expiry timestamp
* Use cases: reduce stored data by keeping only current items, adhere to regulatory obligations, web session handling...


## API GATEWAY
- Amazon API Gateway to create, publish, maintain, monitor, and secure APIs at any scale.
- APIs act as the front door for applications to access data, business logic, or functionality from your backend services.
- Using API Gateway, you can create RESTful APIs and WebSocket APIs that enable real-time two-way communication applications.

* Endpoint Type:
  * Edge-Optimize(default): For global clients
  * Regional:
  * Private:
* Security:
  * IAM Role
  * Cognito
  * Custom Authorize(Lamda)
* How to API gateway work:

## Choosing right database
- RDBMS (SQL/OLTP) - Great for joins
  - RDS
  - Aurora
- NoSQL database - no joins, no SQL
  - DynamoDB(~JSON)
  - ElasticCache(Key/Value Paris)
  - Neptune(graphs)
  - DocumentDB(For MogoDB)
- Object Store:
  - S3(for big objects)
  - Glacier(for backups/chive)
- **Data Warehouse**(SQL Analytics / BI)
  + Reshift(OLAP)
  + Athena
  + EMR
- Search:
  - OpenSearch(Json) - free text, unstructured search
- Graphs: Amazone Neptune - displays relationships between data
- Ledger: Amazone Quantum Ledger Database
- Time series: AmazonTimestream

## RDS
- RDS makes it easy to set up, operate, and scale a relational database in the cloud. 
- It provides cost-efficient and resizable capacity while automating time-consuming administration tasks such as hardware provisioning, database setup, patching, and backups. 
- RDS allows you to create, read, update, and delete records without any item lock or ambiguity.
- All RDS transactions must be ACID compliant(Atomic, Consistent, Isolated, and Durable) to ensure data integrity.
  1. Atomicity requires that either transaction as a whole is successfully executed or if a part of the transaction fails, then the entire transaction be invalidated. 
  2. Consistency mandates the data written to the database as part of the transaction must adhere to all defined rules, and restrictions including constraints, cascades, and triggers. 
  3. Isolation is critical to achieving concurrency control and makes sure each transaction is independent unto itself. 
  4. Durability requires that all of the changes made to the database be permanent once a transaction is completed

- Managed Postgres / Mysql / Oracle / SQL Server / DB2 / MariaDB
- Provision
  - Rds Instace Size and EBS VolumneType & size
- Auto-scaling for storage
- Support
  - Read Replicas
  - Multi AZ
- Security
  - IAM
  - Security Group
  - KMS
  - SSL in transit
- Auotmated Backup with Point in time restore feature(35 days)
- Manual DB Snapshot for longer-term recoverry
- Support IAM Authentication, integration with Secrets Manager
### RDS_Comparable
![](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/images/read-and-standby-replica.png)
![CompareTable](https://assets-pt.media.datacumulus.com/aws-saa-pt/assets/pt2-q8-i1.jpg)
### RDS_Read_Replicas
- Amazon RDS Read Replicas provide enhanced performance and durability for RDS database (DB) instances.
- Easy to elastically scale out beyond the capacity constraints of a single DB instance for read-heavy database workloads.

- For the MySQL, MariaDB, PostgreSQL, Oracle, and SQL Server database engines, RDS creates a second DB instance using a snapshot of DB. 

- It then uses the engines native asynchronous replication to update the read replica whenever there is a change to the source DB instance. 
- Can be within an Availability Zone, Cross-AZ, or Cross-Region.
- A read replica is billed as a standard DB Instance and at the same rates. You are not charged for the data transfer incurred in replicating data between your source DB instance and read replica within the same AWS Region.
- There are a variety of scenarios where deploying one or more read replicas for a given source DB instance may make sense. Common reasons for deploying a read replica include:

  1. Scaling beyond the compute or I/O capacity of a single DB instance for read-heavy database workloads. This excess read traffic can be directed to one or more read replicas.
  2. Serving read traffic while the source DB instance is unavailable. If your source DB Instance cannot take I/O requests (e.g. due to I/O suspension for backups or scheduled maintenance), you can direct read traffic to your read replica(s). For this use case, keep in mind that the data on the read replica may be “stale” since the source DB Instance is unavailable.
  3. Business reporting or data warehousing scenarios; you may want business reporting queries to run against a read replica, rather than your primary, production DB Instance.
  4. You may use a read replica for disaster recovery of the source DB instance, either in the same AWS Region or in another Region.
- ![Read Replicas Link](https://assets-pt.media.datacumulus.com/aws-saa-pt/assets/pt2-q44-i1.jpg)
- ![Compare](https://assets-pt.media.datacumulus.com/aws-saa-pt/assets/pt4-q41-i1.jpg)
### storage_auto_scaling
- If your workload is unpredictable, you can enable storage autoscaling for an Amazon RDS DB instance. 
- When Amazon RDS detects that you are running out of free database space it automatically scales up your storage. 
- Amazon RDS starts a storage modification for an autoscaling-enabled DB instance when these factors apply:
  - Free available space is less than 10 percent of the allocated storage.
  - The low-storage condition lasts at least five minutes.
  - At least six hours have passed since the last storage modification.
  - The maximum storage threshold is the limit that you set for autoscaling the DB instance. You can't set the maximum storage threshold for autoscaling-enabled instances to a value greater than the maximum allocated storage.
### RDS_Multi_AZ
![](https://d1.awsstatic.com/asset-repository/multi-az-deployments.bda9d7bf45a74103d0331a985baf2c5fb838a0fa.png)
When you provision an RDS Multi-AZ DB Instance, Amazon RDS automatically creates a primary DB Instance and synchronously replicates the data to a standby instance in a different Availability Zone (AZ). Each AZ runs on its own physically distinct, independent infrastructure, and is engineered to be highly reliable. Running a DB instance with high availability can enhance availability during planned system maintenance, and help protect your databases against DB instance failure and Availability Zone disruption. In the event of a planned or unplanned outage of your DB instance, Amazon RDS automatically switches to a standby replica in another Availability Zone if you have enabled Multi-AZ. The time it takes for the failover to complete depends on the database activity and other conditions at the time the primary DB instance became unavailable. Failover times are typically 60–120 seconds.


## Aurora
![](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/images/AuroraArch001.png)

- MySQL and PostgreSQL-compatible relational database built for the cloud, that combines the performance and availability of traditional enterprise databases with the simplicity and cost-effectiveness of open source databases. 
- **Aurora DB cluster** consists of one or more DB instances and a cluster volume that manages the data for those DB instances. 
-  **An Aurora cluster volume** is a virtual database storage volume that spans multiple AZs, with each Availability Zone (AZ) having a copy of the Amazon Aurora DB cluster data. Aurora supports Multi-AZ Aurora Replicas that improve the application's read-scaling and availability.
- Amazon Aurora features a distributed, fault-tolerant, self-healing storage system that auto-scales up to 128TB per database instance.

- Two types of DB instances make up an Aurora DB cluster:
  - **Primary DB instance** 
    - Supports read and write operations, and performs all of the data modifications to the cluster volume. 
    - Each Aurora DB cluster has one primary DB instance.
  - **Aurora Replica**
    - Connects to the same storage volume as the primary DB instance and supports only read operations. 
    - Each Aurora DB cluster can have up to 15 Aurora Replicas in addition to the primary DB instance.
-  Aurora automatically fails over to an Aurora Replica in case the primary DB instance becomes unavailable. 
-  You can specify the failover priority for Aurora Replicas.
-  Aurora Replicas can also offload read workloads from the primary DB instance.
-  You use the reader endpoint for read-only connections for your Aurora cluster. 
-  This endpoint uses a load-balancing mechanism to help your cluster handle a query-intensive workload. 
-  The reader endpoint is the endpoint that you supply to applications that do reporting or other read-only operations on the cluster. 
-  The reader endpoint load-balances connections to available Aurora Replicas in an Aurora DB cluster.
- Compatilbe API for Post
- Store in 6 replica - 3 AZ
- Cluster: Customer endopint for writer and reader DB instaces
- Aurora Machine Learning: Perfrm ML using SageMaker & Comprehend on Aurora
### Aurora_Serverless
- Amazon Aurora Serverless is an on-demand, auto-scaling configuration for Amazon Aurora (MySQL-compatible and PostgreSQL-compatible editions), where the database will automatically start-up, shut down, and scale capacity up or down based on your application's needs. 
- It enables you to run your database in the cloud without managing any database instances. 
- It's a simple, cost-effective option for infrequent, intermittent, or unpredictable workloads. 
- You pay on a per-second basis for the database capacity you use when the database is active and migrate between standard and serverless configurations with a few clicks in the Amazon RDS Management Console.
### Aurora_Back_Up
![](https://assets-pt.media.datacumulus.com/aws-saa-pt/assets/pt2-q52-i1.jpg)
- Aurora backs up your cluster volume automatically and retains restore data for the length of the backup retention period. 
- Aurora backups are continuous and incremental so you can quickly restore to any point within the backup retention period. 
- *No performance impact or interruption of database service* occurs as backup data is being written.

- Automated backups occur daily during the preferred backup window. If the backup requires more time than allotted to the backup window, the backup continues after the window ends, until it finishes. The backup window can't overlap with the weekly maintenance window for the DB cluster. Aurora backups are continuous and incremental, but the backup window is used to create a daily system backup that is preserved within the backup retention period. The latest restorable time for a DB cluster is the most recent point at which you can restore your DB cluster, typically within 5 minutes of the current time.


### Aurora_Disaster_Recovery
With an Aurora global database, you can choose from two different approaches to failover:

- **Managed planned failover** – This feature is intended for controlled environments, such as disaster recovery (DR) testing scenarios, operational maintenance, and other planned operational procedures. Managed planned failover allows you to relocate the primary DB cluster of your Aurora global database to one of the secondary Regions. Because this feature synchronizes secondary DB clusters with the primary before making any other changes, RPO is 0 (no data loss).

- **Unplanned failover ("detach and promote")** – To recover from an unplanned outage, you can perform a cross-Region failover to one of the secondaries in your Aurora global database. The RTO for this manual process depends on how quickly you can perform the tasks listed in Recovering an Amazon Aurora global database from an unplanned outage. The RPO is typically measured in seconds, but this depends on the Aurora storage replication lag across the network at the time of the failure.
### Aurora_Global_Table
![Aurora_Global_Table](https://assets-pt.media.datacumulus.com/aws-saa-pt/assets/pt2-q5-i1.jpg)
- Amazon Aurora Global Database is designed for globally distributed applications, allowing a single Amazon Aurora database to span multiple AWS regions.
- It replicates your data with no impact on database performance, enables fast local reads with low latency in each region, and provides disaster recovery from region-wide outages.
- By using an Aurora global database, you can plan for and recover from disaster fairly quickly. Recovery from disaster is typically measured using values for RTO and RPO.

-- Recovery time objective (RTO) – The time it takes a system to return to a working state after a disaster. In other words, RTO measures downtime. For an Aurora global database, RTO can be in the order of minutes.

- Recovery point objective (RPO) – The amount of data that can be lost (measured in time). For an Aurora global database, RPO is typically measured in seconds.

- https://aws.amazon.com/rds/aurora/global-database/

### Aurora_Replica
- Scale read operations of your app(reader endpoint) -> Increase avaibility
- If the writer instance becomes unavailable, automatically promotes one of the reader instances to take its place as the new write
- Up to 15 Aurora Replicas xacross the Availability Zones (AZs) tha DB cluster spans within an AWS Region.


## Elasticache
![](https://docs.aws.amazon.com/AmazonElastiCache/latest/mem-ug/images/ElastiCache-Caching.png)


- Amazon ElastiCache allows you to run in-memory data stores in the AWS cloud. Amazon ElastiCache is a popular choice for real-time use cases like Caching, Session Stores, Gaming, Geospatial Services, Real-Time Analytics, and Queuing.

- Amazon ElastiCache can be used to significantly improve latency and throughput for many read-heavy application workloads (such as social networking, gaming, media sharing, leaderboard, and Q&A portals) or compute-intensive workloads (such as a recommendation engine) by allowing you to store the objects that are often read in the cache.
- Overview of Amazon ElastiCache features: 
  - ![](https://assets-pt.media.datacumulus.com/aws-saa-pt/assets/pt4-q33-i2.jpg)


- Managed Redis / Memchaed
- In-memory datastore, sub-milisecond latency
- Support for Clustering(Redis) and Multi Az,

## DynamoDB
- A key-value and document database that delivers single-digit millisecond performance at any scale.
- It's a fully managed, multi-region, multi-master, durable database with built-in security, backup and restore, and in-memory caching for internet-scale applications.
- Can replace ElastiCahe as a key/value store
- Highly Available, Multi Az by default
- DAX cluster for reading cache
- Event Processing: DynamoDB Streaam to integrate with AWS Lamda, or Kinesis Data Streams
- Global Table feature: active-ative setup
- Export to S3
- DynamoDB can handle more than 10 trillion requests per day and can support peaks of more than 20 million requests per second
## DynamoDB_GlobalTable
![DynamoDB_GlobalTable](https://assets-pt.media.datacumulus.com/aws-saa-pt/assets/pt2-q5-i2.jpg)
- Global Tables builds upon DynamoDB’s global footprint to provide you with a fully managed, multi-region, and multi-master database that provides fast, local, read, and write performance for massively scaled, global applications. 
- Global Tables replicates your Amazon DynamoDB tables automatically across your choice of AWS region

## S3 - Lifecycle transtion
[- ![alt text](image-74.png)](https://docs.aws.amazon.com/images/AmazonS3/latest/userguide/images/lifecycle-transitions-v4.png)
## S3 - Storage Classes
[Link](https://aws.amazon.com/s3/storage-classes/)
### S3 One Zone-IA
- Amazon S3 One Zone-IA is for
  - data that is accessed less frequently,
  - requires rapid access when needed.
- Other S3 Storage Classes which store data in a minimum of three Availability Zones (AZs), IA stores data in a single Availability Zone (AZ) and costs 20% less than Standard-IA.
- One Zone-IA is ideal for customers want a lower-cost option for infrequently accessed and re-creatable data but do not require the availability and resilience of Standard or Standard-IA.
- The minimum storage duration is 30 days before you can transition objects from Standard to One Zone-IA.

## AWS_System_Manager
- Using AWS Systems Manager, you can group resources, like Amazon EC2 instances, Amazon S3 buckets, or Amazon RDS instances, by application, view operational data for monitoring and troubleshooting, and take action on your groups of resources
- 
## Cloudwatch
- [Link](https://aws.amazon.com/cloudwatch/faqs/)
- Monitoring and observability service built for DevOps engineers, developers, site reliability engineers (SREs), and IT managers. 
- Provides you with data and actionable insights to monitor your applications, respond to system-wide performance changes, optimize resource utilization, and get a unified view of operational health. 
- Allows you to monitor AWS cloud resources and the applications you run on AWS.


## SNS
- [Link](https://aws.amazon.com/sns/)
- A highly available, durable, secure, fully managed pub/sub messaging service.
- Enables you to decouple
  - microservices
  - distributed systems
  - serverless applications.
- Fully dynamically server - dynamically scale with your application
- SNS provides *topics* for high-throughput, push-based, many-to-many messaging.
## S3
- an object storage service that offers industry-leading scalability, data availability, security, and performance.
- Your applications can easily achieve thousands of transactions per second in request performance when uploading and retrieving storage from Amazon S3.
- Amazon S3 automatically scales to high request rates. For example, your application can achieve at least
  - 3,500 PUT/COPY/POST/DELETE or 5,500 GET/HEAD requests per second per prefix in a bucket.
- There are no limits to the number of prefixes in a bucket. For example, if you create 10 prefixes in an Amazon S3 bucket to parallelize reads, you could scale your read performance to 55,000 read requests per second.

- A key/value store for objects
- Great for bigger objects, not so greate for many small object
- Serverless, scale infinitely, max object size if 5 TB, versioning capacity
- Tiers: S3 Standard, S3 Infrequent Access, S3 Intelligent, S3 Galcier + Life Cycle Policty
- Security SSE-S3, SSE-KMS, SSE-C, TLS in trasit, default ecnrtypion
- Batch Operation on objects using S3 Batch, Listing file using S3 repository
- Performanace: Moti-part upload, S3 Tranfer Accelator, S3 Seelct
- Automation: S3 Event Notification(SNS, SQS, Lambda, EventBride)
## Hosting_Static_Website
![](https://assets-pt.media.datacumulus.com/aws-saa-pt/assets/pt2-q2-i1.jpg)


## Macie
![](https://d1.awsstatic.com/product-marketing/macie/Product-Page-Diagram_AWS-Macie%402x.369dcc5a001e7a44b121d65637ff82b60b809148.png)
- Amazon Macie is a fully managed data security and data privacy service that uses machine learning and pattern matching to discover and protect your sensitive data on Amazon S3. Macie automatically detects a large and growing list of sensitive data types, including personally identifiable information (PII) such as names, addresses, and credit card numbers. It also gives you constant visibility of the data security and data privacy of your data stored in Amazon S3.


## GuardDuty
![](https://d1.awsstatic.com/product-marketing/Amazon%20GuardDuty/product-page-diagram-Amazon-GuardDuty_how-it-works.a4daf7e3aaf3532623a3797dd3af606a85fc2e7b.png)

- Amazon GuardDuty offers threat detection that enables you to continuously monitor and protect your AWS accounts, workloads, and data stored in Amazon S3. GuardDuty analyzes continuous streams of meta-data generated from your account and network activity found in AWS CloudTrail Events, Amazon VPC Flow Logs, and DNS Logs. It also uses integrated threat intelligence such as known malicious IP addresses, anomaly detection, and machine learning to identify threats more accurately.


## Simple_AD
- Simple AD provides a subset of the features offered by AWS Managed Microsoft AD. Simple AD is a standalone managed directory that is powered by a Samba 4 Active Directory Compatible Server. Simple AD does not support features such as trust relationships with other domains. Therefore, this option is not correct.
## Cloud_Directory 
- Amazon Cloud Directory is a cloud-native directory that can store hundreds of millions of application-specific objects with multiple relationships and schemas. Use Amazon Cloud Directory if you need a highly scalable directory store for your application’s hierarchical data. You cannot use it to establish trust relationships with other domains on the on-premises infrastructure. Therefore, this option is not correct.
## Active_Directory_Connector
- Use AD Connector if you only need to allow your on-premises users to log in to AWS applications and services with their Active Directory credentials. AD Connector simply connects your existing on-premises Active Directory to AWS. You cannot use it to run directory-aware workloads on AWS, hence this option is not correct.
## AWS_Directory_Service
AWS Directory Service provides multiple ways to use **Amazon Cloud Directory** and **Microsoft Active Directory (AD)** with other AWS services.
- AWS Directory Service for Microsoft Active Directory (aka AWS Managed Microsoft AD) is powered by an actual Microsoft Windows Server Active Directory (AD), managed by AWS.
- With AWS Managed Microsoft AD, you can run directory-aware workloads in the AWS Cloud such as SQL Server-based applications. 
- You can also configure a trust relationship between AWS Managed Microsoft AD in the AWS Cloud and your existing on-premises Microsoft Active Directory, providing users and groups with access to resources in either domain, using single sign-on (SSO).

## DocumentDB
- Aurora is an "AWS-IMplementation" of PostgreSQL/SQL
- DocumentDB is the same for MongoDB(No SQL DB)

- MonggoDB is sued to store, query and index  JSON Data
- Similiar "deployment concepts" as Aurora
- Fully Managed, hightly available with replication aross 3 AZ
- Auto grows of 10 GB
- Automatically scales to workloads

## Neptune
- Amazon Neptune is a fast, reliable, fully-managed graph database service that makes it easy to build and run applications that work with highly connected datasets. The core of Amazon Neptune is a purpose-built, high-performance graph database engine optimized for storing billions of relationships and querying the graph with milliseconds latency.
-  Amazon Neptune is highly available, with read replicas, point-in-time recovery, continuous backup to Amazon S3, and replication across Availability Zones. Neptune is secure with support for HTTPS encrypted client connections and encryption at rest. Amazon Neptune is fully managed, so you no longer need to worry about database management tasks such as hardware provisioning, software patching, setup, configuration, or backups.
-  
- Fully managed graph database
- Higly available with repliactions across multiple AZs
- Great for
  - knowledge graphs(Wikipedia)
  - Fraud detection
  - Recommedation egnines


## Keyspace
- For apache Casandra
- Using

## Amazon QLDB
- Stand for Quantum Ledger Database
- Ledger is a book recording financial Transactions
- Review history of all chanages made to your app
- Immutable system
- Difference with Amazone Managed Blockchain: No decentralization component

## 244 Timestream
- Time series database
- Automatically Scales up/down
- Faster and cheaper


## 245 Amazon athena
- Severless query service to analyze data in S3
- SQL language(Build in Presto)
- Support CSV, Json, ORC, AVRO, Parquet
- 5 USD per TB
- With Amazone Quicksight
- Use case
  - BI
  - Analytic
  - Report & Analytic & Query VPC Flow Logs, ELB Logs, CloudTrail trails,
- Improve performance
  - Column data for cost saving
    - Apache Parquet is recomment
    - Huge Performace Improvement
    - Use glue to convert to Parquet or ORC
- Compress data for retrivil
- Partion datasets in S3
- Use larger file
- Federated query:
  - Allow to run query on AWS or on premise
  - Store result back in S3

## Redshift
- A fully-managed petabyte-scale cloud-based data warehouse product designed for large scale data set storage and analysis.
- Is base on PostgresSQL but not use for Online Tracsactio Processing
- For OLAP(Online Analytic Processing)
- Should load the data(From Kinesis Firehose)
- Ingest data to redshiff
  - Firehose -> Write S3 ->  S3 Copy -> RedShift
- EC2 -> Redshift by JDBC Driver
- Reshift Spectrum: Query data is already in S3 without loading it.

## 248 Open Search
- Amazon OpenSearch Service is a managed service that makes it easy for you to perform interactive log analytics, real-time application monitoring, website search, and more. OpenSearch is an open source, distributed search and analytics suite derived from Elasticsearch. It cannot be used as a caching layer for Amazon DynamoDB.
-
- Succesor to Elastic Search
- On DynamoDB, queries only exist by primary key or indexs
- Could search any field
- Two mode: Managed Cluster or Serverless cluster
- Security: Cognito, IAM Role
- Have OpenSearch Dashboard
- OpenSearch Patterns DynamoDB
  - DymamoDB Table -> DynamoDB Stream -> Lambda Function -> OpenSearch -> Search for Item Name -> Retrive ID -> Search Full Item in DynamoDB

- OpenSearch Patterns Clouwatch Logs

- OpenSearch Pattern Kisesis DataStream and FireHorse

## EMR
-  Amazon EMR is the industry-leading cloud big data platform for processing vast amounts of data
-  Using open source tools such as 
   -  Apache Spark
   -  Apache Hive
   -  Apache HBase
   -  Apache Flink
   -  Apache Hudi
   -  Presto. 
- Amazon EMR uses Hadoop, an open-source framework, to distribute your data and processing across a resizable cluster of EC2s
  
- Stand for Elastic MapReduce
- Create Hadoop cluster(Bigdata) -> analyze & process vast amount data

- takes care of all the provisioning and configuration
- Use cases: data processing, machine learning, web indexing, big data...
- Master Node: Manage the cluster
- Core Node: Run task and store data
- Task Note(optional)
- Purchasing Options
  - On Demand
  - Reserverd
  - Spot Intances

## DMS
![](https://d1.awsstatic.com/product-marketing/DMS/product-page-diagram-AWS-DMS_continuous-data-replication.a0e3bd328d2a4bd9b40a83e767199dcc13cf678f.png)
- **AWS Database Migration Service** helps you migrate databases to AWS quickly and securely. 
- The source database remains fully operational during the migration, minimizing downtime to applications that rely on the database. 
- Continuously replicate your data with high availability and consolidate databases into a petabyte-scale data warehouse by streaming data to *Amazon Redshift* and *Amazon S3*.
### heterogeneous_migrations
![](https://d1.awsstatic.com/product-marketing/DMS/product-page-diagram_AWS-DMS_heterogeneous-database-migrations-2.3616bac30ab86d4310ddadfdec5d6e6ba4d8b81d.png)

## 250 Quick Sight
- Severless machine learning BI Service create interative Dashboar
- Use cases:
  - Business analytics
  - Building visualizations
  - Perform ad-hoc analysis
  - Get business insights using data
- Integrated with RDS, Aurora, Athena, Redshift, S3...
- In-memory computation using SPICE engine if data is imported into QuickSight
- Enterprise edition: Possibility to setup Column-Level security (CLS)

## glue
![](https://d1.awsstatic.com/Products/product-name/diagrams/product-page-diagram_Glue_Event-driven-ETL-Pipelines.e24d59bb79a9e24cdba7f43ffd234ec0482a60e2.png)
- Serverless ETL service
- Prepare vs Tranform data for analytics
- Convert data into Parquet Format
- stored in a compressed format via the Glue job
- Glue Data Catalog:
- Glue Job Bookmarks: prevent re-processing old data
- Glue Elastic Views
  - Combine and replicate data across lultiple data stores using SQL

- Glue DataBew: Clean and nomalize data using prebuild tranformerm
- Glue Studio: new GUI to create, run and monitor ETL jobs in Glue
- Glue Streaming ETL (built on Apache Spark Structured Streaming): compatible with Kinesis Data Streaming, Kafka, MSK (managed Kafka)

## 252 AWS Lake Formation
- Data lake = central palce to have all your data for analytics purpose
- Easy to setup data lake in days
- It automates many complex manual steps(Collecting, cleansing, moveing, catloging data) and de-duplicate
- Combine Structured and untructured data in datalake
- S3, Rds, Relation & NoSql DB.
- Fine-grained access control
- Build on to of AWS Blue
- Many place in setup security

## 314 Amazon GuardDuty
-- Offers threat detection that enables you to continuously monitor and protect your AWS accounts, workloads, and data stored in Amazon S3. - GuardDuty analyzes continuous streams of meta-data generated from your account and network activity found in AWS CloudTrail Events, Amazon VPC Flow Logs, and DNS Logs.
- It also uses integrated threat intelligence such as known malicious IP addresses, anomaly detection, and machine learning to identify threats more accurately.
  ![](https://d1.awsstatic.com/product-marketing/Amazon%20GuardDuty/product-page-diagram-Amazon-GuardDuty_how-it-works.a4daf7e3aaf3532623a3797dd3af606a85fc2e7b.png)


- Intelligent Threat discover y to protect your AWS Account
- Uses Machine Learning algorithms, anomaly detection, 3rd party data
- Input data includes:
  - CloudTrail Events Logs – unusual API calls, unauthorized deployments
    - CloudTrailManagementEvents - createVPCsubnet,createtrail,...
    - CloudTrailS3DataEvents–getobject,listobjects,deleteobject,...
  - VPC Flow Logs – unusual internal traffic, unusual IP address
  - DNS Logs – compromised EC2 instances sending encoded data within DNS queries
  - Optional Features: EKS Audit Logs, RDS & Aurora, EBS, Lambda, S3 Data Events...
  - Can setup EventBridge rules to be notified in case of findings

  ## Task
  - Review cloudfront, Global Accelerator
