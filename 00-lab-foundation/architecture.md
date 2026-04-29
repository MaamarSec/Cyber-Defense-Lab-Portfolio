# SOC Home Lab Architecture

This document describes the core architecture of my Security Operations Center (SOC) home lab.  
The goal is to build a realistic defensive environment for learning network monitoring, endpoint security, SIEM engineering, detection engineering, and threat hunting.

---

## 🏗️ Virtualization Platform
**VirtualBox**  
All virtual machines run inside an isolated VirtualBox environment using multiple network segments.

---

## 🖥️ Virtual Machines

### 1. **Ubuntu Server 22.04 (Defense Platform)**
- Runs Zeek, Suricata, Wazuh/ELK (later phases)
- Acts as the main monitoring and log collection server

### 2. **Windows 10 Endpoint**
- Used for Sysmon logging, malware simulation, and endpoint monitoring

### 3. **Ubuntu Desktop**
- Secondary monitored endpoint
- Used for Linux audit logs and user activity simulation

---

## 🌐 Network Architecture

### **Networks Used**
- **NAT Network** — Internet access for updates  
- **Host‑Only Network** — Admin access from host machine  
- **Internal Network** — Isolated traffic for monitoring (Zeek/Suricata)

---

## 📡 High‑Level Diagram (ASCII)

                 [ Host Machine ]
                        |
                Host‑Only Network
                        |
        -----------------------------------------
        |                   |                   |
 [Ubuntu Server]     [Windows 10]       [Ubuntu Desktop]
     (Sensor)            (Client)             (Client)
        |                   |                   |
        ---------------- Internal Network ----------------

---

## 🎯 Purpose of This Architecture
- Simulate real enterprise traffic  
- Capture logs from multiple OS types  
- Build and test detection rules  
- Practice threat hunting techniques  
- Perform incident response case studies  
- Create a realistic SOC-style learning environment  

---

## 📌 Notes
This architecture will expand in later phases to include:
- Firewall (pfSense/OPNsense)
- SIEM dashboards
- Threat intelligence feeds
- Additional endpoints
- Purple team testing tools
