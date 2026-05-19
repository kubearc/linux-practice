# RHCSA Practical Exam Auto-Checking Script


On **Node1**
```bash
vim node1-script.sh
```

Copy the below script in file  
```bash
#!/bin/bash

# ==========================================
# RHCSA Practical Exam Checker
# Kubearc Academy
# ==========================================

PASS=0
FAIL=0
REPORT=/root/rhcsa_exam_report.txt

clear

echo "==========================================" | tee $REPORT
 echo " RHCSA PRACTICAL EXAM REPORT " | tee -a $REPORT
 echo "==========================================" | tee -a $REPORT
 echo "Hostname: $(hostname)" | tee -a $REPORT
 echo "Date: $(date)" | tee -a $REPORT
 echo "==========================================" | tee -a $REPORT
 echo "" | tee -a $REPORT

check_pass() {
    echo "[PASS] $1" | tee -a $REPORT
    PASS=$((PASS+1))
}

check_fail() {
    echo "[FAIL] $1" | tee -a $REPORT
    FAIL=$((FAIL+1))
}

# ==========================================
# NETWORK CHECK
# ==========================================

echo "========== NETWORK CHECK ==========" | tee -a $REPORT

HOSTNAME=$(hostname)

if [[ "$HOSTNAME" == "servera.example.com" || "$HOSTNAME" == "serverb.example.com" ]]; then
    check_pass "Hostname configured"
else
    check_fail "Hostname configuration"
fi

ip addr | grep -q "192.168.1."
if [ $? -eq 0 ]; then
    check_pass "IP Address configured"
else
    check_fail "IP Address configuration"
fi

grep -q "servera.example.com" /etc/hosts && grep -q "serverb.example.com" /etc/hosts
if [ $? -eq 0 ]; then
    check_pass "/etc/hosts configured"
else
    check_fail "/etc/hosts configuration"
fi

# ==========================================
# USER AND GROUP CHECK
# ==========================================

echo "" | tee -a $REPORT
 echo "========== USER & GROUP CHECK ==========" | tee -a $REPORT

id devuser &>/dev/null
if [ $? -eq 0 ]; then
    check_pass "User devuser exists"
else
    check_fail "User devuser"
fi

id backupuser &>/dev/null
if [ $? -eq 0 ]; then
    check_pass "User backupuser exists"
else
    check_fail "User backupuser"
fi

getent group developers &>/dev/null
if [ $? -eq 0 ]; then
    check_pass "Group developers exists"
else
    check_fail "Group developers"
fi

getent group backupteam &>/dev/null
if [ $? -eq 0 ]; then
    check_pass "Group backupteam exists"
else
    check_fail "Group backupteam"
fi

id devuser | grep -q developers
if [ $? -eq 0 ]; then
    check_pass "devuser added to developers"
else
    check_fail "devuser group membership"
fi

id backupuser | grep -q backupteam
if [ $? -eq 0 ]; then
    check_pass "backupuser added to backupteam"
else
    check_fail "backupuser group membership"
fi

# ==========================================
# PASSWORD AGING
# ==========================================

echo "" | tee -a $REPORT
 echo "========== PASSWORD AGING ==========" | tee -a $REPORT

chage -l devuser | grep -q "Maximum.*45"
if [ $? -eq 0 ]; then
    check_pass "Password max days configured"
else
    check_fail "Password max days"
fi

# ==========================================
# DIRECTORY AND ACL CHECK
# ==========================================

echo "" | tee -a $REPORT
 echo "========== PERMISSION & ACL CHECK ==========" | tee -a $REPORT

if [ -d /projectdata ]; then
    check_pass "/projectdata exists"
else
    check_fail "/projectdata directory"
fi

stat -c %G /projectdata | grep -q developers
if [ $? -eq 0 ]; then
    check_pass "Group ownership correct"
else
    check_fail "Group ownership"
fi

stat -c %A /projectdata | grep -q s
if [ $? -eq 0 ]; then
    check_pass "SGID enabled"
else
    check_fail "SGID configuration"
fi

getfacl /projectdata/data.txt 2>/dev/null | grep -q backupuser
if [ $? -eq 0 ]; then
    check_pass "ACL configured"
else
    check_fail "ACL configuration"
fi

# ==========================================
# SSH CONFIGURATION
# ==========================================

echo "" | tee -a $REPORT
 echo "========== SSH CHECK ==========" | tee -a $REPORT

if [ -f /home/devuser/.ssh/authorized_keys ]; then
    check_pass "SSH key authentication configured"
else
    check_fail "SSH key authentication"
fi

grep -i "PermitRootLogin no" /etc/ssh/sshd_config &>/dev/null
if [ $? -eq 0 ]; then
    check_pass "Root SSH login disabled"
else
    check_fail "Root SSH login"
fi

# ==========================================
# STORAGE CHECK
# ==========================================

echo "" | tee -a $REPORT
 echo "========== STORAGE CHECK ==========" | tee -a $REPORT

mount | grep -q "/backup"
if [ $? -eq 0 ]; then
    check_pass "/backup mounted"
else
    check_fail "/backup mount"
fi

swapon --show | grep -q "/dev"
if [ $? -eq 0 ]; then
    check_pass "Swap configured"
else
    check_fail "Swap configuration"
fi

# ==========================================
# LVM CHECK
# ==========================================

echo "" | tee -a $REPORT
 echo "========== LVM CHECK ==========" | tee -a $REPORT

vgs | grep -q vgdata
if [ $? -eq 0 ]; then
    check_pass "VG vgdata exists"
else
    check_fail "VG creation"
fi

lvs | grep -q lvbackup
if [ $? -eq 0 ]; then
    check_pass "LV lvbackup exists"
else
    check_fail "LV creation"
fi

mount | grep -q /lvbackup
if [ $? -eq 0 ]; then
    check_pass "/lvbackup mounted"
else
    check_fail "/lvbackup mount"
fi

# ==========================================
# APACHE AND FIREWALL CHECK
# ==========================================

echo "" | tee -a $REPORT
 echo "========== APACHE & FIREWALL CHECK ==========" | tee -a $REPORT

systemctl is-active httpd &>/dev/null
if [ $? -eq 0 ]; then
    check_pass "HTTPD running"
else
    check_fail "HTTPD service"
fi

systemctl is-enabled httpd &>/dev/null
if [ $? -eq 0 ]; then
    check_pass "HTTPD enabled"
else
    check_fail "HTTPD enable"
fi

firewall-cmd --list-services 2>/dev/null | grep -q http
if [ $? -eq 0 ]; then
    check_pass "Firewall configured for HTTP"
else
    check_fail "Firewall HTTP rule"
fi

curl -s http://localhost | grep -q "Kubearc"
if [ $? -eq 0 ]; then
    check_pass "Website working"
else
    check_fail "Website content"
fi

# ==========================================
# SELINUX CHECK
# ==========================================

echo "" | tee -a $REPORT
 echo "========== SELINUX CHECK ==========" | tee -a $REPORT

ls -Zd /webdata 2>/dev/null | grep -q httpd_sys_content_t
if [ $? -eq 0 ]; then
    check_pass "SELinux context configured"
else
    check_fail "SELinux context"
fi

# ==========================================
# CRON CHECK
# ==========================================

echo "" | tee -a $REPORT
 echo "========== CRON CHECK ==========" | tee -a $REPORT

crontab -l 2>/dev/null | grep -q time.log
if [ $? -eq 0 ]; then
    check_pass "Cron job configured"
else
    check_fail "Cron job"
fi

# ==========================================
# SCRIPT CHECK
# ==========================================

echo "" | tee -a $REPORT
 echo "========== SHELL SCRIPT CHECK ==========" | tee -a $REPORT

if [ -x /root/systemreport.sh ]; then
    check_pass "systemreport.sh executable"
else
    check_fail "systemreport.sh"
fi

# ==========================================
# PODMAN CHECK
# ==========================================

echo "" | tee -a $REPORT
 echo "========== PODMAN CHECK ==========" | tee -a $REPORT

podman ps 2>/dev/null | grep -q nginx
if [ $? -eq 0 ]; then
    check_pass "Podman nginx container running"
else
    check_fail "Podman container"
fi

# ==========================================
# FINAL REPORT
# ==========================================

echo "" | tee -a $REPORT
 echo "==========================================" | tee -a $REPORT
 echo " FINAL RESULT " | tee -a $REPORT
 echo "==========================================" | tee -a $REPORT
 echo "PASS: $PASS" | tee -a $REPORT
 echo "FAIL: $FAIL" | tee -a $REPORT

TOTAL=$((PASS + FAIL))

if [ $TOTAL -gt 0 ]; then
    PERCENT=$((PASS * 100 / TOTAL))
else
    PERCENT=0
fi

echo "Percentage: $PERCENT%" | tee -a $REPORT

if [ $PERCENT -ge 70 ]; then
    echo "STATUS: PASS" | tee -a $REPORT
else
    echo "STATUS: FAIL" | tee -a $REPORT
fi

echo "==========================================" | tee -a $REPORT
 echo "Report saved to: $REPORT"

```
```bash
bash node1-script.sh
```

On **Node2**
```bash
vim node2-script.sh
```

Copy the below script in file  
```bash
#!/bin/bash

# ==========================================
# RHCSA Practical Exam Checker
# Kubearc Academy
# ==========================================

PASS=0
FAIL=0
REPORT=/root/rhcsa_exam_report.txt

clear

echo "==========================================" | tee $REPORT
 echo " RHCSA PRACTICAL EXAM REPORT " | tee -a $REPORT
 echo "==========================================" | tee -a $REPORT
 echo "Hostname: $(hostname)" | tee -a $REPORT
 echo "Date: $(date)" | tee -a $REPORT
 echo "==========================================" | tee -a $REPORT
 echo "" | tee -a $REPORT

check_pass() {
    echo "[PASS] $1" | tee -a $REPORT
    PASS=$((PASS+1))
}

check_fail() {
    echo "[FAIL] $1" | tee -a $REPORT
    FAIL=$((FAIL+1))
}

# ==========================================
# NETWORK CHECK
# ==========================================

echo "========== NETWORK CHECK ==========" | tee -a $REPORT

HOSTNAME=$(hostname)

if [[ "$HOSTNAME" == "servera.example.com" || "$HOSTNAME" == "serverb.example.com" ]]; then
    check_pass "Hostname configured"
else
    check_fail "Hostname configuration"
fi

ip addr | grep -q "192.168.1."
if [ $? -eq 0 ]; then
    check_pass "IP Address configured"
else
    check_fail "IP Address configuration"
fi

grep -q "servera.example.com" /etc/hosts && grep -q "serverb.example.com" /etc/hosts
if [ $? -eq 0 ]; then
    check_pass "/etc/hosts configured"
else
    check_fail "/etc/hosts configuration"
fi

# ==========================================
# USER AND GROUP CHECK
# ==========================================

echo "" | tee -a $REPORT
 echo "========== USER & GROUP CHECK ==========" | tee -a $REPORT

id devuser &>/dev/null
if [ $? -eq 0 ]; then
    check_pass "User devuser exists"
else
    check_fail "User devuser"
fi

id backupuser &>/dev/null
if [ $? -eq 0 ]; then
    check_pass "User backupuser exists"
else
    check_fail "User backupuser"
fi

getent group developers &>/dev/null
if [ $? -eq 0 ]; then
    check_pass "Group developers exists"
else
    check_fail "Group developers"
fi

getent group backupteam &>/dev/null
if [ $? -eq 0 ]; then
    check_pass "Group backupteam exists"
else
    check_fail "Group backupteam"
fi

id devuser | grep -q developers
if [ $? -eq 0 ]; then
    check_pass "devuser added to developers"
else
    check_fail "devuser group membership"
fi

id backupuser | grep -q backupteam
if [ $? -eq 0 ]; then
    check_pass "backupuser added to backupteam"
else
    check_fail "backupuser group membership"
fi

# ==========================================
# PASSWORD AGING
# ==========================================

echo "" | tee -a $REPORT
 echo "========== PASSWORD AGING ==========" | tee -a $REPORT

chage -l devuser | grep -q "Maximum.*45"
if [ $? -eq 0 ]; then
    check_pass "Password max days configured"
else
    check_fail "Password max days"
fi

# ==========================================
# DIRECTORY AND ACL CHECK
# ==========================================

echo "" | tee -a $REPORT
 echo "========== PERMISSION & ACL CHECK ==========" | tee -a $REPORT

if [ -d /projectdata ]; then
    check_pass "/projectdata exists"
else
    check_fail "/projectdata directory"
fi

stat -c %G /projectdata | grep -q developers
if [ $? -eq 0 ]; then
    check_pass "Group ownership correct"
else
    check_fail "Group ownership"
fi

stat -c %A /projectdata | grep -q s
if [ $? -eq 0 ]; then
    check_pass "SGID enabled"
else
    check_fail "SGID configuration"
fi

getfacl /projectdata/data.txt 2>/dev/null | grep -q backupuser
if [ $? -eq 0 ]; then
    check_pass "ACL configured"
else
    check_fail "ACL configuration"
fi

# ==========================================
# SSH CONFIGURATION
# ==========================================

echo "" | tee -a $REPORT
 echo "========== SSH CHECK ==========" | tee -a $REPORT

if [ -f /home/devuser/.ssh/authorized_keys ]; then
    check_pass "SSH key authentication configured"
else
    check_fail "SSH key authentication"
fi

grep -i "PermitRootLogin no" /etc/ssh/sshd_config &>/dev/null
if [ $? -eq 0 ]; then
    check_pass "Root SSH login disabled"
else
    check_fail "Root SSH login"
fi

# ==========================================
# STORAGE CHECK
# ==========================================

echo "" | tee -a $REPORT
 echo "========== STORAGE CHECK ==========" | tee -a $REPORT

mount | grep -q "/backup"
if [ $? -eq 0 ]; then
    check_pass "/backup mounted"
else
    check_fail "/backup mount"
fi

swapon --show | grep -q "/dev"
if [ $? -eq 0 ]; then
    check_pass "Swap configured"
else
    check_fail "Swap configuration"
fi

# ==========================================
# LVM CHECK
# ==========================================

echo "" | tee -a $REPORT
 echo "========== LVM CHECK ==========" | tee -a $REPORT

vgs | grep -q vgdata
if [ $? -eq 0 ]; then
    check_pass "VG vgdata exists"
else
    check_fail "VG creation"
fi

lvs | grep -q lvbackup
if [ $? -eq 0 ]; then
    check_pass "LV lvbackup exists"
else
    check_fail "LV creation"
fi

mount | grep -q /lvbackup
if [ $? -eq 0 ]; then
    check_pass "/lvbackup mounted"
else
    check_fail "/lvbackup mount"
fi

# ==========================================
# APACHE AND FIREWALL CHECK
# ==========================================

echo "" | tee -a $REPORT
 echo "========== APACHE & FIREWALL CHECK ==========" | tee -a $REPORT

systemctl is-active httpd &>/dev/null
if [ $? -eq 0 ]; then
    check_pass "HTTPD running"
else
    check_fail "HTTPD service"
fi

systemctl is-enabled httpd &>/dev/null
if [ $? -eq 0 ]; then
    check_pass "HTTPD enabled"
else
    check_fail "HTTPD enable"
fi

firewall-cmd --list-services 2>/dev/null | grep -q http
if [ $? -eq 0 ]; then
    check_pass "Firewall configured for HTTP"
else
    check_fail "Firewall HTTP rule"
fi

curl -s http://localhost | grep -q "Kubearc"
if [ $? -eq 0 ]; then
    check_pass "Website working"
else
    check_fail "Website content"
fi

# ==========================================
# SELINUX CHECK
# ==========================================

echo "" | tee -a $REPORT
 echo "========== SELINUX CHECK ==========" | tee -a $REPORT

ls -Zd /webdata 2>/dev/null | grep -q httpd_sys_content_t
if [ $? -eq 0 ]; then
    check_pass "SELinux context configured"
else
    check_fail "SELinux context"
fi

# ==========================================
# CRON CHECK
# ==========================================

echo "" | tee -a $REPORT
 echo "========== CRON CHECK ==========" | tee -a $REPORT

crontab -l 2>/dev/null | grep -q time.log
if [ $? -eq 0 ]; then
    check_pass "Cron job configured"
else
    check_fail "Cron job"
fi

# ==========================================
# SCRIPT CHECK
# ==========================================

echo "" | tee -a $REPORT
 echo "========== SHELL SCRIPT CHECK ==========" | tee -a $REPORT

if [ -x /root/systemreport.sh ]; then
    check_pass "systemreport.sh executable"
else
    check_fail "systemreport.sh"
fi

# ==========================================
# PODMAN CHECK
# ==========================================

echo "" | tee -a $REPORT
 echo "========== PODMAN CHECK ==========" | tee -a $REPORT

podman ps 2>/dev/null | grep -q nginx
if [ $? -eq 0 ]; then
    check_pass "Podman nginx container running"
else
    check_fail "Podman container"
fi

# ==========================================
# FINAL REPORT
# ==========================================

echo "" | tee -a $REPORT
 echo "==========================================" | tee -a $REPORT
 echo " FINAL RESULT " | tee -a $REPORT
 echo "==========================================" | tee -a $REPORT
 echo "PASS: $PASS" | tee -a $REPORT
 echo "FAIL: $FAIL" | tee -a $REPORT

TOTAL=$((PASS + FAIL))

if [ $TOTAL -gt 0 ]; then
    PERCENT=$((PASS * 100 / TOTAL))
else
    PERCENT=0
fi

echo "Percentage: $PERCENT%" | tee -a $REPORT

if [ $PERCENT -ge 70 ]; then
    echo "STATUS: PASS" | tee -a $REPORT
else
    echo "STATUS: FAIL" | tee -a $REPORT
fi

echo "==========================================" | tee -a $REPORT
 echo "Report saved to: $REPORT"

```
```bash
bash node2-script.sh
```
