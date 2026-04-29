# Virtual Machine Specifications

This document lists the hardware and configuration settings for each virtual machine in the SOC home lab.  
These specifications ensure consistent performance and make the lab easy to rebuild or expand.

---

## 🖥️ Ubuntu Server 22.04 (Defense Platform)

**Purpose:**  
Runs Zeek, Suricata, Wazuh/ELK (future phases), and acts as the main monitoring/log collection server.

**Specs:**  
- CPU: 2 cores  
- RAM: 4–6 GB  
- Disk: 40–60 GB  
- Network Adapters:  
  - Adapter 1: NAT Network  
  - Adapter 2: Host‑Only  
  - Adapter 3: Internal Network  

---

## 🪟 Windows 10 Endpoint

**Purpose:**  
Used for Sysmon logging, malware simulation, and endpoint monitoring.

**Specs:**  
- CPU: 2 cores  
- RAM: 4 GB  
- Disk: 40 GB  
- Network Adapters:  
  - Adapter 1: NAT Network  
  - Adapter 2: Internal Network  

---

## 🐧 Ubuntu Desktop

**Purpose:**  
Secondary monitored endpoint for Linux audit logs and user activity simulation.

**Specs:**  
- CPU: 2 cores  
- RAM: 2–4 GB  
- Disk: 30–40 GB  
- Network Adapters:  
  - Adapter 1: NAT Network  
  - Adapter 2: Internal Network  

---

## 📌 Notes

- Specs may be adjusted depending on host machine performance.  
- Snapshots are recommended before major configuration changes.  
- All VMs are isolated from the host except through the Host‑Only network.  
