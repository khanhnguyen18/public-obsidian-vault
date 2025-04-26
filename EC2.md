# EC2

## AMI
#ami
![](https://assets-pt.media.datacumulus.com/aws-saa-pt/assets/pt1-q41-i1.jpg)
- AMI provides the information required to launch an instance. You must specify an AMI when you launch an instance. 
-  https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AMIs.html



## EC2 Placement Group
- https://nab.udemy.com/course/aws-certified-solutions-architect-associate-saa-c03/learn/lecture/26118770#overview

- Depending on the type of workload, you can create a placement group using one of the following placement strategies:
  - **Cluster** 
    - Packs instances close together inside an AZ. ![](https://assets-pt.media.datacumulus.com/aws-saa-pt/assets/pt2-q12-i1.jpg)
    - This strategy enables workloads to achieve the low-latency network performance necessary for tightly-coupled node-to-node communication that is typical of high-performance computing (HPC) applications.
  - **Partition**:
    - do not share underlying harware with groups instances(Kafka, Hadoop , Cassandra)
    - A partition placement group can have a maximum of seven partitions per AZ
    ![Partition](https://assets-pt.media.datacumulus.com/aws-saa-pt/assets/pt2-q12-i2.jpg)
  - **Spead**: 
    - Strictly place small group of intances accross distince underlying harware to reduce correlated failures.
    - seven partitions per AZ
  ![](https://assets-pt.media.datacumulus.com/aws-saa-pt/assets/pt2-q12-i3.jpg)
- More information: https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/placement-groups.html

## EC2 Intance Storage
### EFS
#efs
- Managed NFS(Network file system)
- ECS in multi-az
- Highly available, scalable, expensive
- Use case: content management, web serving, data sharing, wordpress
- Use security group for access EFS
- Enryption KMS
- POSIX file system(Linus)
- Scale Automatically, no capacity planing
- Storage class:
  - EFS Scale
  - Performance Mode
  - Throughput Mode

### EBS
#ebs
- Network Drive(as USB Stick - a bit latency) you can attach to your instance while they run -> persist data -> even after they terminated
  - Detach and attach to EC2
- One intance at a time(CPP level) specific **AZ**
  - move need to snapshot it
- Have provisioned capacity(size in **GBs**, and **IOPS**)

- Delete on Termination attribute
  - Root are default
  - Other  EBS is not deleted 
  - -> *preserve root volumne when instanc is termintate*

#### EBS Snapshot
#ebs-snapshot
- https://nab.udemy.com/course/aws-certified-solutions-architect-associate-saa-c03/learn/lecture/26098276#overview
- Make backup(EBS) of EBS volume at a point of time
- Don't need to detach volumne, but recommend
- Can copy across AZ, Region
- Type
  - 1. EBS Snapshot Archive
    - Move Snapshot -> archive tier 75% cheaper
    - 24 to 72hour to restore
  - 2. Recycle bin 
    - Setup rule for this
    - Specific retention(1 day to 1 year)
  - 3. Fast  snapshot restore
    - No latency on the first use(More money)

#### EBS Volume type
- https://nab.udemy.com/course/aws-certified-solutions-architect-associate-saa-c03/learn/lecture/26098296#overview


### AMI
- https://nab.udemy.com/course/aws-certified-solutions-architect-associate-saa-c03/learn/lecture/26098284#overview
- Is cutomization of EC2 Instance
- For specific region(cp)
- Launch EC2 from
  - Public AMI: AWS provide
  - Your own AMI
  - Market AMI: from someone sale
  - Build AMI -> EBS snapshot
### Instance store
#instance-store
- need high-performance hardware disk, EC2 instance
- lose their storage if thery're stop(ephemeal)