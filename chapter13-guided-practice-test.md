# 🔐 Firewall & SELinux Practice Tasks

**Level:** Beginner to Intermediate  
**Environment:** RHEL, CentOS, Fedora, Rocky Linux (with firewalld & SELinux)

---

## 🔥 Firewall Tasks

### Task 1: Check firewalld status
```bash
sudo systemctl status firewalld
```

---

### Task 2: List all open ports and active services
```bash
sudo firewall-cmd --list-all
```

---

### Task 3: Open port 8080/tcp permanently and reload firewall
```bash
sudo firewall-cmd --permanent --add-port=8080/tcp
sudo firewall-cmd --reload
```

---

### Task 4: Block ICMP (ping) using firewalld
```bash
sudo firewall-cmd --zone=public --set-target=DROP --permanent
sudo firewall-cmd --reload
```

---

### Task 5: Remove FTP service
```bash
sudo firewall-cmd --permanent --remove-service=ftp
sudo firewall-cmd --reload
```

---

### Task 11: Create custom zone and assign interface
```bash
sudo firewall-cmd --permanent --new-zone=labzone
sudo firewall-cmd --permanent --zone=labzone --add-interface=eth0
sudo firewall-cmd --reload
```

---

### Task 12: Allow SSH in custom zone
```bash
sudo firewall-cmd --permanent --zone=labzone --add-service=ssh
sudo firewall-cmd --reload
```

---

### Task 13: Allow only SSH and HTTP, block rest
```bash
sudo firewall-cmd --permanent --remove-service=dhcpv6-client
sudo firewall-cmd --permanent --zone=public --add-service=ssh
sudo firewall-cmd --permanent --zone=public --add-service=http
sudo firewall-cmd --zone=public --set-target=DROP --permanent
sudo firewall-cmd --reload
```

---

### Task 14: Log dropped packets
```bash
sudo firewall-cmd --permanent --zone=public --add-rich-rule='rule family="ipv4" drop log prefix="DROP: " level="info"'
sudo firewall-cmd --reload
```

---

## 🔒 SELinux Tasks

### Task 6: Check SELinux status
```bash
getenforce
sestatus
```

---

### Task 7: Set SELinux to permissive temporarily
```bash
sudo setenforce 0
```

---

### Task 8: View recent denied entries in audit log
```bash
sudo grep denied /var/log/audit/audit.log | tail -n 10
```

---

### Task 9: Change file context to httpd_sys_content_t
```bash
sudo chcon -t httpd_sys_content_t /var/www/html/index.html
```

---

### Task 10: List SELinux contexts in /var/www/html
```bash
ls -Z /var/www/html
```

---

### Task 15: Set SELinux to enforcing permanently
```bash
sudo nano /etc/selinux/config
# Set: SELINUX=enforcing
sudo reboot
```

---

### Task 16: Generate custom policy module from denied log
```bash
sudo grep denied /var/log/audit/audit.log | audit2allow -m mypol
```

---

### Task 17: Install the custom SELinux policy module
```bash
sudo grep denied /var/log/audit/audit.log | audit2allow -M mypol
sudo semodule -i mypol.pp
```

---

### Task 18: Enable Apache network connect SELinux boolean
```bash
sudo getsebool httpd_can_network_connect
sudo setsebool -P httpd_can_network_connect on
```

---

### Task 19: List all SELinux booleans for Apache
```bash
getsebool -a | grep httpd
```

---

### Task 20: Restore default SELinux context
```bash
sudo restorecon -v /home/user/test.sh
```

---
