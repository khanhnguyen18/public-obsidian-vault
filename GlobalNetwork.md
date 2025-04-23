# Global Network

## *AWS Global Accelerator* 
#global_accelerator
- [Link](https://nab.udemy.com/course/aws-certified-solutions-architect-associate-saa-c03/learn/lecture/18078277)


- Utilizes the *Amazon global network*, allowing you to improve the performance of your applications by lowering first-byte latency (the round trip time for a packet to go from a client to your endpoint and back again) and jitter (the variation of latency), and increasing throughput (the amount of time it takes to transfer data) as compared to the public internet.
- AWS Global Accelerator improves performance for a wide range of applications over TCP or UDP by proxying packets at the edge to applications running in one or more AWS Regions. 
- Global Accelerator is a good fit for non-HTTP use cases, such as gaming (UDP), IoT (MQTT), or Voice over IP, as well as for HTTP use cases that specifically require static IP addresses or deterministic, fast regional failover.

- Unicast IP vs AnyCast IP
  - UI: one server hold 1 IP
  - AI: All ervers hold same IP and client is route to the neast one
- Work with Elastic IP, EC2, ALB, NLP, publish or private
## Cloud_Front
- Amazon CloudFront is a fast content delivery network (CDN) service that securely delivers data, videos, applications, and APIs to customers globally with low latency, high transfer speeds, all within a developer-friendly environment. #cloundfront