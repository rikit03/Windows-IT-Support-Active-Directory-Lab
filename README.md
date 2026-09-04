# Windows IT Support & Active Directory Lab

A hands-on Windows IT support lab built to demonstrate practical experience with **Windows Server 2022, Active Directory, DNS, Group Policy, Windows 11 domain administration, user management, permissions, and troubleshooting**.

Designed as a portfolio project for **IT Support, Help Desk, Service Desk, Desktop Support, and Junior IT** roles.

---

## 🎯 Project Overview

Built a small enterprise-style Windows environment using:

* **Windows Server 2022** — Domain Controller
* **Windows 11** — Domain-joined client
* **Active Directory Domain Services (AD DS)**
* **DNS**
* **Group Policy**
* **VirtualBox**
* **PowerShell / Windows administration tools**

**Domain:** `corp.albion.local`

The lab simulates common IT support and system administration tasks performed in a business environment.

---

## 🖥️ Lab Environment

| Component         | Configuration       |
| ----------------- | ------------------- |
| Domain Controller | Windows Server 2022 |
| Client            | Windows 11          |
| Domain            | `corp.albion.local` |
| Server IP         | `192.168.56.20`     |
| Client IP         | `192.168.56.10`     |
| DNS               | `192.168.56.20`     |
| Virtualization    | Oracle VirtualBox   |

---

## 🔧 Implementation

### 1. Windows Server 2022 Domain Controller

Configured Windows Server 2022 and deployed **Active Directory Domain Services and DNS**.

![Server Baseline](screenshots/01-server-baseline.png)

---

### 2. Static IP & DNS Configuration

Configured the Domain Controller with a static IP address and configured the Windows 11 client to use the Domain Controller for DNS resolution.

![Static IP and DNS](screenshots/02-static-ip-dns.png)

---

### 3. Active Directory Structure

Created organizational units to organize users and groups:

```text
corp.albion.local
├── Users
│   ├── IT
│   ├── HR
│   ├── Finance
│   └── Sales
└── Groups
```

Created test users and security groups to simulate departmental administration.

---

### 4. Windows 11 Domain Join

Joined the Windows 11 workstation to the `corp.albion.local` domain.

![Domain Join](screenshots/03-domain-join.png)

---

### 5. Domain Authentication

Verified successful domain authentication using the test account:

`CORP\amorgan`

![Domain Login Verification](screenshots/04-domain-login-verification.png)

---

### 6. Active Directory Computer Management

Verified that the Windows 11 workstation was successfully registered in Active Directory.

![Computer Account in AD](screenshots/05-domain-computer-in-ad.png)

---

### 7. Group Policy — Password Policy

Created and configured the `Corp-Password-Policy` GPO with password requirements including:

* Minimum password length
* Password complexity
* Password history
* Password expiration

![Password Policy](screenshots/07-password-policy.png)

---

### 8. Group Policy — Account Lockout

Configured account lockout controls to help protect user accounts from repeated failed authentication attempts.

![Account Lockout Policy](screenshots/07b-account-lockout-policy.png)

---

## 🧪 Verification & Troubleshooting

Used Windows administration and troubleshooting tools to verify the environment, including:

```text
ipconfig
nslookup
ping
whoami
gpupdate /force
gpresult /r
Active Directory Users and Computers
Group Policy Management
```

Troubleshooting followed a structured approach:

**Identify → Investigate → Isolate → Resolve → Verify**

---

## 🔐 Security Concepts Practiced

* Active Directory authentication
* Role-based security groups
* Organizational Units
* Password policies
* Account lockout policies
* DNS-based domain resolution
* Least-privilege concepts
* Centralized Group Policy management

---

## 💼 IT Support Scenarios

This lab provides practical exposure to tasks such as:

* Creating and managing users
* Managing security groups
* Joining computers to a domain
* Troubleshooting domain login issues
* Verifying DNS configuration
* Applying Group Policy
* Managing password and account policies
* Investigating Windows authentication problems

---

## 🛠️ Skills Demonstrated

**Windows:** Windows Server 2022, Windows 11, Active Directory, DNS, Group Policy

**IT Support:** User administration, account troubleshooting, domain authentication, permissions, troubleshooting

**Tools:** PowerShell, Active Directory Users and Computers, Group Policy Management, VirtualBox

**Networking:** IPv4, DNS, static addressing, client/server connectivity

---

## 📂 Repository Structure

```text
Windows-IT-Support-Active-Directory-Lab/
│
├── README.md
│
└── screenshots/
    ├── 01-server-baseline.png
    ├── 02-static-ip-dns.png
    ├── 03-domain-join.png
    ├── 04-domain-login-verification.png
    ├── 05-domain-computer-in-ad.png
    ├── 07-password-policy.png
    └── 07b-account-lockout-policy.png
```

---

## 📌 Portfolio Value

This project demonstrates hands-on experience with **Windows administration, Active Directory, DNS, Group Policy, user management, domain environments, and structured troubleshooting**.

It was built independently to strengthen practical IT support skills and provide documented evidence of technical work.

**Target Roles:**
IT Support Technician · Service Desk Analyst · Help Desk Analyst · Desktop Support Technician · Junior IT Technician · NOC Technician

---

## 🚀 Future Improvements

Planned extensions include:

* File and folder permissions
* Shared network drives
* User onboarding/offboarding
* Additional Group Policy testing
* Realistic Windows troubleshooting scenarios
* PowerShell administration tasks
