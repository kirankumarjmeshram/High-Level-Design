Question: **Introduction to Apache Kafka - Building a Simple Messaging System**

Create a simple messaging system using Kafka. Your task is to produce messages from one application and consume them in another application, simulating a basic publish-subscribe model.

Assignment Steps:

Set Up Kafka:
Download and install Apache Kafka on your local machine. Use the installation guide available on the Kafka website.
Start Zookeeper and Kafka server using the appropriate commands.

**Create a Kafka Topic:**
Create a topic named simple-messages. Ensure it has at least one partition and one replication factor.

**Produce Messages:**
Write a simple producer program in your preferred language (e.g., Python, Java) that sends messages to the simple-messages topic.
The producer should send at least 10 messages to the topic.

**Consume Messages:**
Write a simple consumer program that listens to the simple-messages topic and prints out the messages.
Ensure that the consumer starts from the beginning of the topic to consume all the messages sent by the producer.

**Test the System:**
Run your producer program to send messages to the topic.
Run your consumer program to receive and print the messages.
Verify that all messages produced are being consumed correctly.

**Deliverables:**
Submit your producer and consumer code.
Include a screenshot of the terminal showing both the producer sending messages and the consumer receiving messages.

**Bonus**:
Modify the producer to send JSON messages.
Modify the consumer to parse and display the JSON messages in a structured format.
