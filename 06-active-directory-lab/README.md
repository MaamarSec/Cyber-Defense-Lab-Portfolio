# Active Directory Lab Build

Active Directory (AD) serves as the centralized identity and access management backbone for enterprise Windows networks worldwide. Because AD controls authentication, authorization, and domain policies, it is a primary target for threat actors — gaining full control over AD effectively grants complete domain dominance.

This project documents the step-by-step deployment of an Active Directory domain environment, covering domain controller installation, network configuration, client endpoint domain join, user provisioning, and command-line authentication verification.

---

## Technical Overview & Prerequisites

* **Domain Controller (`DC01`):** Windows Server 2019 Standard Evaluation (GUI)
* **Domain Name:** `cdmdc.local` (NetBIOS: `CDMDC`)
* **Static IP Address:** `192.168.56.10`
* **Network Gateway:** pfSense Virtual Firewall
* **Client Workstation (`WIN10-CLI01`):** Windows 10 Enterprise
* **Core Protocols:** Kerberos, NTLM, DNS, LDAP

---

## Deployment Lifecycle

1. **Infrastructure Setup:** Deploy Windows Server 2019 and configure static IP addressing.
2. **AD DS Deployment:** Install Active Directory Domain Services and promote the server to the Forest Root Domain Controller.
3. **Endpoint Integration:** Configure client DNS to point to `DC01` and perform a domain join on the Windows 10 host.
4. **User Provisioning:** Create standard domain user accounts using Active Directory Users and Computers (ADUC).
5. **Authentication & Validation:** Verify Kerberos ticket issuance, client domain connectivity, and AD database attributes via PowerShell and CLI tools.

---

## Step-by-Step Implementation

### Phase 1: Virtual Machine Provisioning & Network Configuration

1. **VM Setup:** Created a new virtual machine in VirtualBox using the **Windows Server 2019 Standard Evaluation** ISO.

   ![VM creation — name and OS selection](screenshots/VM_Creation.png)

   > **Note:** During VM creation, ensure **Unattended Installation** is disabled to retain manual control over partition layout, component selection, and setup configuration.

2. **Post-Installation Maintenance:** Unmounted the Windows Server ISO from the virtual optical drive prior to reboot to prevent an installation boot loop, then renamed the server to `DC01` to reflect its intended role.

3. **Static Network Allocation:** Configured `DC01` with a fixed IP address (`192.168.56.10`) on a VirtualBox Host-Only adapter. Domain Controllers require persistent static IP addressing so network endpoints can reliably locate authentication services and resolve SRV records.

   ![Static IP configuration on DC01](screenshots/static-ip-configuration.png)

4. **Connectivity Verification:** Confirmed IP assignment and tested gateway/internet reachability before proceeding to AD DS installation.

   ![ipconfig and ping tests confirming gateway and internet connectivity](screenshots/Network_Verification___Gateway_Connectivity_Test.png)

---

### Phase 2: Promoting DC01 to Forest Root Domain Controller

1. Installed the **Active Directory Domain Services (AD DS)** role, along with **DNS Server**, via Server Manager.

   ![Selecting the AD DS and DNS Server roles](screenshots/server-manager-roles-adds-dns-selection.png)

2. Promoted the server to a Domain Controller, establishing a new forest named **`cdmdc.local`**, setting the forest/domain functional level, and configuring the DSRM (Directory Services Restore Mode) password.

   ![AD DS installation results — server successfully configured as a domain controller](screenshots/ad-ds-installation-results-reboot.png)

3. Verified core AD DS services (`NTDS`, `DNS`, `KDC`, `Netlogon`) were fully operational following the post-promotion reboot, including the `cdmdc.local` Active Directory-integrated DNS zone.

   ![DNS Manager showing the cdmdc.local forward lookup zone](screenshots/dns-manager-forward-lookup-zones.png)

---

### Phase 3: Client Integration & User Provisioning

1. Configured the Windows 10 client host's primary DNS to point directly to `DC01` (`192.168.56.10`).

2. Successfully joined `WIN10-CLI01` to the `cdmdc.local` domain.

   ![Successful domain join confirmation — Welcome to the cdmdc.local domain](screenshots/Successful_Active_Directory_Workstation_Domain_Join.png)

3. Opened **Active Directory Users and Computers (ADUC)** on `DC01` and provisioned a standard domain user:
   * **Full Name:** John Doe
   * **Logon Name:** `jdoe` (`jdoe@cdmdc.local`)

   ![Creating a new domain user object in ADUC](screenshots/aduc-creating-new-domain-user-object.png)

4. Performed the first interactive domain logon on the client as `jdoe`, confirming end-to-end authentication and profile creation.

   ![Verifying standard user profile creation via domain logon](screenshots/win10-john-doe-first-logon-welcome__Verifying_Standard_User_Profile_Creation_via_Domain.png)

---

## Validation & Verification

### 1. Client Domain Controller Discovery (`WIN10-CLI01`)

Executed `nltest` on the Windows 10 client workstation to verify DC locator services, site binding, and secure channel communication with `DC01`.

```powershell
nltest /dsgetdc:cdmdc.local
```

![nltest output confirming DC discovery and secure channel status with DC01](screenshots/Validating_Active_Directory_Domain_Controller.png)

*Figure 1: `nltest` output confirming DC discovery and secure channel status with `DC01`.*

### 2. Domain Identity Query (`DC01`)

Ran the Active Directory PowerShell module on `DC01` to query the domain database and inspect account properties for the newly provisioned user object.

```powershell
Get-ADUser -Identity jdoe
```

![Get-ADUser output for jdoe](screenshots/Querying_Provisioned_Active_Directory_User_via_ActiveDirectory_PowerShell_Module.png)

*Figure 2: PowerShell output displaying DistinguishedName (DN), SID, and account status for user `jdoe`.*

### 3. Active Directory Computer Objects Query (`DC01`)

Ran `Get-ADComputer` to verify that both the Domain Controller (`DC01`) and the Windows 10 workstation (`DESKTOP-C8UKIEA`) are successfully registered as active machine accounts in the AD database.

```powershell
Get-ADComputer -Filter *
```

![Get-ADComputer output listing DC01 and the domain-joined workstation](screenshots/powershell_get_adcomputer_verification.png)

*Figure 3: PowerShell output displaying DistinguishedName (DN), SAMAccountName, and SID attributes for all domain-joined computer objects.*

---

## SOC Analyst Takeaways

* **Kerberos & NTLM Traffic:** This lab setup allows for capturing authentication traffic (AS-REQ / AS-REP exchanges) via Wireshark to observe how Kerberos issues Ticket Granting Tickets (TGTs) versus legacy NTLM fallback behavior.
* **Event Log Monitoring:** Successful logins, domain joins, and user provisioning events can be analyzed directly in Windows Event Viewer (e.g., Event IDs 4624, 4720, 4768) to build detection rules for threat hunting.
