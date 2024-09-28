### Designing a Scalable Online IIT JEE Exam Portal

### **Key Requirements:**

1. User Registration and Authentication
2. Exam Creation and Management
3. Real time Exam Taking
   1. Handle real-time answer submission. upto 1 million concurrent students
   2. Exam integrity is critical, including time-tracking, submission logs, and prevention of multiple logins
4. Exam integrity and anti-cheating Mechanism
   1. implement real time proctoring, question randomization, and tab-switching detection to prevent cheating
5. Result calculation and distribution
6. Scalability and availability
   1. the platform must support 10 million daily users with 99.99% uptime, spacially during national exam with a large volume of concurrent students
7. Data Constistency and Availability
8. Performance Requirements
   1. Exam submissions must have a latency of <200ms. The system should ensure zero data loose on submission and keep the platorm

**System Design to Address**

1. High Level Architectuer
   1. Choose Betweeen microservises, monolithic, or serverless architecture based on scalability, resilience, and ease of deployment
   2. handling real time trafic
2. Concurrency Control and Data Consistency
   1. multiple students submitting answeer at same time
   2. implement optimistic locking, pessimistic locking, or distributed locks
3. Database design
   1. Choose approprite db for:
      1. User Authentication and Session Management
      2. Exam Questions, Answer Submissions, ans results
      3. Real time monitoring: Ensure
   2. Discuss sharding, replecation (read/write replecas), and scalling strategies to handle millions of students taking exam concurrently
4. Load balancing and Scaling
   1. implement horizontal vs vertical scalling for handling the peak load during exam days
   2. what are load balancing strategies will u ensure smooth trafic distribution among servers?
5. Caching Strategy
   1. Discuss where and how you would use caching (Redis, CDN) for performance improvements. perticulary for student sessions and exam question retrieval
6. Handling Peak Load during IIT JEE Exams
   1. design the system to handle trafic spikes during the exam day, ensuring no downtime
   2. Discuss auto-scalling, circuit breakers, and rate limiting to handle trafic overload and prevent denial-ofservice attack
7. Event-Driven Architecture
   1. explain use of Event-Driven Architecture with message queues (Kafka, SQS) to decouple system for scalability and resilience in processing student notification, suspicious activity alerts, and result distribution
8. Anti-Cheating Mechanisms
   1. How will you Impement realtime proctoring, question randomisation, and tab switch detection without affecting system performance
   2. Discuss the detection of cheating attempts and how you would notify examiners.
9. Fault Tolerance, high availability and Disaster Recovery
10. API Gateway and Rate Limiting
11. Monitoring and Logging


### Deliverables:

* High Level System Architectural Diagram
  * Include key components like user management, exam creation, exam taking, and monitoring. Represent data flow and communication paths using arrows
* Detailed Explanation of :
  * Architecture (microservies, monolithic, serverless)
  * Concurrency controll and answer submission strategy
  * Database choises, sharding, and replecation
  * Load balancing, caching and scaling mechanisms
  * Handling high-trafic exam periods
  * Fault tolerance, disaster recovery, and monitoring
