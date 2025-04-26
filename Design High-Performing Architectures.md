# Design High-Performing Architectures

## Api Gateway
#api-gateway
![](https://d1.awsstatic.com/serverless/New-API-GW-Diagram.c9fc9835d2a9aa00ef90d0ddc4c6402a2536de0d.png)
- APIs act as the front door for applications to access data, business logic, or functionality from your backend services.
- RESTful APIs and WebSocket APIs that enable real-time two-way communication applications.
- Supports containerized and serverless workloads, as well as web applications.

- Amazon API Gateway creates **RESTful APIs** that:
    + Are HTTP-based.
    + Enable stateless client-server communication.
    + Implement standard HTTP methods such as GET, POST, PUT, PATCH, and DELETE.

- Amazon API Gateway creates **WebSocket APIs** that:
    * Adhere to the WebSocket protocol, which enables stateful, full-duplex communication between client and server. Route incoming messages based on message content.


### Api_Gateway_Caching
- You can enable Amazon API caching in Amazon API Gateway to cache your endpoint's responses.
- With caching, you can reduce the number of calls made to your endpoint and also improve the latency of requests to your API.
- When you enable caching for a stage, API Gateway caches responses from your endpoint for a specified time-to-live (TTL) period, in seconds.
- Amazon API Gateway then responds to the request by looking up the endpoint response from the cache instead of requesting your endpoint.
- The default TTL value for API caching is 300 seconds.
- The maximum TTL value is 3600 seconds. TTL=0 means caching is disabled.
- Using API Gateway Caching feature is the answer for the use case, as we can accept stale data for about 24 hours.