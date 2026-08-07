# Cyber-Defense-Lab-Portfolio

I'm building a hands-on Security Operations Center (SOC) home lab from scratch and documenting my progress as I learn defensive security across network monitoring, endpoint security, identity & access management, SIEM engineering, threat hunting, and cloud defense.

**Created by:** Maamar-Sec
**Status:** 🚧 In Progress
**Started:** April 2026

---

## 📊 Current Progress

| Folder | Topic | Status |
|---|---|---|
| `00-lab-foundation/` | Lab Foundation & Infrastructure Setup | ✅ Completed |
| `01-monitoring-infrastructure/` | Network Traffic Monitoring (TShark, Zeek, Suricata) | ✅ Completed |
| `02-threat-detection/` | Network Monitoring & Threat Detection | ✅ Completed |
| `03-network-protection-layer/` | Network Protection Layer (pfSense + Suricata IPS + pfBlockerNG) | ✅ Completed |
| `04-endpoint-hardening/` | Windows 10 Endpoint Hardening | ✅ Completed |
| `05-linux-server-hardening/` | Linux Server Hardening (UFW, Fail2Ban, auditd) | ✅ Completed |
| `06-active-directory-lab/` | Active Directory Domain Deployment & Administration | ✅ Completed |
| Upcoming | SIEM, Threat Intel, Threat Hunting, IR, Forensics, Cloud Security, Purple Team | 🔜 Planned |

---

## 🏗️ Lab Architecture

**Infrastructure Components**
- Defense Platform: Ubuntu Server 22.04
- Monitored Endpoints: Windows 10, Ubuntu Desktop
- Identity Infrastructure: Windows Server 2019 Active Directory Domain Controller
- Virtualization: VirtualBox
- Network Segmentation: NAT + Host-Only + Internal networks
- Firewall & IPS: pfSense + Suricata Inline IPS
- Threat Filtering: pfBlockerNG GeoIP + Reputation Lists

---

## 🎯 Skills Progress

### ✅ Completed
- Virtual lab infrastructure setup
- Basic network configuration and segmentation
- Suricata installation, configuration, IDS/IPS testing
- Network threat detection fundamentals
- pfSense firewall rule design
- pfBlockerNG Geo-blocking & IP reputation filtering
- Full VM routing through pfSense
- Windows 10 endpoint hardening
- Linux server hardening (UFW, Fail2Ban, auditd, SSH hardening)
- Active Directory Domain Services deployment & forest promotion
- Domain-joining Windows endpoints and provisioning domain user accounts
- Kerberos/NTLM authentication verification via PowerShell and CLI tools

### 🔄 Currently Learning
- SIEM ingestion pipeline design (logs → ELK/Wazuh)
- IDS/IPS tuning
- Network access control

### ⏳ Upcoming
- SIEM deployment (ELK Stack or Wazuh)
- Threat intelligence integration
- Threat hunting methodology
- Incident response workflows
- Forensics and log analysis
- Cloud security fundamentals
- Purple team testing inside the lab

---

## 📂 Portfolio Structure

**Active**
- `00-lab-foundation/` — Core VM and network foundation for the lab
- `01-monitoring-infrastructure/` — Network traffic monitoring with TShark, Zeek, Suricata
- `02-threat-detection/` — Threat detection rules and analysis
- `03-network-protection-layer/` — pfSense, Suricata IPS, pfBlockerNG
- `04-endpoint-hardening/` — Windows 10 endpoint hardening
- `05-linux-server-hardening/` — Linux server hardening (UFW, Fail2Ban, auditd)
- `06-active-directory-lab/` — Active Directory domain deployment, client integration, and authentication validation

**Planned**
- `07-siem-detections/`
- `08-threat-intelligence/`
- `09-threat-hunting/`
- `10-incident-response/`
- `11-forensics/`
- `12-edr-configurations/`
- `13-vulnerability-management/`
- `14-cloud-security/`
- `15-purple-team/`

---

## 🛠️ Technologies & Tools

**Currently Using**
- VirtualBox, Ubuntu Server 22.04, Windows 10, Windows Server 2019
- Wireshark, Zeek, Suricata, Nmap
- pfSense firewall, pfBlockerNG GeoIP filtering
- Active Directory Domain Services, DNS, Group Policy fundamentals

**Planned**
- ELK Stack, Wazuh
- Volatility, KAPE, OSQuery, MISP
- AWS logging & monitoring
- Atomic Red Team

---

## 📈 Goals

By the end of this project, I aim to have:
- A complete SOC-style home lab
- 20–30 custom detection rules
- A working SIEM with dashboards
- Hardened Windows & Linux endpoints
- A functioning Active Directory environment for identity-based detection scenarios
- Basic incident response playbooks
- Documented investigations and lab reports

**Career Target:** Entry-Level SOC Analyst / Junior Security Engineer

---

## 📺 Learning Sources

This portfolio is based on:
- The Cyber Defense Mastery series by TechSky
- Additional blogs, documentation, and labs I explore independently

---

## ⚖️ Legal & Ethics

All security activities are carried out strictly within controlled lab environments on systems that I own. This project is dedicated solely to ethical and defensive cybersecurity practices.
