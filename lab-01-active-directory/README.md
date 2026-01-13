# Lab 01 – Active Directory: User Locked Out

## Overview
This lab simulates a real-world Help Desk incident where a domain user is unable to log in due to authentication issues in an Active Directory environment. The objective is to reproduce the problem, perform structured troubleshooting, identify root causes, and restore user access.

The lab was built using a virtualized environment and focuses on common Level 1–2 IT Support tasks, including networking, DNS, Active Directory user management, and Kerberos time synchronization.

---

## Environment
- Hypervisor: VirtualBox
- Domain Controller:
  - Windows Server (Server Core)
  - Active Directory Domain Services (AD DS)
  - DNS Server
  - Domain: `lab.local`
- Client Machine:
  - Windows 11 Pro
  - Joined to `lab.local`
- Network:
  - Host-Only Adapter
  - Static IP for Domain Controller
  - Client DNS pointing to Domain Controller

---

## Lab Structure

lab-01-active-directory/
├── README.md
├── problem.md
├── diagnosis.md
└── solution.md


Each file documents a specific phase of the incident lifecycle, following a Help Desk troubleshooting methodology.

---

## Skills Practiced
- Active Directory user management
- Domain join troubleshooting
- DNS configuration for AD
- Firewall and network profile analysis
- Kerberos authentication and time synchronization
- Structured incident documentation

---

## Outcome
User access was successfully restored after identifying and resolving multiple underlying issues, including DNS misconfiguration, firewall behavior, network adapter conflicts, and Kerberos time desynchronization.

This lab represents a realistic Help Desk support scenario and its resolution.
