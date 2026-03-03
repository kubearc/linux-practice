# RHCSA LVM Practice 

------------------------------------------------------------------------
> ⚠️ **Lab Requirement:** Before starting this LVM practice, ensure your VM has **3 additional disks** attached (e.g., /dev/vdb, /dev/vdc, /dev/vdd) besides the primary OS disk.

> ℹ️ **Note:** Disk names may vary depending on your system (e.g., /dev/sdb, /dev/vdb, /dev/nvme0n1). Replace the disk names in the tasks according to your environment.

------------------------------------------------------------------------
## Question 1

Create PV with name `/dev/vdb`, 
Create VG with name `vgdata`, 
Create LV with name `lvdata` (300M).
Mount at `/mnt/data` permanently.

### Solution

    pvcreate /dev/vdb
    vgcreate vgdata /dev/vdb
    lvcreate -n lvdata -L 300M vgdata
    mkfs.xfs /dev/vgdata/lvdata
    mkdir -p /mnt/data
    mount /dev/vgdata/lvdata /mnt/data
    blkid /dev/vgdata/lvdata
    vim /etc/fstab
    UUID=<UUID> /mnt/data xfs defaults 0 0
    mount -a

------------------------------------------------------------------------

## Question 2

Create 500M LVM using `/dev/vdc` and mount at `/storage`.

### Solution

    pvcreate /dev/vdc
    vgcreate vgstorage /dev/vdc
    lvcreate -n lvstorage -L 500M vgstorage
    mkfs.xfs /dev/vgstorage/lvstorage
    mkdir /storage
    mount /dev/vgstorage/lvstorage /storage

------------------------------------------------------------------------

## Question 3

Create two LVs in `vgdata`: 200M and 300M.

### Solution

    lvcreate -n lvbackup -L 200M vgdata
    lvcreate -n lvlogs -L 300M vgdata

------------------------------------------------------------------------

## Question 4

Create ext4 LV (400M) mounted at `/test`.

### Solution

    lvcreate -n lvtest -L 400M vgdata
    mkfs.ext4 /dev/vgdata/lvtest
    mkdir /test
    mount /dev/vgdata/lvtest /test

------------------------------------------------------------------------

## Question 5

Extend `lvdata` by 200M.

### Solution

    lvextend -L +200M /dev/vgdata/lvdata
    xfs_growfs /mnt/data

------------------------------------------------------------------------

## Question 6

Reduce ext4 LV from 600M to 400M.

### Solution

    umount /dev/vgdata/lvtest
    e2fsck -f /dev/vgdata/lvtest
    resize2fs /dev/vgdata/lvtest 400M
    lvreduce -L 400M /dev/vgdata/lvtest
    mount /dev/vgdata/lvtest /test

------------------------------------------------------------------------

## Question 7

Add `/dev/vdc` to `vgdata` and extend LV.

### Solution

    pvcreate /dev/vdc
    vgextend vgdata /dev/vdc
    lvextend -L +500M /dev/vgdata/lvdata
    xfs_growfs /mnt/data

------------------------------------------------------------------------

## Question 8

Rename `lvdata` to `lvproject`.

### Solution

    lvrename vgdata lvdata lvproject

------------------------------------------------------------------------

## Question 9

Remove `lvbackup` safely.

### Solution

    umount /backup
    lvremove /dev/vgdata/lvbackup

------------------------------------------------------------------------

## Question 10

Create LV using 10 extents.

### Solution

    vgcreate vgdev /dev/vdb
    lvcreate -n lvdev -l 10 vgdev

------------------------------------------------------------------------

## Question 11

Extend VG and create 400M LV.

### Solution

    vgextend vgdata /dev/vdc
    lvcreate -n lvextra -L 400M vgdata

------------------------------------------------------------------------

## Question 12

Extend LV online by 300M.

### Solution

    lvextend -L +300M /dev/vgdata/lvonline
    xfs_growfs /online

------------------------------------------------------------------------

## Question 13

Remove LV, VG, and PV safely.

### Solution

    umount /mnt/data
    lvremove /dev/vgdata/lvdata
    vgremove vgdata
    pvremove /dev/vdb
