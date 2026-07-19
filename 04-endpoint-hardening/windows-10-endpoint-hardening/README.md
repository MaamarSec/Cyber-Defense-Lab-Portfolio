# Lab 4 — Windows 10 Endpoint Hardening (CIS Benchmark + Sysmon + Audit Policies)

This lab transforms a default Windows 10 virtual machine into a CIS‑aligned, hardened, and fully monitored enterprise endpoint. It includes password policy enforcement, account lockout protection, UAC hardening, service attack‑surface reduction, Sysmon deployment, and advanced audit logging. This prepares the endpoint for SIEM ingestion in Lab 5 (Linux Endpoint Hardening).

---

## 1. CIS Benchmark & Security Framework

**Screenshot:** `CIS-Security-Portal-Dashboard.png`  
Accessed the official CIS Portal to download the Windows 10 Enterprise Benchmark and follow industry‑standard hardening guidelines.

---

## 2. Password Policy Hardening

### Baseline  
**Screenshot:** `Windows-Default-Password-History-Policy.png`  
Default configuration allowed weak password history (0 remembered).

### Hardened (CIS‑Aligned)  
**Screenshot:** `CIS-Hardened-Password-Complexity-Policies.png`  
Applied CIS Benchmark recommendations:
- Minimum length: **14 characters**
- Password history: **24 remembered**
- Complexity: **Enabled**

### Enforcement Test  
**Screenshot:** `Password-Policy-Enforcement-Validation-Test.png`  
Attempting a weak password triggers a Windows error — confirming policy enforcement.

---

## 3. Account Lockout Policies

### Baseline  
**Screenshot:** `Windows-Baseline-Account-Lockout-Policies.png`

### Hardened  
**Screenshot:** `CIS-Hardened-Account-Lockout-Policies.png`  
Applied CIS recommendations:
- Lockout threshold: **5 attempts**
- Lockout duration: **15 minutes**
- Reset counter: **15 minutes**
- Administrator lockout: **Enabled**

Tested by simulating failed logins → Event ID **4740** generated.

---

## 4. User Account Control (UAC) Hardening

Configured UAC to enforce secure desktop prompts and prevent silent privilege escalation.

Path:  
`Local Policies → Security Options`

---

## 5. Services Hardening

**Screenshot:** `Windows-Services-Hardening-Disabling-Unused-Features.png`  
Disabled unnecessary or risky services to reduce attack surface:
- **Print Spooler** (PrintNightmare vulnerability)
- **Xbox services** (non‑enterprise, resource‑consuming)

---

## 6. Apply Policies Immediately

**Screenshot:** `PowerShell-Force-Group-Policy-Update.png`  
Used PowerShell to apply all GPO changes instantly:

```
gpupdate /force
```

---

## 7. Sysmon Deployment (Advanced Endpoint Telemetry)

Sysmon provides high‑fidelity forensic logging beyond default Windows logs.

### Sysmon Installation  
**Screenshot:** `Sysmon-Install-Command.png`  
Installed using SwiftOnSecurity community configuration:

```
Sysmon64.exe -accepteula -i sysmonconfig-export.xml
```

### Sysmon Service Status  
**Screenshot:** `Sysmon-Service-Running.png`

### Sysmon Operational Log  
**Screenshot:** `Sysmon-Operational-Log.png`  
Verified process creation and network events (e.g., `ping 8.8.8.8`).

### Log Configuration  
**Screenshot:** `Sysmon-Log-Properties.png`  
Configured:
- Large log size  
- Archive logs when full  

Sysmon provides:
- Process creation  
- Network connections  
- Registry changes  
- File creation time changes  
- DLL/driver loading  

---

## 8. Advanced Audit Policies (CIS Benchmark)

### User Account Management  
**Screenshot:** `Audit-Policy-User-Account-Management.png`  
Enabled Success + Failure auditing.

### Credential Validation  
**Screenshot:** `Audit-Policy-Credential-Validation.png`  
Enabled Success + Failure auditing.

These logs are essential for SIEM ingestion in Lab 5.

---

## 9. Tools Used (Win+R Commands)

Administrative tools used throughout the hardening process:

- `gpedit.msc` — Group Policy Editor  
- `secpol.msc` — Local Security Policy  
- `services.msc` — Services Hardening  
- `eventvwr.msc` — Event Viewer  

---

## Outcome

This Windows 10 endpoint is now:

- CIS Benchmark hardened  
- Protected against brute‑force attacks  
- Enforcing strong password policies  
- Logging advanced security events  
- Running Sysmon for forensic visibility  
- Reduced attack surface through service hardening  
- Ready for SIEM ingestion in Lab 5  



