# 00‑Lab‑Foundation — Notes

## 1. Purpose of the Lab Foundation

This phase builds the core environment required for all future SOC, detection engineering, and threat‑hunting work.  
The goal is to create a stable, isolated, and well‑documented virtual network that simulates a small enterprise.

Key objectives:

- Create and configure all virtual machines  
- Establish proper network segmentation  
- Verify connectivity between endpoints  
- Prepare the monitoring server for future tools (Zeek, Suricata, ELK, Wazuh, etc.)

(See screenshot: screenshots/01-vbox-vm-list.png)

---

## 2. Virtual Machines Created

### **Ubuntu Server 22.04 — Monitoring Server**
Used later for:
- Zeek  
- Suricata  
- Log collection  
- Packet capture  

Network adapters:
- NAT  
- Host‑Only  
- Internal Network  

(See screenshot: screenshots/02-ubuntu-server-system-info.png)

---

### **Windows 10 Endpoint**
Represents a typical corporate workstation.

Used for:
- Traffic generation  
- Sysmon (later)  
- Malware testing (later)

---

### **Ubuntu Desktop**
Represents a Linux workstation.

Used for:
- Traffic generation  
- Linux endpoint monitoring (later)

---

## 3. Network Configuration

### **NAT Network**
- Provides internet access  
- Used for updates and package installation  

### **Host‑Only Network**
Used for administrative access:
- SSH into Ubuntu Server  
- RDP into Windows  
- Host machine management  

Example range: 192.168.56.0/24

### **Internal Network**
Isolated network used for:
- Endpoint‑to‑endpoint communication  
- Attack simulation  
- Packet capture  

Example range: 10.0.2.0/24

(See screenshot: screenshots/03-ubuntu-server-ip.png)

---

## 4. IP Addressing

All IPs below are private, non‑routable lab addresses.

### **Windows 10**
- Host‑Only: 192.168.56.103  
- NAT: 10.0.2.15  

### **Ubuntu Desktop**
- Host‑Only: 192.168.56.102  
- NAT: 10.0.2.15  

### **Ubuntu Server**
- Host‑Only: 192.168.56.101  
- NAT: 10.0.2.15  

### **Host Machine**
- Host‑Only: 192.168.56.1  

---

## 5. Connectivity Tests

### **Ubuntu Server → Windows 10**
Initial ping failed due to Windows Firewall blocking ICMP.  
After enabling ICMP rules, ping succeeded.

(See screenshot: screenshots/05-ubuntu-to-windows10-ping.png)

---

### **Ubuntu Server → Host Machine**
Ping successful.

(See screenshot: screenshots/04-ubuntu-to-host-ping.png)

---

### **Windows → Ubuntu Server (SSH)**
SSH successful via Host‑Only network.

Command: ssh user@192.168.56.101


(See screenshot: screenshots/06-windows-to-ubuntu-ssh.png)

---

### **Internet Connectivity**
- Ubuntu: `ping google.com`  
- Windows: Browser test  

---

## 6. Issues Encountered & Fixes

### **Issue: Ubuntu Server could not ping Windows 10**
**Cause:**  
Windows Defender Firewall blocks ICMPv4 (ping) by default.

**Fix:**  
Enabled the following rules in  
Windows Defender Firewall → Advanced Settings:

- File and Printer Sharing (Echo Request – ICMPv4-In)  
- File and Printer Sharing (Echo Request – ICMPv4-Out)  

(See screenshots: screenshots/07-windows-firewall-icmpv4-in.png, screenshots/08-windows-firewall-icmpv4-out.png)

---

### **Issue: No internet on Ubuntu Server**
**Fix:**  
Enabled NAT as the first network adapter.

---

### **Issue: SSH not available on Ubuntu Server**
**Fix:**  
Installed OpenSSH server:  sudo apt install openssh-server


---

## 7. Status

The lab foundation is complete.  
The environment is now ready for:

- Installing Zeek  
- Installing Suricata  
- Deploying Sysmon  
- Building detection pipelines  
- Packet capture and analysis  
- Threat‑hunting exercises  



