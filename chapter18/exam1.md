# RHCSA Practical Test – 2 Nodes
## Kubearc Academy

---

# Exam Instructions

- Total Time: 3 Hours
- Total Marks: 100
- Do not copy from other students
- Verify every task before submission
- Reboot system only if required
- Use proper Linux administration practices

---

# Environment Details

| Node | Hostname |
|---|---|
| Node 1 | servera.example.com |
| Node 2 | serverb.example.com |

---

# SECTION 1 — NETWORK CONFIGURATION (10 Marks)

## Task 1
Configure static networking on both nodes.

### Node 1

```bash
IP Address: 192.168.1.10/24
Gateway: 192.168.1.254
DNS: 8.8.8.8
Hostname: servera.example.com
```

### Node 2

```bash
IP Address: 192.168.1.20/24
Gateway: 192.168.1.254
DNS: 8.8.8.8
Hostname: serverb.example.com
```

---

## Task 2
Configure `/etc/hosts` on both nodes.

Verify communication between both nodes using ping.

---

# SECTION 2 — USER & GROUP MANAGEMENT (10 Marks)

## Task 3
On **Node 1** create the following users:

```bash
devuser
backupuser
```

Create the following groups:

```bash
developers
backupteam
```

Add:
- devuser → developers
- backupuser → backupteam

Set password for all users:

```bash
Redhat@123
```

---

## Task 4
Configure password aging for `devuser`.

Requirements:
- Maximum days: 45
- Minimum days: 7
- Warning before expiry: 5 days

---

# SECTION 3 — FILE PERMISSIONS & ACL (10 Marks)

## Task 5
Create the following directory on Node 1:

```bash
/projectdata
```

Requirements:
- Group owner should be `developers`
- Enable SGID bit
- Others should not have access

---

## Task 6
Create the following file:

```bash
/projectdata/data.txt
```

Provide read/write permission to `backupuser` using ACL.

---

# SECTION 4 — SSH CONFIGURATION (10 Marks)

## Task 7
Configure SSH key-based authentication from Node 1 to Node 2 for user:

```bash
devuser
```

Password authentication should not be required after setup.

---

## Task 8
Disable root login over SSH on Node 2.

Restart SSH service after configuration.

---

# SECTION 5 — STORAGE MANAGEMENT (15 Marks)

## Task 9
On Node 2:

Create a 1GB partition.

Format it with XFS filesystem.

Mount permanently on:

```bash
/backup
```

---

## Task 10
Create a 512MB swap partition.

Activate swap permanently.

---

# SECTION 6 — LVM MANAGEMENT (10 Marks)

## Task 11
On Node 2 create:

```bash
VG Name : vgdata
LV Name : lvbackup
Size    : 700MB
```

Mount the logical volume on:

```bash
/lvbackup
```

---

## Task 12
Extend logical volume `lvbackup` by 300MB without data loss.

---

# SECTION 7 — SERVICES & FIREWALL (10 Marks)

## Task 13
On Node 1:

Install and configure Apache HTTP server.

Create a webpage with the following content:

```html
Welcome to Kubearc Academy
```

---

## Task 14
Allow HTTP service permanently in firewall.

Verify website access from Node 2.

---

# SECTION 8 — SELINUX (10 Marks)

## Task 15
Create website directory:

```bash
/webdata
```

Move website content to `/webdata`.

Configure SELinux context properly so Apache can access the content.

---

# SECTION 9 — PROCESS MANAGEMENT & CRON (5 Marks)

## Task 16
Create the following process:

```bash
sleep 4000
```

Find the PID and terminate the process.

---

## Task 17
Create a cron job on Node 1.

Requirements:
- Execute every 5 minutes
- Save current date output to:

```bash
/var/log/time.log
```

---

# SECTION 10 — SHELL SCRIPTING (10 Marks)

## Task 18
Create the following shell script:

```bash
/root/systemreport.sh
```

The script should display:
- Hostname
- IP Address
- Logged-in users
- Memory usage
- Disk usage

Make the script executable and execute it successfully.

---

# BONUS TASKS (OPTIONAL – 10 Marks)

## Bonus 1
Transfer an archive file from Node 1 to Node 2 using `scp`.

---

## Bonus 2
Create Podman container on Node 2.

Requirements:
- Use nginx image
- Run in detached mode
- Expose port 8080

Verify access from Node 1.

---

# MARKING SCHEME

| Section | Marks |
|---|---|
| Network Configuration | 10 |
| Users & Groups | 10 |
| Permissions & ACL | 10 |
| SSH Configuration | 10 |
| Storage Management | 15 |
| LVM Management | 10 |
| Services & Firewall | 10 |
| SELinux | 10 |
| Process & Cron | 5 |
| Shell Scripting | 10 |
| Bonus | 10 |

---

# END OF PAPER
## Kubearc Academy
