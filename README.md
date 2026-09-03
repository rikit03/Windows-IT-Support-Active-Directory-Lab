# Active Directory IT Administration Lab

## 📌 Project Overview

This project is a hands-on **Active Directory IT Administration Lab** built to simulate a small business Windows domain environment.

The lab demonstrates practical skills in:

* Active Directory Domain Services (AD DS)
* Windows Server 2022 administration
* DNS configuration
* Organizational Unit (OU) management
* User and security group management
* Group Policy
* Account security and password policies
* Windows 11 domain client administration
* PowerShell-based administration

> **Project Status:** Steps 1–7 completed. Windows 11 client configuration is the next phase.

---

## 🖥️ Lab Environment

| Component               | Configuration                |
| ----------------------- | ---------------------------- |
| Host OS                 | Windows 11                   |
| Domain Controller       | Windows Server 2022          |
| Client OS               | Windows 11                   |
| Virtualization          | Oracle VirtualBox            |
| Domain Controller Name  | DC01                         |
| Active Directory Domain | `corp.albion.local`          |
| NetBIOS Name            | `CORP`                       |
| Private Network         | VirtualBox Host-Only Network |
| Internet Network        | VirtualBox NAT               |
| DC01 Private IP         | `192.168.56.10`              |
| Windows 11 Private IP   | `192.168.56.20`              |
| Subnet Mask             | `255.255.255.0`              |
| DNS Server              | `192.168.56.10`              |

---

# Phase 1 — Server Environment Setup

### Completed

* Installed Windows Server 2022.
* Renamed the server to **DC01**.
* Configured VirtualBox networking.
* Configured:

  * Adapter 1 → NAT
  * Adapter 2 → Host-Only
* Configured a static IP address for the private AD network.
* Configured DC01 as the DNS server for the domain environment.
* Verified the server network configuration.

### Evidence

* `01-server-baseline.png`
* `02-static-ip-dns.png`

---

# Phase 2 — Active Directory Domain Services

### Completed

Installed and configured **Active Directory Domain Services (AD DS)** on DC01.

Created a new Active Directory forest:

```text
corp.albion.local
```

### Domain Controller Configuration

* Domain Controller: `DC01`
* Forest: `corp.albion.local`
* NetBIOS Name: `CORP`
* DNS Server: Enabled
* Global Catalog: Enabled
* Read-only domain controller: Disabled
* Forest functional level: Windows Server 2016
* Domain functional level: Windows Server 2016
* DNS delegation: Not configured

DC01 was successfully promoted as the domain controller.

---

# Phase 3 — Active Directory Structure

Created organizational units to organize users and groups.

### User Organization

```text
corp.albion.local
└── Users
    ├── IT
    ├── HR
    ├── Finance
    └── Sales
```

### Groups Organization

```text
corp.albion.local
└── Groups
```

---

# Phase 4 — User Administration

Created test domain users for the lab environment.

### Test Users

| User          | Username  | Department |
| ------------- | --------- | ---------- |
| Alex Morgan   | `amorgan` | IT         |
| Taylor Morgan | `tmorgan` | HR         |
| Jordan Lee    | `jlee`    | Finance    |
| Sarah Chen    | `schen`   | Sales      |

The built-in Active Directory accounts such as **Administrator** and **Guest** were left unchanged.

---

# Phase 5 — Security Group Administration

Created the following security groups:

```text
IT-Admins
IT-Support
HR-Users
Finance-Users
Sales-Users
```

### Group Membership

| Security Group | Member        |
| -------------- | ------------- |
| IT-Admins      | Alex Morgan   |
| IT-Support     | Alex Morgan   |
| HR-Users       | Taylor Morgan |
| Finance-Users  | Jordan Lee    |
| Sales-Users    | Sarah Chen    |

The groups were configured as:

* **Group Scope:** Global
* **Group Type:** Security

---

# Phase 6 — Group Policy

Created and linked the following Group Policy Object:

```text
Corp-Password-Policy
```

The policy was linked to the:

```text
corp.albion.local
```

domain.

## Password Policy

Configured:

* Password history: **5 passwords**
* Maximum password age: **90 days**
* Minimum password age: **1 day**
* Minimum password length: **8 characters**
* Password complexity requirements: **Enabled**
* Reversible password encryption: **Disabled**

## Account Lockout Policy

Configured:

* Account lockout threshold: **5 invalid attempts**
* Account lockout duration: **15 minutes**
* Reset account lockout counter after: **15 minutes**

The policy was updated using:

```cmd
gpupdate /force
```

Policy application can be verified using:

```cmd
gpresult /r
```

---

# 📸 Current Project Evidence

Current screenshots include:

```text
screenshots/
├── 01-server-baseline.png
├── 02-static-ip-dns.png
├── 07-password-policy.png
└── 07b-account-lockout-policy.png
```

Additional screenshots will be added as each phase is completed.

---

# ⏭️ Next Phase

## Windows 11 Client Configuration

The next stage is to configure the Windows 11 client for the private Active Directory network.

Planned configuration:

```text
Windows 11 Client
├── Adapter 1 → NAT → Internet
└── Adapter 2 → Host-Only → AD Network
```

Private network configuration:

```text
IP Address:       192.168.56.20
Subnet Mask:      255.255.255.0
Default Gateway:  [Blank]
Preferred DNS:    192.168.56.10
```

After configuration, connectivity will be tested using:

```cmd
ping 192.168.56.10
```

DNS will then be verified before joining the Windows 11 client to:

```text
corp.albion.local
```

---

## 🎯 Project Goal

The completed lab will demonstrate practical entry-level IT administration skills including:

**Configure → Administer → Troubleshoot → Verify → Document**

The final project will simulate common tasks performed by an **IT Support Technician, Service Desk Analyst, Desktop Support Technician, or Junior Systems Administrator** in a Windows/Active Directory environment.
