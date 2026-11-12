# CAP Theorem

#  What is CAP Theorem?

CAP Theorem is a fundamental concept in distributed database systems.

It states that when a network partition occurs, a distributed system must choose between:

- **Consistency (C)**
- **Availability (A)**

A distributed system cannot guarantee both consistency and availability during a network partition.

The three properties of CAP are:

- **C – Consistency**
- **A – Availability**
- **P – Partition Tolerance**

## Why Do We Need CAP Theorem?

Imagine an online shopping application storing data on multiple servers located in different countries.

All servers maintain copies of the same data.

Now, suppose a network failure prevents these servers from communicating with each other.

For example:
1. A customer's balance is ₹5,000.
2. Server 1 updates it to ₹3,000.
3. Due to a network failure, Server 2 still has ₹5,000.
4. If a request reaches Server 2, it may return outdated information.
This creates a conflict between Consistency and Availability.

CAP Theorem helps us understand how distributed databases handle such situations.

---

#  Understanding the Three Properties of CAP

##  Consistency (C)

In CAP Theorem, consistency means that every read receives the most recent successful write, or an error if the latest value cannot be provided.

**Remember:** CAP Consistency = Latest successful write must be visible to reads.

### Example
If Server A updates a bank balance to ₹3,000, other servers should also return ₹3,000.


## Availability (A)

Availability means that every request received by a non-failing node must receive a response.

The response does not necessarily have to contain the latest data.

**Remember:** CAP Availability = The system continues responding to requests.

### Example
If Server A is down, Server B still responds to customer requests.

## Partition Tolerance (P)

 The system continues to operate correctly even if the network between nodes experiences a partition — meaning some nodes temporarily cannot communicate with others at all.

### What is a Network Partition?

A network partition occurs when a communication failure divides a distributed system into groups of nodes that cannot communicate with one another.

Example:

A distributed database has three servers: A, B, and C.
- Server A can communicate with Server B.
- Server C cannot communicate with A or B due to a network failure.
Now, the servers are divided into two groups.

This situation is called a Network Partition.

### Example
If Server A cannot communicate with Server B, both servers continue operating independently.


# 3. The Main Idea of CAP Theorem

CAP Theorem states:

**When a network partition occurs, a distributed system cannot guarantee both consistency and availability at the same time.**

It must choose one of the following approaches:

1. CP – Consistency and Partition Tolerance.
2. AP – Availability and Partition Tolerance.

---

# CP System (Consistency + Partition Tolerance)

A CP system prioritizes:

- Consistency.
- Partition tolerance.

During a network failure: The system may stop responding rather than return incorrect or outdated data.

**Example: Banking System**
If two bank servers lose connection, the system may reject transactions temporarily rather than risk showing incorrect account balances.
- Consistency: Ensures correct data.
- Partition Tolerance: Handles network failures.
- Availability may be sacrificed.

**Best for:** Banking and inventory systems where correct data is more important than continuous availability.

---

# 5. AP System (Availability + Partition Tolerance)

An AP system prioritizes:

- Availability.
- Partition tolerance.

During a network partition, it continues responding to requests, even if some responses contain outdated data.

**Example: Social Media (Instagram)**
If some servers lose connection, Instagram may still allow users to view posts, even if some likes or comments are not immediately updated.
- Availability: System remains accessible.
- Partition Tolerance: Handles network failures.
- Consistency may be sacrificed temporarily.

**Best for:** Social media, shopping carts, and recommendation systems where continuous service is more important than always showing the latest data.

---


#  CA Systems

A CA system aims to provide:

- Consistency.
- Availability.

However, it does not tolerate network partitions.

This means it can provide both consistency and availability as long as the nodes can communicate properly.

But when a network partition occurs, it cannot guarantee both properties.

**Example:** A single-server database.

**Best for:** Single-server databases where network communication between multiple database nodes is not required.


---

#  What Happens After a Network Partition Is Recovered?

Suppose Server A and Server B can communicate again.

Their data may be different:

```text
Server A = ₹8,000
Server B = ₹10,000
```

The distributed system needs to synchronize the data.

Depending on the system, it may use:

- Replication.
- Conflict resolution.
- Version numbers.
- Timestamps.
- Application-specific rules.

For example, if Server B had accepted additional transactions during the partition, simply copying Server A's balance to Server B might not be correct.

The system must determine how to reconcile the changes without losing valid operations.

This is particularly important in AP systems.

---

#  Real-World Database Examples

The following examples are commonly associated with CAP trade-offs. They should not be interpreted as saying that an entire database product always belongs to only one category. Actual guarantees depend on configuration, data model, consistency settings, and operation type.

| Database / System | Common CAP Association | Explanation |
|---|---|---|
| Apache Cassandra | AP-oriented | Supports high availability and tunable consistency. |
| Amazon DynamoDB | AP-oriented in common simplified examples | Provides configurable consistency options and high availability. |
| MongoDB | CP-oriented in common simplified examples | Uses replica-set coordination and may reject writes when a suitable majority is unavailable. |
| etcd | CP-oriented | Uses consensus to maintain consistent distributed state. |
| HBase | CP-oriented | Prioritizes consistency and may become unavailable for affected operations during partitions. |

### Important Note About Database Classification

A database should not be classified only by its name.

For example, Cassandra supports tunable consistency levels. MongoDB also provides different read and write concern configurations.

Therefore, actual behaviour depends on how the database is configured and used.

---

#  CAP Theorem vs ACID Consistency

These two concepts use the same word, but their meanings are different.

| ACID Consistency | CAP Consistency |
|---|---|
| Ensures database rules and constraints remain satisfied. | Ensures reads observe the latest successful write under the consistency guarantee. |
| Focuses on valid database states. | Focuses on consistent data across distributed nodes. |
| Example: Account balance cannot be negative if that rule is enforced. | Example: A read should not return an outdated account balance after a successful write. |

**Remember:** ACID Consistency and CAP Consistency are not the same concept.

---
