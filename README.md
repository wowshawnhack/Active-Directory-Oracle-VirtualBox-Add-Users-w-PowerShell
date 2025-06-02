# 🏠 Active Directory Home Lab with VirtualBox & PowerShell

This project guides you through setting up a basic Active Directory (AD) home lab using Oracle VirtualBox, Windows Server 2019, and Windows 10. You'll create a domain controller, configure networking, install essential services like DHCP and NAT, and automate the creation of over 1,000 users using PowerShell.

---

## 🎯 Project Overview

- **Platform**: Oracle VirtualBox  
- **Operating Systems**: Windows Server 2019 (Domain Controller), Windows 10 (Client)  
- **Key Services**: Active Directory Domain Services (AD DS), DHCP, NAT  
- **Automation**: PowerShell scripting for bulk user creation

---

## 📦 Prerequisites

- Oracle VirtualBox installed on your host machine  
- Windows Server 2019 ISO  
- Windows 10 ISO  
- Basic understanding of networking concepts

---

## 🛠️ Setup Instructions

### 1. Download Required Software

- [Oracle VirtualBox](https://www.virtualbox.org/wiki/Downloads)  
- [Windows Server 2019 ISO](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2019)  
- [Windows 10 ISO](https://www.microsoft.com/en-us/software-download/windows10ISO)

### 2. Create the Domain Controller (DC) VM

- Create a VM named `DC` in VirtualBox
- Type: `Microsoft Windows`, Version: `Windows 2019 (64-bit)`
- Allocate at least 4 GB RAM and 50 GB disk
- Attach the Windows Server 2019 ISO

### 3. Configure Network Adapters

- Adapter 1: NAT (for internet access)  
- Adapter 2: Internal Network (for private LAN)

### 4. Install Windows Server 2019

- Complete the installation and set a strong admin password  
- Rename the server to `DC` and restart

### 5. Configure Static IP for Internal Network

- IP Address: `172.16.0.1`  
- Subnet Mask: `255.255.255.0`  
- DNS: `127.0.0.1`  
- Leave default gateway blank

### 6. Install Active Directory Domain Services (AD DS)

- Use Server Manager > Add Roles and Features  
- Select "Active Directory Domain Services"  
- Promote the server to a domain controller with root domain `mydomain.com`  
- Set a Directory Services Restore Mode (DSRM) password

### 7. Install and Configure DHCP

- Add "DHCP Server" role  
- Create a scope:
  - IP Range: `172.16.0.100` to `172.16.0.200`  
  - Subnet: `255.255.255.0`  
  - Gateway: `172.16.0.1`  
  - DNS Server: `172.16.0.1`  
- Activate the scope

### 8. Install and Configure NAT

- Add "Remote Access" > "Routing" role  
- Use the Routing and Remote Access console to enable NAT  
- Select the NAT interface as the public-facing (NAT) adapter

### 9. Create Organizational Units (OUs) and Users

- Open Active Directory Users and Computers  
- Create a new OU named `Admins`  
- Add a new user account to the `Admins` OU

### 10. Automate User Creation with PowerShell

- Download the PowerShell script and `names.txt` file  
- Run the script in PowerShell as Administrator:
  ```powershell
  .\1_CREATE_USERS.ps1
