# Splunk SIEM Deployment

Splunk Enterprise is one of the most widely used SIEM platforms in the SOC/security analyst job market, making it a core skill for identity- and log-based threat detection. This lab documents the deployment of a dedicated Splunk Enterprise instance to serve as the central log aggregation and search platform for the rest of the home lab — including the pfSense/Suricata network layer and the Active Directory environment built in `06-active-directory-lab`.

This project covers VM provisioning, static network configuration (including a real cloud-init persistence issue encountered and resolved), Splunk Enterprise installation, firewall configuration, and initial access validation.

---

## Technical Overview & Prerequisites

* **Host VM:** `Splunk-SIEM` — Ubuntu Server 22.04 (cloned from the existing `Ubuntu-Server` base image)
* **Static IP Address:** `192.168.56.15` (deliberately placed outside pfSense's DHCP pool of `192.168.56.100`–`192.168.56.200`)
* **Gateway:** `192.168.56.254` (pfSense)
* **DNS:** `192.168.56.10` (DC01) with `8.8.8.8` as fallback
* **Splunk Version:** Splunk Enterprise 10.4.3 (Linux .deb package)
* **Web Interface Port:** `8000/tcp`

---

## Deployment Lifecycle

1. **VM Provisioning:** Clone the existing Ubuntu-Server VM to create a dedicated Splunk host, avoiding a full OS reinstall.
2. **Network Configuration:** Assign a static IP outside the DHCP pool, and resolve a cloud-init persistence issue that silently reverted the config on reboot.
3. **Splunk Installation:** Transfer and install the Splunk Enterprise `.deb` package, then start the service and create the admin account.
4. **Firewall Configuration:** Open the Splunk Web port through UFW, which was blocking external access by default.
5. **Validation:** Confirm Splunk Web is reachable and the admin login works from the host machine.

---

## Step-by-Step Implementation

### Phase 1: VM Provisioning & Network Configuration

1. **Cloning:** Right-clicked the existing `Ubuntu-Server` VM in VirtualBox → **Clone** → selected **Current Machine State** and **Full Clone**, with **Generate new MAC addresses** enabled to avoid network conflicts with the original VM. Named the result `Splunk-SIEM`.

   ![Splunk-SIEM VM listed in VirtualBox Manager](screenshots/Splunk-SIEM_VM_in_VirtualBox_Manager.png)

2. **Hostname:** Set the hostname to `splunk-siem` via `hostnamectl` to distinguish it clearly from the original Ubuntu-Server box in logs and SSH sessions.

3. **Static IP Assignment:** Initially attempted a static IP via Netplan, but the address kept reverting to a DHCP-assigned `192.168.56.101` after reboot. Root cause: **cloud-init regenerates `/etc/netplan/50-cloud-init.yaml` on every boot**, silently overwriting manual edits to that file.

   **Fix applied:**
   - Disabled cloud-init's network management via `/etc/cloud/cloud.cfg.d/99-disable-network-config.cfg` (`network: {config: disabled}`)
   - Created a separate, higher-priority netplan file (`99-static.yaml`) that cloud-init does not touch
   - Removed the conflicting `50-cloud-init.yaml`

   The final static configuration:
   ```yaml
   network:
     version: 2
     ethernets:
       enp0s8:
         dhcp4: no
         addresses:
           - 192.168.56.15/24
         routes:
           - to: default
             via: 192.168.56.254
         nameservers:
           addresses:
             - 192.168.56.10
             - 8.8.8.8
   ```

   ![Static IP 192.168.56.15 confirmed via ip a, surviving a full reboot](screenshots/static-ip-verification-192.168.56.15.png)

---

### Phase 2: Splunk Enterprise Installation

1. Downloaded the Splunk Enterprise 10.4.3 Linux `.deb` package and transferred it to the VM via `scp` over the established SSH connection.
2. Installed the package with `dpkg -i`.
3. Reassigned ownership of `/opt/splunk` to a non-root user, since running Splunk as root is deprecated.
4. Started Splunk with `splunk start --accept-license`, creating the initial `admin` account.
5. Enabled Splunk to auto-start on boot with `splunk enable boot-start`.

---

### Phase 3: Firewall Configuration

By default, `ufw` on the VM only allowed inbound SSH (port 22), which silently blocked all browser connection attempts to Splunk Web on port 8000 — Splunk itself was running correctly (`splunkd is running`, confirmed via `splunk status` and `ss -tlnp`), but the firewall was dropping the traffic before it reached the service.

**Fix applied:**
```bash
sudo ufw allow 8000/tcp
```

![UFW status showing port 8000/tcp now allowed for Splunk Web](screenshots/splunk_ufw_allow_port_8000.png)

---

## Validation & Verification

### 1. Splunk Web Accessibility

Confirmed the Splunk Web interface loads correctly from the host machine's browser at `http://192.168.56.15:8000`, following the firewall fix above.

![Splunk Web login page loading successfully](screenshots/splunk_web_login_page.png)

### 2. Admin Login & Dashboard Access

Logged in with the `admin` account created during installation, confirming full access to the Splunk home dashboard.

![Splunk home dashboard after logging in as admin](screenshots/splunk_home_dashboard.png)

---

## Troubleshooting Notes

This deployment surfaced a few real-world issues worth documenting explicitly, since they reflect practical SOC/sysadmin problem-solving rather than a clean happy-path install:

* **IP address conflict avoidance:** Verified pfSense's DHCP pool range (`192.168.56.100`–`.200`) via the pfSense web GUI before assigning a static IP, to avoid future lease collisions.
* **Cloud-init network persistence bug:** Diagnosed why a seemingly-correct static IP configuration reverted after reboot, and resolved it by disabling cloud-init's network config management rather than repeatedly re-applying a config that would keep getting overwritten.
* **Firewall silently blocking a working service:** Used `splunk status` and `ss -tlnp` to confirm Splunk itself was healthy before correctly isolating the problem to UFW, rather than assuming the installation had failed.

---

## SOC Analyst Takeaways

* **Centralized Log Aggregation:** This Splunk instance is now positioned to ingest logs from the pfSense/Suricata network layer (`03-network-protection-layer`) and the Active Directory environment (`06-active-directory-lab`), enabling correlation across network and identity events.
* **Detection Engineering Foundation:** With Splunk Web accessible, the next phase involves configuring log forwarding and building initial detection searches — for example, alerting on the AD authentication events already identified in the Active Directory lab (Event IDs 4624, 4720, 4768).
