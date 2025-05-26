Amazon S3 (Simple Storage Service) and Amazon EC2 (Elastic Compute Cloud) are two core services provided by **Amazon Web Services (AWS)**. They serve different purposes but are often used together in cloud-based applications.

---

## **Amazon S3 (Simple Storage Service)**

### **Purpose**:

Amazon S3 is an object storage service designed to store and retrieve any amount of data from anywhere on the web. It's ideal for storing backups, static website files, media files, data lakes, and more.

### **Key Features**:

- **Object Storage**: Data is stored as _objects_ in _buckets_. An object consists of:
    
    - **Data** (file)
    - **Metadata** (key-value pairs)
    - **Unique Identifier (key)**
- **Scalability**: Automatically scales to store virtually unlimited data.
    
- **Durability & Availability**:
    
    - **99.999999999% durability** (11 9's)
    - **High availability** across multiple Availability Zones (AZs)
- **Security**:
    
    - Supports **encryption** (server-side and client-side)
    - **Access control** via IAM policies, bucket policies, ACLs
    - **Versioning** to preserve, retrieve, and restore every version of every object
- **Storage Classes**:
    
    - **S3 Standard** (frequent access)
    - **S3 Infrequent Access (IA)**
    - **S3 Glacier** (archival)
    - **S3 Intelligent-Tiering**
- **Static Website Hosting**: You can host a static website directly from S3.
    

### **Common Use Cases**:

- Backup and restore
- Data lakes
- Hosting static websites
- Media hosting (images, videos, etc.)
- Log storage
- Big data analytics input/output

---

## **Amazon EC2 (Elastic Compute Cloud)**

### **Purpose**:

Amazon EC2 provides **resizable compute capacity in the cloud**. It allows you to run virtual machines (called instances) in the AWS cloud.

### **Key Features**:

- **Virtual Servers**: Run Linux, Windows, or other OS instances.
    
- **Instance Types**:
    
    - **General Purpose** (e.g., t2, t3, t4g)
    - **Compute Optimized** (e.g., c5, c6g)
    - **Memory Optimized** (e.g., r5, x1)
    - **Storage Optimized** (e.g., i3, d2)
    - **GPU Instances** (e.g., p3, g4)
- **Elasticity**: Scale capacity up or down within minutes.
    
- **Persistent Storage**:
    
    - Use **Elastic Block Store (EBS)** for persistent disk storage.
    - You can also mount **S3** for object-based storage.
- **Networking**:
    
    - Attach **Elastic IPs**
    - Place instances in **VPCs**
    - Configure **Security Groups** (firewall rules)
- **Load Balancing & Auto Scaling**:
    
    - Integrates with **Elastic Load Balancing (ELB)** and **Auto Scaling Groups (ASG)**
- **Pricing Models**:
    
    - **On-Demand**: Pay per hour/second
    - **Reserved**: Commit to 1 or 3 years for discount
    - **Spot**: Use unused capacity at deep discounts
    - **Savings Plans**

### **Common Use Cases**:

- Web and application hosting
- Batch processing
- High-performance computing
- Game servers
- Dev/test environments
- Machine learning model hosting

---

## **S3 vs EC2 (Differences)**

|Feature|Amazon S3|Amazon EC2|
|---|---|---|
|Type|Object storage|Compute (Virtual Server)|
|Use Case|Store/retrieve files|Run applications, services|
|Persistent?|Yes (object-level)|No (unless EBS attached)|
|Pricing|Based on storage & data transfer|Based on instance uptime & usage|
|Data Access|REST API, SDK, CLI|SSH, remote access|

---

## **Using S3 and EC2 Together**

A common pattern is to:

- Use **EC2** to run a web application
- Store user-uploaded files or logs in **S3**
- Use **S3** to serve static content like images or JavaScript files to your EC2-hosted app

---

