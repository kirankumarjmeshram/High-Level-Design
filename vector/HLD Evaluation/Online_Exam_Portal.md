# **Scalable Online IIT JEE Exam Portal**

### 1. High-Level Architecture

#### **Architecture Type: Microservices**

* **Why Microservices?**
  * **Scalability** : Each service can be scaled independently. Exam-taking service needs to scale more than the registration service.
  * **Resilience** : If one service fails (e.g., result calculation), others (e.g., exam-taking) remain operational.
  * **Ease of Deployment** : With continuous deployment pipelines, each service can be updated independently without taking down the entire system.

#### **Main Services:**

1. **User Management Service** : Handles registration, login (Aadhaar-based, third-party like Google), and session management.
2. **Exam Management Service** : For examiners to create and manage exams with different question types (MCQs, numerical, subjective).
3. **Exam Taking Service** : Manages real-time exam interactions, handles submissions, and enforces exam time limits.
4. **Proctoring Service** : Implements real-time webcam monitoring, tab-switch detection, and question randomization.
5. **Result Calculation Service** : Calculates and distributes results for objective and subjective exams.
6. **Monitoring Service** : Logs system activities and user behavior for audit and proctoring.

Each of these services will be built as independent microservices deployed on containers using **Kubernetes** for orchestration and autoscaling.

### 2.	Handling Concurrency & Scalability Calculations

With **1 million concurrent users** submitting answers at the same time, handling concurrency and maintaining data consistency is critical.

#### **Concurrency Control** :

* **Optimistic Locking** : To handle concurrent updates (e.g., students submitting answers at the same time), use optimistic locking techniques where the system detects conflicts only when updates happen and retries accordingly.
* **Pessimistic Locking** : For critical sections such as database updates or student submission writes, apply pessimistic locks to ensure data consistency.


#### **Handling Exam Submissions** :

* **Queueing** : Use **message queues** (e.g.,  **Apache Kafka** ,  **Amazon SQS** ) to queue exam submission requests, ensuring submissions are processed sequentially without overloading the database.
* **Database Transactions** : Each answer submission must be written to the database in an **atomic** **transaction** to prevent data loss.
* **Eventual Consistency** : For non-critical operations (e.g., log updates, audit trails), **eventual consistency using background workers** can be employed to improve performance.

### **3. Database Design**

The system needs to handle different types of data, such as user authentication information, exam questions, answer submissions, logs, and results. **Polyglot persistence** (using different types of databases for different use cases) is an ideal solution.

**Database Choices** :

* **User Authentication & Session Management** : Use **SQL databases** like **PostgreSQL** or **MySQL** to handle ACID transactions and enforce data integrity.
* **Exam Questions and Submissions** : Use **NoSQL databases** like **Cassandra** or **MongoDB** to handle write-heavy workloads with fast read/write performance and horizontal scaling.
* **Real-Time Proctoring and Monitoring** : For storing logs (proctoring data, activity logs), use a time-series database like **InfluxDB**
* **Result Storage** : Use **SQL databases** to handle grading, ensuring ACID properties for critical data like student results.

**Sharding and Replication** :

* **Sharding** : For **Cassandra** or  **MongoDB** , shard the data by student ID or exam ID to distribute the load evenly across database nodes.
* **Replication** : Implement **replication** for both read and write-heavy workloads. Read replicas can handle requests for session data or exam questions, while the master nodes handle the write operations.

### **4. Load Balancing and Scaling**

#### **Horizontal Scaling** :

For a system that handles millions of users, horizontal scaling is preferred over vertical scaling. This allows for adding more servers instead of upgrading existing ones.

#### **Load Balancing Strategies** :

* **Global Load Balancer** : Use **DNS-based global load balancers** (e.g.,  **AWS Route 53** ) to distribute traffic to regional data centers closer to users, reducing latency.
* **Layer 7 Load Balancer** : Use  **NGINX** ,  **HAProxy** , or cloud-based load balancers like **AWS ALB** to distribute requests across application servers.
* **Load Distribution Across Services** : Use **Kubernetes** to deploy and scale microservices, dynamically adding more instances when traffic spikes.

#### **Auto-scaling** :

* Use **Kubernetes Horizontal Pod Autoscaler (HPA)** to auto-scale microservice pods based on CPU and memory utilization.
* **Pre-warmed instances** : Keep a buffer of pre-warmed instances ready to handle traffic surges when the exam starts.


### **5. Caching Strategy**

To improve performance, reduce database load, and ensure fast data retrieval:

* **Redis** : Cache  **exam questions** ,  **student session data** , and **exam state** in **Redis** for fast lookups. Redis will handle the in-memory storage of commonly accessed data, reducing database reads.
* **Cache Size Calculation** : Assume each session is **2KB** and we have  **1 million concurrent users** , then **2GB** of Redis memory will be required for caching active session states.
* **CDN** : Use a **Content Delivery Network (CDN)** (e.g.,  **Cloudflare** ) to cache and serve static content such as exam interfaces, images, and scripts.


### **6. Handling Peak Load During IIT JEE Exams**

#### **Peak Load Handling Strategy** :

* **Auto-scaling** : Scale microservice instances dynamically based on CPU/memory usage and traffic patterns.
* **Circuit Breakers** : Use circuit breakers to temporarily block excess traffic to prevent the backend systems from being overwhelmed.
* **Rate Limiting** : Implement **rate limiting** at the API gateway level to control the rate of requests per user.

#### **Traffic Estimation** :

* **1 million concurrent users** submitting **10 answers** each at **peak** translates to  **10 million requests per second** . Each request might be around **2KB** in size, requiring significant infrastructure to handle traffic spikes.
* To handle  **10 million requests per second** , the system needs **10,000 servers** if each server can process  **1000 requests per second** .

### **7. Event-Driven Architecture**

To decouple services, improve scalability, and make the system more resilient:

* **Message Queues** : Use **Apache Kafka** or **Amazon SQS** for asynchronous communication between services (e.g., exam submission, result calculation, suspicious activity alerts).
* **Student Notifications** : When a student submits an exam, an event can be published to a message queue, and the result calculation service will consume this event to start processing.
* **Proctoring Alerts** : When suspicious activity (e.g., multiple tab switches) is detected, send an alert to the proctoring service via the message queue.


### **8. Anti-Cheating Mechanisms**

 **Real-time Proctoring** :

* Use **WebRTC** for real-time audio/video streaming to proctors, and collect data on student activity.
* Use **AI/ML algorithms** to monitor and flag suspicious behavior, such as multiple tab switches, unusual mouse movements, or prolonged inactivity.

 **Question Randomization** :

* Use a question pool for each subject and **randomly assign** different sets of questions to each student.
* Implement server-side logic to randomize both the order of the questions and the choices within multiple-choice questions.

**Tab-Switch Detection** :

* Use JavaScript events to detect if a student switches tabs or moves away from the exam interface and log such events.
* Generate alerts if a student switches tabs frequently or stays outside the exam window for too long.

### **9. Fault Tolerance, High Availability, and Disaster Recovery**

#### **Fault Tolerance** :

* Ensure microservices are replicated across multiple data centers (using  **Kubernetes** ) to avoid single points of failure.
* Implement **multi-region** deployment across cloud providers for high availability.

#### **Disaster Recovery** :

* Use **cross-region backups** and  **disaster recovery strategies** . Databases should be backed up regularly, and replicas should be deployed across different availability zones or regions.

#### **API Gateway and Rate Limiting** :

* The **API Gateway** (e.g.,  **AWS API Gateway** ) will serve as the entry point for all client requests and will be responsible for routing traffic to the right microservices.
* Implement **rate limiting** to prevent DDoS attacks or misuse of system resources by limiting the number of API calls per user per second.

### **10. Monitoring and Logging**

#### **Monitoring** :

* Use tools like **Prometheus** and **Grafana** to monitor application performance, server health, memory usage, and API response times.
* **Real-time Alerts** : Set up real-time alerts (via **PagerDuty** or  **Slack** ) for issues like server failures, high latency, or traffic spikes.

#### **Logging** :

* Use **ELK Stack (Elasticsearch, Logstash, Kibana)** for centralized logging of all events (e.g., submissions, proctoring, suspicious activities, server logs).
* Analyze logs in real-time to detect patterns of system failure or cheating attempts.
