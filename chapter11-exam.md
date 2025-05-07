
# 🧪 Linux System Administration Test

## 🖥️ Systems: Node1 and Node2

> 📌 **Instructions**:
- Reset both nodes on the fresh snapshots.
- Perform each task on the specified node(s).
- Show all relevant commands and outputs.
- Avoid using `sudo` unless required.
- Use man pages if unsure.
- Time limit: **2 hours**.

---

## ✅ SECTION A: Users and Groups (Node1)

1. Create a new group called `devops`.
2. Add a user named `john` to the system and assign them to the `devops` group.
3. Set password `trootent` for the user `john`.
4. Create another user called `admin`, assign them a `/bin/bash` shell and a home directory at `/data/admin`.
5. Verify that both users exist and are members of the correct groups.

---

## ✅ SECTION B: File and Directory Permissions (Node1)

1. Create a directory `/shared/devops` and ensure:
   - It is owned by group `devops`
   - It has **setgid** permission so all new files belong to `devops`
   - It is readable and writable by group members only
2. Inside `/shared/devops`, create a file `readme.txt` as user `john` and restrict access so:
   - Only the owner has read and write permission
   - No one else can access the file

---

## ✅ SECTION C: systemctl Services Management (Node1)

1. Check the status of the `sshd` service.
2. Enable the `sshd` service to disable at boot.
3. Restart the service.
4. Mask the `chronyd` service and verify it cannot be started.

---

## ✅ SECTION D: YUM Package Management (Node1)

1. Configure local YUM server
2. Check if the `httpd` package is installed. If not, install it.
3. Remove the `wget` package if installed.
4. Clear the YUM cache.

---

## ✅ SECTION E: Networking (Node1 & Node2)

1. Set a static IP address `192.168.10.11/24` on Node1 and `192.168.10.12/24` on Node2.
2. Configure Node1 to use Node2 as its default gateway.
3. Verify connectivity using `ping` from Node1 to Node2.
4. Display the routing table on Node1.

---

## ✅ SECTION F: File Transfer: `scp` and `rsync` (Node1 & Node2)

1. On Node1, create a file `/home/john/testfile.txt`.
2. Use `scp` to copy it to Node2 under `/tmp`.
3. Modify `testfile.txt` on Node1, then use `rsync` to sync the changes to Node2.

---

## ✅ SECTION G: File Archiving with `tar` (Node1)

1. Archive the `/shared/devops` directory as `/tmp/devops_backup.tar.gz`.
2. List the contents of the archive without extracting.
3. Extract the archive to `/restore/devops`.

---

## ✅ SECTION H: Hostname Configuration

1. Set the hostname of Node1 to `training-node1` and Node2 to `training-node2`.
2. Verify the hostname changes persist after reboot.

---


