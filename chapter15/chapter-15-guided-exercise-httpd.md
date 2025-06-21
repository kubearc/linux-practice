
# 🛠️ Practice Task: Set Up an Apache Web Server on Red Hat

## 🎯 Goal:
Deploy a simple HTML website using Apache HTTP Server on a Red Hat system.

---

## ✅ Task Steps:

### 1. Update the System
```bash
yum update -y
```

---

### 2. Install Apache (httpd)
```bash
yum install httpd -y
```

---

### 3. Enable and Start Apache
```bash
systemctl enable httpd
systemctl start httpd
```

---

### 4. Verify Apache Service
```bash
systemctl status httpd
```
You should see `active (running)`.

---

### 5. Configure Firewall
```bash
firewall-cmd --permanent --add-service=http
firewall-cmd --permanent --add-service=https
firewall-cmd --reload
```

---

### 6. Create a Simple Web Page
```bash
echo "<h1>Welcome to My Red Hat Web Server!</h1>" >> /var/www/html/index.html
```

---

### 7. Check Web Page in Browser
Open your browser and go to:
```
http://<your-server-ip>
```
You should see the "Welcome to My Red Hat Web Server!" message.

---

