# AWS Storage Extras


## AWS Snow Family

### Snowmobile
#snowmobile
- Each AWS Snowmobile has a total capacity of up to 100 petabytes. To migrate large datasets of 10 petabytes or more in a single location, you should use AWS Snowmobile.

### AWS Snowball
#snowball
- Highly-secure, portable devices to collect and process data at the edge, and migrate data into and out of AWS
- Offline devices(More than a week)
- Migrate Petabyte of data
- Type
    - Edge Storage Optimized 210 TB 105 CPU(Replace for 80 TB)
    - Edge Computed Optimized 28 TB(Edge computing) 104 CPUs
        - Process data when it's being created on an edge location
        - Limited internet and no access to compter power
        - We setup Snowball Edge device to do edge computing
        - Run EC2 & Lambda function at the edge
        - Use case: preprocess data, machine learning, transcoding Media

- Glacier
    - Cannot import to Galcier
    - Combine with S3 lifecycle policy
        - SnowBall -import> S3 -policy> Glacier

### Amazone FSx
- Launch 3rd party high-performace file system on AWS
- Full managed service
- Type
    - For Luster
    - For window file server
    - NetApp on tap
    - Open Zfs

## Storage Gateway Overview
#storage-gateway
![alt text](StorageGateway.png)
- https://nab.udemy.com/course/aws-certified-solutions-architect-associate-saa-c03/learn/lecture/13528358

- Bridge between on-premise data and cloud data
- Use cases
    - disaster recovery
    - backup-restore
    - tiered storage
    - on-premise cach && low-lantacy file access

- AWS is publish for `hydrid cloud` because of
    - security
    - Long migration
- S3 data on on-premises server
- Options
    - Block
        - EBS
        - EC2 Intance Store
    - File
        - EFS
        - FSs
    - Object
        - S3
        - Glacier
- Type
    - S3 File Gateway
    - Fsx File gate way
    - Volumne Gate way
    - Tape Gateway

## S3 File Gateway
- ![](https://d1.awsstatic.com/cloud-storage/Amazon%20S3%20File%20Gateway%20How%20It%20Works%20Diagram.96e9f7180c6ec8b6212b4d6fadc4a9ac4507b421.png)

## FSx File Gateway
## Volume Gateway
- ![](https://d1.awsstatic.com/cloud-storage/volume-gateway-diagram.eedd58ab3fb8a5dcae088622b5c1595dac21a04b.png)


- Block storage using iSCSI p protocol backed by S3
- backed by EBS Snapshot help
- Cached volume: low latecy  access to most recent data
- Stored volume: entire  datashet is on premise

## Tape gateway
![](https://d1.awsstatic.com/product-marketing/Product-Page-Diagram_Tape-Gateway_HIW%402x%20(2).5ba3326ea93003722acc487804a34971613ec3c1.png)
- Backup process for physical tape
- Virtaul Tape Libray(VTL) backed by S3 and Glacier

## Hardware appliance


## AWS Transfer family
- Full-managed services file transfer in/out S3 or EFS using FTB protocol
- Support:
    - Ftp
    - Ftps
    - SFTP
- Pay per provisioned endpoint per hour + data transfer in GB
- Integraed with authentication service(Cognito, Active Directory, LDAP ...)

## Data sync
- Move large amount data to and from:
    - On-premiese
    - AWS to AWS
- Can sync to
    - S3
    - EFS
    - FSx

## Storage comparison
- S3: Object Storage
- S3 Glacier: Object Archival
- EBS volumes: Network storage for one EC2 instance at a time
- Instance Storage: Physical storage for your EC2 instance (high IOPS)
- EFS: Network File System for Linux instances, POSIX filesystem
- FSx for Windows: Network File System for Windows servers
- FSx for Lustre: High Performance Computing Linux file system
- FSx for NetApp ONTAP: High OS Compatibility
- FSx for OpenZFS: Managed ZFS file system
- Storage Gateway: S3 & FSx File Gateway, Volume Gateway (cache & stored), Tape Gateway
- Transfer Family: FTP, FTPS, SFTP interface on top of Amazon S3 or Amazon EFS
- DataSync: Schedule data sync from on-premises to AWS, or AWS to AWS
- Snowcone / Snowball / Snowmobile: to move large amount of data to the cloud, physically
- Database: for specific workloads, usually with indexing and querying