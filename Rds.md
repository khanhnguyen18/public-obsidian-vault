# Rds



## Multi az
Amazon RDS Multi-AZ deployments provide enhanced availability and durability for RDS database (DB) instances, making them a natural fit for production database workloads. When you provision a Multi-AZ DB Instance, Amazon RDS automatically creates a primary DB Instance and synchronously replicates the data to a standby instance in a different Availability Zone (AZ). Multi-AZ spans at least two Availability Zones (AZs) within a single region. #multi-az

## Read replica

Amazon RDS Read Replicas provide enhanced performance and durability for RDS database (DB) instances. They make it easy to elastically scale out beyond the capacity constraints of a single DB instance for read-heavy database workloads. For the MySQL, MariaDB, PostgreSQL, Oracle, and SQL Server database engines, Amazon RDS creates a second DB instance using a snapshot of the source DB instance. It then uses the engines' native asynchronous replication to update the read replica whenever there is a change to the source DB instance. #read-replica

Amazon RDS replicates all databases in the source DB instance. Read replicas can be within an Availability Zone (AZ), Cross-AZ, or Cross-Region.

- ![Compare aureca multi-az multi region](https://assets-pt.media.datacumulus.com/aws-saa-pt/assets/pt1-q52-i1.jpg)


## RDS custom for oracle
#rds-custome
![](https://assets-pt.media.datacumulus.com/aws-saa-pt/assets/pt1-q3-i1.jpg)
- Amazon RDS is a managed service that makes it easy to set up, operate, and scale a relational database in the cloud. It provides cost-efficient and resizable capacity while managing time-consuming database administration tasks. Amazon RDS can automatically back up your database and keep your database software up to date with the latest version. However, RDS does not allow you to access the host OS of the database.