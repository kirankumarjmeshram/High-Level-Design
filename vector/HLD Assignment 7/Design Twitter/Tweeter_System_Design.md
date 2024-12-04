### **System Design for a Scalable and Highly Available Social Media Platform (Twitter)**

---

#### 1. **Non-Functional Requirements**

##### **Scalability**

* **Horizontal Scaling** : Utilize horizontal scaling across all tiers (web servers, application servers, databases) to handle increased users, traffic, and storage requirements.
* **Auto-scaling** : Implement auto-scaling groups to add/remove servers based on traffic and load.
* **Database Sharding** : Partition user data (e.g., posts, profiles) across multiple databases using sharding strategies based on user ID, ensuring each shard handles a manageable amount of data.
