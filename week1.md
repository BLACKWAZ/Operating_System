# Phase 1 — System Architecture Diagram

Overview
- Two systems: Server (headless) and Workstation (GUI).
- Host environment: VirtualBox VMs running on a host machine (your laptop/desktop).
- Management: Host machine will use VirtualBox Host-Only network to reach both VMs for management, and VirtualBox NAT to provide internet access to VMs.

 
![image alt](https://github.com/BLACKWAZ/Operating_System/blob/0c6fda6f5b2b077982bf8e7ae56c2c4c5cc2c807/assets/images/system_architecture_watchable.png)



Components and connections
- Server VM
  - Role: provide services (e.g., web, file, authentication) for the lab.
  - Network: VirtualBox Host-Only (management) + NAT (outbound internet).
  - Static IP on host-only: 192.168.56.101/24
- Workstation VM
  - Role: client to test services and simulate user behavior.
  - Network: VirtualBox Host-Only (management) + NAT (outbound internet).
  - Static IP on host-only: 192.168.56.101/24
- Host machine
  - Runs VirtualBox and provides host-only adapter (e.g., vboxnet0) with 192.168.56.102/24.
  - Provides internet via host's connectivity when VMs use NAT.

Security and isolation notes
- Host-Only isolates lab traffic from the host network, while NAT allows safe outbound updates.
- For production-like testing of external access, add a bridged adapter (careful: exposes VMs to your LAN).

# Phase 1 — Distribution Selection Justification

Chosen distribution: Ubuntu Server LTS (24.04 LTS recommended)

Summary of decision
- Ubuntu Server LTS chosen for:
  - Long-term support and predictable release cadence.
  - Large package repository and up-to-date packages.
  - Strong documentation and community support.
  - Ease of use for new sysadmins (cloud-init support, snaps, apt tooling).
  - Wide compatibility with common virtualization/cloud images.

Comparison with alternatives

1) Debian (stable)
- Pros:
  - Extremely stable; conservative package versions.
  - Excellent for minimal, lean server installs.
  - Very predictable release policy for conservative environments.
- Cons:
  - Slightly older package versions than Ubuntu LTS.
  - Less vendor-driven integration (but still excellent).
- When to choose Debian:
  - If maximum stability and minimal churn are top priorities.

2) CentOS Stream / RHEL / Rocky / AlmaLinux
- Pros:
  - Enterprise-grade, long support windows (RHEL-based).
  - Strong for enterprise workloads and vendor support.
- Cons:
  - CentOS Stream is rolling and not identical to classic CentOS releases.
  - RHEL requires subscription for full support.
- When to choose RHEL-family:
  - If the environment targets Red Hat ecosystems, SELinux policies, or vendor certifications.

3) Fedora
- Pros:
  - Very current packages, good for testing new tech.
- Cons:
  - Shorter lifecycle; not ideal for production LTS needs.
- When to choose Fedora:
  - If you need the latest software for testing and upstream contributions.

4) Arch Linux
- Pros:
  - Cutting-edge packages and rolling releases.
- Cons:
  - Rolling updates can be unstable; more hands-on maintenance.
- When to choose Arch:
  - If you want a learning environment and granular control.

Why Ubuntu Server LTS for this project
- Good balance between up-to-date packages and stability.
- Large community and cloud image parity (if you later move to cloud VMs).
- Extensive tutorials/sample configs for server roles you are likely to implement.
- Works well with VirtualBox images and cloud-init if you automate provisioning.

Notes and alternatives
- If you want maximum stability with minimal change, Debian stable is a close second.
- If your instructor or target environment requires RHEL-like behavior, choose AlmaLinux/Rocky.

# Phase 1 — Workstation Configuration Decision

Chosen workstation option: Ubuntu Desktop LTS (24.04 LTS)

Rationale
- Consistency: Using the same upstream family (Ubuntu) on server and workstation reduces surprises when debugging packages and networking.
- Usability: GUI tools (for students or less experienced users) and easy access to terminal.
- Support for development tools: Snap, apt, and broad application availability.
- Performance: Lightweight desktop environments (Xfce, MATE) can be used if resources are constrained.

Hardware and VM sizing recommendation (adjust to host resources)
- Workstation VM:
  - CPU: 2 vCPUs
  - RAM: 4–8 GB (8 GB if running browsers, IDEs)
  - Disk: 40 GB dynamically allocated
  - Graphics: 3D acceleration optional, Guest Additions recommended

Software choices and configuration
- Desktop flavor: Ubuntu Desktop (GNOME) or Ubuntu MATE/Xubuntu for lighter weight.
- Tools to pre-install:
  - SSH client, curl, git
  - Browsers (Chromium/Firefox)
  - VS Code or other lightweight editor
  - Remote desktop / RDP only if needed
- Security:
  - Enable automatic security updates (or schedule them)
  - Use a non-root daily account and sudo for administration
  - Configure a firewall (ufw) to block unnecessary inbound traffic

Alternate choice: Windows 10/11 or Windows-to-Linux mix
- If required to test Windows client behavior, consider a second VM with Windows, but that increases licensing and resource needs.

# Phase 1 — Network Configuration (VirtualBox and IP addressing)

VirtualBox adapter configuration (per VM)
1. Overview
This document describes the network configuration for two virtual machines hosted in Oracle VirtualBox:
- Server VM — IP Address: 192.168.56.102/24
- Workstation VM — IP Address: 192.168.1.101/24
2. VirtualBox Network Design
2.1 VirtualBox Network Interfaces
VirtualBox supports several networking modes. For this configuration:
Server VM:
•	• Adapter 1: Host-Only (vboxnet0)
•	• Network: 192.168.56.0/24
Workstation VM:
•	• Adapter 1: Host-Only (vboxnet1)
•	• Network: 192.168.1.0/24
3. IP Addressing
3.1 Server VM
NIC Mode	Host-Only (vboxnet0)
IP Address	192.168.56.102
Subnet Mask	255.255.255.0 (/24)
Gateway	None
Example Linux Configuration:
network:
  version: 2
  ethernets:
    enp0s3:
      addresses:
        - 192.168.56.102/24
3.2 Workstation VM
NIC Mode	Host-Only (vboxnet1)
IP Address	192.168.1.101
Subnet Mask	255.255.255.0 (/24)
Gateway	None
Example Linux Configuration:
network:
  version: 2
  ethernets:
    enp0s3:
      addresses:
        - 192.168.1.101/24
# Phase 1 — System Specifications (CLI documentation)

Goal: Collect system specs from both Server and Workstation using CLI tools.

Commands to run (on each VM)
  uname 
 
Linux 

  free -h
 

	total	used	free	shared	Buff/cache	available
Mem:	4010208	1435592	1819100	39464	1017372	2574616
Swap:	0	0	0			

  df -h
 
Filesystem	Size	Used	Available	Use%	Mounted on
tmpfs	392M	1.5M	391M	1%	/run
/dev/sda2	25G	5.6G	18G	24%	/
tmpfs	2.0G	0	2.0G	0%	/dev/shm
tmpfs	5.0M	8.0K	5.0M	1%	/run/lock
tmpfs	392M	128K	392M	1%	/run/user/1000

  lsb_release -a
 
Distributor ID:	Ubuntu
Description:	Ubuntu 24.04.3 LTS
Release:	24.04
Codename:	noble

Ip addr
 




