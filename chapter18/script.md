# RHCSA Practical Exam Auto-Checking Script


On **Node1**
```bash
vim node1-script.sh
```

Copy the below script in file  
```bash
#!/bin/bash

# ==========================================
# RHCSA AUTO CHECKER
# Kubearc Academy
# Smart Node Detection Version
# ==========================================

PASS=0
FAIL=0

HOSTNAME=$(hostname)

REPORT="/root/rhcsa_exam_report.txt"

clear

echo "==========================================" | tee $REPORT
echo " RHCSA PRACTICAL EXAM REPORT " | tee -a $REPORT
echo "==========================================" | tee -a $REPORT
echo "Hostname: $HOSTNAME" | tee -a $REPORT
echo "Date: $(date)" | tee -a $REPORT
echo "==========================================" | tee -a $REPORT
echo "" | tee -a $REPORT

pass() {
    echo "[PASS] $1" | tee -a $REPORT
    PASS=$((PASS+1))
}

fail() {
    echo "[FAIL] $1" | tee -a $REPORT
    FAIL=$((FAIL+1))
}

# ==========================================
# COMMON NETWORK CHECK
# ==========================================

echo "========== NETWORK CHECK ==========" | tee -a $REPORT

if [[ "$HOSTNAME" == "servera.example.com" || "$HOSTNAME" == "serverb.example.com" ]]; then
    pass "Hostname configured"
else
    fail "Hostname configuration"
fi

ip addr | grep -q "192.168.1."
if [ $? -eq 0 ]; then
    pass "IP configured"
else
    fail "IP configuration"
fi

grep -q "servera.example.com" /etc/hosts && grep -q "serverb.example.com" /etc/hosts
if [ $? -eq 0 ]; then
    pass "/etc/hosts configured"
else
    fail "/etc/hosts configuration"
fi

# =====================================================
# NODE 1 CHECKS
# =====================================================

if [[ "$HOSTNAME" == "servera.example.com" ]]; then

echo "" | tee -a $REPORT
echo "========== NODE 1 TASKS ==========" | tee -a $REPORT

# USER CHECK

id devuser &>/dev/null
[ $? -eq 0 ] && pass "User devuser exists" || fail "User devuser"

id backupuser &>/dev/null
[ $? -eq 0 ] && pass "User backupuser exists" || fail "User backupuser"

getent group developers &>/dev/null
[ $? -eq 0 ] && pass "Group developers exists" || fail "Group developers"

getent group backupteam &>/dev/null
[ $? -eq 0 ] && pass "Group backupteam exists" || fail "Group backupteam"

id devuser | grep -q developers
[ $? -eq 0 ] && pass "devuser group membership" || fail "devuser group membership"

id backupuser | grep -q backupteam
[ $? -eq 0 ] && pass "backupuser group membership" || fail "backupuser group membership"

# PASSWORD AGING

chage -l devuser | grep -q "Maximum.*45"
[ $? -eq 0 ] && pass "Password aging configured" || fail "Password aging"

# DIRECTORY CHECK

[ -d /projectdata ] && pass "/projectdata exists" || fail "/projectdata"

stat -c %G /projectdata 2>/dev/null | grep -q developers
[ $? -eq 0 ] && pass "Group ownership correct" || fail "Group ownership"

stat -c %A /projectdata 2>/dev/null | grep -q s
[ $? -eq 0 ] && pass "SGID configured" || fail "SGID"

getfacl /projectdata/data.txt 2>/dev/null | grep -q backupuser
[ $? -eq 0 ] && pass "ACL configured" || fail "ACL configuration"

# SSH CHECK

[ -f /home/devuser/.ssh/authorized_keys ] && pass "SSH key authentication" || fail "SSH key authentication"

# APACHE CHECK

systemctl is-active httpd &>/dev/null
[ $? -eq 0 ] && pass "HTTPD running" || fail "HTTPD service"

systemctl is-enabled httpd &>/dev/null
[ $? -eq 0 ] && pass "HTTPD enabled" || fail "HTTPD enable"

firewall-cmd --list-services 2>/dev/null | grep -q http
[ $? -eq 0 ] && pass "Firewall HTTP rule" || fail "Firewall HTTP rule"

curl -s http://localhost | grep -qi "Kubearc"
[ $? -eq 0 ] && pass "Website working" || fail "Website content"

# SELINUX CHECK

ls -Zd /webdata 2>/dev/null | grep -q httpd_sys_content_t
[ $? -eq 0 ] && pass "SELinux context correct" || fail "SELinux context"

# CRON CHECK

crontab -l 2>/dev/null | grep -q time.log
[ $? -eq 0 ] && pass "Cron job configured" || fail "Cron job"

# SCRIPT CHECK

[ -x /root/systemreport.sh ] && pass "systemreport.sh executable" || fail "systemreport.sh"

fi

# =====================================================
# NODE 2 CHECKS
# =====================================================

if [[ "$HOSTNAME" == "serverb.example.com" ]]; then

echo "" | tee -a $REPORT
echo "========== NODE 2 TASKS ==========" | tee -a $REPORT

# STORAGE CHECK

mount | grep -q "/backup"
[ $? -eq 0 ] && pass "/backup mounted" || fail "/backup mount"

swapon --show | grep -q "/dev"
[ $? -eq 0 ] && pass "Swap configured" || fail "Swap configuration"

# LVM CHECK

vgs | grep -q vgdata
[ $? -eq 0 ] && pass "VG vgdata exists" || fail "VG vgdata"

lvs | grep -q lvbackup
[ $? -eq 0 ] && pass "LV lvbackup exists" || fail "LV lvbackup"

mount | grep -q /lvbackup
[ $? -eq 0 ] && pass "/lvbackup mounted" || fail "/lvbackup mount"

# SSH ROOT LOGIN CHECK

grep -iq "^PermitRootLogin no" /etc/ssh/sshd_config
[ $? -eq 0 ] && pass "Root SSH login disabled" || fail "Root SSH login"

# PODMAN CHECK

podman ps 2>/dev/null | grep -q nginx
[ $? -eq 0 ] && pass "Podman nginx container running" || fail "Podman container"

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

echo ""
echo "Report saved to:"
echo "$REPORT"
echo ""
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
# RHCSA AUTO CHECKER
# Kubearc Academy
# Smart Node Detection Version
# ==========================================

PASS=0
FAIL=0

HOSTNAME=$(hostname)

REPORT="/root/rhcsa_exam_report.txt"

clear

echo "==========================================" | tee $REPORT
echo " RHCSA PRACTICAL EXAM REPORT " | tee -a $REPORT
echo "==========================================" | tee -a $REPORT
echo "Hostname: $HOSTNAME" | tee -a $REPORT
echo "Date: $(date)" | tee -a $REPORT
echo "==========================================" | tee -a $REPORT
echo "" | tee -a $REPORT

pass() {
    echo "[PASS] $1" | tee -a $REPORT
    PASS=$((PASS+1))
}

fail() {
    echo "[FAIL] $1" | tee -a $REPORT
    FAIL=$((FAIL+1))
}

# ==========================================
# COMMON NETWORK CHECK
# ==========================================

echo "========== NETWORK CHECK ==========" | tee -a $REPORT

if [[ "$HOSTNAME" == "servera.example.com" || "$HOSTNAME" == "serverb.example.com" ]]; then
    pass "Hostname configured"
else
    fail "Hostname configuration"
fi

ip addr | grep -q "192.168.1."
if [ $? -eq 0 ]; then
    pass "IP configured"
else
    fail "IP configuration"
fi

grep -q "servera.example.com" /etc/hosts && grep -q "serverb.example.com" /etc/hosts
if [ $? -eq 0 ]; then
    pass "/etc/hosts configured"
else
    fail "/etc/hosts configuration"
fi

# =====================================================
# NODE 1 CHECKS
# =====================================================

if [[ "$HOSTNAME" == "servera.example.com" ]]; then

echo "" | tee -a $REPORT
echo "========== NODE 1 TASKS ==========" | tee -a $REPORT

# USER CHECK

id devuser &>/dev/null
[ $? -eq 0 ] && pass "User devuser exists" || fail "User devuser"

id backupuser &>/dev/null
[ $? -eq 0 ] && pass "User backupuser exists" || fail "User backupuser"

getent group developers &>/dev/null
[ $? -eq 0 ] && pass "Group developers exists" || fail "Group developers"

getent group backupteam &>/dev/null
[ $? -eq 0 ] && pass "Group backupteam exists" || fail "Group backupteam"

id devuser | grep -q developers
[ $? -eq 0 ] && pass "devuser group membership" || fail "devuser group membership"

id backupuser | grep -q backupteam
[ $? -eq 0 ] && pass "backupuser group membership" || fail "backupuser group membership"

# PASSWORD AGING

chage -l devuser | grep -q "Maximum.*45"
[ $? -eq 0 ] && pass "Password aging configured" || fail "Password aging"

# DIRECTORY CHECK

[ -d /projectdata ] && pass "/projectdata exists" || fail "/projectdata"

stat -c %G /projectdata 2>/dev/null | grep -q developers
[ $? -eq 0 ] && pass "Group ownership correct" || fail "Group ownership"

stat -c %A /projectdata 2>/dev/null | grep -q s
[ $? -eq 0 ] && pass "SGID configured" || fail "SGID"

getfacl /projectdata/data.txt 2>/dev/null | grep -q backupuser
[ $? -eq 0 ] && pass "ACL configured" || fail "ACL configuration"

# SSH CHECK

[ -f /home/devuser/.ssh/authorized_keys ] && pass "SSH key authentication" || fail "SSH key authentication"

# APACHE CHECK

systemctl is-active httpd &>/dev/null
[ $? -eq 0 ] && pass "HTTPD running" || fail "HTTPD service"

systemctl is-enabled httpd &>/dev/null
[ $? -eq 0 ] && pass "HTTPD enabled" || fail "HTTPD enable"

firewall-cmd --list-services 2>/dev/null | grep -q http
[ $? -eq 0 ] && pass "Firewall HTTP rule" || fail "Firewall HTTP rule"

curl -s http://localhost | grep -qi "Kubearc"
[ $? -eq 0 ] && pass "Website working" || fail "Website content"

# SELINUX CHECK

ls -Zd /webdata 2>/dev/null | grep -q httpd_sys_content_t
[ $? -eq 0 ] && pass "SELinux context correct" || fail "SELinux context"

# CRON CHECK

crontab -l 2>/dev/null | grep -q time.log
[ $? -eq 0 ] && pass "Cron job configured" || fail "Cron job"

# SCRIPT CHECK

[ -x /root/systemreport.sh ] && pass "systemreport.sh executable" || fail "systemreport.sh"

fi

# =====================================================
# NODE 2 CHECKS
# =====================================================

if [[ "$HOSTNAME" == "serverb.example.com" ]]; then

echo "" | tee -a $REPORT
echo "========== NODE 2 TASKS ==========" | tee -a $REPORT

# STORAGE CHECK

mount | grep -q "/backup"
[ $? -eq 0 ] && pass "/backup mounted" || fail "/backup mount"

swapon --show | grep -q "/dev"
[ $? -eq 0 ] && pass "Swap configured" || fail "Swap configuration"

# LVM CHECK

vgs | grep -q vgdata
[ $? -eq 0 ] && pass "VG vgdata exists" || fail "VG vgdata"

lvs | grep -q lvbackup
[ $? -eq 0 ] && pass "LV lvbackup exists" || fail "LV lvbackup"

mount | grep -q /lvbackup
[ $? -eq 0 ] && pass "/lvbackup mounted" || fail "/lvbackup mount"

# SSH ROOT LOGIN CHECK

grep -iq "^PermitRootLogin no" /etc/ssh/sshd_config
[ $? -eq 0 ] && pass "Root SSH login disabled" || fail "Root SSH login"

# PODMAN CHECK

podman ps 2>/dev/null | grep -q nginx
[ $? -eq 0 ] && pass "Podman nginx container running" || fail "Podman container"

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

echo ""
echo "Report saved to:"
echo "$REPORT"
echo ""
```
```bash
bash node2-script.sh
```
