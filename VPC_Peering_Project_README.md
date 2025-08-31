
# 🚀 AWS VPC Peering Project  

This project demonstrates how to set up **VPC Peering** between two VPCs in AWS.  
- **VPC1 (192.168.5.0/24)** → Contains **Public** and **Private** subnets  
- **VPC2 (192.168.6.0/24)** → Contains **Private** subnet  
- **Goal:** Allow private subnet of VPC1 to communicate with the private subnet of VPC2 via **VPC Peering**.

---

## 🏗️ Architecture  

```
            +------------------+         +------------------+
            |   VPC 1          |         |   VPC 2          |
            | 192.168.5.0/24   |         | 192.168.6.0/24   |
            |                  |         |                  |
   Public Subnet    Private Subnet   <-- Peering -->   Private Subnet
   192.168.5.0/25   192.168.5.128/25               192.168.6.0/24
            +------------------+         +------------------+
```

---

## 🛠️ Steps to Create the Setup  

### 1️⃣ Create VPC1  
- CIDR: `192.168.5.0/24`  
- Subnets:  
  - Public Subnet → `192.168.5.0/25`  
  - Private Subnet → `192.168.5.128/25`  
- Attach **Internet Gateway** to Public Subnet  
- Create **Route Tables**:  
  - Public Route Table → Add IGW route for internet  
  - Private Route Table → Default local route only  

---

### 2️⃣ Create VPC2  
- CIDR: `192.168.6.0/24`  
- Subnet:  
  - Private Subnet → `192.168.6.0/24`  
- Create Route Table with default local route  

---

### 3️⃣ Create VPC Peering  
- Request Peering from **VPC1 → VPC2**  
- Accept Peering in **VPC2**  
- Update Route Tables:  
  - VPC1 Private Route Table → Add `192.168.6.0/24` → Target: Peering ID  
  - VPC2 Route Table → Add `192.168.5.0/24` → Target: Peering ID  

---

### 4️⃣ Launch EC2 Instances  
- VPC1 Private Subnet → EC2-1  
- VPC2 Private Subnet → EC2-2  
- Ensure **Security Groups** allow inbound/outbound traffic for testing (e.g., SSH or ICMP).  

---

## ✅ Verification  

1. SSH into EC2 instance in VPC1 Private Subnet  
2. Ping private IP of EC2 in VPC2  
3. Successful response confirms **VPC Peering** connectivity 🎉  

---

## 📂 Project Structure  

```
VPC-Peering-Project/
│-- README.md
│-- architecture.png (Optional if you create a diagram image)
│-- setup-steps.txt
```

---

## 👩‍💻 Author  

**Prajakta Pandaram**  
*Cloud & DevOps Enthusiast | AWS Projects*  

---

## 📌 Future Enhancements  

- Add **Transit Gateway** for multiple VPC connectivity  
- Automate with **Terraform** or **CloudFormation**  
- Add **NAT Gateway** for internet access from private subnet  

---
