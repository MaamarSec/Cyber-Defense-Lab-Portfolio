
# pfBlockerNG — GeoIP & IP Reputation Blocking

This folder contains pfBlockerNG configuration screenshots used in Phase 3 of the Network Protection Layer. These images document the country‑level blocking and IP reputation filtering configured in the home SOC lab.

## Screenshots

### 1. Installed Packages — pfBlockerNG
Shows pfBlockerNG installed and active on pfSense.  
Confirms the package is configured and ready for GeoIP/IP reputation filtering.

### 2. IPv4 Summary — GeoIP & Reputation Lists  
**File:** pfblockerng-ipv4-summary.png  
Displays the active IPv4 lists, including:  
- **PRI1** — reputation-based IP list (deny outbound)  
- **Block_countries** — GeoIP blocklist (deny both)  

This confirms pfBlockerNG is enforcing both country-level and reputation-based filtering.

### 3. GeoIP Country Block Configuration (upload your screenshot here)
Shows China (CN), North Korea (KP), and Russia (RU) added to the blocklist.  
This demonstrates geographic filtering of high‑risk regions.

### 4. Auto‑Generated Firewall Rule (if available)
Shows the pfBlockerNG rule created on the WAN interface to enforce GeoIP blocking.

## Purpose
These screenshots demonstrate:

- Country‑level GeoIP blocking  
- IP reputation filtering  
- Automatic firewall rule generation  
- Integration with pfSense WAN filtering  

This validates the ability to configure pfBlockerNG as part of a defensive network stack in a home SOC lab.
