🔐 Cybersecurity Lab Environment Setup
Building an isolated virtual lab for penetration testing and ethical hacking practice

![Skill](https://img.shields.io/badge/Skill-Cybersecurity-red) ![Ver](https://img.shields.io/badge/Ver-Virtualbox%20v7.2-blue) ![Kali Linux](https://img.shields.io/badge/Kali%20Linux-v2026.2-red) ![Skill](https://img.shields.io/badge/Skill-Linux-red) ![Network](https://img.shields.io/badge/Network-10.0.0.0%2F24-teal) ![Penetration Testing](https://img.shields.io/badge/Penetration%20Testing-red) ![Skill](https://img.shields.io/badge/Skill-Virtualization-red) ![GitHub](https://img.shields.io/badge/GitHub-black?logo=github) ![Kali Linux](https://img.shields.io/badge/Kali%20Linux-red?logo=kalilinux) ![NetworkWalks](https://img.shields.io/badge/NetworkWalks-red) ![Ethical Hacking](https://img.shields.io/badge/Ethical%20Hacking-orange) ![Author](https://img.shields.io/badge/Aboderin%20Semilore%20Gold-red)

---

📌 Project Overview
This project documents the setup of a virtual cybersecurity lab using VirtualBox and Kali Linux. The lab provides a safe, self-contained environment where security tools, network scanning, and vulnerability testing can be carried out without any risk to real systems or networks.

The network is built on a private virtual subnet, which allows additional machines to be added later as targets for hands-on security practice.

🎯 Objectives
By the end of this setup, the lab should have:

- A working VirtualBox installation acting as the hypervisor
- A Kali Linux VM imported and running
- A dedicated internal network (separate from the default NAT) that supports both internet access and future multi-VM communication
- A Kali machine with a fixed IP instead of a DHCP-assigned one
- Verified internet access and working DNS lookups
- Shared clipboard, drag-and-drop, and a shared folder enabled between host and Kali
- A saved snapshot marking this as a known-good starting point
- Room to expand the lab with more VMs down the line for actual practice exercises

🛡️ Purpose of the Lab
Security tools and techniques need somewhere safe to be tested — not on a live network, and never against systems that aren't yours. This lab exists to solve that problem: everything runs inside a virtual machine, cut off from the host network, so tools can be run, scans can be launched, and mistakes can be made without any real-world consequences.

Down the line, this same environment can host additional vulnerable machines to scan and exploit as practice targets — things like:

- Scanning a network to see what's on it
- Identifying open ports and running services
- Looking for known vulnerabilities
- Inspecting network traffic
- Practicing exploitation in a safe, contained setting

⚠️ Note: Every tool and technique used in this lab is restricted to machines within the lab itself. Nothing here should ever be pointed at a system without clear, explicit permission.

⚙️ Lab Configuration
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
| Shared Folder | Downloads (host) ↔ /media/sf_Downloads (Kali) |
| Clipboard / Drag & Drop | Bidirectional |

🪜 Lab Setup Procedure

**Step 1: Install 7-Zip**
7-Zip is used to extract the Kali Linux VM package, which is distributed as a compressed .7z file.

**Step 2: Install VirtualBox**
VirtualBox is installed and used as the hypervisor for running the Kali Linux virtual machine.

**Step 3: Create a NAT Network**
A dedicated NAT Network is created inside VirtualBox so the VM has internet access while also being able to communicate with other VMs added later.

Configuration:
- Network Name: NatNetwork
- IPv4 Prefix: 10.0.0.0/24
- DHCP: Enabled

**Step 4: Import Kali Linux**
The Kali Linux VM image is downloaded and imported into VirtualBox, with its network adapter attached to the NatNetwork created above.

**Step 5: Configure Kali's Network Settings**
A static IP address is set on Kali's network connection so the machine has a consistent, predictable address every time it starts:

- IP Address: 10.0.0.2/24
- Gateway: 10.0.0.1
- DNS Server: 8.8.8.8

**Step 6: Enable Shared Folder & Clipboard**
A shared folder was configured (host `Downloads` folder ↔ Kali `/media/sf_Downloads`) with Auto-mount and Make Permanent enabled, to move files easily between host and VM. Shared Clipboard and Drag'n'Drop were both set to Bidirectional for smoother workflow.

**Step 7: Verify Connectivity**
Connectivity and DNS resolution are confirmed by pinging the gateway and testing internet access.

**Step 8: Take a Snapshot**
A snapshot of the VM is taken once the setup is complete, providing a clean recovery point in case future changes cause issues.

🔎 Lab Verification
| Test | Command | Result |
|---|---|---|
| Check IP address | `ip a` | 10.0.0.2/24 confirmed on eth0 |
| Test gateway | `ping 10.0.0.1` | Successful replies, 0% packet loss |
| Test internet access | `curl -I https://google.com` | Valid HTTP response received |
| DNS resolution | `ping google.com` | Resolved to a valid IP address |
| Shared folder | `ls /media/sf_Downloads` | Host files listed correctly |

🐞 Problems Encountered & Solutions

**Problem 1: No connectivity despite correct static IP and gateway configuration**
Kali was configured with IP `10.0.0.2` and gateway `10.0.0.1`, but pinging the gateway returned "Destination Host Unreachable."

Cause: The VirtualBox NAT Network's IPv4 Prefix was actually set to `10.0.2.0/24` by default — a different subnet than the one Kali was configured for.

Fix: Changed the NAT Network's IPv4 Prefix to `10.0.0.0/24` in VirtualBox (File → Tools → Network → NAT Networks), then fully restarted the VM. Confirmed the fix with `ping 10.0.0.1`, which returned successful replies.

**Problem 2: `ping 8.8.8.8` and `ping google.com` showed 100% packet loss despite internet working**
Cause: ICMP (ping) traffic was being silently dropped somewhere upstream — a common occurrence and not an actual connectivity problem.

Fix: Verified real internet access using `curl -I https://google.com`, which returned a valid HTTP response, confirming DNS resolution and internet connectivity were both working correctly even though ping itself was blocked.

**Problem 3: Screenshot tool failed to save directly into the shared folder**
Cause: VirtualBox shared folders (vboxsf) don't fully support the "rename temp file" operation some save dialogs use, resulting in a "Text file busy" error.

Fix: Adopted a two-step workflow — save screenshots locally first (`~/Pictures`), then move them into the shared folder using `mv ~/Pictures/*.png /media/sf_Downloads/`.

💡 What I Learned
- The difference between a standard NAT adapter and a NAT Network, and why NAT Network is required for multi-VM lab communication
- How to configure static IP addressing, gateway, and DNS settings in Kali Linux
- That ping failing doesn't always mean no internet access — other tools like curl can confirm real connectivity
- How to set up and troubleshoot VirtualBox shared folders and bidirectional clipboard/drag-and-drop
- Why taking a clean VM snapshot before further work is essential for safe experimentation
- The importance of documenting problems and fixes clearly, not just the steps that worked

🔐 Security & Ethical Use
This laboratory is intended strictly for education purposes only. All tools and techniques are confined to machines within this lab and are never to be used against systems without explicit permission.

🔗 Tools & Resources
- 7-Zip: https://7-zip.org/download.html
- VirtualBox: https://virtualbox.org/wiki/Downloads
- Kali Linux: https://kali.org/get-kali

👤 Author
Aboderin Semilore Gold
Cybersecurity Intern, Batch B083

GitHub: https://github.com/phetisaboy

📌 Project Information
Program: Cybersecurity at Networkwalks | Week: 01 | Project: Cybersecurity & Pentesting Lab Setup | Repository: GitHub
