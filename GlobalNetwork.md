# Global Network

## *AWS Global Accelerator* 
#global-accelerator
- [Link](https://nab.udemy.com/course/aws-certified-solutions-architect-associate-saa-c03/learn/lecture/18078277)


- Utilizes the *Amazon global network*, allowing you to improve the performance of your applications by lowering first-byte latency (the round trip time for a packet to go from a client to your endpoint and back again) and jitter (the variation of latency), and increasing throughput (the amount of time it takes to transfer data) as compared to the public internet.
- AWS Global Accelerator improves performance for a wide range of applications over TCP or UDP by proxying packets at the edge to applications running in one or more AWS Regions. 
- Global Accelerator is a good fit for non-HTTP use cases, such as gaming (UDP), IoT (MQTT), or Voice over IP, as well as for HTTP use cases that specifically require static IP addresses or deterministic, fast regional failover.

- Unicast IP vs AnyCast IP
  - UI: one server hold 1 IP
  - AI: All ervers hold same IP and client is route to the neast one
- Work with Elastic IP, EC2, ALB, NLP, publish or private

## Cloudfront
#cloundfront
- CDN service that securely delivers data, videos, applications, and APIs to customers globally with low latency, high transfer speeds, all within a developer-friendly environment.
- CloudFront points of presence (POPs) (edge locations) make sure popular content can be served quickly to your viewers. 
### Cloudfront_route_mulitple_origin
- Can route to **multiple origins based** on the content type
  - You can configure a single Amazon CloudFront web distribution to serve different types of requests from multiple origins. For example, if you are building a website that serves static content from an Amazon Simple Storage Service (Amazon S3) bucket and dynamic content from a load balancer, you can serve both types of content from a Amazon CloudFront web distribution.
### Cloudfront_secondary_origin
- Use an *origin group with primary and secondary origins* to configure Amazon CloudFront for high-availability and failover
  - ![](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/images/origingroups-overview.png)
  - You can set up Amazon CloudFront with origin failover for scenarios that require high availability. To get started, you create an origin group with two origins: a primary and a secondary. If the primary origin is unavailable or returns specific HTTP response status codes that indicate a failure, CloudFront automatically switches to the secondary origin.
### Cloudfront_field_level_encryption
- Use **field level encryption** in Amazon CloudFront to protect sensitive data for specific content
  - Field-level encryption allows you to enable your users to securely upload sensitive information to your web servers. The sensitive information provided by your users is encrypted at the edge, close to the user, and remains encrypted throughout your entire application stack. This encryption ensures that only applications that need the data—and have the credentials to decrypt it—are able to do so.

- To use field-level encryption, when you configure your Amazon CloudFront distribution, specify the set of fields in POST requests that you want to be encrypted, and the public key to use to encrypt them. You can encrypt up to 10 data fields in a request. (You can’t encrypt all of the data in a request with field-level encryption; you must specify individual fields to encrypt.)

To set up origin failover, you must have a distribution with at least two origins. Next, you create an origin group for your distribution that includes two origins, setting one as the primary. Finally, you create or update a cache behavior to use the origin group.


- CloudFront has regional edge caches that bring more of your content closer to your viewers, even when the content is not popular enough to stay at a POP, to help improve performance for that content.
- You can use different origins for different types of content on a single site – e.g:
  - Amazon S3 for static objects
  - Amazon EC2 for dynamic content
  - Custom origins for third-party content.
- **Regional edge caches** help with all types of content, particularly content that tends to become less popular over time. Examples include user-generated content, such as video, photos, or artwork; e-commerce assets such as product photos and videos; and news and event-related content that might suddenly find new popularity.
### Cloudfront With S3
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

### Cloudfront Origin failover feature
#cloudfront-origin-failover
- help support your data resiliency needs. Amazon CloudFront is a global service that delivers your content through a worldwide network of data centers called edge locations or points of presence (POPs). 
- If your content is not already cached in an edge location, x retrieves it from an origin that you've identified as the source for the definitive version of the content.


