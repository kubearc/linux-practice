# 🔐 Firewall & SELinux Practice Tasks

**Level:** Beginner to Intermediate  
**Environment:** Linux with firewalld & SELinux

---

## 🔥 Firewall Tasks

### Task 1: Check firewalld status
```bash
systemctl status firewalld
```

---

### Task 2: List all open ports and active services
```bash
firewall-cmd --list-all
```

---

### Task 3: Open port 8080/tcp permanently and reload firewall
```bash
firewall-cmd --permanent --add-port=8080/tcp
firewall-cmd --reload
```

---

### Task 4: Block ICMP (ping) using firewalld
```bash
firewall-cmd --zone=public --set-target=DROP --permanent
firewall-cmd --reload
```

---

### Task 5: Remove FTP service
```bash
firewall-cmd --permanent --remove-service=ftp
firewall-cmd --reload
```

---

### Task 11: Create custom zone and add SSH service
```bash
firewall-cmd --permanent --new-zone=labzone
firewall-cmd --permanent --zone=labzone --add-service=ssh
firewall-cmd --reload
```

---

### Task 12: Allow http in custom zone
```bash
firewall-cmd --permanent --zone=labzone --add-service=http
firewall-cmd --reload
```

---

### Task 13: Allow only SSH and HTTP, block rest
```bash
firewall-cmd --permanent --remove-service=dhcpv6-client
firewall-cmd --permanent --zone=public --add-service=ssh
firewall-cmd --permanent --zone=public --add-service=http
firewall-cmd --reload
```
---


### Task 20: Restore default SELinux context
```bash
sudo restorecon -v /home/user/test.sh
```

---
