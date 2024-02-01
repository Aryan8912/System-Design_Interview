# System-Design_Interview

Hi my Fellow Developers this repo is for all you need to know about System Design if you read this repo you will be a master in System Design 

# Load Balancer
A load balancer is a critical component in distributed computing and networking that plays a central role in distributing incoming network traffic or requests across multiple servers or nodes in a way that optimizes resource utilization, maximizes throughput, minimizes response time, and ensures high availability and reliability. Load balancers are essential for several reasons in distributed systems:

*1. Distribution of Workload:* Load balancers evenly distribute incoming requests or network traffic across multiple servers. This distribution prevents any single server from becoming overwhelmed with requests while others remain underutilized. This balance optimizes the overall system's performance and ensures that resources are used efficiently.

*2. High Availability:* Load balancers enhance system availability by spreading traffic across multiple servers. If one server becomes unavailable due to hardware failure, maintenance, or other reasons, the load balancer can redirect traffic to healthy servers. This results in increased fault tolerance and reduced downtime.

*3. Scalability:* As traffic to a system grows, adding more servers or nodes can help handle the increased load. Load balancers make it easy to scale horizontally by accommodating new servers seamlessly. This scalability is essential for systems that experience variable or unpredictable workloads.

*4. Redundancy:* Load balancers can be configured with redundant components to ensure high availability. If the primary load balancer fails, a secondary one can take over without service interruption.

*5. Session Persistence:* In some cases, it's necessary to maintain session persistence, ensuring that a user's requests are consistently routed to the same server. Load balancers can be configured to support session affinity, which is important for applications that require stateful sessions.

*6. Health Checks:* Load balancers monitor the health of backend servers by periodically sending health checks or probes. If a server fails to respond or exhibits performance issues, the load balancer can automatically remove it from the pool of available servers until it recovers.

*7. Security:* Load balancers can act as a security barrier by hiding the internal infrastructure details from external users. They can also perform tasks like SSL termination, which offloads the SSL/TLS encryption and decryption process from backend servers, reducing their computational burden.

*8. Traffic Management:* Load balancers can route traffic based on various criteria, such as round-robin (equal distribution), weighted distribution (assigning different weights to servers), IP-based routing, and content-based routing (routing based on content type or URL path).

*9. Content Caching:* Some load balancers have built-in caching capabilities. They can cache static content like images or frequently accessed data to reduce the load on backend servers and improve response times.

*10. Disaster Recovery:* Load balancers can help with disaster recovery scenarios by rerouting traffic to backup data centers or locations in case of catastrophic failures or network issues.

*11. Global Server Load Balancing (GSLB):* GSLB extends load balancing to a global scale, distributing traffic across multiple data centers or geographic regions. This improves application performance, resilience, and disaster recovery capabilities.

In summary, load balancers are essential components in distributed systems because they ensure high availability, reliability, and optimal performance by distributing traffic across multiple servers or nodes. They play a crucial role in scaling applications, managing network resources, and providing fault tolerance in modern distributed computing environments.

# ACID Properties in System Design:
ACID properties are a set of principles that guarantee reliable processing of database transactions. They are crucial for ensuring data integrity and consistency in relational databases, especially in the presence of errors, power failures, and other anomalies. ACID stands for Atomicity, Consistency, Isolation, and Durability.

1. *Atomicity:*
- *What It Means:* Atomicity ensures that a transaction is treated as a single, indivisible unit, which means either all its operations are completed successfully, or none are.
- *In Practice:* If an error occurs during a transaction, any changes made up to that point are rolled back, and the database state remains unchanged. For example, in a banking system, when transferring money from one account to another, both the debit and credit operations must complete successfully; otherwise, the transaction is aborted.

2. *Consistency:*
- *What It Means:* Consistency ensures that a transaction brings the database from one valid state to another valid state, maintaining all predefined rules, such as constraints, cascades, and triggers.
- *In Practice:* After a transaction completes, all data in the database must be correct according to all defined rules. For instance, in an inventory system, a transaction should not allow the quantity of items to become negative.

3. *Isolation:*
- *What It Means:* Isolation ensures that concurrently executed transactions do not affect each other’s execution and final result. This means the transactions are isolated from each other.
- *In Practice:* The effects of an incomplete transaction should not be visible to other transactions. Different levels of isolation can be achieved (Read Uncommitted, Read Committed, Repeatable Read, Serializable), each with its trade-offs between performance and accuracy.

4. *Durability:*
- *What It Means:* Durability guarantees that once a transaction has been committed, it will remain so, even in the event of power loss, crashes, or errors.
- *In Practice:* After a transaction is completed and the changes are committed to the database, these changes are permanently recorded and will not be lost even if the system crashes immediately afterward.

Understanding ACID properties is essential in system design, particularly for applications that require high reliability and data integrity. SQL databases, like PostgreSQL, MySQL, Oracle, and SQL Server, are designed to provide these ACID guarantees, ensuring that transactions are processed reliably. This makes them suitable for a wide range of applications, including financial systems, e-commerce platforms, and any other system where data accuracy and consistency are crucial.

# Content Delivery Network (CDN)
A Content Delivery Network (CDN) is a distributed network of servers strategically located in various data centers around the world. The primary purpose of a CDN is to deliver web content, such as text, images, videos, scripts, and other media files, to end-users in a faster, more efficient, and reliable manner. CDNs offer several advantages, including:

1. *Reduced Latency:* CDNs cache content on servers that are geographically closer to end-users. This proximity reduces the time it takes for content to travel over the internet, significantly lowering latency and improving website loading times.

2. *Improved Performance:* Faster loading times lead to a better user experience. Websites and applications served through CDNs are more responsive, resulting in higher user engagement and satisfaction.

3. *Scalability:* CDNs distribute the load across multiple servers, making it easier to handle high levels of traffic and sudden spikes in demand. This scalability is essential for websites and applications with varying traffic patterns.

4. *Load Balancing:* CDNs often include load balancing mechanisms that route user requests to the nearest and least congested server, ensuring efficient content delivery and optimal performance.

5. *Distributed Redundancy:* CDNs replicate content on multiple servers in different locations. This redundancy enhances reliability and fault tolerance. If one server fails or experiences issues, traffic is automatically redirected to another server with the same content.

6. *Security:* CDNs offer security features like Distributed Denial of Service (DDoS) protection, Web Application Firewall (WAF) services, and SSL/TLS encryption to safeguard websites and applications from various threats and attacks.

7. *Bandwidth Savings:* CDNs help reduce the load on origin servers by serving cached content. This saves bandwidth and reduces hosting costs, especially for websites with extensive media content.

8. *Global Reach:* CDNs have a vast network of servers worldwide, ensuring that content is readily available to users regardless of their geographical location. This is crucial for serving a global audience.

9. *Analytics and Reporting:* Many CDNs provide analytics and reporting tools that offer insights into user behavior, traffic patterns, and performance metrics. This information can help optimize content delivery strategies.

10. *Support for Mobile Devices:* CDNs are equipped to deliver content efficiently to various devices, including desktops, smartphones, tablets, and IoT devices, ensuring a consistent user experience across platforms.

Popular CDN providers include Amazon CloudFront, Akamai, Cloudflare, Fastly, and others. Implementing a CDN typically involves configuring your domain's DNS settings to point to the CDN's servers and configuring caching and delivery rules.

CDNs are widely used by websites, e-commerce platforms, media streaming services, and any online service that relies on delivering content quickly and reliably to users across the globe. They are an essential component of modern web infrastructure, helping businesses provide a seamless online experience to their customers.

# HTTP
HTTP, which stands for Hypertext Transfer Protocol, is a fundamental protocol of the World Wide Web. It is the foundation of data communication on the internet, allowing web browsers (like Chrome, Firefox, and Safari) to retrieve and display web pages and enabling users to interact with web applications and services. Here are some key points about HTTP:

1. *Client-Server Communication:* HTTP operates on a client-server model, where one entity (the client) makes requests, and another entity (the server) responds to those requests. The client is typically a web browser or a mobile app, while the server hosts websites, web applications, or web services.

2. *Stateless Protocol:* HTTP is a stateless protocol, which means that each request from a client to a server is treated as an independent transaction. The server does not retain any information about previous requests from the same client. This statelessness simplifies the protocol but can pose challenges for maintaining user sessions in web applications.

3. *Request-Response Cycle:* An HTTP interaction follows a request-response cycle. The client sends an HTTP request to the server, specifying the desired resource (e.g., a web page URL). The server processes the request and sends back an HTTP response, which includes the requested resource or an error message.

4. *Methods (HTTP Verbs):* HTTP defines various request methods, also known as HTTP verbs, to indicate the action the client wants the server to perform. Common HTTP methods include:
   - *GET:* Retrieve data from the server.
   - *POST:* Submit data to the server for processing (e.g., submitting a form).
   - *PUT:* Update an existing resource on the server.
   - *DELETE:* Remove a resource from the server.
   - *HEAD:* Retrieve only the headers of a resource (useful for checking if a resource has been modified).
   - *OPTIONS:* Request information about the communication options supported by the server.

5. *Headers:* HTTP messages (requests and responses) include headers, which provide additional information about the message and its content. Headers can convey details like the content type, caching directives, authentication credentials, and more.

6. *Status Codes:* HTTP responses include status codes that indicate the outcome of the request. Common status codes include 200 (OK), 404 (Not Found), 500 (Internal Server Error), and many others. Status codes help clients understand how to handle the response.

7. *HTTPS:* While HTTP is the standard protocol for web communication, it does not provide data encryption or secure data transmission. To address security concerns, HTTPS (HTTP Secure) uses encryption (usually TLS/SSL) to secure data transmitted between the client and server. It's commonly used for secure online transactions, login pages, and any sensitive data transfer.

HTTP is a crucial part of the modern internet, facilitating the exchange of web content, data, and services. It forms the basis for web development and enables users to interact with websites, web applications, APIs, and various online resources.

# CAP Theorem
The CAP theorem, also known as Brewer's theorem, is a fundamental principle in distributed systems that was formulated by computer scientist Eric Brewer in 2000. The theorem highlights the inherent trade-offs between three desirable properties of a distributed system: Consistency, Availability, and Partition Tolerance. These properties are often referred to as the CAP triad:

1. *Consistency:* In a distributed system, consistency means that all nodes or components in the system see the same data at the same time. In other words, when a write operation is performed, all subsequent read operations should return the updated value. Achieving consistency ensures that the system provides strong data integrity guarantees but may lead to increased latency and decreased availability during network partitions or failures.

2. *Availability:* Availability implies that every request made to a distributed system receives a response, without guaranteeing that the response contains the most up-to-date data. An available system continues to function and respond to requests even if some nodes or components are experiencing failures. High availability is critical for systems that need to remain operational and responsive, but it may result in temporary inconsistencies between nodes.

3. *Partition Tolerance:* Partition tolerance addresses the system's ability to function and maintain its desired properties (consistency and availability) even when network partitions or communication failures occur between nodes. Network partitions can cause some nodes to become unreachable or isolated from the rest of the system. A partition-tolerant system can continue to operate despite these network issues.

The CAP theorem asserts that in a distributed system, you can achieve at most two out of the three properties simultaneously but not all three. Here are the three classic scenarios described by the CAP theorem:

1. *CA (Consistency and Availability):* In this scenario, the system prioritizes both consistency and availability at the expense of partition tolerance. It ensures that all nodes have consistent data and responds to every request, even if it means rejecting requests when a partition occurs. This model is suitable for systems where data consistency is paramount, and it can tolerate temporary unavailability.

2. *CP (Consistency and Partition Tolerance):* In this scenario, the system prioritizes both consistency and partition tolerance at the expense of availability. It guarantees that data remains consistent across all nodes and can handle network partitions, but during a partition, it may choose to become temporarily unavailable to ensure data consistency.

3. *AP (Availability and Partition Tolerance):* In this scenario, the system prioritizes availability and partition tolerance at the expense of strong consistency. It ensures that the system remains available and responsive, even during network partitions, but it may allow some degree of inconsistency between nodes, which can be resolved later.

It's important to note that the CAP theorem provides a framework for understanding trade-offs in distributed systems but does not prescribe a specific choice. The choice between CA, CP, or AP depends on the specific requirements and use cases of the distributed system. Different applications may prioritize different aspects of the CAP triad based on their needs for data consistency, availability, and fault tolerance. Additionally, advancements in distributed database technologies have led to systems that attempt to provide various degrees of consistency, availability, and partition tolerance, blurring the lines between these traditional categories.
