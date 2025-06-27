# 🛡️ SELinux Practice Task (No Apache, No sudo)

## 🎯 Objective
Learn how to allow a custom user or process to access a restricted directory by setting SELinux file contexts — **without using sudo**.

---

## 🖥️ System Requirements
- RHEL/CentOS/AlmaLinux/Rocky Linux
- Running as `root`
- SELinux in **Enforcing** mode
- `semanage` tool installed (`dnf install policycoreutils-python-utils`)

---

## 🔧 Task Steps

### ✅ 1. Check SELinux Mode
```bash
getenforce
# Should return: Enforcing
```

---

### ✅ 2. Create a Custom Application Directory
```bash
mkdir -p /myapp/logs
echo "Log file started" > /myapp/logs/app.log
```

---

### ✅ 3. Create a Custom User
```bash
useradd myappuser
chown -R myappuser:myappuser /myapp
```

---

### ❌ 4. Try Accessing Log File as `myappuser`
```bash
runuser -l myappuser -c 'cat /myapp/logs/app.log'
```
> If SELinux blocks access due to the wrong context, this command may fail or be denied.

---

### 🔍 5. Check SELinux Context
```bash
ls -Z /myapp/logs
# Likely shows: default_t — not suitable for logs
```

---

### ✅ 6. Apply Correct SELinux Context
```bash
semanage fcontext -a -t var_log_t "/myapp/logs(/.*)?"
restorecon -Rv /myapp/logs
```

---

### 🔁 7. Re-test Access
```bash
runuser -l myappuser -c 'cat /myapp/logs/app.log'
```
> Now it should work, as the context `var_log_t` allows reading logs.

---

### 🧪 8. (Bonus) Set Wrong Context to See SELinux Block
```bash
chcon -t httpd_sys_content_t /myapp/logs/app.log
runuser -l myappuser -c 'cat /myapp/logs/app.log'
```
> This may now be **denied** by SELinux even if permissions allow it.

---

### ✅ 9. Temporary change SELinux to permissive mode 
```bash 
setenforce 0
```

## Note: Reboot the system and check the SELinux state
-- Run the following command 
``` bash 
getenforce
``` 
### ✅ 10. Permanently change SELinux to permissive mode 
```bash 
vim /etc/selinux/config 

### change the SELINUX = enforcing to permissive 
```
## Note: Reboot the system and check the selinux state

----
