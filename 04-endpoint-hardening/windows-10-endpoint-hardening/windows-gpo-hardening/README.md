# Windows GPO Hardening (CIS Benchmark for Windows 10)

## 1. CIS Portal Access
**Screenshot:** CIS-Security-Portal-Dashboard.png  
Shows the official CIS Benchmark source used for Windows 10 hardening.

---

## 2. Account Lockout Policies

### Baseline
**Screenshot:** Windows-Baseline-Account-Lockout-Policies.png

### Hardened (CIS Recommended)
**Screenshot:** CIS-Hardened-Account-Lockout-Policies.png

---

## 3. Password Policies

### Baseline
**Screenshot:** Windows-Default-Password-History-Policy.png

### Hardened (CIS Recommended)
**Screenshot:** CIS-Hardened-Password-Complexity-Policies.png

### Enforcement Test
**Screenshot:** Password-Policy-Enforcement-Validation-Test.png

---

## 4. Services Hardening
**Screenshot:** Windows-Services-Hardening-Disabling-Unused-Features.png

### Disabled Services
- Print Spooler — disabled due to the PrintNightmare (CVE‑2021‑34527) vulnerability  
- Xbox services — non‑enterprise, unnecessary services that increase attack surface

---

## 5. Apply Policies
**Screenshot:** PowerShell-Force-Group-Policy-Update.png

### Command Used


gpupdate /force


Applies all modified Group Policy settings immediately.

---

## Tools Used (Win+R Commands)
- **[gpedit.msc](ca://s?q=Explain_gpedit.msc)** — Local Group Policy Editor  
- **[secpol.msc](ca://s?q=Explain_secpol.msc)** — Local Security Policy  
- **[services.msc](ca://s?q=Explain_services.msc)** — Windows Services Manager  
- **[eventvwr.msc](ca://s?q=Explain_eventvwr.msc)** — Event Viewer

