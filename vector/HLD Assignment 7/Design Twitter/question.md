## Problem 1 :

## Assignment Overview

You are tasked with designing a scalable and highly available social media platform similar to  **Twitter** . Your design should fulfill the functional requirements listed below and demonstrate sound architectural principles.

---

## Functional Requirements

### 1. User Management

* **User Registration & Authentication**
  * Users can create an account using email and password.
  * Support for password recovery and account verification.
* **Profile Management**
  * Users can create and edit their profile (name, bio, profile picture).
* **Follow/Unfollow**
  * Users can follow or unfollow other users to curate their content feed.

### 2. Posting & Interactions

* **Posts (Tweets)**
  * Users can post short messages up to 280 characters.
* **Likes & Retweets**
  * Users can like and retweet posts from other users.
* **Replies**
  * Users can reply to posts, allowing for nested conversations.

### 3. Feed/Timeline

* **Personalized Feed**
  * Users see a feed of posts from users they follow, sorted by recency.
* **Infinite Scrolling**
  * The feed supports infinite scrolling to load more content seamlessly.

### 4. Notifications

* **Real-time Notifications**
  * Users receive notifications for likes, retweets, replies, and new followers.
* **Mention Alerts**
  * Users are notified when they are mentioned in a post.

### 5. Search

* **Keyword Search**
  * Users can search for posts containing specific keywords or hashtags.
* **User Search**
  * Users can search for other user profiles.

---

## Assignment Deliverables

You are expected to provide the following components:

### 1. Non-Functional Requirements

Define the non-functional requirements of the system, considering aspects such as:

* **Scalability** : How the system will handle an increasing number of users and data.
* **Availability** : Strategies to ensure the system is highly available and fault-tolerant.
* **Consistency** : Data consistency models appropriate for the platform.
* **Latency** : Expected response times for different operations.
* **Security** : Measures for authentication, authorization, and data protection.
* **Data Storage** : Considerations for data persistence, backup, and recovery.

### 2. Back-of-the-Envelope Calculations

Perform estimations to understand the scale of the system:

* **User Base Estimation**
  * Active monthly users, daily active users, peak concurrent users.
* **Data Storage Requirements**
  * Average size of user profiles, posts, media content.
  * Total storage needed per year.
* **Throughput Estimations**
  * Number of posts per second, read/write ratios.
* **Network Bandwidth**
  * Estimate bandwidth requirements for data transfer.

Provide justifications for all assumptions and calculations.

### 3. High-Level Design Diagram

Create a high-level architecture diagram that includes:

* **System Components**
  * Web servers, application servers, databases, cache servers, message queues, etc.
* **Data Flow**
  * How data moves through the system from user actions to database transactions.
* **Load Balancing**
  * Strategies for distributing incoming traffic.
* **Caching Mechanisms**
  * Use of caches to improve performance (e.g., CDN, in-memory caches).
* **Data Partitioning**
  * Sharding strategies for databases to handle large volumes of data.
* **Microservices (if applicable)**
  * Breakdown of services and their responsibilities.

### 4. API Design for Each Service

Define the APIs for the services involved:

* **Endpoint Definitions**
  * URL paths, HTTP methods (GET, POST, PUT, DELETE).
* **Request and Response Formats**
  * JSON schemas for requests and responses.
* **Authentication**
  * How APIs handle security and authentication tokens.
* **Rate Limiting**
  * Any limitations on API usage to prevent abuse.
