# 🧪 LVM Practice Test
---
## 🛠️ Prerequisites
- RHEL 9 system (physical or virtual)
- At least **two additional empty disks** attached (e.g., `/dev/sdb` and `/dev/sdc`)
- All the tasks should be done from User "root"

---

## 🧺 Part 1: Create a Physical Volume (PV)

### Task:
```bash
lsblk
pvcreate /dev/sdb /dev/sdc
```

### Verify:
```bash
pvs
pvdisplay
```

---

## 🧺 Part 2: Create a Volume Group (VG)

### Task:
```bash
vgcreate vg_test /dev/sdb /dev/sdc
```

### Verify:
```bash
vgs
vgdisplay vg_test
```

---

## 🧺 Part 3: Create Logical Volumes (LVs)

### Task:
```bash
lvcreate -L 1G -n lv_data vg_test
lvcreate -l 100%FREE -n lv_extra vg_test
```

### Verify:
```bash
lvs
lvdisplay
```

---

## 🧺 Part 4: Format and Mount LVs

### Task:
```bash
mkfs.ext4 /dev/vg_test/lv_data
mkdir /mnt/data
mount /dev/vg_test/lv_data /mnt/data
```
## 🧺 Part 5: Make the Mount Permanent 
```bash
vim /etc/fstab
```

### Add this line 
/dev/vg_test/lv_data /mnt/data ext4 defaults 0 0"

### Verify:
```bash
df -h
mount | grep lv_data
cat /etc/fstab
```

---

## 🧺 Part 6: Resize Logical Volume

### Task:
```bash
lvextend -L +500M /dev/vg_test/lv_data
resize2fs /dev/vg_test/lv_data
```

### Verify:
```bash
lvdisplay /dev/vg_test/lv_data
df -h /mnt/data
```

---

## 🧺 Part 7: Remove LVM Setup

### Task:
```bash
umount /mnt/data
lvremove /dev/vg_test/lv_data
lvremove /dev/vg_test/lv_extra
vgremove vg_test
pvremove /dev/sdb /dev/sdc
```

---
