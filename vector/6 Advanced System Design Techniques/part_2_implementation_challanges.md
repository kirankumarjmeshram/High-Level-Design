### **Part 2: Implementation Challenges**

#### **Question 1 (DFS):**

* Your distributed file system (DFS) is distributed across multiple regions for better availability. Describe how you would handle **replication and fault tolerance** in this DFS. How do you ensure that user data is always available even in case of regional failures?
  **Hints:**
  * Consider replication across regions and ensure **consistency** of files across replicas.
  * Think about how **eventual consistency** vs. **strong consistency** impacts user experience in a cloud storage service.

---

#### **Question 2 (API Gateway with Rate Limiting):**

* You are tasked with implementing **rate limiting** on the API Gateway to limit file uploads and downloads. Use a **sliding window** algorithm to implement rate limiting and explain how you would store the rate limit data in a centralized store like  **Redis** .
  **Hints:**

  * Implement the rate limit using Redis commands like `ZADD` and `ZRANGEBYSCORE`.
  * Use the **sliding window** technique to ensure that users are only allowed a certain number of API calls within a minute.

  **Follow-up:**

  * How will you handle rate limits in a distributed environment where multiple instances of the API Gateway are running?

---

#### **Question 3 (Monitoring & Logging):**

* As the system grows, you notice that file download latencies are increasing for some users. Describe how you would use **monitoring** and **logs** to identify the cause of the issue.
  * What metrics would you track (e.g., latency, throughput)?
  * What log entries would be useful for diagnosing the root cause (e.g., user ID, request timestamps, request paths)?
  * How would you visualize this data for better insights?
