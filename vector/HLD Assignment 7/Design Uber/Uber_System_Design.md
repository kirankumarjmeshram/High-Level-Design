## Ride sharing app System Design (Uber)

## 1. Non-Functional Requirements

### Scalability

* **Horizontal Scaling** : Use microservices architecture to scale individual components (e.g., user service, ride matching service) independently.
* **Load Balancers** : Distribute incoming traffic across multiple instances of services to handle high user demand.
* **Auto-Scaling** : Utilize cloud services that allow automatic scaling based on traffic patterns

### Availability

* **Redundancy** : Deploy services in multiple geographical locations and use failover mechanisms to ensure availability in case of failures.
* **Health Checks** : Implement regular health checks on services to monitor their status and automatically reroute traffic as needed

### Consistency

* **Eventual Consistency** : Use an eventual consistency model for non-critical data (e.g., user ratings).
* **Strong Consistency** : For financial transactions, use strong consistency models to ensure accurate fare calculations and payments.

### Latency

* **Response Times** : Aim for sub-second response times for ride requests and driver matching, leveraging in-memory databases like Redis for caching.
* **Real-time Updates** : Use WebSocket connections for real-time tracking of driver and rider locations.


### Security

* **Authentication** : Use OAuth 2.0 for secure authentication and authorization of users.
* **Data Encryption** : Encrypt sensitive data (e.g., payment details) both at rest and in transit.
* **Fraud Prevention** : Implement anomaly detection algorithms to identify and prevent fraudulent activities.

### Data Storage

* **Database Types** : Use a combination of SQL databases (e.g., PostgreSQL) for structured data and NoSQL databases (e.g., MongoDB) for unstructured data.
* **Backup and Recovery** : Implement automated backup solutions and disaster recovery plans.
