# System-Design_Interview

Hi my Fellow Developers this repo is for all you need to know about System Design if you read this repo you will be a master in System Design 

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
