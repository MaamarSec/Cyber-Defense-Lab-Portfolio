# SSH Hardening (Production‑Grade Remote Access Security)

SSH is the primary remote access method for the monitoring tower.  
Hardening SSH ensures that only authorized cryptographic keys can access the server, eliminating password‑based attacks and brute‑force attempts.

This layer aligns with CIS Ubuntu 22.04 LTS Benchmark v3.0.0.

---

## 1. Backup Critical SSH Configuration Files

Before making changes, create a backup:

```
sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.backup
ls -lh /etc/ssh/sshd_config*
```

This ensures you can restore SSH if needed.

---

## 2. Generate a Modern ED25519 Key Pair (Windows Host)

On your Windows host machine:

```
ssh-keygen -t ed25519 -C "defender@ubuntu-server"
```

Display the public key:

```
type ~\.ssh\id_ed25519.pub
```

Copy the entire key.

---

## 3. Install the Public Key on the Ubuntu Server

Create the `.ssh` directory:

```
mkdir -p ~/.ssh
chmod 700 ~/.ssh
```

Create the authorized keys file:

```
nano ~/.ssh/authorized_keys
```

Paste your public key into the file.

Set secure permissions:

```
chmod 600 ~/.ssh/authorized_keys
cat ~/.ssh/authorized_keys
```

---

## 4. Test Key‑Based Authentication

Reconnect to the server:

```
ssh defender@<server-ip>
```

You should connect **instantly** without a password prompt.

This confirms your key is installed correctly.

---

## 5. Disable Password Authentication (CIS Requirement)

Edit both SSH configuration files:

```
sudo nano /etc/ssh/sshd_config
sudo nano /etc/ssh/sshd_config.d/50-cloud-init.conf
```

Set:

```
PasswordAuthentication no
```

This disables password login across the entire SSH service.

---

## 6. Validate SSH Configuration

Check for syntax errors:

```
sudo sshd -t
```

If no output appears, the configuration is valid.

---

## 7. Restart SSH Service

```
sudo systemctl restart sshd
sudo systemctl status sshd
```

SSH is now enforcing key‑only authentication.

---

## 8. Final Security Test

Force SSH to ignore your key:

```
ssh -o PubkeyAuthentication=no defender@192.168.56.101
```

Expected result:

```
Permission denied (publickey).
```

Now connect normally:

```
ssh defender@192.168.56.101
```

You should authenticate instantly using your ED25519 key.

---

## 9. Hardening Summary

SSH is now configured with:

- Key‑only authentication  
- Password login fully disabled  
- Modern ED25519 cryptographic keys  
- Secure `.ssh` directory permissions  
- Validated daemon configuration  
- Verified rejection of password‑based access  

This forms the remote access security layer of your monitoring tower.
