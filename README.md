# Active Directory IT Administration Lab

## Project Overview

This is an independent hands-on lab designed to simulate a small business **Active Directory environment** using Windows Server 2022 and Windows 11 virtual machines.

The project focuses on practical IT administration skills including Active Directory Domain Services, DNS, user and group management, Group Policy, Windows domain joining, file permissions, PowerShell administration, and IT troubleshooting.

The environment is being built incrementally, with each major configuration and troubleshooting milestone documented through technical evidence and screenshots.

---

## Lab Environment

| Component             | Configuration                |
| --------------------- | ---------------------------- |
| Server                | Windows Server 2022          |
| Client                | Windows 11                   |
| Virtualization        | Oracle VirtualBox            |
| Domain Controller     | DC01                         |
| Planned Domain        | `corp.albion.local`          |
| Private Network       | VirtualBox Host-Only Network |
| Internet Connectivity | VirtualBox NAT               |

---

## Network Architecture

The lab uses a dual-network design. NAT provides internet connectivity, while the Host-Only network provides private communication between the Domain Controller and Windows 11 client.

```text
                         Internet
                            │
                           NAT
                            │
                    ┌───────────────┐
                    │     DC01      │
                    │ Windows Server │
                    │     2022      │
                    └───────┬───────┘
                            │
                    Host-Only Network
                            │
                    ┌───────┴───────┐
                    │   Windows 11  │
                    │     Client    │
                    └───────────────┘
```

---

## Completed Work

### 1. Windows Server 2022 Deployment

* Deployed Windows Server 2022 as a virtual machine using VirtualBox.
* Completed the Windows Server installation.
* Configured the virtual machine for the lab environment.
* Removed the Windows Server installation ISO from the virtual DVD drive after installation.
* Renamed the server to **DC01**.

### 2. Virtual Network Configuration

* Configured a VirtualBox Host-Only network for the private lab environment.
* Configured DC01 to use the Host-Only network for communication with the future Windows 11 client.
* Configured NAT connectivity for internet access.
* Verified that internet connectivity is working on DC01.

### 3. Initial Network Preparation

* Configured the server's private network addressing.
* Prepared DC01 for its future role as the Active Directory Domain Controller and DNS server.

---

## Current Project Status

**Phase 1 — Infrastructure Setup: COMPLETE ✅**

The Windows Server 2022 environment and basic networking have been prepared.

**Phase 2 — Active Directory Configuration: NEXT**

Planned tasks:

* [ ] Install Active Directory Domain Services (AD DS)
* [ ] Install/configure DNS
* [ ] Promote DC01 to Domain Controller
* [ ] Create `corp.albion.local` domain
* [ ] Verify Active Directory and DNS functionality
* [ ] Create Organizational Units (OUs)
* [ ] Create domain users
* [ ] Create security groups
* [ ] Configure Group Policy
* [ ] Configure password and account lockout policies
* [ ] Configure Windows 11 client
* [ ] Join Windows 11 to the domain
* [ ] Test domain user authentication
* [ ] Configure shared folders and NTFS permissions
* [ ] Perform Active Directory administration using PowerShell
* [ ] Create and resolve a realistic IT support troubleshooting scenario
* [ ] Document the completed environment

---

## Organizational Unit Structure

The planned Active Directory structure will be:

```text
corp.albion.local
│
├── Users
│   ├── IT
│   ├── HR
│   ├── Finance
│   └── Sales
│
├── Computers
│   ├── Workstations
│   └── IT-Computers
│
└── Groups
```

This structure will be implemented during the Active Directory configuration phase.

---

## Evidence

Only completed work is documented with screenshots.

### Screenshot 01 — Server Baseline

Shows the Windows Server 2022 environment configured as **DC01**.

### Screenshot 02 — Network Configuration

Shows the network/IP configuration used to prepare DC01 for the Active Directory environment.

Additional screenshots will be added as major technical milestones are completed.

---

## Planned Technical Skills Demonstrated

By completion, this project will demonstrate hands-on experience with:

* Windows Server 2022
* Active Directory Domain Services
* DNS
* Domain Controllers
* Organizational Units
* User and group administration
* Security groups
* Group Policy
* Password and account lockout policies
* Windows 11 domain joining
* Domain authentication
* NTFS permissions
* Shared folders
* PowerShell
* IT troubleshooting
* Technical documentation

---

## Tools & Technologies

* **Windows Server 2022**
* **Windows 11**
* **Oracle VirtualBox**
* **Active Directory Domain Services**
* **DNS**
* **Group Policy**
* **PowerShell**
* **NTFS Permissions**
* **VirtualBox Host-Only Networking**
* **NAT Networking**

---

## Project Objective

The objective of this lab is to build and administer a realistic Windows-based business environment from the ground up.

The project emphasizes practical IT administration tasks that are relevant to **Service Desk, IT Support, Desktop Support, MSP, and Junior Systems Administration roles**.

The lab follows an evidence-based approach:

```text
Configure → Test → Troubleshoot → Verify → Document
```

All configurations, tests, and troubleshooting activities will be documented as the project progresses.
