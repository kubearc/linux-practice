# Linux Permissions Practice: `chmod`, `chown`, and `umask`

This README provides a set of commands for practicing Linux file permission management using `chmod`, `chown`, and `umask`. These commands help you understand file security and access control on Unix-like systems.

---
## Note. Create a dir with the name of "/home/student/project" and do all work in that dir 
## 🔧 Setup and Practice Commands

### 1. Create a log file with owner-only access
```bash
touch ~/log.txt
chmod 600 ~/log.txt
```

### 2. Create a report file for owner and group editing
```bash
touch report.docx
chmod 760 report.docx
```

### 3. Create a script executable by everyone, writable by owner only
```bash
touch install.sh
chmod 755 install.sh
```

### 4. Create a secure private directory
```bash
mkdir ~/secure_data
chmod 700 ~/secure_data
```

### 5. Create a file and change ownership to student:developers
```bash
touch example.txt
sudo chown student:developers example.txt
```

### 6. Create a group-shared folder with full access
```bash
mkdir shared_folder
chmod 770 shared_folder
```

### 7. Set umask to restrict access for group and others
```bash
umask 077
```

### 8. Create a notes file readable by everyone, writable only by owner
```bash
touch notes.txt
chmod 644 notes.txt
```

### 9. Create a directory executable by everyone, writable only by owner
```bash
mkdir ~/scripts
chmod 711 ~/scripts
```

### 10. Set ownership and permissions for a group-specific script
```bash
touch run_tests.sh
sudo chown student:qa run_tests.sh
chmod 750 run_tests.sh
```

### 11. Set a secure umask for new files and directories
```bash
umask 0027
```

### 12. Create a read-only script for all users
```bash
touch readonly_script.sh
chmod 555 readonly_script.sh
```

### 13. Create a file with no permissions for anyone
```bash
touch confidential.doc
chmod 000 confidential.doc
```

### 14. Create a file with owner read/write and group read access
```bash
touch financial_data.csv
chmod 640 financial_data.csv
```

### 15. Create a public directory with full permissions
```bash
mkdir public_upload
chmod 777 public_upload
```

---

## ✅ Notes

- Use `ls -l` to verify permission settings.
- Use `id` to confirm current user and group.
- Always test your `umask` changes by creating new files after applying the command.

---

## 📂 Author

Prepared for Linux file permissions training and system administration practice.
