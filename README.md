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

# SQL VS NO SQL Database
Choosing between SQL (Structured Query Language) databases and NoSQL databases depends on various factors including the nature of your data, scalability needs, and the specific requirements of your application. Here are some key considerations to help decide when to use each:

SQL Databases
1. **Structured Data**: Best for handling structured data with a fixed schema, such as customer information in a CRM system.
2. **Complex Queries**: Ideal for complex query requirements. SQL databases excel in powerful query languages that can handle complex joins and transactions.
3. **ACID Transactions**: Suitable for applications that require Atomicity, Consistency, Isolation, and Durability (ACID) in transactions, like banking or financial applications.
4. **Relational Data**: If your data is heavily interrelated and you need to maintain those relationships, SQL is typically a better choice.
5. **Stability and Maturity**: SQL databases, such as MySQL and PostgreSQL, are mature technologies with a wealth of support and documentation.
6. **Reporting and Analysis**: Better for scenarios where you need to perform in-depth analysis and generate reports.

NoSQL Databases
1. **Unstructured or Semi-Structured Data**: Ideal for unstructured or semi-structured data, such as JSON, XML, and other document formats.
2. **Scalability**: More suitable for applications that require horizontal scalability, as they are designed to expand easily across multiple servers.
3. **High-Volume Data**: Better for handling large volumes of data at high speed, like real-time analytics or big data applications.
4. **Flexible Schema**: Useful when you have rapidly changing schemas or when you want to iterate quickly without having to migrate a database schema.
5. **Variety of Data Types**: They support a wide range of data types and structures, such as key-value, document, columnar, and graph databases.
6. **Simplicity and Speed**: Generally simpler and can offer higher write and read speeds for certain workloads.

Considerations
- **Consistency Requirements**: SQL databases often offer stronger consistency models compared to NoSQL databases.
- **Skill Set**: Consider the expertise available in your team. SQL is a widely known language, whereas NoSQL databases might require additional learning.
- **Vendor Lock-In**: Some NoSQL databases are proprietary, which might lead to vendor lock-in.
- **Cost**: Evaluate the total cost of ownership, including licensing, maintenance, and scaling costs.

In summary, use SQL when you need to work with structured data with complex relationships and require strong transactional integrity. Opt for NoSQL when dealing with large volumes of diverse, unstructured, or semi-structured data and when you need high throughput and horizontal scalability. Often, the choice isn't strictly binary; many modern applications use a combination of both SQL and NoSQL databases to meet their diverse data needs.

# Token Bucket Algorithm

The Token Bucket Algorithm is a popular method for controlling the rate at which events occur in distributed systems, particularly in scenarios where events or requests need to be limited to a specified rate. It's commonly used for rate limiting, traffic shaping, and ensuring that a system does not exceed a defined rate or burstiness of events. Here's how the Token Bucket Algorithm works:

1. *Token Bucket:* Imagine a bucket that gets filled with tokens at a fixed rate. These tokens represent permission or credit to perform an action or event. The bucket has a maximum capacity, and any tokens beyond this capacity are discarded.

2. *Token Generation:* Tokens are generated at a constant rate and added to the bucket. For example, if you want to allow 10 requests per second, you might add one token every 100 milliseconds.

3. *Request Processing:* When an event or request arrives, it must consume one or more tokens from the bucket to proceed. If there are not enough tokens available, the event is delayed until there are sufficient tokens or discarded if the bucket is empty.

4. *Bucket Capacity:* The bucket has a maximum capacity that limits the number of tokens it can hold. Tokens added to a full bucket are simply discarded.

Key Characteristics and Advantages:

- *Rate Control:* The Token Bucket Algorithm provides precise control over the rate at which events or requests are allowed to occur.

- *Burst Handling:* The algorithm can handle bursts of traffic efficiently. If tokens accumulate in the bucket, short bursts of events can be accommodated.

- *Simplicity:* It's a straightforward algorithm to implement and understand, making it a popular choice for rate limiting.

- *Predictable Behavior:* The Token Bucket Algorithm ensures a predictable and stable rate of event processing, which can be beneficial for system stability.

- *Adaptability:* By adjusting the token generation rate or bucket capacity, you can easily adapt the algorithm to different rate-limiting requirements.

- *Enforcement:* It enforces rate limits effectively, preventing excessive resource consumption or abuse of a service.

Use Cases:

1. *API Rate Limiting:* Many APIs use the Token Bucket Algorithm to limit the number of requests a user or client can make within a certain time frame.

2. *Traffic Shaping:* Network devices use token buckets to shape traffic, ensuring that data flows conform to a specified rate or burstiness.

3. *Distributed Systems:* Token buckets are employed in distributed systems to control the rate of events or messages exchanged between nodes.

4. *Resource Allocation:* It can be used to allocate resources, such as CPU time or bandwidth, among competing processes or users.

In summary, the Token Bucket Algorithm is a valuable tool for controlling the rate of events in distributed systems, ensuring that they stay within defined limits and preventing overuse of resources. It provides predictable and stable rate limiting, making it suitable for various rate control scenarios.

# Round Robin Load Balancing
Round Robin is a straightforward and widely used load balancing algorithm that distributes incoming network requests or tasks evenly among a group of backend servers or resources. It's a simple algorithm that ensures that each server in the pool gets a turn to handle a request in a cyclic or circular fashion. Here's how Round Robin load balancing works:

1. *Server List:* The load balancer maintains a list of available servers that can handle incoming requests. These servers are typically identical in terms of capacity and capabilities.

2. *Request Arrival:* When a new request arrives at the load balancer, it needs to be directed to one of the servers in the list.

3. *Server Selection:* The load balancer selects the next server from the list to handle the request. It follows a cyclical pattern, meaning that it starts from the beginning of the list and goes through the servers in order.

4. *Request Forwarding:* The selected server is then assigned the incoming request to process. The load balancer forwards the request to the chosen server.

5. *Rotation:* After handling a request, the selected server moves to the end of the server list. The next request will be directed to the server that follows it in the list. This rotation continues for each incoming request.

Key characteristics and considerations of Round Robin load balancing:

- *Even Distribution:* Round Robin ensures that requests are distributed evenly among the servers. Each server gets an equal share of incoming traffic, preventing overloading of any one server.

- *Simplicity:* Round Robin is straightforward to implement and doesn't require complex algorithms or state tracking. It's easy to understand and manage.

- *No Server State Consideration:* Round Robin does not take into account the current load or performance of each server. It treats all servers equally and doesn't consider factors like server health or response times.

- *Predictable Behavior:* Since the distribution pattern is deterministic, you can predict which server will handle the next request in the rotation.

Round Robin load balancing is suitable for scenarios where servers are relatively homogeneous in terms of capacity and performance, and where simplicity and equal distribution are more important than advanced load balancing considerations. However, it may not be the best choice in situations where server capacities vary significantly or when you want to consider server health, response times, or load before distributing traffic. In such cases, more advanced load balancing algorithms, such as weighted Round Robin or least connections, may be used.

Overall, Round Robin load balancing is a reliable and easy-to-implement approach that is commonly used in various network and web hosting setups to distribute traffic among a group of servers.
