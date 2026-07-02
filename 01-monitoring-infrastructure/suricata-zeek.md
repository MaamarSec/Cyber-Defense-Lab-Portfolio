# Phase 01 – Network Monitoring (TShark, Zeek, Suricata)

This phase establishes full network visibility across the SOC lab using three complementary monitoring engines:

- **TShark** → Packet-level visibility  
- **Zeek** → Protocol-level intelligence  
- **Suricata** → Signature + behavioral threat detection  

Together, they provide complete monitoring coverage for all east-west traffic inside the VirtualBox host-only network.

---

## 1. TShark – Packet Capture Visibility

TShark is used to verify raw packet flow on the monitoring interface (`enp0s8`).

### Live Capture
`tshark -i enp0s8`

Shows:
- All packets entering the interface  
- Connectivity between Ubuntu Server, Ubuntu Desktop, and Windows 10  
- Baseline traffic (DNS, ICMP, TCP handshakes)

### DNS Capture
`tshark -i enp0s8 -f "port 53"`

Shows:
- DNS queries from Windows 10  
- mDNS / LLMNR traffic  
- Name resolution behavior inside the lab

TShark acts as the “microscope” of the SOC lab.

---

## 2. Zeek – Protocol Intelligence

Zeek converts raw packets into structured logs stored in:

`/opt/zeek/logs/current/`

### Key Logs

**conn.log**  
Tracks every connection (source, destination, ports, protocol, state).

**dns.log**  
Shows DNS queries and responses from internal hosts.

**weird.log**  
Captures anomalies such as malformed packets or unexpected protocol behavior.

**http.log**  
Shows HTTP requests, including curl and Python SimpleHTTPServer traffic.

Zeek acts as the “brain” of the monitoring stack.

---

## 3. Suricata – Threat Detection

Suricata provides signature-based and behavioral detection.

### Configuration Highlights
- AF_PACKET capture on `enp0s8`
- Emerging Threats Open rules
- Custom rules for:
  - Non-browser HTTP clients (curl)
  - Internal host scanning (Nmap)
  - SMB port access (ransomware behavior)

### Alert Output
Suricata logs alerts to:

`/var/log/suricata/fast.log`

Suricata acts as the “security guard” of the SOC lab.

---

## 4. Combined Visibility

By running TShark, Zeek, and Suricata together, the lab achieves:

- Packet visibility  
- Protocol visibility  
- Behavioral visibility  
- Threat visibility  

This forms a complete monitoring pipeline used in real SOC environments.


