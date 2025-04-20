# EC2

### EC2 Placement Group
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

