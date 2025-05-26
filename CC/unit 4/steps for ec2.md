# **Step-by-Step Guide to Configuring an Amazon EC2 VM Instance**

Amazon Elastic Compute Cloud (EC2) provides scalable virtual servers in the cloud. Below is a detailed, step-by-step guide to launching and configuring an EC2 instance.
---
![[Pasted image 20250523190613.png]]
---

## **Step 1: Sign in to AWS Management Console**
1. Go to **[AWS Console](https://aws.amazon.com/console/)**.
2. Sign in with your AWS account (or create one if needed).

---

## **Step 2: Navigate to EC2 Dashboard**
1. From the **AWS Services** menu, select **EC2** under **Compute**.
2. Click **"Launch Instance"** to create a new VM.

---

## **Step 3: Choose an Amazon Machine Image (AMI)**
- An **AMI** is a pre-configured template for your VM (OS + software).
- Options:
  - **Amazon Linux** (Recommended for AWS-optimized workloads)
  - **Ubuntu** (Popular for development)
  - **Windows Server** (For .NET applications)
  - **Custom AMIs** (Marketplace or your own)

➔ Select an AMI and click **"Select"**.

---

## **Step 4: Select an Instance Type**
AWS offers different **instance families** based on workload needs:
| Type | Use Case | Example |
|------|----------|---------|
| **General Purpose (t3, m6i)** | Web servers, small databases | `t3.micro` (Free Tier eligible) |
| **Compute Optimized (c6i)** | High-performance computing | `c6i.large` |
| **Memory Optimized (r6i)** | Databases, big data | `r6i.xlarge` |
| **GPU Instances (g4dn)** | Machine learning, gaming | `g4dn.xlarge` |

➔ Choose an instance type and click **"Next: Configure Instance Details"**.

---

## **Step 5: Configure Instance Details**
- **Number of Instances**: Default is `1` (increase for scaling).
- **Network**: Select a **VPC** (Default VPC works for beginners).
- **Subnet**: Choose availability zone (`us-east-1a`, `us-east-1b`, etc.).
- **Auto-assign Public IP**: Enable if internet access is needed.
- **IAM Role** (Optional): Assign permissions for AWS services.
- **Shutdown Behavior**: `Stop` or `Terminate` the instance.
- **Advanced Options** (Optional):
  - User data (Bash/Powershell script for auto-configuration).

➔ Click **"Next: Add Storage"**.

---

## **Step 6: Add Storage (EBS Volumes)**
- **Root Volume**: Default is `8 GB` (SSD `gp3` recommended).
- **Add New Volumes**: 
  - **EBS (Elastic Block Store)** → Persistent storage.
  - **Instance Store (Ephemeral)** → Temporary, high-speed storage.
- **Encryption**: Enable for sensitive data.

➔ Click **"Next: Add Tags"**.

---

## **Step 7: Add Tags (Optional but Recommended)**
- Tags help organize instances (e.g., `Name=WebServer`, `Environment=Prod`).
- Example:  
  - **Key**: `Name`  
  - **Value**: `MyFirstEC2Instance`  

➔ Click **"Next: Configure Security Group"**.

---

## **Step 8: Configure Security Group (Firewall Rules)**
- A **security group** acts as a virtual firewall.
- **Default Rule**: SSH (Port 22) for Linux / RDP (Port 3389) for Windows.
- **Add Custom Rules**:
  - **HTTP (Port 80)** → For web servers.
  - **HTTPS (Port 443)** → Secure web traffic.
  - **Custom TCP/UDP** → For specific apps.

➔ Click **"Review and Launch"**.

---

## **Step 9: Review & Launch**
- Verify all settings.
- Click **"Launch"**.

---

## **Step 10: Select or Create a Key Pair**
- A **key pair** (.pem file) is required for SSH access.
- Options:
  - **Create a new key pair** → Download `.pem` file (keep it secure!).
  - **Use an existing key pair** (if you have one).

➔ Click **"Launch Instances"**.

---

## **Step 11: Access the EC2 Instance**
### **For Linux (SSH Access)**
```bash
chmod 400 my-key-pair.pem  # Set correct permissions
ssh -i "my-key-pair.pem" ec2-user@<Public-IP>
```
### **For Windows (RDP Access)**
1. Use **Remote Desktop Protocol (RDP)** with the `.pem` key.
2. Get the **admin password** from AWS Console (EC2 → Instance → "Get Password").

---

## **Step 12: Post-Configuration (Optional)**
- **Install Software**: Use `sudo yum install` (Amazon Linux) or `apt-get` (Ubuntu).
- **Attach Elastic IP** (Static IP) if needed.
- **Set Up Auto-Scaling** for high availability.
- **Enable Monitoring** with **Amazon CloudWatch**.

---

## **Summary of Key Steps**
1. **Log in to AWS Console** → EC2 Dashboard.
2. **Choose AMI** (OS template).
3. **Select Instance Type** (CPU, RAM, GPU).
4. **Configure Network & Storage**.
5. **Set Security Group** (Firewall rules).
6. **Launch with Key Pair** (SSH/RDP access).
7. **Connect & Manage** the VM.

---

