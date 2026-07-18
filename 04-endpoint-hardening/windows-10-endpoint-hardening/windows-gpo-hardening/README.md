Windows GPO Hardening (CIS Benchmark for Windows 10)
1. CIS Portal Access

Screenshot: CIS-Security-Portal-Dashboard.png  
Shows official CIS Benchmark source.
2. Account Lockout Policies

    Baseline: Windows-Baseline-Account-Lockout-Policies.png

    Hardened: CIS-Hardened-Account-Lockout-Policies.png

3. Password Policies

    Baseline: Windows-Default-Password-History-Policy.png

    Hardened: CIS-Hardened-Password-Complexity-Policies.png

    Enforcement Test: Password-Policy-Enforcement-Validation-Test.png

4. Services Hardening

Screenshot: Windows-Services-Hardening-Disabling-Unused-Features.png  
Disabled:

    Print Spooler (PrintNightmare)

    Xbox services

5. Apply Policies

Screenshot: PowerShell-Force-Group-Policy-Update.png  
Command used:
Code

gpupdate /force

Tools Used (Win+R Commands)

    gpedit.msc

    secpol.msc

    services.msc

    eventvwr.msc
