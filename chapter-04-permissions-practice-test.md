
# 🧪 Linux Commands Practice Test (chmod, chown, umask)

This document provides a hands-on practice set for essential Linux file management commands: `chmod`, `chown`, and `umask`.

---

## 📁 Section A: chmod Tasks

### 1. Create a file `/home/user/notes.txt`, then give the owner full permissions, and read-only for group and others.
```bash
touch /home/user/notes.txt
chmod 744 /home/user/notes.txt
```

### 2. Create a file `/home/user/app.sh`, then remove execute permission for group and others.
```bash
touch /home/user/app.sh
chmod go-x /home/user/app.sh
```

### 3. Create a file `/home/user/secret.key`, then make it accessible only to the owner.
```bash
touch /home/user/secret.key
chmod 700 /home/user/secret.key
```

### 4. Create a directory `/home/user/scripts/`, then add execute permission for others.
```bash
mkdir /home/user/scripts
chmod o+x /home/user/scripts/
```

### 5. Create a file `/home/user/test.c`, then make it read-only for everyone.
```bash
touch /home/user/test.c
chmod 444 /home/user/test.c
```

### 6. Create a directory `/home/user/bin/`, then make all files in it executable by the owner.
```bash
mkdir /home/user/bin
chmod u+x /home/user/bin/*
```

### 7. Create some `.conf` files in `/home/user/`, then remove all permissions for others from `.conf` files.
```bash
touch /home/user/file1.conf /home/user/file2.conf
chmod o= /home/user/*.conf
```

### 8. Create a file `/home/user/db.sqlite`, then set permissions: owner=rwx, group=r--, others=none.
```bash
touch /home/user/db.sqlite
chmod 740 /home/user/db.sqlite
```

### 9. Create `.sh` files in `/home/user/`, then make them executable by everyone.
```bash
touch /home/user/script1.sh /home/user/script2.sh
chmod a+x /home/user/*.sh
```

### 10. Create a file `/home/user/final.txt`, then set it as read-only for all.
```bash
touch /home/user/final.txt
chmod 444 /home/user/final.txt
```

---

## 👤 Section B: chown Tasks

### 11. Create a file `/home/user/project.txt`, then change owner of `/home/user/project.txt` to `alex`.
```bash
touch /home/user/project.txt
chown alex /home/user/project.txt
```

### 12. Create a directory `/home/user/project/` with files inside, then recursively change owner and group to `devuser:devgroup`.
```bash
mkdir -p /home/user/project
touch /home/user/project/file1 /home/user/project/file2
chown -R devuser:devgroup /home/user/project/
```

### 13. Create a file `/home/user/file.log`, then change group of `/home/user/file.log` to `admins`.
```bash
touch /home/user/file.log
chown :admins /home/user/file.log
```

### 14. Create a file `/home/user/backup.tar.gz`, then change owner of `/home/user/backup.tar.gz` to `root`.
```bash
touch /home/user/backup.tar.gz
chown root /home/user/backup.tar.gz
```

### 15. Create a directory `/var/www/html/`, then change ownership of `/var/www/html/` and its contents to `webadmin:www-data`.
```bash
sudo mkdir -p /var/www/html
sudo chown -R webadmin:www-data /var/www/html
```

### 16. Create files `/home/user/file1`, `/home/user/file2`, and `/home/user/file3`, then assign `john` ownership.
```bash
touch /home/user/file1 /home/user/file2 /home/user/file3
chown john /home/user/file1 /home/user/file2 /home/user/file3
```

### 17. Create `.txt` files in `/home/user/`, then set group `students` for all `.txt` files.
```bash
touch /home/user/file1.txt /home/user/file2.txt
chown :students /home/user/*.txt
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

---

## 🙋 Contributions Welcome

Feel free to submit PRs with more tasks, corrections, or additional sections like `find`, `tar`, or `cron`.
