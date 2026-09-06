# Windows IT Support & Active Directory Lab

A hands-on Windows IT Support and Active Directory lab designed to simulate common enterprise IT administration and service desk tasks.

The project demonstrates practical experience with **Windows Server 2022, Windows 11, Active Directory, DNS, Group Policy, user and group management, permissions, shared network resources, and troubleshooting**.

The lab was independently built using virtual machines to practice real-world IT support and systems administration workflows.

---

## 📌 Project Overview

This lab simulates a small organizational Windows environment where IT support tasks are performed from both a Windows Server and Windows 11 client.

The environment includes:

* Windows Server 2022 domain controller
* Windows 11 domain-joined client
* Active Directory Domain Services
* DNS
* Organizational Units (OUs)
* User and security group management
* Group Policy
* Password and account lockout policies
* NTFS permissions
* Network file sharing
* Mapped network drives
* User access verification
* Basic troubleshooting and connectivity testing

The project focuses on the practical workflow of:

**Configure → Test → Troubleshoot → Verify → Document**

---

# 🖥️ Lab Environment

| Component         | Configuration              |
| ----------------- | -------------------------- |
| Server OS         | Windows Server 2022        |
| Client OS         | Windows 11                 |
| Virtualization    | Oracle VirtualBox          |
| Domain            | `corp.albion.local`        |
| NetBIOS Name      | `CORP`                     |
| Domain Controller | `DC`                       |
| Server IP         | `192.168.56.20`            |
| Windows 11 IP     | `192.168.56.10`            |
| DNS Server        | `192.168.56.20`            |
| Network           | VirtualBox Host-Only + NAT |

---

# 🏗️ Active Directory Structure

The Active Directory environment was organized using Organizational Units to simulate departmental administration.

```text
corp.albion.local
│
├── Users
│   ├── IT
│   ├── HR
│   ├── Finance
│   └── Sales
│
└── Groups
```

Test users were created for different departments:

* **Alex Morgan** — IT
* **Taylor Morgan** — HR
* **Jordan Lee** — Finance
* **Sarah Chen** — Sales

Security groups were also created to control access to departmental resources.

---

# 🔧 Implementation & Verification

## 01 — Windows Server Baseline

Configured the Windows Server 2022 virtual machine as the foundation for the lab environment.

The server was prepared for Active Directory, DNS, and domain services.

![Windows Server Baseline](screenshots/01-server-baseline.png)

---

## 02 — Static IP & DNS Configuration

Configured a static IP address for the domain controller and configured DNS for the internal Active Directory environment.

Server IP:

```text
192.168.56.20
```

DNS:

```text
192.168.56.20
```

![Static IP and DNS](screenshots/02-static-ip-dns.png)

---

## 03 — Windows 11 Domain Join

Configured the Windows 11 client and joined it to:

```text
corp.albion.local
```

This established communication between the client and the Active Directory domain.

![Domain Join](screenshots/03-domain-join.png)

---

## 04 — Domain Login Verification

Verified that a domain user could successfully authenticate to the Windows 11 client.

Example domain account:

```text
CORP\amorgan
```

![Domain Login Verification](screenshots/04-domain-login-verification.png)

---

## 05 — Computer Account in Active Directory

Verified that the Windows 11 computer account was successfully registered in Active Directory.

This demonstrates basic endpoint/domain administration.

![Computer in Active Directory](screenshots/05-domain-computer-in-ad.png)

---

## 06 — Password Policy

Created and configured a domain password policy using Group Policy.

Configured requirements included:

* Minimum password length
* Password complexity
* Password history
* Maximum password age
* Minimum password age

![Password Policy](screenshots/07-password-policy.png)

---

## 07 — Account Lockout Policy

Configured account lockout controls to help protect domain accounts from repeated failed authentication attempts.

Configured controls included:

* Failed login threshold
* Lockout duration
* Lockout counter reset period

![Account Lockout Policy](screenshots/07b-account-lockout-policy.png)

---

## 08 — Shared Folder Access

Created a shared IT resource for authorized users.

Server-side folder:

```text
C:\CompanyShares\IT-Shared
```

Network path:

```text
\\DC01\CompanyShares\IT-Shared
```

Access was controlled through the Active Directory security group:

```text
IT-Shared-Access
```

Alex Morgan was granted access through the security group and successfully accessed the shared resource from Windows 11.

![Shared Folder Access](screenshots/shared-drive/08-shared-folder-access.png)

---

## 09 — Mapped Network Drive

Mapped the shared IT resource as a network drive on the Windows 11 client.

Drive:

```text
Z:
```

Network location:

```text
\\DC01\CompanyShares\IT-Shared
```

The mapped drive was successfully accessed by the domain user.

![Mapped Network Drive](screenshots/shared-drive/09-mapped-network-drive.png)

---

# 🔐 Access Control & Permissions

The shared IT resource uses both **NTFS permissions** and **network share permissions**.

The Active Directory security group:

```text
IT-Shared-Access
```

was used to control access rather than assigning permissions individually to users.

The configuration demonstrates an important enterprise administration principle:

**Use security groups to manage resource access.**

The shared drive was also tested from the Windows 11 client to verify that the authorized user could access and modify resources.

---

# 🧪 Verification & Troubleshooting

The environment was verified through practical testing rather than configuration alone.

Examples included:

* Domain authentication testing
* DNS verification
* Active Directory computer verification
* Group membership verification
* Shared folder access testing
* Network share testing
* Mapped drive testing
* File creation and modification testing
* User permission verification

Common Windows administration and troubleshooting tools used or practiced include:

```text
ipconfig
ping
nslookup
gpupdate /force
gpresult /r
```

---

# 🛠️ IT Support Scenarios

The lab is designed around situations commonly encountered by entry-level IT support technicians.

Examples include:

### User & Account Management

* Creating user accounts
* Organizing users into departmental OUs
* Assigning security group membership
* Verifying account access

### Authentication

* Domain login verification
* Password policy configuration
* Account lockout configuration
* Basic authentication troubleshooting

### File & Resource Access

* Configuring shared folders
* Managing NTFS permissions
* Managing share permissions
* Mapping network drives
* Testing user access

### Endpoint & Network Troubleshooting

* DNS verification
* IP configuration
* Domain connectivity
* Client/server communication
* Access troubleshooting

---

# 🧰 Technologies & Skills

### Operating Systems

* Windows Server 2022
* Windows 11

### Microsoft Technologies

* Active Directory Domain Services
* DNS
* Group Policy
* Windows user administration
* Security groups
* Organizational Units
* NTFS permissions
* Windows file sharing

### Networking

* IPv4
* DNS
* Host-only networking
* NAT
* Client/server connectivity
* Network shares
* Mapped network drives

### Virtualization

* Oracle VirtualBox

### Troubleshooting

* `ipconfig`
* `ping`
* `nslookup`
* `gpupdate`
* `gpresult`
* Windows administrative tools
* Active Directory Users and Computers
* Computer Management

---

# 📂 Repository Structure

```text
Windows-IT-Support-Active-Directory-Lab/
│
├── README.md
│
├── screenshots/
│   ├── 01-server-baseline.png
│   ├── 02-static-ip-dns.png
│   ├── 03-domain-join.png
│   ├── 04-domain-login-verification.png
│   ├── 05-domain-computer-in-ad.png
│   ├── 07-password-policy.png
│   ├── 07b-account-lockout-policy.png
│   │
│   └── shared-drive/
│       ├── 08-shared-folder-access.png
│       └── 09-mapped-network-drive.png
│
└── documentation/
```

---

# 🎯 Skills Demonstrated

This project demonstrates practical exposure to:

* Windows Server administration
* Active Directory administration
* User and group management
* Organizational Unit design
* Domain joining
* DNS configuration
* Group Policy
* Password policies
* Account lockout policies
* File and folder permissions
* Network shares
* Mapped network drives
* Client/server troubleshooting
* Access verification
* Technical documentation

---

# 💼 Relevance to IT Support Roles

This project was designed to demonstrate hands-on skills relevant to entry-level positions such as:

* IT Support Technician
* Service Desk Analyst
* Help Desk Analyst
* Desktop Support Technician
* Junior Systems Administrator
* Technical Support Specialist
* Junior IT Support Technician

Rather than focusing only on configuration, the lab demonstrates the complete support workflow:

**Configure → Troubleshoot → Verify → Document**

This reflects common responsibilities in Windows-based IT support environments, including user administration, access management, endpoint troubleshooting, and resource management.

---

# 📈 Future Improvements

Future phases of the lab can include:

* User onboarding and offboarding workflows
* Additional Group Policy configurations
* File and folder access scenarios
* Three structured IT troubleshooting scenarios
* PowerShell automation
* Additional endpoint management
* Security hardening
* Event Viewer troubleshooting
* Windows service troubleshooting
* More advanced Active Directory administration

---

# 💡 Key Takeaways

This lab strengthened my practical understanding of how Windows-based enterprise environments are administered and supported.

The project provided hands-on practice with:

**Active Directory → DNS → Group Policy → Users & Groups → Permissions → File Sharing → Endpoint Testing → Troubleshooting**

The emphasis was on building practical troubleshooting and administration skills that can be applied in an entry-level IT support environment.

---

## 👤 About This Project

This is an **independently completed IT support and Active Directory lab** created to demonstrate hands-on technical skills and practical problem-solving.

**Focus Areas:**

`IT Support` · `Active Directory` · `Windows Server` · `Windows 11` · `DNS` · `Group Policy` · `User Management` · `Permissions` · `Networking` · `Troubleshooting`
