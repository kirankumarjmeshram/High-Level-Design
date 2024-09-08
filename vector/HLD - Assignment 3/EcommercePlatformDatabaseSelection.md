You are tasked with designing the database architecture for a new e-commerce platform that needs to handle millions of users, real-time inventory management, order processing, and product searches. The platform is expected to scale globally, requiring low latency for users in different regions.


**a. Choose a suitable database type (SQL, NoSQL, or a combination) and justify your choice based on the requirements of the platform.**
  For an e-commerce platform wih millions of users, real-time inventory management, order processing, and global scalability, a combination of SQL and NoSQL databases would be suitable
  1. SQL DB:
      **Options** :**PostgreSQL, MySQL, or Microst SQL Server**
     **Use Cases**:
     -  **Order Processing**: SQL db are well-suited for transactional data and maintaining ACID properties, which are crucial for processing orders, handling payment, and ensuring data integrity.
     -  **User Accounts**  : Relational db handles stractured data efficiently, ensuring strong consistency and complex queries, such as retrieving user order histories and managing user authentication and authorisation
  2. NoSQL DB:
      **Options** : MongoDB, Redis, Cassendra
     **Use Cases**:
     -  **Real-Time Inventory Management** : NoSQL db like MongoDB or cassandra are designed for high write throughput and can handle large volume of inventory data with low latency. They also provide **horizontal scalibility, which is essential for real-time updates and global distribution**.
     -  **Product Searches**:  A NoSQL database like MongoDB can be used for handling product catalogs and searches,leveraging its flesible schema for various attributes and its availability to schele horizontally to manage large dataset

**b. Discuss how you would ensure scalability and high availability in your chosen database solution.**
  **1  Scalability**
      **SQL Database**:
      -  **Sharding** : Implement sharding to distribute data across multiple database instance. For ex. you can shard data by user ID or geographic region
      -  **Read Replicas** : Use read replicas to distribute read queries, reducing the load on the primary database and improving read performance.
      **NoSQL DB**
      -  **Horizontal Scalling** : NoSQL databases are designed for horizontal scaling. Add more nodes to the cluster to handle increased load, and distribute data across multiple nodes.
      -  **Automatic Sharding** : Use automatic sharding (eg, in MongoDB or Cassendra) to partition data and distribute it across the cluster, balancing the load and enabling efficient scalling
  **2  High Availability**
      **SQL Database**:
        -  **Replecation** : Set up Replication to create multiple copies of the db, Implement failover mechanism to ensure that a standby replica can take over in case of primary database failure
        -  **Backup and Restore** : Regularly back up the database and test restoration procedures to ensure data can be recovered in case of outage.
      **NoSQL DB**
        -  **Replecation** : Configure replecation to Ensure that multiple copies of Data are maintained across different nodes. This provides fault tolerance and high availability
        -  **Data Consistency** : Implement eventual consistency model (if acceptable) to ensure that data is eventully consistence across distributed system.

**c. Explain how you would handle the need for both read and write operations efficiently.**
  **1 Read Operations:**
    **SQL Database** :
      **Indexes** : Create appropriate indexes on frequently queried columns to speedup read operations. For eg. index user ID, Product ID, and other IDs.
      **Caching** : Use caching layer (eg redis or memcached) to cache frequently accessed data and improve read performance
        **SQL Database** :
      **Indexes** : Use indexing features in NoSQL databases to improve query performance. For example, MongoDB provides secondary indexes that can enhance search operations on product catalogs
      **Distribute Queries** : Utilize distributed query capabilities to balance the load and efficiently handle read requests across multiple nodes.
  **2 Write Operations:**
    **SQL Database** :
      **Batch Processing** :  Use batch processing to handle multiple writes in a single transaction, reducing the overhead of individual write operations.
      **Write-Ahead Logging**: Implement write-ahead logging to ensure data integrity and durability during operations.
    **NoSQL Database** :
      **Write Optimisation** : Use write-optimized data structures and techniques to handle high write throughput. For example, Cassandra's write path is optimized for high-speed writes.
      **Data Modelling** : Design data models to minimize write amplification and ensure efficient writes. For instance, in MongoDB, structure documents to reduce the need for multiple updates.

      
