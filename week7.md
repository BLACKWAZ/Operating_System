# System Security and Hardening Report - Week 7

## 1. System Hardening via Lynis Security Audit

### Prerequisite Software Installation

The following command is used to install the necessary security tools, Lynis for auditing and Nmap for network scanning:

```bash
sudo apt install lynis nmap -y 
# Installs the Lynis auditing tool and the Nmap network scanner.
```

### Software Version Confirmation

To confirm the successful installation and check the versions of the utilities:

``` bash 
nmap --version 
lynis --version
```

### Initiating the System Audit with Lynis

The system-wide security audit is executed using the Lynis utility with the following command:

``` bash 
sudo lynis audit system 

# Elevated privileges (sudo) are required to perform a comprehensive system scan.
```

### Audit Execution Progress

![](/week7_images/auditing.png)

NOTE: The security assessment process may take several minutes to complete.

### Initial Audit Score

The system's security posture, as measured by the initial Lynis score before any changes were applied:

![](/week7_images/audit_score.png)

### Security Warnings and Remediation Steps

The audit identified several areas for improvement, with corresponding solutions implemented:

**Suggestion 1: Package Bug Reporting**

![](/week7_images/suggestion(1).png)

**Solution:** Install `apt-listbugs` to proactively check for critical bugs in packages before installation or upgrade.

``` bash 
sudo apt update
sudo apt install apt-listbugs

# This utility automatically runs during 'apt upgrade' or 'apt install' to display serious bug reports.
# Manual check can be performed with: apt-listbugs list package-name
```

**Suggestion 2: Reviewing Package Changelogs**

![](/week7_images/suggestion(2).png)

**Solution:** Install `apt-listchanges` to review important upstream changelogs for packages.

``` bash 
sudo apt install apt-listchanges

# Automatically displays significant changes in packages during the upgrade/installation process.
```

**Suggestion 3: SSH Configuration Hardening**

![](/week7_images/suggestion(ssh).png)

### Implemented SSH Hardening Measures

Based on the audit's recommendations, the SSH daemon configuration was modified to enhance security:

```
AllowTcpForwarding no
ClientAliveInterval 300
ClientAliveCountMax 2
LogLevel VERBOSE
MaxAuthTries 3
MaxSessions 2
TCPKeepAlive no
X11Forwarding no
AllowAgentForwarding no
```

**Description:** This configuration set was applied to mitigate various risks. Disabling `AllowTcpForwarding` and `AllowAgentForwarding` prevents SSH tunneling and credential forwarding abuse. Setting `ClientAliveInterval` and `ClientAliveCountMax` ensures that inactive sessions are automatically terminated. `LogLevel VERBOSE` facilitates detailed logging for auditing purposes. Limits on `MaxAuthTries` and `MaxSessions` reduce the risk of brute-force attacks and resource exhaustion. Finally, disabling `TCPKeepAlive` and `X11Forwarding` further reduces the attack surface.

**Suggestion 4: Malware and Rootkit Detection**

![](/week7_images/suggestion(malware).png)

**Solution:** Deploy a rootkit and malware detection tool, and configure it for automated execution.

``` bash
sudo apt install rkhunter
sudo rkhunter --update
sudo rkhunter --propupd

# Installs and initializes the Rootkit Hunter (rkhunter) tool.
```

**Automating Scans:** A daily cron job can be configured to ensure regular, automated scanning. This is achieved by editing the default configuration file:

``` bash 
sudo nano /etc/default/rkhunter

# The following lines should be modified within the file:

CRON_DAILY_RUN="yes"
CRON_DB_UPDATE="yes"
```

### Final Audit Score

The security score after implementing the recommended changes and hardening the system:

![](/week7_images/after_audit.png)

## 2. Network Security Verification

### Firewall Configuration

The current firewall rules in place:

![](/week7_images/firewallrule.png)

### Nmap Port Scan Results

The output from the Nmap scan confirms the active network services:

![](/week7_images/nmap(2).png)

**Observation:** Port 2424 is open for remote SSH access. This is a deliberate configuration, as the default SSH port (22) was changed to 2424 during the hardening phase, and the firewall rules were updated accordingly to permit connections on this new port.

### Active Service Inventory and Justification

A summary of the services listening on the network interfaces:

| Service | Port/Protocol | Listening Interface | Purpose and Operational Status |
| :--- | :--- | :--- | :--- |
| **systemd-resolve** | 53 (TCP/UDP) | Localhost | **Core Function:** Local DNS resolution service required for system operations. Securely bound to the loopback interface. |
| **systemd-network** | 68 (UDP) | Internal IP | **Networking:** DHCP client responsible for obtaining and maintaining the system's IP address. |
| **sshd** | 2424 (TCP) | All Interfaces | **Remote Access:** Provides secure shell access for administration. **Security Note:** Port changed from default 22 to 2424 to deter automated scanning. |
| **apache2** | 80 (TCP) | All Interfaces | **Main Application:** The web server hosting the primary required web application. |
| **iperf3** | 5201 (TCP) | All Interfaces | **Testing Utility:** Currently active for network performance benchmarking. *Recommendation: It is advised to disable this service once testing is complete to minimize the attack surface.* |

## 3. Operational Challenges Encountered

### System Instability and Crashes

The system experienced multiple unexpected crashes and boot failures during the week.

**Resolution:** The issue was resolved by adjusting the virtual machine's resource allocation, specifically by modifying the number of allocated CPU cores (e.g., changing from 8 to 4) or reallocating a greater amount of RAM.

### Network Interface Failure

The primary network interface, identified as `enp03s`, became completely unresponsive, preventing all network connectivity (e.g., pinging). Attempts to manually bring the interface up using `sudo ip link set enp03s up` were unsuccessful. After extensive troubleshooting, including multiple reboots, the solution involved changing the network adapter type and reapplying the existing network settings:

![](/week7_images/networkproblem.png)

Following this change, a new IP address was assigned, which necessitated updating the firewall rules and SSH configuration to allow remote access on the new IP.


