
# 🧪 Linux Commands Practice Test (chmod, chown, umask)

This document provides a hands-on practice set for essential Linux file management commands: `chmod`, `chown`, and `umask`.

---

## 📁 Section A: chmod Tasks

### 1. Give the owner full permissions, and read-only for group and others on `notes.txt`.
```bash
chmod 744 notes.txt
```
¯
### 2. Remove execute permission for group and others from `app.sh`.
```bash
chmod go-x app.sh
```

### 3. Make `secret.key` accessible only to the owner.
```bash
chmod 700 secret.key
```

### 4. Add execute permission for others on directory `scripts/`.
```bash
chmod o+x scripts/
```

### 5. Make `test.c` read-only for everyone.
```bash
chmod 444 test.c
```

### 6. Make all files in `bin/` executable by the owner.
```bash
chmod u+x bin/*
```

### 7. Remove all permissions for others from `.conf` files.
```bash
chmod o= *.conf
```

### 8. Set `db.sqlite` permissions: owner=rwx, group=r--, others=none.
```bash
chmod 740 db.sqlite
```

### 9. Make `.sh` files executable by everyone.
```bash
chmod a+x *.sh
```

### 10. Set `final.txt` as read-only for all.
```bash
chmod 444 final.txt
```

---

## 👤 Section B: chown Tasks

### 11. Change owner of `project.txt` to `alex`.
```bash
chown alex project.txt
```

### 12. Recursively change owner and group of `project/` to `devuser:devgroup`.
```bash
chown -R devuser:devgroup project/
```

### 13. Change group of `file.log` to `admins`.
```bash
chown :admins file.log
```

### 14. Change owner of `backup.tar.gz` to `root`.
```bash
chown root backup.tar.gz
```

### 15. Change ownership of `/var/www/html` and its contents to `webadmin:www-data`.
```bash
sudo chown -R webadmin:www-data /var/www/html
```

### 16. Assign `john` ownership of `file1`, `file2`, and `file3`.
```bash
chown john file1 file2 file3
```

### 17. Set group `students` for all `.txt` files.
```bash
chown :students *.txt
```

---

## ⚙️ Section C: umask Tasks

### 18. Set default file permission to `rw-r-----` (640).
```bash
umask 027
```

### 19. Set umask so directories default to `rwxr-x---` (750).
```bash
umask 027
```

### 20. Temporarily change umask to `027` for current shell.
```bash
umask 027
```

### 21. Permanently set umask to `077` for user.
```bash
echo 'umask 077' >> ~/.bashrc
```

### 22. Set umask to allow files readable/writable only by owner.
```bash
umask 077
```

### 23. Set umask for: files → `rw-rw----`, dirs → `rwxrwx---`.
```bash
umask 007
```

### 24. Show current umask value.
```bash
umask
```

### 25. Reset umask to default value (usually 022).
```bash
umask 022
```

---

## ✅ How to Use

- Read each task carefully.
- Try to write the command yourself before revealing the solution.
- Copy the command from the bash block and test it in a real or virtual Linux environment.

---

## 📄 License

This content is available under the [MIT License](LICENSE).

---

## 🙋 Contributions Welcome

Feel free to submit PRs with more tasks, corrections, or additional sections like `find`, `tar`, or `cron`.
