# pfSense Setup — Network Protection Layer

This folder contains the pfSense configuration and firewall rule screenshots used in Phase 3 of the Network Protection Layer. These images document the core defensive controls implemented in the home SOC lab.

## Screenshots

### 1. pfSense Console Network Status
**File:** pfsense-console-network-status.png  
Shows the pfSense system console with WAN/LAN interface assignments and network status.  
This confirms the firewall is correctly configured as the central gateway for all VMs.

### 2. LAN Firewall Rules (with pfBlockerNG Auto Rule)
**File:** pfsense-lan-rules-with-pfblockerng-auto-rule.png  
Displays LAN-side firewall rules, including pfBlockerNG auto-generated rules.  
These rules enforce internal segmentation and apply reputation-based filtering.

### 3. WAN Rules — Malicious / Private IP Region Blocking
**File:** pfsense-wan-rules-malicious-private-ip-region.png  
Shows WAN-side rules blocking:
- Known malicious IP ranges  
- Unauthorized private IP ranges  
- Geo-blocked regions  
This strengthens perimeter defense and reduces attack surface.

### 4. WAN Firewall Rules Overview
**File:** wan-firewall-rules.png  
Provides a full view of WAN firewall rules applied to inbound and outbound traffic.  
These rules ensure only legitimate traffic reaches the internal network.

## Purpose
These screenshots demonstrate:
- Proper pfSense deployment  
- Firewall rule design  
- Geo-blocking and IP reputation filtering  
- Network segmentation  
- Integration with Suricata IPS and pfBlockerNG  

They validate the ability to configure and manage enterprise-grade defensive controls in a home SOC lab environment.

