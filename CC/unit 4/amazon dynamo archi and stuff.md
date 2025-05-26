Amazon DynamoDB is a **fully managed NoSQL database service** built for high availability, low-latency, and massive scalability. It was inspired by the **Amazon Dynamo** paper (2007), which described a **decentralized key-value storage system** used by Amazon's own services. While the original Dynamo is a peer-to-peer system, **DynamoDB is a managed service** based on similar principles but refined for the cloud.

---

## **High-Level Architecture of Amazon DynamoDB**

DynamoDB hides most of the underlying complexity from users, but internally, it uses a **distributed architecture** built on several key principles:

---

### **1. Partitioning (Sharding)**

- **Tables are partitioned across multiple nodes** automatically.
- **Partition key (hash key)** is used to determine the data’s location.
- DynamoDB uses a **partition key’s hash value** to determine which internal partition stores the item.
- Each partition has:
    - Storage (for data)
    - Compute (to serve read/write requests)
    - Capacity units (RCUs/WCUs)

**Partition = physical storage + compute units**

---

### **2. Data Distribution – Partition Key Hashing**

- DynamoDB uses **MD5 hash** of the partition key to evenly distribute data.
- This avoids "hot partitions" or data skew.
- A **table is split into partitions** based on:
    - Data size (each partition can store ~10 GB)
    - RCU/WCU throughput (each partition supports ~3000 RCUs and 1000 WCUs)

---

### **3. Replication and Availability**

- **Multi-AZ replication**:
    
    - Data is automatically **replicated across multiple Availability Zones (AZs)** in a region.
    - This provides **fault tolerance** and **high availability**.
- **Eventually or Strong Consistency**:
    
    - By default, reads are eventually consistent.
    - Can opt-in for **strongly consistent reads** (returns the latest data from a quorum of replicas).

---

### **4. Request Routing and Load Balancing**

- DynamoDB uses **front-end request routers** (also called request coordinators) to:
    - Authenticate and authorize the request
    - Route the request to the correct partition
    - Apply throttling if capacity limits are exceeded
    - Retry failed requests (in case of transient failures)

---

### **5. Storage Engine**

- Uses a **log-structured storage engine**, similar to **LSM trees (Log-Structured Merge Trees)**.
- Write operations are:
    - Written to a **commit log**
    - Then added to an **in-memory buffer**
    - Periodically flushed to **disk in sorted order**
- Supports **SSTables** (Sorted String Tables) for fast key-based access.

---

### **6. Secondary Indexes**

- **Global Secondary Index (GSI)**:
    
    - Can span all partitions
    - Allows querying by alternate attributes
    - Has its own RCU/WCU
- **Local Secondary Index (LSI)**:
    
    - Shares partition key but has different sort key
    - Shares table capacity

Indexes are stored as **separate data structures** but managed by DynamoDB internally.

---

### **7. DynamoDB Streams**

- **Change Data Capture (CDC)** for item-level modifications.
- Streams capture `INSERT`, `MODIFY`, and `REMOVE` events.
- Can be used for:
    - Replication
    - Triggering Lambda functions
    - Auditing and analytics

---

### **8. Auto Scaling**

- **DynamoDB Auto Scaling** adjusts RCUs/WCUs automatically based on usage.
- Monitors **CloudWatch metrics** like `ConsumedReadCapacityUnits` and `WriteThrottleEvents`.

---

### **9. Transactions and ACID Support**

- DynamoDB supports **transactions** since 2018:
    - **Transactional writes** across multiple items and tables
    - Guarantees **ACID** (Atomicity, Consistency, Isolation, Durability)

---

### **10. Security and Access Control**

- **IAM Policies** for access control
- **Encryption at rest** (AWS KMS)
- **VPC endpoints** for private access
- **Fine-grained access control (FGAC)** with attribute-level restrictions

---

## **DynamoDB vs Original Dynamo (from 2007 paper)**

|Feature|Original Dynamo|DynamoDB|
|---|---|---|
|Peer-to-peer|Yes|No (managed service)|
|Consistency|Eventual only|Strong/Eventually|
|CAP Tradeoff|AP (Availability + Partition Tolerance)|Tunable (via strong/transactional reads)|
|Management|Self-hosted|Fully managed|
|Use Cases|Amazon internal (cart, user data)|Open to all AWS users|

---

## **Visual Overview**

Here's a simplified architectural flow:

```
Client Request
   |
   v
DynamoDB API Gateway
   |
   v
Request Router (Auth, Throttle, Route)
   |
   v
Partition (based on hash of key)
   |
   v
Storage Engine (Write logs, flush to disk)
   |
   v
Replicate to AZs + Update Streams
```

---

