# Chapter 09 - Guided Exercise 01 
# Linux Process & Resource Management - Hands-on Tasks

---

## 📋 Task 1: View All Running Processes

**Objective:** List all running processes on the system in a detailed format.  
**Solution:**
```bash
ps aux
```
---

## 📋 Task 2: Find the PID of a Process

**Objective:** Find the PID of the `sshd` process.  
**Solution:**
```bash
pidof sshd
# or
pgrep sshd
```

---

## 📋 Task 3: Monitor Real-time Processes

**Objective:** Launch the `top` command and observe which processes consume the most CPU and memory.  
**Solution:**
```bash
top
# Press `P` to sort by CPU, `M` to sort by memory
```

---

## 📋 Task 4: Kill a Process

**Objective:** Kill the process with PID 1234 (replace with an actual PID).  
**Solution:**
```bash
kill 1234
# or to force kill:
kill -9 1234
```

---

## 📋 Task 5: Kill All Instances of a Process

**Objective:** Kill all running instances of the Firefox browser.  
**Solution:**
```bash
killall firefox
# or
pkill firefox
```

---

## 📋 Task 6: Run a firefox Job in the Background

**Objective:** Run `firefox` in the background and check its status.  
**Solution:**
```bash
firefox &
jobs
```

---


## 📋 Task 7: Run a sleep in the Background

**Objective:** Run `firefox` in the background and check its status.  
**Solution:**
```bash
sleep &
jobs
```
---

## 📋 Task 8: Bring the firefox background job in the foreground.

**Note:** First get the job id of firefox and then bring it in the foreground with fg command.   
**Solution:**
```bash
jobs
fg %jobid-of--firefox
```
---

## 📋 Task 9: Close the firefox job which is running on the terminal by pression ctrl+c
 
**Solution:**
```bash
ctrl+c
```
---

## 📋 Task 10: Kill the sleep job which is running in the background.

**Note:** First find the job id and then provide along with the kill command.
**Solution:**
```bash

jobs
kill %job-id-of-sleep
```

---

## 📋 Task 11: View Memory Usage

**Objective:** Display memory usage in human-readable format.  
**Solution:**
```bash
free -h
```

---

## 📋 Task 12: Check System Uptime

**Objective:** Display how long the system has been running.  
**Solution:**
```bash
uptime
```
---

## 📋 Task 13: View Detailed Hardware Information

**Objective:** Use `dmidecode` to view system hardware info.  
**Solution:**
```bash
sudo dmidecode | less
# or narrow it down:
sudo dmidecode -t processor
sudo dmidecode -t memory
```

---

## 📋 Task 14: Read CPU Information from /proc

**Objective:** Display detailed CPU info from `/proc/cpuinfo`.  
**Solution:**
```bash
cat /proc/cpuinfo
```

---

## 📋 Task 15: Read Memory Information from /proc

**Objective:** Display memory-related info from `/proc/meminfo`.  
**Solution:**
```bash
cat /proc/meminfo
```
---
---

## 💾 Disk Usage & Filesystem Monitoring Tasks

### 📋 Task 16: Check Disk Space Usage of All Mounted Filesystems

**Objective:** View overall disk space usage in human-readable format.  
**Solution:**
```bash
df -h
```

---

### 📋 Task 17: View Inodes Usage on Filesystems

**Objective:** Display inode usage (important for file-heavy systems).  
**Solution:**
```bash
df -i
```

---

### 📋 Task 18: Check Disk Usage of a Directory

**Objective:** Show the total disk usage of `/var/log` in human-readable form.  
**Solution:**
```bash
du -sh /var/log
```

---

### 📋 Task 19: Show Disk Usage of Each Subdirectory

**Objective:** Show how much space each subdirectory in `/home` consumes.  
**Solution:**
```bash
du -h --max-depth=1 /home
```

---

### 📋 Task 20: Display Disk Mount Information

**Objective:** List all mounted filesystems with type and mount options.  
**Solution:**
```bash
mount
```

---

### 📋 Task 21: Check Filesystem Type of a Mount

**Objective:** Identify the filesystem type of `/` (root).  
**Solution:**
```bash
df -T /
```

---

### 📋 Task 22: List All Disks and Partitions

**Objective:** View available disks and partitions with sizes.  
**Solution:**
```bash
lsblk
```

---
