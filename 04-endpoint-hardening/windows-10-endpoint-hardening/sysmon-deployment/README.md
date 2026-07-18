# Sysmon Deployment (SwiftOnSecurity Config)

This section documents the deployment, configuration, and validation of Sysmon on the Windows 10 endpoint. Sysmon provides high‑fidelity telemetry essential for threat detection, incident response, and forensic analysis. The configuration used is the community‑maintained SwiftOnSecurity Sysmon config, optimized for detecting malicious behavior.

---

## 1. Sysmon Files

**Screenshot:** `Sysmon-Files-Directory.png`  
Shows the Sysmon executables and the imported SwiftOnSecurity configuration file (`sysmonconfig-export.xml`) located in the Downloads/Sysmon directory.

---

## 2. Installation

**Screenshot:** `Sysmon-Install-Command.png`  
Sysmon was installed using the following command:

```
Sysmon64.exe -accepteula -i sysmonconfig-export.xml
```

This command accepts the Sysmon EULA and installs Sysmon with the provided configuration file.

---

## 3. Sysmon Service Status

**Screenshot:** `Sysmon-Service-Running.png`  
Confirms that the Sysmon64 service is running and actively collecting telemetry.

---

## 4. Sysmon Operational Log

**Screenshot:** `Sysmon-Operational-Log.png`  
Displays the Sysmon Operational log under:

```
Event Viewer → Applications and Services Logs → Microsoft → Windows → Sysmon → Operational
```

This log contains detailed events such as process creation, network connections, registry modifications, and more.

---

## 5. Log Properties

**Screenshot:** `Sysmon-Log-Properties.png`  
Sysmon log settings were modified to support long‑term forensic retention:

- Increased maximum log size  
- Enabled log archiving when full  

---

## Sysmon Provides

Sysmon significantly enhances endpoint visibility by logging:

- **Process creation** (with full command line)  
- **Network connections**  
- **Registry changes**  
- **File creation time changes** (detects timestomping)  
- **DLL and driver loading**  
- **Named pipe events**  
- **WMI events**  

These logs are essential for threat hunting, detection engineering, and incident response.

