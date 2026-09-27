# NETWORKWALKS-B083-WEEK1-PM1-CYBERSECURITY-LAB-SETUP
This is my cybersecurity Lab setup
<div align="center">

# 🔐 Cybersecurity Lab Environment Setup

**Building an isolated virtual lab for penetration testing and ethical hacking practice**
</div>


<p align="center">
  <img src="https://img.shields.io/badge/Skill-Cybersecurity-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/Ver-Virtualbox%20v7.2-0070C0?style=flat-square&labelColor=000000" />
  <img src="https://img.shields.io/badge/Kali%20Linux-v2026.2-E87500?style=flat-square&labelColor=000000&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/Skill-Linux-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/Network-10.0.0.0%2F24-238F89?style=flat-square&labelColor=000000" />
  <img src="https://img.shields.io/badge/Penetration%20Testing-C00000?style=flat-square&labelColor=000000&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/Skill-Virtualization-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/GitHub-404040?style=flat-square&labelColor=0070C0&logo=github&logoColor=white" />
  <img src="https://img.shields.io/badge/Kali%20Linux-404040?style=flat-square&labelColor=C00000&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/NetworkWalks-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/Ethical%20Hacking-E87500?style=flat-square&labelColor=000000&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/Aboderin%20Semilore%20Gold-C00000?style=flat-square" />
</p>
---

## 📌 Project Overview

This project documents the setup of a virtual cybersecurity lab using VirtualBox and Kali Linux. The lab provides a safe, self-contained environment where security tools, network scanning, and vulnerability testing can be carried out without any risk to real systems or networks.

The network is built on a private virtual subnet, which allows additional machines to be added later as targets for hands-on security practice.

---

## 🎯 Objectives

By the end of this setup, the lab should have:

1. A working VirtualBox installation acting as the hypervisor
2. A Kali Linux VM imported and running
3. A dedicated internal network (separate from the default NAT) that supports both internet access and future multi-VM communication
4. A Kali machine with a fixed IP instead of a DHCP-assigned one
5. Verified internet access and working DNS lookups
6. A saved snapshot marking this as a known-good starting point
7. Room to expand the lab with more VMs down the line for actual practice exercises

---

## 🛡️ Purpose of the Lab

Security tools and techniques need somewhere safe to be tested — not on a live network, and never against systems that aren't yours. This lab exists to solve that problem: everything runs inside a virtual machine, cut off from the host network, so tools can be run, scans can be launched, and mistakes can be made without any real-world consequences.

Down the line, this same environment can host additional vulnerable machines to scan and exploit as practice targets — things like:

- Scanning a network to see what's on it
- Identifying open ports and running services
- Looking for known vulnerabilities
- Inspecting network traffic
- Practicing exploitation in a safe, contained setting

**⚠️ Note:** Every tool and technique used in this lab is restricted to machines within the lab itself. Nothing here should ever be pointed at a system without clear, explicit permission.

---

## ⚙️ Lab Configuration

| Component | Configuration |
|---|---|
| Host OS | Windows 10 |
| Hypervisor | VirtualBox 7.2 |
| Guest OS | Kali Linux 2026.2 |
| Virtual Network | NAT Network |
| Network Address | 10.0.0.0/24 |
| Kali IP Address | 10.0.0.2/24 |
| Default Gateway | 10.0.0.1 |
| DNS Server | 8.8.8.8 |

---

## 🪜 Lab Setup Procedure

### Step 1: Install 7-Zip
7-Zip is used to extract the Kali Linux VM package, which is distributed as a compressed `.7z` file.

### Step 2: Install VirtualBox
VirtualBox is installed and used as the hypervisor for running the Kali Linux virtual machine.

### Step 3: Create a NAT Network
A dedicated NAT Network is created inside VirtualBox so the VM has internet access while also being able to communicate with other VMs added later.

**Configuration:**
- Network Name: `NatNetwork`
- IPv4 Prefix: `10.0.0.0/24`
- DHCP: Enabled

### Step 4: Import Kali Linux
The Kali Linux VM image is downloaded and imported into VirtualBox, with its network adapter attached to the NatNetwork created above.

### Step 5: Configure Kali's Network Settings
A static IP address is set on Kali's network connection so the machine has a consistent, predictable address every time it starts:

- IP Address: `10.0.0.2/24`
- Gateway: `10.0.0.1`
- DNS Server: `8.8.8.8`

### Step 6: Verify Connectivity
Connectivity and DNS resolution are confirmed by pinging the gateway and an external domain to ensure both internal routing and internet access are working correctly.

### Step 7: Take a Snapshot
A snapshot of the VM is taken once the setup is complete, providing a clean recovery point in case future changes cause issues.

---

## ✅ Outcome

The result is a fully functional Kali Linux VM on an isolated private network, with internet access and a fixed IP address, ready to be used for future cybersecurity practice and exercises.
