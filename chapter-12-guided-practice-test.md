
# 🧪 RHEL 9 Command Practice Test – Logs, Cron, and At Jobs

**Type**: Hands-on Command-line Practice  
**Level**: Beginner to Intermediate  
**Platform**: RHEL 9 or compatible Linux system

---

## 🔹 Section 1: Logs and Journalctl

### 1. View logs from the current boot session:
```bash
journalctl -b
```

### 2. Show logs from yesterday:
```bash
journalctl --since=yesterday --until=today
```

### 3. Display logs related to the sshd service:
```bash
journalctl -u sshd
```

### 4. Follow logs from crond in real time:
```bash
journalctl -u crond -f
```

### 5. View kernel messages:
```bash
journalctl -k
```

### 6. Export all logs to a file:
```bash
journalctl > all-logs.txt
```

### 7. Show logs between 10:00 and 11:00 AM:
```bash
journalctl --since "10:00" --until "11:00"
```

### 8. Show only error or higher level logs:
```bash
journalctl -p err
```

### 9. Clear journal logs (requires root):
```bash
sudo journalctl --vacuum-time=1s
```

---

## 🔹 Section 2: Cron Jobs

### 1. List user cron jobs:
```bash
crontab -l
```

### 2. Edit current user’s crontab:
```bash
crontab -e
```

### 3. Schedule `/usr/local/bin/backup.sh` at 2:30 AM daily:
```bash
# Inside crontab editor:
30 2 * * * /usr/local/bin/backup.sh
```

### 4. Run a job every Monday at 9:00 AM:
```bash
# Inside crontab editor:
0 9 * * 1 echo "Weekly report" >> /var/log/weekly.log
```

### 5. Remove all cron jobs:
```bash
crontab -r
```

### 6. View system-wide cron jobs:
```bash
cat /etc/crontab
```

### 7. View cron logs via journal:
```bash
journalctl -u crond
```

### 8. Restrict `john` from using cron:
```bash
echo "john" | sudo tee -a /etc/cron.deny
```

---

## 🔹 Section 3: At Jobs

### 1. Schedule system shutdown at 11:45 PM:
```bash
echo "shutdown now" | at 11:45 PM
```

### 2. List pending at jobs:
```bash
atq
```

### 3. Remove job #5:
```bash
atrm 5
```

### 4. Echo "System checked" to /tmp/log.txt at 3:15 PM:
```bash
echo 'echo "System checked" >> /tmp/log.txt' | at 3:15 PM
```

### 5. Allow only `admin` to use at:
```bash
echo "admin" | sudo tee /etc/at.allow
```

### 6. Deny `bob` from using at:
```bash
echo "bob" | sudo tee -a /etc/at.deny
```

---

## ✅ Notes
- Use `man`, `--help`, or `info` with any command for further options.
- Ensure `crond` and `atd` services are running to test cron and at jobs.

---
