# TShark Analysis – Packet-Level Visibility

TShark provides raw packet capture visibility inside the SOC lab.  
It is used to validate network connectivity, inspect traffic, and confirm that Zeek and Suricata are receiving packets correctly.

---

## 1. Live Packet Capture

Command:
`tshark -i enp0s8`

This shows:
- All packets entering the monitoring interface  
- Traffic between Ubuntu Server, Ubuntu Desktop, and Windows 10  
- Baseline activity such as DNS, ICMP, TCP SYN/ACK handshakes  

This confirms the host-only network is functioning and monitored.

---

## 2. DNS Traffic Capture

Command:
`tshark -i enp0s8 -f "port 53"`

This captures:
- DNS queries from Windows 10  
- mDNS / LLMNR traffic  
- Internal name resolution behavior  

This validates Zeek’s `dns.log` accuracy.

---

## 3. Why TShark Matters in SOC Monitoring

TShark acts as the **microscope** of the SOC lab:

- Shows raw packets before any processing  
- Helps troubleshoot connectivity issues  
- Confirms Zeek and Suricata see the same traffic  
- Provides packet-level evidence for analysis  

TShark is the foundation of Phase 01 network visibility.
