
# 🧪 Linux Commands Practice Test (chmod, chown, umask)


This document provides a hands-on practice set for essential Linux file management commands: `chmod`, `chown`, and `umask`.

---
### Create a directory with the named permission practice test 
```bash 
mkdir /home/student/permision-practice-test 
```
### Make sure your present Working directory is /home/student/permision-practice-test

## 📁 Section A: chmod Tasks

### 1. Create a file `notes.txt`, then give the owner full permissions, and read-only for group and others.
```bash
touch notes.txt
chmod 744 notes.txt
```

### 2. Create a file `app.sh`, then remove execute permission for group and others.
```bash
touch app.sh
chmod go-x app.sh
```

### 3. Create a file `secret.key`, then make it accessible only to the owner.
```bash
touch secret.key
chmod 700 secret.key
```

### 4. Create a directory `scripts/`, then add execute permission for others.
```bash
mkdir scripts
chmod o+x scripts/
```

### 5. Create a file `test.c`, then make it read-only for everyone.
```bash
touch test.c
chmod 444 test.c
```

### 6. Create a directory `bin/`, then make all files in it executable by the owner.
```bash
mkdir bin
chmod u+x bin/*
```

### 7. Create some `.conf` files, then remove all permissions for others from `.conf` files.
```bash
touch file1.conf file2.conf
chmod o= *.conf
```

### 8. Create a file `db.sqlite`, then set permissions: owner=rwx, group=r--, others=none.
```bash
touch db.sqlite
chmod 740 db.sqlite
```

### 9. Create `.sh` files, then make them executable by everyone.
```bash
touch script1.sh script2.sh
chmod a+x *.sh
```

### 10. Create a file `final.txt`, then set it as read-only for all.
```bash
touch final.txt
chmod 444 final.txt
```

---

## 👤 Section B: chown Tasks

### 11. Create a file `project.txt`, then change owner of `project.txt` to `alex`.
```bash
touch project.txt
chown alex project.txt
```

### 12. Create a directory `project/` with files inside, then recursively change owner and group to `devuser:devgroup`.
```bash
mkdir -p project
touch project/file1 project/file2
chown -R devuser:devgroup project/
```

### 13. Create a file `file.log`, then change group of `file.log` to `admins`.
```bash
touch file.log
chown :admins file.log
```

### 14. Create a file `backup.tar.gz`, then change owner of `backup.tar.gz` to `root`.
```bash
touch backup.tar.gz
chown root backup.tar.gz
```

### 15. Create a directory `/var/www/html`, then change ownership of `/var/www/html` and its contents to `webadmin:www-data`.
```bash
sudo mkdir -p /var/www/html
sudo chown -R webadmin:www-data /var/www/html
```

### 16. Create files `file1`, `file2`, and `file3`, then assign `john` ownership.
```bash
touch file1 file2 file3
chown john file1 file2 file3
```

### 17. Create `.txt` files, then set group `students` for all `.txt` files.
```bash
touch file1.txt file2.txt
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
