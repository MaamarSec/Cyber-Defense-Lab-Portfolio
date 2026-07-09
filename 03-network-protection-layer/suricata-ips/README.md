# Suricata IPS — Network Protection Layer

This folder contains Suricata IDS/IPS configuration, rule management, and detection/blocking screenshots used in Phase 3 of the Network Protection Layer. These images document Suricata running in Inline IPS mode, rule tuning, and real-world detection tests.

## Screenshots

### 1. Suricata Interface Status — Inline IPS Mode
Shows Suricata running on the LAN interface with:
- **Status:** Active  
- **Pattern Match:** AUTO  
- **Blocking Mode:** INLINE IPS  
This confirms Suricata is operating as a full IPS, not just IDS.

### 2. Suricata Logging & IPS Configuration
Displays key settings:
- Inline Mode enabled  
- Block Offenders enabled  
- HTTP/TLS inspection  
- File-store logging  
- EVE JSON output  
These settings ensure SOC-grade visibility and prevention.

### 3. Suricata Rule Categories (LAN)
Shows enabled rulesets including:
- Emerging Threats  
- Attack Response  
- Malware  
- Exploit  
- DNS  
- Policy  
- Suspicious Traffic  
This demonstrates proper rule tuning for detection and prevention.

### 4. Suricata Rule Text — SID 2100498
Shows the exact rule triggered during testing:
```
alert ip any any -> any any (msg:"GPL ATTACK_RESPONSE id check returned root";
content:"uid=0|28|root|29|"; classtype:bad-unknown; sid:2100498; rev:7;)
```
This rule detects suspicious “id check returned root” responses.

### 5. IDS Test — Alert Mode
Triggered by:
```bash
curl testmynids.org/uid/index.html
```
Suricata generated the alert:
> GPL ATTACK_RESPONSE id check returned root  
Screenshot shows the alert in **yellow (ALERT)**.

### 6. IPS Test — Block Mode
After switching the rule from **ALERT → DROP**, Suricata blocked the same traffic.  
Screenshot shows:
- **Red BLOCK icon**  
- Same SID (2100498)  
- No output from curl  
This confirms Suricata is successfully blocking malicious traffic inline.

### 7. Suricata Alerts Log (Last 250 Entries)
Shows multiple alerts and blocks, including:
- Source IP  
- Destination IP  
- Ports  
- Priority  
- Rule SID  
- Classification  
This demonstrates active monitoring and prevention.

### 8. Suricata Rule Updates
Shows Suricata downloading and updating rule sets.  
This ensures the IPS stays current with new threats.

### 9. Suricata Ruleset Download Settings
Displays configuration for:
- Emerging Threats Open  
- Snort Community Rules  
- Feodo Tracker  
- ABUSE.ch SSL Blacklist  
This shows proper ruleset management.

## Purpose
These screenshots demonstrate:

- Inline IPS configuration  
- Real detection and blocking tests  
- Rule tuning and category management  
- SOC-grade logging and visibility  
- Integration with pfSense firewall  
- Continuous rule updates  

This validates the ability to deploy, configure, tune, and test Suricata as an enterprise-grade IDS/IPS in a home SOC lab.

