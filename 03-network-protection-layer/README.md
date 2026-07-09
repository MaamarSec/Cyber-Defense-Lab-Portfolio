# Phase 3 — Network Protection Layer (pfSense + Suricata IPS + pfBlockerNG)

## Overview
This phase implements a complete defensive network stack using pfSense, Suricata IPS, and pfBlockerNG.  
All virtual machines (Ubuntu Server, Ubuntu Desktop, Windows 10) route through the pfSense firewall, enabling full inspection, detection, and prevention of malicious traffic.

## Components
- pfSense firewall with segmented WAN/LAN interfaces  
- Suricata IPS operating in Inline Mode (active blocking)  
- pfBlockerNG Geo-blocking and IP reputation filtering  
- Custom firewall rules blocking known malicious IP ranges  
- Centralized gateway routing for all VMs through pfSense  

## Skills Demonstrated
- **[IDS vs IPS](ca://s?q=Explain_IDS_vs_IPS)**  
- **[pfSense deployment](ca://s?q=Explain_pfSense_deployment)**  
- **[Suricata IPS configuration](ca://s?q=Explain_Suricata_IPS)**  
- **[pfBlockerNG Geo-blocking](ca://s?q=Explain_pfBlockerNG_GeoBlocking)**  
- **[Firewall rule design](ca://s?q=Explain_firewall_rule_design)**  
- **[Routing VMs through pfSense](ca://s?q=Explain_VM_routing_through_pfSense)**  
- **[Testing IPS blocking](ca://s?q=Explain_IPS_blocking_test)**  

## Key Results

### Suricata Detection (IDS Mode)
Running:
```bash
curl testmynids.org/uid/index.html
```
triggered the alert:
> **GPL ATTACK_RESPONSE id check returned root**

This confirmed Suricata was inspecting and detecting suspicious LAN traffic.

### Suricata Prevention (IPS Mode)
After switching the rule action from **ALERT → DROP**, the same test returned **no output**.  
Suricata blocked the connection inline, demonstrating successful IPS functionality.

### pfBlockerNG Geo-Blocking
Country-level blocks were applied successfully, dropping traffic originating from restricted regions.

### Malicious IP Firewall Rules
Custom WAN rules blocked known malicious IP ranges, strengthening perimeter defense.

## Folder Structure
```text
03-network-protection-layer/
    pfsense-setup/
    suricata-ips/
    pfblockerng/
    screenshots/
```

## Conclusion
This phase demonstrates a fully functional SOC-grade network protection layer:

- **Detection (IDS)**  
- **Prevention (IPS)**  
- **Geo-blocking**  
- **Malicious IP filtering**  
- **Full VM routing through pfSense**

It validates the ability to deploy, configure, tune, and test enterprise-level defensive technologies within a home SOC lab environment.
