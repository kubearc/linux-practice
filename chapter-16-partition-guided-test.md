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

## ✅ Step 3: Create a new MBR partition on `/dev/sdb`
```bash
fdisk /dev/sdb
```
**Inside `fdisk`:**
- `n` → new partition  
- `p` → primary  
- `1` → partition number  
- `Enter` → accept default first sector  
- `Enter` → accept default last sector  
- `w` → write and exit

---

## ✅ Step 4: Reload partition table (if needed)
```bash
partprobe
```

---

## ✅ Step 5: Confirm new partition exists
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

## ✅ Step 9: Mount the partition
```bash
mount /dev/sdb1 /mnt/data
```

---

## ✅ Step 10: Check if it mounted correctly
```bash
df -h | grep sdb1
```

---

## ✅ Step 11: Set permissions for shared use
```bash
chmod 777 /mnt/data
```

---

## ✅ Step 12: Get UUID for fstab entry
```bash
blkid /dev/sdb1
```

---

## ✅ Step 13: Add entry to `/etc/fstab`
```bash
nano /etc/fstab
```
**Add line (replace `<UUID>`):**
```
UUID=<UUID>  /mnt/data  ext4  defaults  0 0
```

---

## ✅ Step 14: Test `fstab` without rebooting
```bash
umount /mnt/data
mount -a
```

---

## ✅ Step 15: Verify everything
```bash
mount | grep sdb1
ls -ld /mnt/data
```

---
