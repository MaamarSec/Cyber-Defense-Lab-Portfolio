# Zeek Protocol Intelligence

Zeek converts raw packets into structured logs that provide deep visibility into network behavior.

---

## 1. Zeek Deployment

Zeek runs on Ubuntu Server and monitors interface `enp0s8`.  
It generates logs inside `/opt/zeek/logs/current/`.

---

## 2. Key Zeek Logs

### conn.log
Tracks every TCP/UDP/ICMP connection.
Shows:
- Source/destination IP
- Ports
- Protocols
- Connection state

### dns.log
Shows DNS queries from Windows 10 and Ubuntu Desktop.
Useful for:
- Detecting suspicious domains
- Monitoring internal name resolution

### weird.log
Shows anomalies such as:
- Malformed packets
- Unexpected protocol behavior
- Suspicious traffic patterns

### http.log
Shows HTTP requests, including curl and Python SimpleHTTPServer traffic.

---

## 3. Why Zeek Matters

Zeek provides:
- Behavioral visibility
- Protocol-level intelligence
- High-fidelity logs for SOC analysis
