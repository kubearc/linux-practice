# 🔗 Linux Tasks Using find, du, df, locate, grep, mount, and Links

This document contains practical tasks using essential Linux commands: `find`, `du`, `df`, `locate`, `grep`, `mount`, and handling of hard and soft links.

---

## ✅ 1. `find` – Search for Files and Directories

### Task: Find all `.log` files modified in the last 7 days in `/var/log`

```bash
find /var/log -name "*.log" -mtime -7
````

### Task: Find all symbolic links in `/home`

```bash
find /home -type l
````

---

## ✅ 2. `du` – Check Disk Usage

### Task: Show size of each subdirectory in `/home`

```bash
du -h --max-depth=1 /home
````

### Task: Show size of a directory without following symlinks

````bash
```bash
du -h --no-dereference /path/to/symlink
````

---

## ✅ 3. `df` – Report Disk Space Usage

### Task: Show disk space usage in human-readable format

````bash
```bash
df -h
````

### Task: Show space used by the root partition

```bash
df -h /
````

---

## ✅ 4. `locate` – Quickly Find Files

### Task: Locate all `.conf` files on the system
```bash
locate "*.conf"
````

### Task: Find the location of the `passwd` file
```bash
locate passwd
````

---

## ✅ 5. `grep` – Search Text in Files

### Task: Find lines containing the word "error" in a log file
```bash
grep "error" /var/log/syslog
````

### Task: Search for a username in the `/etc/passwd` file
```bash
grep "^user" /etc/passwd
````

---

## ✅ 6. `mount` – Mount a Filesystem

### Task: Mount a USB drive to `/mnt/usb`

````bash
```bash
sudo mount /dev/sdb1 /mnt/usb
````

### Task: View all currently mounted filesystems
```bash
mount
````

---

# 🔗 Tasks for Hard and Soft Links

## ✅ Task 1: Create a Soft (Symbolic) Link to a File

### Step 1: Create Directory and File
```bash
mkdir -p ~/linkdemo/task1
cd ~/linkdemo/task1
echo "This is file1" > file1.txt
````

### Step 2: Create Soft Link
```bash
ln -s file1.txt softlink_to_file1.txt
````

### Step 3: Verify
```bash
ls -l
````

---

## ✅ Task 2: Create a Hard Link to a File

### Step 1: Create Directory and File

```bash
mkdir -p ~/linkdemo/task2
cd ~/linkdemo/task2
echo "This is file2" > file2.txt
````

### Step 2: Create Hard Link

```bash
ln file2.txt hardlink_to_file2.txt
````

### Step 3: Check Inodes


```bash
ls -li file2.txt hardlink_to_file2.txt
````

---

## ✅ Task 3: Create a Symbolic Link to a Directory

### Step 1: Create Directory and File Inside It


```bash
mkdir -p ~/linkdemo/task3/original_dir
cd ~/linkdemo/task3
touch original_dir/sample.txt
````

### Step 2: Create Symbolic Link to Directory


```bash
ln -s original_dir symlink_to_dir
````

### Step 3: Verify

```bash
ls -l
````

---

## ✅ Task 4: Test Behavior When Original File is Deleted

### Step 1: Create Directory and File

```bash
mkdir -p ~/linkdemo/task4
cd ~/linkdemo/task4
echo "Important data" > original.txt
````

### Step 2: Create Hard and Soft Links

```bash
ln -s original.txt symlink.txt
ln original.txt hardlink.txt
````

### Step 3: Delete Original File

```bash
rm original.txt
````

### Step 4: Test Both Links

```bash
cat symlink.txt       # This will fail (broken link)
cat hardlink.txt      # This will still work
````

---

## ✅ Task 5: Find All Symbolic Links in a Directory

### Step 1: Create Directory and Files

```bash
mkdir -p ~/linkdemo/task5
cd ~/linkdemo/task5
echo "test" > testfile.txt
ln -s testfile.txt link1.txt
ln -s /bin /usr_linked_bin
````

### Step 2: Find All Symbolic Links


```bash
find . -type l
````

---
