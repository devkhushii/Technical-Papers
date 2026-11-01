# Messaging Queues

---

## 1. Overview of Distributed Systems

A **distributed system** is a group of independent computers, called *nodes*, that work together as one system.

Each node may perform a different task, but all nodes communicate and share information to complete a common goal.

**Example:*** Online Shopping Application

An online shopping application may have different services:

- **Order Service:** Manages customer orders.
- **Payment Service:** Handles payments.
- **Inventory Service:** Manages product stock.
- **Notification Service:** Sends order updates.
- **Delivery Service:** Manages the delivery process.

These services work together to complete a customer's order.

---

## 2. Communication Between Applications and Services

Applications often need to communicate with other applications or services to exchange information or request an action.

For example, when a customer places an order:

1. The order details must be stored.
2. The payment must be processed.
3. The inventory must be updated.
4. The customer must receive an order confirmation.
5. The delivery service must be notified.

These tasks may be handled by different applications or services. For them to work together, they need a way to communicate and exchange data.

This is called **application-to-application communication**.

---

## 3. What Is Message Passing?

**Message passing** is a way for different parts of a computer system to communicate by sending and receiving messages.

It can be used between:

- Different threads within the same process.
- Different processes running on the same computer.
- Different processes running on separate computers.

A **message** contains data or instructions that one part of a system wants to send to another.

**Example**

When a customer places an order, the order application may send this message:

```json
{
  "order_id": 101,
  "customer": "Khushi",
  "product": "Laptop",
  "amount": 50000
}
```

This message contains the order information. The receiving application can use it to process the payment, update the inventory or send a notification.

---

## 4. What Is Middleware?

**Middleware** is software that helps different applications, systems or services communicate with each other.

It works between applications and provides common services that make communication easier.

Middleware is sometimes called the **“plumbing of IT systems”** because it helps different parts of a system connect and exchange information.

For example, middleware can help an application communicate with a database or send information to another application.

### Types of Middleware

1. **Database Middleware**
   - Helps applications connect to databases.
   - Allows applications to send queries and access data.

2. **Message-Oriented Middleware (MOM)**
   - Allows applications to exchange messages through queues or topics.
   - Enables communication without waiting for an immediate response.

3. **Remote Procedure Call (RPC) Middleware**
   - Allows an application to call a function on another system.
   - Makes remote functions work like local functions.

4. **Transaction Processing Middleware**
   - Helps manage transactions involving multiple operations.
   - Ensures that related steps complete correctly.

5. **API and Web Middleware**
   - Helps manage web requests and API communication.
   - Handles tasks such as authentication and routing.

6. **Object Middleware**
   - Helps applications exchange structured objects or data.
   - Supports communication between different systems.

7. **Cloud Middleware**
   - Helps connect applications running in cloud environments.
   - Supports communication between cloud-based and on-premises systems.

---

## 5. Messaging Queues as Message-Oriented Middleware (MOM)

**Message-Oriented Middleware (MOM)** allows applications to communicate by sending and receiving messages.

The sender does not need to wait for the receiver to respond immediately. The message can be stored until the receiving application is ready to process it.

A **message queue** acts as a temporary storage area for these messages.

This allows applications to work independently and helps make communication more reliable.

![Messaging Queue](https://media.geeksforgeeks.org/wp-content/uploads/20211126103158/UntitledDiagram8.jpg)

---

## 6. Synchronous vs Asynchronous Communication

There are two common ways applications communicate.

| Synchronous Communication | Asynchronous Communication |
|---|---|
| The sender waits for the receiver to respond. | The sender does not wait for an immediate response. |
| Both applications usually need to be available at the same time. | The receiver can process the message later. |
| A slow receiver may delay the sender. | The sender can continue its work after sending the message. |
| Example: Direct API request. | Example: Messaging queue. |

---

## 7. What Is a Messaging Queue?

- A **messaging queue** is a system that temporarily stores messages until they are received and processed by another application.
- It allows applications to communicate asynchronously, which helps improve reliability, scalability and flexibility.

- Messages are sent by a **producer** to a queue. The messages remain in the queue until a **consumer** receives and processes them.

### Main Components

- **Producer:** Creates and sends messages.
- **Queue:** Temporarily stores messages.
- **Consumer:** Receives and processes messages.
- **Message Broker:** Manages message delivery and routing between applications.

![Message Queue](https://media.geeksforgeeks.org/wp-content/uploads/20250930085200425394/message_queue_.webp)

---

## 8. Need for Messaging Queues

Messaging queues are used to:

- **Reduce dependency:** Applications do not need to communicate directly with each other.
- **Handle large workloads:** Messages can wait in the queue during busy periods.
- **Support background processing:** Tasks can be completed without making the user wait.
- **Improve reliability:** Messages can remain stored while a receiver is temporarily unavailable.
- **Support scalability:** More consumers can be added to process messages.
- **Handle temporary failures:** Failed messages can be retried, depending on the system.

---

## 9. Messaging Models

Two common messaging models are **Point-to-Point** and **Publish-Subscribe**.

### 9.1 Point-to-Point Messaging

In Point-to-Point messaging, a producer sends a message to a queue. The message is generally processed by one consumer.

![Point to point meassengaing](https://media.geeksforgeeks.org/wp-content/uploads/20261019103754450740/message_quese.webp)


**Example:** An order message is placed in a queue. One available worker receives and processes that order.

### 9.2 Publish-Subscribe Messaging

In Publish-Subscribe messaging, a publisher sends a message to a topic. Multiple subscribers can receive the message.

![Publish-subscribe Messaging](https://media.geeksforgeeks.org/wp-content/uploads/20261019103844116047/message_quese_2.webp)

**Example:** When an order is placed, the order service publishes an event. The inventory, notification and analytics services can all receive that event through their subscriptions.

---

## 10. Working and Architecture of Messaging Queues

A message queue allows producers and consumers to communicate without needing to work at the same time.

### Step 1: Sending Messages

The producer creates a message containing data or instructions and sends it to the message queue.

### Step 2: Queuing Messages

The queue temporarily stores the message until a consumer is ready to receive it.

The order in which messages are processed depends on the queue system and its configuration.

### Step 3: Consuming Messages

The consumer receives the message and processes it. Consumers can work independently of producers.

Multiple consumers may process messages at the same time, depending on the system.

### Step 4: Acknowledgement

After successfully processing a message, the consumer may send an acknowledgement to the broker.

If the message is not acknowledged, it may be delivered again, depending on the system's settings.

---

## 11. Popular Messaging Tools and Technologies


### 11.1 RabbitMQ

RabbitMQ is an open-source message broker.

It receives messages from producers and routes them to the correct queues. Consumers can then receive and process those messages.

**Example:** A website sends email tasks to RabbitMQ. Worker applications receive the tasks and send emails in the background.

### 11.2 Apache Kafka

Apache Kafka is mainly used for **event streaming**.

It stores events in topics and allows applications to publish and read those events. Kafka is useful when large amounts of data need to be processed continuously.

**Example:** A shopping website can send events about customer activity to Kafka for real-time analytics.

### 11.3 Apache ActiveMQ

Apache ActiveMQ is an open-source message broker.

It supports different messaging patterns, including Point-to-Point queues and Publish-Subscribe topics.

**Example:** Different business applications can exchange messages through ActiveMQ.

### 11.4 Amazon Simple Queue Service (SQS)

Amazon SQS is a managed message queue service from AWS.

AWS manages the queue infrastructure, while developers use the service to send, store and receive messages.

**Example:** An online store can place order-processing tasks in SQS while worker applications process them.

### 11.5 Google Cloud Pub/Sub

Google Cloud Pub/Sub is a managed messaging service that uses publishers, topics and subscriptions.

It allows different applications to receive messages without directly depending on each other.

**Example:** An application publishes an order event, and several services receive it through their subscriptions.

### 11.6 Redis Streams

Redis Streams is a feature of Redis used to store and process messages as a stream of events.

It supports message IDs and consumer groups, which help applications read and process streams of messages.

**Example:** An application can use Redis Streams to track activity events or process real-time updates.


---

## 12. Enterprise Message Bus (EMB)

### What Is an Enterprise Message Bus?

An **Enterprise Message Bus (EMB)** is a shared messaging system that helps different applications in an organization communicate with each other.

Instead of every application connecting directly to every other application, each application connects to the bus. The bus helps send messages to the correct destination.

It may also help convert message formats or communication protocols when different applications use different technologies.

### Why Is EMB Needed?

Large organizations often use many applications, such as:

- Customer Management System
- Payment System
- Inventory System
- Employee Management System
- Finance System

Connecting every application directly to every other application can become difficult to manage.

An EMB provides a common communication layer and reduces the number of direct connections required.



![EMB](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRapHrpyf6n8au_v4Nlc8-H5mr2Op7lwiy3LSlN9xzaS47RShjg9BUMayg&s=10)

### How Does EMB Work?

1. An application creates a message.
2. The message is sent to the enterprise message bus.
3. The bus checks where the message needs to go.
4. If needed, the bus changes the message format or protocol.
5. The bus sends the message to the correct application.
6. The receiving application processes the message.

### Main Functions of EMB

| Function |  Explanation |
|---|---|
| **Message Routing** | Sends messages to the correct application. |
| **Message Transformation** | Changes message data into a format the receiver can understand. |
| **Protocol Conversion** | Helps applications using different communication methods exchange data. |
| **Application Integration** | Connects different applications through a common messaging layer. |
| **Message Delivery** | Helps deliver messages between connected applications. |

### EMB vs Message Queue

| Enterprise Message Bus | Message Queue |
|---|---|
| Connects multiple applications across an organization. | Temporarily stores messages for consumers. |
| May provide routing and transformation between systems. | Mainly focuses on storing and delivering messages. |
| Provides a broader messaging infrastructure. | Can be one component within an enterprise messaging system. |


---

## 13. Infrastructure as a Service (IaaS)

### What Is IaaS?

**Infrastructure as a Service (IaaS)** is a cloud computing model that provides IT resources such as computing power, storage and networking over the internet.

Instead of buying and maintaining physical servers, an organization can rent the resources it needs from a cloud provider.

The organization pays for the resources it uses and can increase or decrease them as needed.

### Main Components of IaaS

| Component | Simple Explanation |
|---|---|
| **Compute** | Virtual machines and processing power used to run applications. |
| **Storage** | Space used to store files, databases and application data. |
| **Networking** | Virtual networks and connections that allow systems to communicate. |
| **Virtualization** | Technology that allows virtual computers to run on physical hardware. |

### How Does IaaS Work?

```text
             User / Organization
                      |
                      v
          +-------------------------+
          | Select Required Resources|
          +-------------------------+
                      |
                      v
          +-------------------------+
          | Cloud Provider          |
          |                         |
          | Virtual Machines        |
          | Storage                 |
          | Networking              |
          +-------------------------+
                      |
                      v
          +-------------------------+
          | Run Applications        |
          +-------------------------+
```

1. The organization selects the resources it needs.
2. The cloud provider creates virtual machines, storage and networking.
3. The organization installs the operating system and required software.
4. Applications are deployed and run on the resources.
5. The cloud provider maintains the physical hardware.

### Who Manages What?

| Cloud Provider Manages | User / Organization Manages |
|---|---|
| Physical servers | Operating system |
| Data centre hardware | Installed applications |
| Physical networking | Application data |
| Virtualization infrastructure | Software configuration and security settings |

The exact division of responsibility can vary by provider and service.

### Popular IaaS Providers

| Provider | Example Service | Simple Explanation |
|---|---|---|
| **Amazon Web Services (AWS)** | Amazon EC2 | Provides virtual machines for running applications. |
| **Google Cloud** | Compute Engine | Provides virtual machines and computing resources. |
| **Microsoft Azure** | Azure Virtual Machines | Provides virtual machines and cloud infrastructure. |

### How Is IaaS Related to Messaging Queues?

IaaS provides the infrastructure needed to run messaging software.

For example, an organization can:

1. Create a virtual machine using AWS EC2.
2. Install RabbitMQ or Apache Kafka on it.
3. Configure networking and security.
4. Connect producer and consumer applications.
5. Run and monitor the messaging system.

In this example, AWS provides the infrastructure, while the organization manages the messaging software.

**Important:** Amazon SQS and Google Cloud Pub/Sub are managed messaging services. They are not simply IaaS because the cloud provider also manages the messaging service itself.

### IaaS vs PaaS vs SaaS

| Model | What It Provides | Example |
|---|---|---|
| **IaaS** | Computing infrastructure such as virtual machines, storage and networks. | AWS EC2 |
| **PaaS** | A platform for developing and running applications. | Google App Engine |
| **SaaS** | Ready-to-use software accessed over the internet. | Gmail |

---

## 14. Conclusion

Messaging queues help applications communicate by sending and receiving messages without requiring them to work at the same time.

They reduce direct dependencies, support background processing and help applications handle large workloads.

Tools such as RabbitMQ, Apache Kafka, ActiveMQ, Amazon SQS and Google Cloud Pub/Sub provide different ways to implement messaging systems.

An Enterprise Message Bus helps connect applications across an organization, while IaaS provides the computing resources needed to deploy and run messaging software.

Together, messaging queues, enterprise messaging and cloud infrastructure help build flexible and scalable distributed systems.

## References
https://youtu.be/sKXCTtGdxWo?si=7o8FZ410tltWzQWd

https://cs.lmu.edu/~ray/notes/messagepassing/

https://azure.microsoft.com/en-in/resources/cloud-computing-dictionary/what-is-middleware

https://www.geeksforgeeks.org/computer-networks/what-is-message-oriented-middleware-mom/

https://aws.amazon.com/what-is/iaas/

https://www.geeksforgeeks.org/system-design/message-queues-system-design/
