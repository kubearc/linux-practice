
# Guided Exercise: Managing Swap Partition 
---
> **Note:**
- You must be **root** to run these commands. Use `su -` to switch to root if needed.
- All commands assume you are running as root (no `sudo` prefixes).  
- Replace `/dev/sdb` and `/dev/sdb1` with your actual device names if different.
---

## Step 1: Identify Disks and Existing Partitions
```bash
lsblk
fdisk -l
```

---

## Step 2: Create a New Partition with `fdisk`

Assuming the target disk is `/dev/sdb`:

```bash
fdisk /dev/sdb
```

Inside `fdisk`, type the following commands:

- `n` (new partition)  
- `p` (primary)  
- Partition number: press Enter (default, e.g., 1)  
- First sector: press Enter (default)  
- Last sector: type `+1G` (for a 1GB partition)  
- `t` (change partition type)  
- Type `82` (Linux swap)  
- `w` (write changes and exit)

---

## Step 3: Inform Kernel About Partition Changes
```bash
partprobe /dev/sdb
```

---

## Step 4: Format the Partition as Swap
```bash
mkswap /dev/sdb1
```

---

## Step 5: Enable the Swap Partition
```bash
swapon /dev/sdb1
swapon --show
free -h
```

---

## Step 6: Make Swap Permanent

Get the UUID of the swap partition:

```bash
blkid /dev/sdb1
```

Edit `/etc/fstab` using **vim** text editor 
```bash
vim /etc/fstab
```

Add this line to the end of the file (replace `UUID=...` with your actual UUID):

```
UUID=your-uuid none swap sw 0 0
```

---

## Step 7: Verify After Reboot

```bash
reboot
```

After reboot, check that swap is active:

```bash
swapon --show
free -h
```

---

## Optional: Switch to Root User

If you are not root, switch to root with:

```bash
su -
```

---
