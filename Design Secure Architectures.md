# Security Architecture

## Amazon GuardDuty
#guard-duty

![](https://d1.awsstatic.com/product-marketing/Amazon%20GuardDuty/product-page-diagram-Amazon-GuardDuty_how-it-works.a4daf7e3aaf3532623a3797dd3af606a85fc2e7b.png)

- Offers threat detection that enables you to continuously monitor and protect your AWS accounts, workloads, and data stored in Amazon S3.
- GuardDuty analyzes continuous streams of meta-data generated from your account and network activity found in AWS CloudTrail Events, Amazon VPC Flow Logs, and DNS Logs.
- It also uses integrated threat intelligence such as known malicious IP addresses, anomaly detection, and machine learning to identify threats more accurately.

- **Intelligent Threat** discover to protect your AWS Account

- Uses Machine Learning algorithms, anomaly detection, 3rd party data
- Input data includes:
    - CloudTrail Events Logs – unusual API calls, unauthorized deployments
        - CloudTrailManagementEvents - createVPCsubnet,createtrail,...
        - CloudTrailS3DataEvents–getobject,listobjects,deleteobject,...
    - VPC Flow Logs – unusual internal traffic, unusual IP address
    - DNS Logs – compromised EC2 instances sending encoded data within DNS queries
    - Optional Features: EKS Audit Logs, RDS & Aurora, EBS, Lambda, S3 Data Events...
    - Can setup EventBridge rules to be notified in case of findings

- https://aws.amazon.com/guardduty/

## IAM

### IAM Role
#iam-role

- Allow you to delegate access to users or services that normally don't have access to your organization's AWS resources.
- IAM users or AWS services can assume a role to obtain temporary security credentials that can be used to make AWS API calls.
- Consequently, you don't have to share long-term credentials for access to a resource. Using IAM roles, it is possible to access cross-account resources.

https://aws.amazon.com/iam/features/manage-roles/