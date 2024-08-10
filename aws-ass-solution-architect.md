# AWS Solution Architect

## Link

open "/Users/P836088/project/markdown-documents/work/AWS/AWS-Certified-Solutions-Architect-Slides-v37.pdf"

## 11. IAM Introduction: Users, Groups, Policies

* Global service
* Root account use
* Policies is define permission of user
* Apply least previledge principle


## 13. IAM Role

 ![alt text](image-40.png)

* Statment consist of
  * Sid
  * Effect
  * Principal
  * Action
  * Resource


## Section 5

### 30. AWS Budget setup

 ![alt text](image-39.png)o

## 31. EC2 
### EC2 - Pricing
- https://aws.amazon.com/ec2/pricing/


### 32.

## 57

* EBS snapshot archive: 75% cheaper

## EFS
- Provides a simple, scalable, fully managed elastic NFS file system for use with AWS Cloud services and on-premises resources.
- Storing data within and across multiple Availability Zones (AZs) for high availability and durability
- EC2 instances can access your file system across AZs, regions, and VPCs 
- On-premises servers can access using AWS Direct Connect or AWS VPN.

- #1.13: You can connect to EFS file systems from EC2 instances in other AWS regions using an inter-region VPC peering connection, and from on-premises servers using an AWS VPN connection


## 69. High Availability and Scalability

* High Avallability usually goes hand in hand with horizontal
* High availability means running your application / system in at least 2 data centers == AZ)

• Horizontal Scaling: Increase number of instances 😊 scale out / in)

* Auto Scaling Group
* Load Balancer

• High Availability:

* Run instances for the same application across multi AZ
* Auto Scaling Group multi AZ

## 70. Elastic Load Balancing (ELB) Overview 
### Application Load Balancer (ALB)



## 72. ALT

* x-forward-for

## 73. ALB demo

* Create target group
* Practice load balancer

## 74

* Only allow access from ALB
* Define condition rule

## 78

* Sticky cooki

## 79 Cross zone Load Balancing

## 81 SSL Hand on

Add listener

## 83 Auto Scaling Group (ASG)

The goal of an Auto Scaling Group (ASG) is to:
• Scale out (add EC2 instances) to match an increased load
• Scale in (remove EC2 instances) to match a decreased load
• Ensure we have a minimum and a maximum number of EC2 instances running
• Automatically register new instances to a load balancer
• Re-create an EC2 instance in case a previous one is terminated (ex: if unhealthy)

 ![alt text](image-41.png)
Auto Scaling - CloudWatch Alarms & Scaling
• It is possible to scale an ASG based on CloudWatch alarms
• An alarm monitors a metric (such as Average CPU, or a custom metric)
• Metrics such as Average CPU are computed for the overall ASG instances

## 88. Rds red rplicas vs Multiaz

* Network Cost
  * not pay fee for RDS read Rplca winthin in same region
  * \

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

Auto

 ![alt tvsext](image-42.png)

## 98. Elastic Cache HandOn

* Security
   ![alt text](image-43.png)
  * Encryption Config
    * Transit
    * At rest
  * Security
* Cluster detail:
   ![alt text](image-44.png)
  * Primary Endpoint
  * Reader Endpoint

## 99. Elastic Cache for SA

*  ![alt text](image-46.png)
*  ![alt text](image-47.png)

## 101. Route 53








1. What is *DNS* and dd
   \[LINK\](This is a link)
   dns

## Question

* Subnet: Span all azs


 ![alt text](image-48.png)

* *DNS Record Time*:
   ![alt text](image-49.png)

   ![alt text](image-50.png)
* *Go to AWS Cloudshell*
  * sudo yum install -y bind-utils
  * nslookup  test.steahan...
  * dig

## 105 EC2 setup

* Create 3 EC2
* Create load balancer

## 106 TTL(Time to live)

* \

## 107. CNam and Alias

 ![alt text](image-51.png)

* Alias: Point hostname to aws resource
* CName not for apex record

## Route 53 - Health Check


## 127 S3

* So3 looks like a global service but buckets are created in a region
* *Prefix* = Directory
*  ![alt text](image-52.png)
* Bucket
* Object
  * Metadata
  * Tags
  * Version ID(if enable)
* Default *encrytiokn*
  * SSE-S3
  * KMS

### S3 Security

- User base
  - Which url could use for specific user
- Resource Base
  - Bucket Policies: 
  - Object Access Controler LIst - Finer Grant
  - Bucket(ACL)

## 130 Bucket policy

* Use tool to generate policy

## Amazon S3 Transfer Acceleration**
- enables fast, easy, and secure transfers of files over long distances between your client and an S3 bucket. 
- Takes advantage of *Amazon CloudFront’s globally distributed edge locations*.
- As the data arrives at an edge location, data is routed to Amazon S3 over an optimized network path.

## S3 – Requester Pays

* With Requester Pays buckets, the requester instead of the bucket owner pays the cost of the request and the data download from the bucket

## S3 - Access Point

* VPC Origin - *DNS Name*
* EC2 could create VPC Enpoint(Gateway or Interface Endpoint)


## 163 - S3 - Object Standard



## Cloudfront
- CDN service that securely delivers data, videos, applications, and APIs to customers globally with low latency, high transfer speeds, all within a developer-friendly environment.
- CloudFront points of presence (POPs) (edge locations) make sure popular content can be served quickly to your viewers.
- has regional edge caches that bring more of your content closer to your viewers, even when the content is not popular enough to stay at a POP, to help improve performance for that content.

### Origin failover feature
- support your data resiliency needs.
- If your content is not already cached in an edge location, 
    -> CloudFront retrieves it from an origin that you've identified as the source for the definitive version of the content.
#### 165 Cloudfront with S3

* Origin access
* Distribution

## 170. Global Accelator
- Improves the availability and performance of your applications with local or global users. 
- Provides static IP addresses that act as a fixed entry point to your application endpoints in a single or multiple AWS Regions such as ALB, NLB, EC2 instances. 
- Good fit for non-HTTP: UDP, MQTT, Voice Over IP, HTTP specifically IP

- not help in accelerating the file transfer speeds into S3 for the given use-case.
- When go public internet - A lot of latency because there many hops
- Unicast IP: 1 server 1 IP
- Any Cast IP: Same Ip, client is routed to near on
- Global Accelator: Talk to closed Edge location -> Public ALP
- Create Private AWS network
- Perform healcheck for your app

# AWS Direct Connect
- Establish a dedicated network connection from your premises to AWS. 
- AWS Direct Connect lets you establish a dedicated network connection between your network and one of the AWS Direct Connect locations.
- With *AWS Direct Connect* plus *VPN*, you can combine one or more AWS Direct Connect dedicated network connections with the *Amazon VPC VPN*. This combination provides an *IPsec-encrypted private connection* that also reduces network costs, increases bandwidth throughput, and provides a more consistent network experience than internet-based VPN connections.
- Involves significant monetary investment and takes at least a month to set up, therefore it's not the correct fit for this use-case.

## AWS Transit Gateway
-  A network transit hub that you can use to interconnect your virtual private clouds (VPC) and on-premises networks. AWS Transit Gateway by itself cannot establish a low latency and high throughput connection between a data center and AWS Cloud.

## AWS site-to-site VPN
- AWS Site-to-Site VPN enables you to securely connect your on-premises network or branch office site to your Amazon Virtual Private Cloud (Amazon VPC). 
- A VPC VPN Connection utilizes IPSec to establish encrypted network connectivity between your intranet and Amazon VPC over the Internet. 
- VPN Connections are a good solution if you have an immediate need, have low to modest bandwidth requirements, and can tolerate the inherent variability in Internet-based connectivity. 
- However, Site-to-site VPN cannot provide low latency and high throughput connection, therefore this option is ruled out.


## AWS Snow Family

* Ops Hub
* Data transfer

- *AWS Snowball Edge Storage Optimized*: It provides up to 80 Terabytes of usable HDD storage, 40 vCPUs, 1 TB of SATA SSD storage, and up to 40 Gigabytes network connectivity to address large scale data transfer and pre-processing use cases.
- Snowmobile: 100 petabyte in one location

## Amazon FSx for Windows File Server
- provides all of the benefits of a native Windows SMB environment that is fully managed and secured and scaled like any other AWS service. You get detailed reporting, replication, backup, failover, and support for native Windows tools like DFS and Active Directory.
;'lopfdpgtikdcxojjgtkfidcncibdcl  support file shares in Amazon FSx for Windows File Server, so this option is incorrect.
- Amazon FSx File Gateway: low-latency, on-premises access to fully managed file shares in Amazon FSx for Windows File Server. For applications deployed on AWS, you may access your file shares directly from Amazon FSx in AWS
## 178 Storage gateway

* Block storage
* Object Storgae
* File gate
* NFS
* Active Story
* iScis
* *Volume Gateway*
  * Cached Volume
  * Stored Volumne: