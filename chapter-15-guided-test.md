
# MariaDB Step-by-Step Practice Guide on RHEL 9

---

## Step 1: Install MariaDB
Open your terminal and run:
```bash
yum install mariadb* -y
```
Open your terminal and run:
```bash
systemctl enable --now mariadb.service
```
Check if it’s running:
```bash
systemctl status mariadb.service
```

---

## Step 2: Secure MariaDB Installation

```bash
sudo mysql_secure_installation
```

Answer the prompts:

- Set root password? → Yes/no 
- Remove anonymous users? → Yes/no  
- Disallow root login remotely? → Yes/no 
- Remove test database? → Yes/no  
- Reload privilege tables? → Yes/no  

---

## Step 3: Log in as Root User

```bash
sudo mysql -u root -p
```

Enter the root password you set.

---

## Step 4: Create a New Database

```sql
CREATE DATABASE company;
```
It will create the database 

Now Use that database
```sql
USE company;
```

---

## Step 5: Create a Table

```sql
CREATE TABLE employees (id INT,first_name VARCHAR(50),last_name VARCHAR(50),email VARCHAR(100));
```

---

## Step 6: Insert Sample Records

```sql
INSERT INTO employees (first_name, last_name, email) VALUES ('Alice', 'Smith', 'alice@example.com'), ('Bob', 'Jones', 'bob@example.com');
```

---

## Step 7: View the Records

```sql
SELECT * FROM employees;
```

---

## Step 8: Create a New User

```sql
CREATE USER 'john'@'localhost' IDENTIFIED BY 'john123';
```

---

## Step 9: Grant Privileges to the New User

```sql
GRANT ALL PRIVILEGES ON company.* TO 'john'@'localhost';
```
Now apply the changes 
```sql
FLUSH PRIVILEGES;
```

---

## Step 10: Exit MariaDB

```sql
EXIT;
```

---

## Step 11: Log in as New User

```bash
mysql -u john -p
```

Enter password: `john123`

Then:

```sql
USE company;
SELECT * FROM employees;
```

---

## Step 12: Update a Record

```sql
UPDATE employees SET email = 'alice.new@example.com' WHERE first_name = 'Alice';
```

---

## Step 13: Delete a Record

```sql
DELETE FROM employees WHERE first_name = 'Bob';
```

---

## Step 14: Add a New Column to the Table

```sql
ALTER TABLE employees ADD phone VARCHAR(20);
```

---

## Step 15: Backup the Database

```bash
mysqldump -u root -p company > ~/company_backup.sql
```
## Step 16: Send the backup file to node 2
```bash
scp ~/company_backup.sql  root@node2.example.com:/root
```
---

## Step 17: Restore the Database
### On Node2 Install Database by following Step1&2

After installation Create the database:

```bash
mysql -u root -p -e "CREATE DATABASE company;"
```

Restore databse from company_backup.sql

```bash
mysql -u root -p company < ~/company_backup.sql
```
## Step 18: Login in database
```bash
mysql -u root -p
```
## Step 19: Check the restored database
```sql
SELECT * FROM employees;
```
---

