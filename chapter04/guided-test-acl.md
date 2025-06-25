
# 🧪 ACL Practice Task in RHEL (as root)
🖥️ Scenario:
You're logged in as root and need to configure Access Control Lists (ACLs) on a shared directory /project.

🎯 Objectives:
Create three users: alice, bob, and carol

Create a directory /project

Set ACLs:

alice → rwx

bob → r--

carol → r-x

Set default ACLs so all new files inherit these permissions

Verify ACL configuration using getfacl

✅ Commands to Execute (as root)
🔹 1. Create Users
```bash
useradd alice
useradd bob
useradd carol
```

🔹 2. Create Shared Directory
```bash
mkdir /project
chmod 770 /project
chown root:root /project
```

🔹 3. Set ACL Permissions
```bash
setfacl -m u:alice:rwx /project
setfacl -m u:bob:r-- /project
setfacl -m u:carol:rx /project
```

🔹 4. Set Default ACLs (for future files inside /project)
```bash
setfacl -d -m u:alice:rwx /project
setfacl -d -m u:bob:r-- /project
setfacl -d -m u:carol:rx /project
```

🔹 5. Verify ACLs
```bash
getfacl /project
```

✅ You should see something like:

```pgsql
# file: project
# owner: root
# group: root
user::rwx
user:alice:rwx
user:bob:r--
user:carol:r-x
group::---
mask::rwx
other::---
default:user:alice:rwx
default:user:bob:r--
default:user:carol:r-x
```
🧪 Bonus Check:

Create a test file:
```bash
touch /project/testfile.txt
ls -l /project/
getfacl /project/testfile.txt
```
Remove one ACL:
```bash
setfacl -x u:carol /project
```
----

### Section B

## ✅ Task 1: Basic ACL on Shared Directory

### Goal:
Create `/project` and assign ACLs:
- `alice` → rwx
- `bob` → r--
- `carol` → r-x
- Set default ACLs for new files.

### Commands:
```bash
useradd alice
useradd bob
useradd carol

mkdir /project
chmod 770 /project
chown root:root /project

setfacl -m u:alice:rwx /project
setfacl -m u:bob:r-- /project
setfacl -m u:carol:rx /project

setfacl -d -m u:alice:rwx /project
setfacl -d -m u:bob:r-- /project
setfacl -d -m u:carol:rx /project

getfacl /project
```

---

## ✅ Task 2: Group-Based ACL

### Goal:
Create `/repo`, assign `devs` group read-write access.

### Commands:
```bash
groupadd devs
mkdir /repo
chmod 770 /repo
chown root:devs /repo

setfacl -m g:devs:rwX /repo
setfacl -d -m g:devs:rwX /repo

getfacl /repo
```

---

## ✅ Task 3: ACL on a File

### Goal:
Create `/data/report.txt` and assign:
- `alice` → rwx
- `bob` → r--

### Commands:
```bash
mkdir /data
touch /data/report.txt

setfacl -m u:alice:rwx /data/report.txt
setfacl -m u:bob:r-- /data/report.txt

getfacl /data/report.txt
```

---

## ✅ Task 4: Copy File with ACL

### Goal:
Copy `/data/report.txt` to `/backup/` and retain ACLs.

### Commands:
```bash
mkdir /backup
cp -p --preserve=all /data/report.txt /backup/
getfacl /backup/report.txt
```

---

## ✅ Task 5: Remove All ACLs from File

### Goal:
Remove all ACLs from `/data/report.txt`.

### Commands:
```bash
setfacl -b /data/report.txt
getfacl /data/report.txt
```

---

## ✅ Task 6: Sticky Bit for Shared Directory

### Goal:
Create `/shared/` where users can’t delete each other's files.

### Commands:
```bash
mkdir /shared
chmod 1777 /shared
ls -ld /shared
```

Expected Output:
```bash
drwxrwxrwt 2 root root 4096 /shared
```
