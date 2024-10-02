## Problem 2 :

## Assignment Overview

You are tasked with designing a scalable and highly available ride-sharing platform similar to **Uber** or  **Lyft** . Your design should fulfill the functional requirements listed below and demonstrate sound architectural principles.

---

## Functional Requirements

### 1. User Management

* **User Registration & Authentication**
  * Users (both riders and drivers) can create an account using email and password.
  * Support for password recovery and account verification.
* **Profile Management**
  * Riders can create and edit their profile (name, contact information, payment methods).
  * Drivers can create and edit their profile (name, vehicle details, driver's license).
* **Rating System**
  * Riders can rate drivers after a trip.
  * Drivers can rate riders.

### 2. Ride Request and Matching

* **Ride Request**
  * Riders can request a ride by specifying pickup and drop-off locations.
* **Real-time Matching**
  * The system matches riders with the nearest available drivers in real-time.
* **Driver Acceptance**
  * Drivers receive ride requests and can accept or decline them.

### 3. Real-time Tracking

* **Map Integration**
  * Riders and drivers can view their locations and routes on a map.
* **Trip Progress**
  * Riders can track the driver's approach to the pickup location.
  * Both riders and drivers can track the trip progress during the ride.

### 4. Payments

* **Fare Calculation**
  * The system calculates fares based on distance, time, and dynamic pricing.
* **In-App Payments**
  * Riders can pay for rides using stored payment methods.
* **Receipts**
  * Riders receive a receipt after the trip via email or within the app.

### 5. Notifications

* **Push Notifications**
  * Real-time notifications for ride requests, driver arrival, trip start/end.
* **SMS Alerts**
  * Optional SMS notifications for key updates.

### 6. Search and Discovery

* **Destination Search**
  * Riders can search for destinations using autocomplete suggestions.
* **Driver Availability**
  * Drivers can set their availability status (online/offline).

---

## Assignment Deliverables

You are expected to provide the following components:

### 1. Non-Functional Requirements

Define the non-functional requirements of the system, considering aspects such as:

* **Scalability** : How the system will handle an increasing number of users and ride requests.
* **Availability** : Strategies to ensure the system is highly available and fault-tolerant.
* **Consistency** : Data consistency models appropriate for real-time matching and payments.
* **Latency** : Expected response times for ride requests, driver matching, and map updates.
* **Security** : Measures for authentication, authorization, data protection, and fraud prevention.
* **Data Storage** : Considerations for data persistence, backup, and recovery.

### 2. Back-of-the-Envelope Calculations

Perform estimations to understand the scale of the system:

* **User Base Estimation**
  * Number of registered riders and drivers.
  * Daily active users and peak concurrent users.
* **Data Storage Requirements**
  * Average size of user profiles, ride records, and location data.
  * Total storage needed per year.
* **Throughput Estimations**
  * Number of ride requests per second.
  * Read/write ratios for databases.
* **Network Bandwidth**
  * Estimate bandwidth requirements for real-time location updates and data transfer.

Provide justifications for all assumptions and calculations.

### 3. High-Level Design Diagram

Create a high-level architecture diagram that includes:

* **System Components**
  * Mobile clients, API gateways, application servers, databases, cache servers, message queues, etc.
* **Data Flow**
  * How data moves through the system from user actions to backend processes.
* **Load Balancing**
  * Strategies for distributing incoming traffic and requests.
* **Caching Mechanisms**
  * Use of caches to improve performance (e.g., in-memory caches, CDN).
* **Data Partitioning**
  * Sharding strategies for databases to handle large volumes of data.
* **Microservices (if applicable)**
  * Breakdown of services and their responsibilities (e.g., user service, ride-matching service, payment service).

### 4. API Design for Each Service

Define the APIs for the services involved:

* **Endpoint Definitions**
  * URL paths and HTTP methods (GET, POST, PUT, DELETE).
* **Request and Response Formats**
  * JSON schemas for requests and responses.
* **Authentication**
  * How APIs handle security and authentication tokens.
* **Rate Limiting**
  * Any limitations on API usage to prevent abuse.
