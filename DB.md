

# DB

## 
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
### Aurora_Cloning
You can quickly create clones of an Aurora DB by using the database cloning feature. In addition, database cloning uses a copy-on-write protocol, in which data is copied only at the time the data changes, either on the source database or the clone database. Cloning is much faster than a manual snapshot of the DB cluster.

For the given use case, the most optimal solution is to clone the DB cluster. This would allow the performance testing team to have quick access to the production data in an isolated way. The team can iterate over the various test phases by deleting existing test databases and then cloning the production DB to create new test databases.

You cannot clone databases across AWS regions. The clone databases must be created in the same region as the source databases. Currently, you are limited to 15 clones based on a copy, including clones based on other clones. After that, only copies can be created. However, each copy can also have up to 15 clones.
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

### Aurora Replica
#aurora-replica
- Scale read operations of your app(reader endpoint) -> Increase avaibility
- If the writer instance becomes unavailable, automatically promotes one of the reader instances to take its place as the new write
- Up to 15 Aurora Replicas xacross the Availability Zones (AZs) tha DB cluster spans within an AWS Region.
