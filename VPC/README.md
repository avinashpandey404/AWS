# 🌐 AWS VPC to VPC Peering Project (Beginner → DevOps Ready)

## 📌 Overview

This project demonstrates how to **connect two AWS VPCs privately** using **VPC Peering** and verify communication using EC2 instances.
## 🏗️ Architecture Diagram (View 1)

![Architecture-1](https://github.com/avinashpandey404/AWS/blob/main/VPC/AWS%20VPC%20Peering%20Architecture-1.png?raw=true)
This guide is:

* ✅ Beginner-friendly
* ✅ Step-by-step (no steps skipped)
* ✅ Manual setup (no CLI / Terraform)
* ✅ Real-world DevOps project

---

# 🎯 What You Will Learn

* What is VPC, Subnet, CIDR
* How AWS networking works
* What is VPC Peering
* How servers communicate privately
* Security Groups & Routing

---
## 🔄 Traffic Flow (Workflow)

![Workflow](https://github.com/avinashpandey404/AWS/blob/main/VPC/AWS%20VPC%20Peering%20work%20flow.png?raw=true)
# 🧠 Key Concepts

## 🔹 What is VPC?

A **Virtual Private Cloud (VPC)** is your private network in AWS.

## 🔹 What is CIDR?

Defines IP range.

Example:

```
10.0.0.0/16
```

## 🔹 What is VPC Peering?

A **private connection between two VPCs** (no internet used).

## 🔹 What is ICMP?

Protocol used by:

```
ping
```

## 🔹 What is SSH?

Used to connect to EC2:

```
ssh -i key.pem ubuntu@<ip>
```

---

## 🏗️ Architecture Diagram (View 2)

![Architecture-2](https://github.com/avinashpandey404/AWS/blob/main/VPC/AWS%20VPC%20Peering%20Architecture-2.png?raw=true)

---

# 🚀 Step-by-Step Implementation

---

## ✅ STEP 1 — Create VPC-A

* Name: `VPC-A`
* CIDR: `10.0.0.0/16`

---

## ✅ STEP 2 — Create VPC-B

* Name: `VPC-B`
* CIDR: `10.1.0.0/16`

⚠️ CIDR must NOT overlap

---

## ✅ STEP 3 — Create Subnets

* VPC-A → `Subnet-A` → `10.0.1.0/24`
* VPC-B → `Subnet-B` → `10.1.1.0/24`

---

## ✅ STEP 4 — Create Internet Gateway

Attach:

* IGW-A → VPC-A
* IGW-B → VPC-B

👉 Required for SSH access

---

## ✅ STEP 5 — Route Tables (Internet)

VPC-A:

```
0.0.0.0/0 → IGW-A
```

VPC-B:

```
0.0.0.0/0 → IGW-B
```

---

## ✅ STEP 6 — Create Security Groups

### SG-A (VPC-A)

```
SSH → Your IP
ICMP → 10.1.0.0/16
```

### SG-B (VPC-B)

```
SSH → Your IP
ICMP → 10.0.0.0/16
```

---

## ✅ STEP 7 — Launch EC2 Instances

### EC2-A

* VPC: VPC-A
* Subnet: Subnet-A
* SG: SG-A
* OS: Ubuntu

### EC2-B

* VPC: VPC-B
* Subnet: Subnet-B
* SG: SG-B
* OS: Ubuntu

### 🔐 Key Pair

👉 Use SAME key pair for both instances

---

## ✅ STEP 8 — Create VPC Peering

* Requester: VPC-A
* Accepter: VPC-B

---

## ✅ STEP 9 — Accept Peering

Status should be:

```
Active
```

---

## ✅ STEP 10 — Update Route Tables

VPC-A:

```
10.1.0.0/16 → Peering
```

VPC-B:

```
10.0.0.0/16 → Peering
```

---

## ✅ STEP 11 — Connect via SSH

```
chmod 400 key.pem
ssh -i key.pem ubuntu@<public-ip>
```

---

## ✅ STEP 12 — Test Connectivity

From EC2-A:

```
ping <private-ip-of-EC2-B>
```

---

# 🎉 Expected Output

```
64 bytes from 10.1.x.x: icmp_seq=1 ttl=64 time=0.xxx ms
```

---

# ❌ Common Mistakes

| Issue            | Fix               |
| ---------------- | ----------------- |
| Ping not working | Check SG rules    |
| SSH failed       | Use correct key   |
| No connection    | Check route table |
| Wrong CIDR       | Fix IP            |

---

# 🔧 Troubleshooting

* ✔ Peering is ACTIVE
* ✔ Route tables updated
* ✔ SG allows ICMP
* ✔ Correct private IP used

---

# 💸 Cost (Free Tier)

* VPC → Free
* Peering → Free
* EC2 → Free tier

---

# 💼 Resume Ready

**Project: AWS VPC Peering**

* Connected two VPCs using VPC Peering
* Configured route tables and security groups
* Tested private communication using ICMP

---

# 🎤 Interview Questions

**Q: What is VPC Peering?**
Private connection between VPCs

**Q: Does it support transitive routing?**
❌ No

**Q: Why route tables?**
To define traffic path

**Q: What is CIDR?**
IP range

---

# 🚀 Final Result

✔ VPC connected
✔ Private communication working
✔ Real DevOps project

---

# 👨‍💻 Author

Avinash Pandey 🚀
