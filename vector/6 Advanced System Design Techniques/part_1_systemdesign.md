### **Problem :**

#### Instructions

### **Scenario: Building a Distributed Cloud Storage Platform**

You have been hired as a lead architect for a company that is building a cloud-based storage platform similar to **Dropbox** or  **Google Drive** . This system allows users to upload, download, and manage files through web and mobile applications. The system should handle millions of users and must be highly scalable, reliable, and secure. The platform will consist of multiple microservices for various operations like file management, user authentication, and billing.

The key components of the system are:

1. **Distributed File System (DFS)** :

* All user data must be stored in a  **distributed file system** . The DFS should handle large volumes of data, ensure fault tolerance, and provide efficient access to files.

1. **API Gateway** :

* Users interact with the system through an **API Gateway** that handles routing of requests to the appropriate microservices.
* The API Gateway should implement **rate limiting** to protect against abuse or accidental overloading of the system.

1. **Rate Limiting** :

* The system should impose rate limits to prevent individual users from overloading the system. This includes limiting the number of file uploads/downloads per minute.

1. **Monitoring & Logging** :

* The platform should have comprehensive **monitoring** and **logging** to track system health, detect performance bottlenecks, and troubleshoot issues. Logs should capture key events (file uploads/downloads, user activity, API errors), while monitoring should track key performance metrics like file access latency, storage usage, and request rates.

---

### **Part 1: System Design**

**Question:** Design a system architecture for the cloud storage platform using the following components:

* **DFS** to store user files.
* **API Gateway** to handle incoming requests.
* **Rate Limiting** to restrict API calls.
* **Monitoring and Logging** to observe system health and troubleshoot issues.

Your design should include:

1. **Storage Layer:**
   * Describe the role of the **Distributed File System (DFS)** in this platform. What are the key characteristics that the DFS must have (e.g., consistency, fault tolerance, replication)?
   * Which type of DFS would you choose (e.g., HDFS, Amazon S3, Google Cloud Storage) and why?
2. **API Gateway:**
   * Explain how the API Gateway will manage routing requests to the backend services (e.g., file upload, file download, user authentication).
   * How will the API Gateway handle  **authentication and authorization** ?
3. **Rate Limiting:**
   * Propose a rate-limiting strategy for API requests. Users should be limited to 50 file uploads per minute and 100 file downloads per minute.
   * How will you ensure the rate-limiting strategy works across multiple instances of the API Gateway in a distributed environment?
4. **Monitoring and Logging:**
   * Identify the key **metrics** you would monitor to ensure the system is performing efficiently (e.g., latency of file access, error rates, API request throughput).
   * Propose a **logging** strategy that captures relevant events. What specific information would you include in the logs, and how will you ensure that logs are centralized and searchable?

**Solution**

### **Part 1: System Design**

#### **1. Storage Layer (Distributed File System - DFS)**

**Role of DFS:**
The DFS is responsible for storing and managing user files in a highly scalable, fault-tolerant, and distributed manner. The DFS must support high availability and durability of files across multiple nodes and regions. The key characteristics include:

* **Scalability** : The system should be able to store petabytes of data and handle a growing number of users.
* **Fault Tolerance** : Redundancy and replication should ensure no data loss, even if individual nodes fail.
* **Consistency** : Ensuring consistency when multiple clients access or modify files concurrently.
* **Low Latency** : Efficient access times for retrieving files.

**DFS Choice:**

* **Amazon S3 or Google Cloud Storage** : These are ideal for a highly scalable, managed distributed storage system.
* **Why S3/Google Cloud Storage?** They offer built-in redundancy, data replication across regions, automatic failover, and strong APIs for interaction. Moreover, they are highly available, durable, and easy to integrate with other cloud services like Lambda functions for event-driven processing.
* 

#### **2. API Gateway**

The API Gateway serves as the entry point for all user requests, managing routing to the backend services. It handles authentication, rate-limiting, logging, and routing to microservices.

* **Routing** : The API Gateway routes requests to appropriate microservices (file upload/download service, user authentication service, etc.).
* **Example** : For a file upload request, it will route to the file management service, while for user login, it will route to the user service.
* **Authentication & Authorization** : The API Gateway integrates with OAuth2.0 or JWT to handle authentication and authorization of users. The user’s token is verified for each request, and appropriate access controls are applied.
* **Example** : When accessing the file download service, the token is checked to ensure the user has the correct permissions.

#### **3. Rate Limiting**

The API Gateway will enforce rate limits to ensure fair usage and prevent system abuse.

**Rate Limiting Strategy:**

* **Per-user basis** : Each user can upload up to 50 files and download 100 files per minute.
* **Sliding Window Algorithm** : Implemented using Redis, the sliding window will track API requests within a 60-second window.
* Each time a user makes a request, it is recorded in Redis with the current timestamp.
* Redis commands (`ZADD`, `ZRANGEBYSCORE`) are used to add and manage timestamps.

**Distributed Rate Limiting:**

* **Centralized store (Redis)** : The rate limit data for users is stored in Redis, ensuring that all instances of the API Gateway can access and update the rate limit counters.
* **Global consistency** : Redis clusters across regions can help maintain rate-limiting data globally, ensuring users are consistently rate-limited across multiple instances.

#### **4. Monitoring and Logging**

**Key Metrics:**

* **File access latency** : Track how long it takes for files to be uploaded or downloaded.
* **Request rate** : Number of API requests per minute to detect spikes.
* **Storage usage** : Monitor the total amount of storage used and available capacity.
* **Error rates** : Track the number of errors (e.g., failed uploads/downloads).
* **Throughput** : Track the rate at which data is transferred during uploads/downloads.

**Logging Strategy:**

* **Events to Log** :
* User activities (login, file upload/download).
* API errors and responses (HTTP status codes).
* File access patterns (timestamps, file sizes, regions).
* **Centralized Log Storage** :
* Use services like **ELK Stack (Elasticsearch, Logstash, Kibana)** or **AWS CloudWatch** for centralized log collection and analysis.
* Logs should be searchable with structured formats, capturing user IDs, request timestamps, request paths, and error messages.
