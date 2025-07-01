# 🔪 Linux Practical Test – Final Version

### 👨‍💼 For Students – Beginner to Intermediate  
**Total Marks**: 65 (+5 Bonus)  
**Time**: 90 Minutes  
**Instructions**: Execute each task in the terminal. Marks are based on command accuracy, completeness, and clarity.

---

## 🔧 Task 1: Directory & File Management (10 Marks)

- Create a directory named `linux_test` in your home folder.
- Inside `linux_test`, create three files: `file1.txt`, `file2.txt`, and `script.sh`.
- Write "Welcome to Linux" inside `file1.txt`.
- Make a copy of `file1.txt` as `welcome.txt`.
- Move `file2.txt` to `/tmp`.



---

## 🔐 Task 2: User & Permissions (10 Marks)

- Create a user named `testuser`.
- Set a password for `testuser`.
- Create a group `interns` and add `testuser` to it.
- Create a file `secret.txt` and allow read-write for the owner only.
- Change the ownership of `secret.txt` to `testuser`.



---

## 🔎 Task 3: File Search & Filters (10 Marks)

- Find all `.conf` files under `/etc` and save the list to `conf_list.txt`.
- Search `/var/log` for files modified in the last 2 days.
- Count and display the number of `.log` files in `/var/log`.



---

## 💻 Task 4: Basic Networking (10 Marks)

- Display the system’s **IP address**.
- Display the system’s **hostname**.
- Test **internet connectivity** by pinging `google.com`.
- Add a static entry to `/etc/hosts` to map `test.local` to `127.0.0.1`.
- Create a **new network connection** named `lab-connection` with:
  - IP: `192.168.100.50/24`
  - Gateway: `192.168.100.1`
  - DNS: `8.8.8.8`
  - Interface: `eth0`
    *** Note replace the interface  with your systems interface *** 



---

## 💽 Task 5: Partitioning & Disk Management (15 Marks)

### 🔹 Part A: Basic Partition (5 Marks)
- List all available disks using `lsblk` or `fdisk -l`.
- Create a **100MB partition** using `fdisk` or `parted`.
- Format it with `ext4`.
- Mount it to `/mnt/testdisk`.
- Add an entry to `/etc/fstab` for auto-mounting.

### 🔹 Part B: LVM Setup (10 Marks)
- Create a **physical volume** on `/dev/sdb`.
- Create a **volume group** named `vg_test`.
- Create a **logical volume** `lv_data` of size 200MB.
- Format it using `ext4`.
- Mount it to `/mnt/lvdata`.
- Add it to `/etc/fstab` for auto-mounting.



---

## 💻 Task 6: Scripting & Scheduling (10 Marks)

- Write a script `sysinfo.sh` that prints:
  - Current user
  - Hostname
  - Date and time
- Make the script executable.
- Schedule it to run daily at 8 AM using cron.



---

## 🎯 Bonus Task (Optional – 5 Marks)

- Create a symbolic link to `script.sh` on your Desktop (`~/Desktop`).
- Show disk usage of `/home` in human-readable format.



---

