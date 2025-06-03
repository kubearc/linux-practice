# 🧪 Guided Partitioning Lab – 

> ⚠️ Ensure you are **root** when performing these steps.  
> Run: `su -` or log in as root.

---

## ✅ Step 1: List all disks and their partitions
```bash
lsblk
```

---

## ✅ Step 2: View partition table and free space on `/dev/sdb`
```bash
fdisk -l /dev/sdb
```

---

## ✅ Step 3: Verify that a /dev/sdb device is listed in lsblk. If yes then Create a new MBR partition of 100MB on `/dev/sdb`
```bash
lsblk
fdisk /dev/sdb
```
**Inside `fdisk`:**
- `n` → new partition  
- `p` → primary  
- `1` → partition number  
- `Enter` → accept default first sector  
- `+100M` → Type 100M and press enter  
- `w` → write and exit

---

## ✅ Step 4: Reload partition table (if needed)
```bash
partprobe
```

---

## ✅ Step 5: Confirm new partition /dev/sdb1 exists
```bash
lsblk
```

---

## ✅ Step 6: Format `/dev/sdb1` as ext4
```bash
mkfs.ext4 /dev/sdb1
```

---


## ✅ Step 8: Create mount directory
```bash
mkdir -p /mnt/data
```

---

## ✅ Step 9: Mount the partition and create some files in it.
```bash
mount /dev/sdb1 /mnt/data
touch /mnt/data/file{1..10}
```

---

## ✅ Step 10: Check if it mounted correctly
```bash
df -h | grep sdb1
```

---

## ✅ Step 11: Make an FSTAB entry to permanently mount it.
```bash
vim /etc/fstab
```
Add Below Entry, replace the partition ID with ID of newly created partition.
```bash
/dev/partition-id /mnt/data  ext4  defaults  0 0
```

---

## ✅ Step 12: Test `fstab` without rebooting
```bash
umount /mnt/data
mount -a
df -Th
lsblk
```

---

## ✅ Step 13: Verify that files created in **step 9** are there in /mnt/data
```bash
ls -l /mnt/data
```

---
