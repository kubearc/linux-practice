
# Sudo Permission Practice Tasks

A list of Linux administration tasks focused on managing `sudo` permissions for users and groups.

---

## Task 1: Allow user `test` to run all commands without password

Create test user and set passwd as redhat.
```bash
useradd test
passwd test
```
Edit the sudoers file using visudo:
```bash
visudo
```
Add at the end:
```bash
test ALL=(ALL) NOPASSWD:ALL
```

---

## Task 2: Allow user `devops` to restart `httpd` without a password
Create devops user and set passwd as redhat.
```bash
useradd devops
passwd devops
```
Edit the sudoers file:
```bash
visudo
```
Add:
```bash
devops ALL=(ALL) NOPASSWD: /bin/systemctl restart httpd
```

---

## Task 3: Allow user `bob` to run `fdisk -l` with password prompt
Create bob user and set passwd as redhat.
```bash
useradd bob
passwd redhat
```
Edit sudoers:
```bash
visudo
```
Add:
```bash
bob ALL=(ALL) PASSWD: /sbin/fdisk -l
```

---

## Task 4: Login as `dean` and run fdisk command
Create dean user and set passwd as redhat.
```bash
useradd dean
passwd dean
```
```bash
su - dean
sudo fdisk -l
exit
```

---

## Task 5: Add user `alice` to `wheel` group for full admin access
Create alice user and set passwd as redhat.
```bash
useradd alice
passwd alice
```
```bash
usermod -aG wheel alice
```

---

## Task 6: Login as `alice`, run admin command, then logout

```bash
su - alice
sudo useradd newuser
exit
```

---

## Task 7: Allow all users in group `poet` to run all commands

First create the poet group and then create sam user which is part of poet group.
```bash
groupadd poet
useradd -ag poet sam
```
Edit sudoers:
```bash
visudo
```
Add:
```bash
%poet ALL=(ALL) ALL
```

---

## Task 8: Run admin command as `sam` (member of `poet` group)

```bash
su - sam
sudo useradd poetadmin
exit
```

---

## Task 9: Allow group `netadmins` to run `/sbin/ifconfig` only
First create the `netadmins` group and then create `rose` user which is part of poet group.
```bash
groupadd netadmins
useradd -ag netadmins rose
```

Edit sudoers:
```bash
visudo
```
Add:
```bash
%netadmins ALL=(ALL) ALL=/sbin/ifconfig
```

---

## Task 10: Allow `ravi` to run `mount` and `umount` only
First reate the ravi user and set passwd as redhat.
```bash
useradd ravi
passwd ravi
```
Edit sudoers:
```bash
visudo
```
Add:
```bash
ravi ALL=(ALL) ALL= /bin/mount, /bin/umount
```

---
