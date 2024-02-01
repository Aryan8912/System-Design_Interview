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
