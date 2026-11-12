# ACID Properties

# What is ACID?
ACID is a set of four important properties that help databases maintain correct, reliable, and consistent data.

ACID stands for :
- A – Atomicity
- C – Consistency
- I – Isolation
- D – Durability

These properties ensure that database operations are performed safely, even when errors, system failures or unexpected situations occur.


### The Four ACID Properties

| Property | Meaning | Main Question |
|---|---|---|
| Atomicity | All operations happen or none happen. | Did everything complete or nothing? |
| Consistency | Data must follow all defined rules. | Is the data still valid? |
| Isolation | Concurrent operations should not interfere incorrectly. | Can operations affect each other unexpectedly? |
| Durability | Successfully committed changes must survive failures. | Will saved data remain saved? |

---

#  Atomicity

##  What is Atomicity?

Atomicity means **all operations in a transaction must be completed successfully, or none of them should take effect.**

In simple words:

**All or Nothing.**

A database should not leave an operation partially completed.


##  How Does Atomicity Work?

Atomicity is implemented using a Transaction Log (also called WAL, Undo Log, or Redo Log).

It works in the following way:
1. Before changing any data, the database first saves information about the change in a log file.
2. If a transaction fails or is cancelled, the database uses the log to undo the changes already made.
3. If a transaction is successfully committed, the database saves a commit record in the log. If a crash occurs, the database can use the log to redo the changes during recovery.
This process ensures that either all changes of a transaction are saved or none of them are saved.

The method of writing changes to the log before updating the actual data is called Write-Ahead Logging (WAL). It helps maintain Atomicity and Durability.


##  SQL Example of Atomicity

Consider two bank accounts:

```sql
CREATE TABLE accounts (
    account_id INT PRIMARY KEY,
    balance DECIMAL(10, 2)
);

INSERT INTO accounts VALUES
(1, 10000),
(2, 5000);
```

Suppose we want to transfer ₹2,000.

```sql
BEGIN;

UPDATE accounts
SET balance = balance - 2000
WHERE account_id = 1;

UPDATE accounts
SET balance = balance + 2000
WHERE account_id = 2;

COMMIT;
```

Here:

- `BEGIN` starts the transaction.
- The first `UPDATE` deducts money.
- The second `UPDATE` adds money.
- `COMMIT` makes the changes permanent.

If an error occurs before the transaction is committed, we can use:

```sql
ROLLBACK;
```

`ROLLBACK` cancels the uncommitted changes.


---

# Consistency

Consistency means **a transaction must take the database from one valid state to another valid state without breaking any database rules.**

In simple words:

**Data must always follow the defined rules.**

A database should never contain invalid data that violates its defined constraints.

## How Does Consistency Work?

Consistency is maintained using database constraints and application-level rules.

It works in the following way:

1. Before a transaction is committed, the database checks whether all defined constraints are satisfied.
2. If all rules are followed, the transaction is allowed to commit.
3. If any constraint is violated, the transaction fails and its changes are rolled back.

Some common constraints are:

- `PRIMARY KEY` – Prevents duplicate primary key values.
- `FOREIGN KEY` – Ensures that referenced records exist.
- `UNIQUE` – Prevents duplicate values.
- `NOT NULL` – Prevents NULL values.
- `CHECK` – Ensures that values satisfy a given condition.

**Important:** Consistency is the responsibility of both the database and the application. The database checks the rules defined using constraints, while the application handles additional business rules that are not defined in the database.

## SQL Example of Consistency

Consider an accounts table where the account balance should never be negative.

```sql
CREATE TABLE accounts (
    account_id INT PRIMARY KEY,
    balance DECIMAL(10, 2) CHECK (balance >= 0)
);

INSERT INTO accounts VALUES
(1, 10000),
(2, 5000);
```

Suppose we try to deduct ₹12,000 from account 1.

```sql
BEGIN;

UPDATE accounts
SET balance = balance - 12000
WHERE account_id = 1;

COMMIT;
```

Here:

- `CHECK (balance >= 0)` ensures that the balance cannot be negative.
- The `UPDATE` tries to reduce the balance from ₹10,000 to -₹2,000.
- The database detects that the constraint is violated.
- The transaction fails, and the changes are rolled back.

This ensures that the database always follows its defined rules.

# Isolation

## What is Isolation?

Isolation means **multiple transactions can run at the same time without interfering with each other's uncommitted changes.**

In simple words:

**Transactions should work independently of each other.**

Each transaction should behave as if it is running alone, even when multiple transactions are running simultaneously.

## How Does Isolation Work?

Isolation is maintained using concurrency control mechanisms.

These mechanisms control how multiple transactions access and modify the same data.

Some common techniques are:

1. **Locking:** A transaction locks the data it is using so that other transactions cannot make conflicting changes at the same time.
2. **Timestamp Ordering:** Transactions are executed according to their assigned timestamps.
3. **Optimistic Concurrency Control:** Transactions execute without locking initially. Before committing, the database checks whether any conflicts have occurred.
4. **MVCC (Multi-Version Concurrency Control):** The database maintains multiple versions of data so that readers can access a consistent version without waiting for ongoing updates.

Different **Isolation Levels** define how much one transaction can see the changes made by another transaction.

For example, `SERIALIZABLE` provides the highest level of isolation, while weaker isolation levels allow more concurrency.


## SQL Example of Isolation

Consider an account with a balance of ₹1,000.

Suppose two transactions try to update the same account simultaneously.

**Without Proper Isolation:**

```sql
-- Transaction T1
BEGIN;

SELECT balance FROM accounts
WHERE account_id = 1;
-- Balance = 1000

-- T1 calculates 1000 + 100 = 1100


-- Transaction T2
BEGIN;

SELECT balance FROM accounts
WHERE account_id = 1;
-- Balance = 1000

-- T2 calculates 1000 + 200 = 1200


-- T1 updates the balance
UPDATE accounts
SET balance = 1100
WHERE account_id = 1;

COMMIT;


-- T2 updates the balance
UPDATE accounts
SET balance = 1200
WHERE account_id = 1;

COMMIT;
```

**Final Balance = ₹1,200**

Here:

- T1 adds ₹100 to the balance.
- T2 adds ₹200 to the balance.
- Both transactions initially read the same balance of ₹1,000.
- T2 overwrites the changes made by T1.
- T1's update is lost.

This problem is called a **Lost Update**.

**With Proper Isolation:**

The database uses concurrency control mechanisms to prevent conflicting updates from interfering with each other.

As a result, both transactions can complete correctly.

**Final Balance = ₹1,300**

This ensures that transactions do not incorrectly overwrite each other's changes.

# Durability

Durability means **once a transaction is successfully committed, its changes are permanently saved and will not be lost, even if the system crashes or restarts.**

In simple words:

**Once committed, changes are permanent.**

A database must ensure that successfully committed data is not lost.

## How Does Durability Work?

Durability is implemented using a Transaction Log (also called Write-Ahead Logging or WAL).

It works in the following way:

1. The database first writes all transaction changes into the log.
2. When the transaction commits, the database writes a commit record to the log.
3. The database saves the log to permanent storage (disk) before confirming that the transaction was successful.
4. The actual data pages can be saved to disk later. If a crash occurs before that, the database uses the log to restore the committed changes.

This ensures that committed changes are not lost, even if the system crashes immediately after the transaction.

## SQL Example of Durability

Consider two bank accounts:

```sql
BEGIN;

UPDATE accounts
SET balance = balance - 100
WHERE account_id = 1;

UPDATE accounts
SET balance = balance + 100
WHERE account_id = 2;

COMMIT;
```

Here:

- `BEGIN` starts the transaction.
- The first `UPDATE` deducts ₹100.
- The second `UPDATE` adds ₹100.
- `COMMIT` permanently saves the changes.

**What happens if the system crashes after COMMIT?**

- The database has already saved the commit record in its log.
- When the database restarts, it uses the log to restore the committed changes if needed.
- The committed changes will not be lost.

This ensures that once a transaction is committed successfully, its changes remain permanent.

#  How the Four ACID Properties Work Together

All four properties work together to make database operations reliable.

Consider a bank transfer of ₹2,000.

| Property | How It Helps |
|---|---|
| Atomicity | Both account updates succeed, or neither remains applied. |
| Consistency | Account balances follow the defined database rules. |
| Isolation | Concurrent transfers do not produce incorrect results. |
| Durability | Once the transfer is committed, it survives a system crash. |

### Example: Complete Bank Transfer

Suppose:

- Account A has ₹10,000.
- Account B has ₹5,000.
- Transfer amount is ₹2,000.

Expected final balances:

- Account A: ₹8,000.
- Account B: ₹7,000.

Now consider the four properties:

**Atomicity:** Both balance updates must complete together.

**Consistency:** The database must continue satisfying its rules, such as valid account balances.

**Isolation:** Another simultaneous transfer must not interfere and produce an incorrect result.

**Durability:** Once the transfer is committed, the updated balances must remain saved.

Together, these properties protect the correctness and reliability of the transfer.

---

#  Advantages of ACID Properties

1. **Data Reliability:** Helps ensure that database operations produce reliable results.
2. **Data Integrity:** Prevents invalid or partially completed changes.
3. **Failure Recovery:** Helps databases recover from crashes.
4. **Concurrent Access:** Supports safe access by multiple users.
5. **Financial Accuracy:** Important for banking and payment applications.
6. **Trust:** Helps applications maintain accurate records.

# Limitations and Performance Considerations

Although ACID provides strong reliability, maintaining these guarantees can involve additional work.

### 1. Performance Overhead

Logging, validation, recovery, and coordination require additional resources.

### 2. Resource Usage

Database mechanisms may use additional memory, disk space, and processing power.

### 3. Distributed Coordination

Maintaining transactional guarantees across multiple machines can introduce network communication and coordination overhead.

### 4. Scalability Trade-offs

Strong transactional guarantees can make some distributed workloads more difficult to scale efficiently.

**Important:** ACID is not inherently slow. Modern databases optimize their implementations, and the actual performance depends on the workload, database design, configuration, and hardware.
