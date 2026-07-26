# Fail2Ban Hardening (Intrusion Prevention Layer)

Fail2Ban provides automated protection against brute‑force attacks by monitoring authentication logs and banning malicious IP addresses.  
This layer adds intelligence to your firewall and strengthens the monitoring tower against SSH attacks.

---

## 1. Install and Enable Fail2Ban

Start the service:

```
sudo systemctl start fail2ban
```

Enable persistence across reboots:

```
sudo systemctl enable fail2ban
```

Verify service status:

```
sudo systemctl status fail2ban
```

Fail2Ban should show as **active (running)**.

---

## 2. Create Local Jail Configuration

Create a custom configuration file:

```
sudo nano /etc/fail2ban/jail.local
```

Paste the following configuration:

```
[DEFAULT]
bantime = 600
findtime = 600
maxretry = 5
banaction = ufw

[sshd]
enabled = true
port = ssh
filter = sshd
logpath = /var/log/auth.log
maxretry = 5
```

### Explanation

- **bantime**: IP is banned for 10 minutes  
- **findtime**: Fail2Ban checks for repeated failures within 10 minutes  
- **maxretry**: 5 failed attempts triggers a ban  
- **banaction = ufw**: Fail2Ban uses UFW to block attackers  
- **sshd jail**: Protects SSH from brute‑force attacks  

Save and exit.

---

## 3. Restart Fail2Ban

```
sudo systemctl restart fail2ban
```

---

## 4. Verify Fail2Ban Status

Check global status:

```
sudo fail2ban-client status
```

Check SSH jail specifically:

```
sudo fail2ban-client status sshd
```

You should see:

- Jail enabled  
- Log path  
- Max retries  
- Currently banned IPs  

---

## 5. Simulate a Brute‑Force Attack

Inject 5 failed SSH login attempts into the auth log:

```
sudo bash -c 'for i in {1..5}; do echo "$(date "+%b %d %H:%M:%S") $(hostname) sshd[$$]: Failed password for testuser from 192.168.1.100 port 12345 ssh2" >> /var/log/auth.log; done'
```

Wait 5 seconds, then check Fail2Ban again:

```
sudo fail2ban-client status sshd
```

You should now see:

- **1 banned IP**  
- The attacker’s IP: `192.168.1.100`  

Fail2Ban successfully detected and blocked the simulated attack.

---

## 6. Unban All IPs (Optional)

```
sudo fail2ban-client unban --all
```

---

## 7. Hardening Summary

Fail2Ban is now configured with:

- Automated brute‑force detection  
- UFW‑based IP banning  
- SSH protection  
- Real‑time log monitoring  
- Verified attack simulation  

This forms the intrusion prevention layer of your monitoring tower.
