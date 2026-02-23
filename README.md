# 🌐 Active Directory Cross-Forest Trust Implementation Lab

---

## 🧠 Objective

Design and implement a two-way cross-forest trust between two separate Active Directory forests, enabling secure resource sharing across organizational boundaries.

This lab simulates enterprise environments where multiple forests must trust each other for authentication and access control.

---

## 🛠️ Technologies Used

- Windows Server 2016
- Active Directory Domain Services (AD DS)
- DNS Conditional Forwarders
- Active Directory Domains and Trusts
- NTFS Permissions
- SMB Share Permissions
- Hyper-V Virtual Machines

---

# 🏗️ Environment Overview

| Forest | Domain Controller | Domain Name |
|--------|------------------|-------------|
| Forest 1 | RWDC31 | Domain31.local |
| Forest 2 | Server31-C | NewDomain31.local |

| File Server | Role |
|-------------|------|
| Server31-A | Shared Resource Host |

---

# ⚙️ Project Implementation

---

## 1️⃣ Created Second Active Directory Forest

On **Server31-C**:

- Removed server from child domain
- Joined workgroup
- Installed Active Directory Domain Services
- Promoted server to Domain Controller
- Created new forest: `NewDomain31.local`
- Verified successful domain controller deployment

---

## 2️⃣ Configured DNS Conditional Forwarders

To allow name resolution between forests:

### On RWDC31
- Opened DNS Manager
- Created Conditional Forwarder for `NewDomain31.local`
- Entered IP of Server31-C

### On Server31-C
- Created Conditional Forwarder for `Domain31.local`
- Entered IP of RWDC31

This allowed cross-forest DNS name resolution.

---

## 3️⃣ Created Organizational Units & Users

In both forests:

- Created OU: `Pencils`
- Created users:
  - Fred
  - Bill
  - Sue

Verified users appear correctly in Active Directory Users and Computers.

---

## 4️⃣ Configured Two-Way Forest Trust

On RWDC31:

- Opened **Active Directory Domains and Trusts**
- Created new forest trust
- Configured as **Two-Way Trust**
- Verified trust validation succeeded

This enabled bidirectional authentication between both forests.

---

## 5️⃣ Configured Cross-Forest Resource Access

On **Server31-A**:

- Created shared folder: `Money`
- Configured Share Permissions
- Configured NTFS Permissions
- Granted write access to:
  - Users from Domain31.local
  - Users from NewDomain31.local
- Did not use security groups (per lab requirements)

Validated:
- Users from both forests successfully authenticated
- Users could access shared folder
- Write permissions functioned correctly

---

# 🔎 Key Concepts Demonstrated

- Multi-Forest AD Architecture
- DNS Conditional Forwarding
- Forest Trust Relationships
- Cross-Forest Authentication
- SID Filtering & Trust Validation
- NTFS vs Share Permissions
- Enterprise Identity Design

---

# 🔐 Skills Demonstrated

- Active Directory Multi-Forest Deployment  
- Trust Relationship Configuration  
- Cross-Domain Access Control  
- DNS Infrastructure Design  
- Windows File Server Permission Management  
- Enterprise Identity & Access Management Concepts  

---

# 📷 Screenshots

### New Forest Created (Server31-C)
![New Forest](https://i.imgur.com/6iXoNN2.png)

---

### Conditional Forwarder (RWDC31)
![Conditional Forwarder](https://i.imgur.com/m8QYmEB.png)

---

### Two-Way Forest Trust Validation
![Forest Trust](https://i.imgur.com/gUsySDJ.png)

---

### Shared Folder Permissions (Money Folder)
![Share Permissions](https://i.imgur.com/SRISHHD.png)

---

### NTFS Permissions (Advanced Security Settings)
![NTFS Permissions](https://i.imgur.com/IuHlq4e.png)

---

# 🚀 Project Outcome

Successfully deployed a second Active Directory forest and established a two-way cross-forest trust, enabling secure authentication and resource access between separate identity environments.

This lab simulates real-world enterprise mergers, acquisitions, and multi-organization trust scenarios.

## 🔐 Security Insight

Misconfigured forest trusts can introduce authentication vulnerabilities, excessive trust exposure, and unintended resource access. Proper trust validation and DNS configuration are critical to maintaining secure multi-forest environments.

