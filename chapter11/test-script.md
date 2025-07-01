
## Create a File 
```bash
touch testscript.sh
```



## Add the below mentioned Script into the file "testscript.sh"


```bash
#!/bin/bash

echo "🔍 Checking Task 1: Directory & File Management"
[ -d ~/linux_test ] && echo "✅ Directory exists"
[ -f ~/linux_test/file1.txt ] && grep -q "Welcome to Linux" ~/linux_test/file1.txt && echo "✅ file1.txt exists and contains correct text"
[ -f ~/linux_test/welcome.txt ] && echo "✅ welcome.txt exists"
[ ! -f ~/linux_test/file2.txt ] && [ -f /tmp/file2.txt ] && echo "✅ file2.txt moved to /tmp"


echo "\n🔍 Checking Task 2: User & Permissions"
id testuser &>/dev/null && echo "✅ testuser exists"
grep interns /etc/group | grep testuser && echo "✅ testuser is in group interns"
[ -f ~/secret.txt ] && [ $(stat -c "%a" ~/secret.txt) == "600" ] && echo "✅ secret.txt has correct permissions"
[ $(stat -c "%U" ~/secret.txt) == "testuser" ] && echo "✅ secret.txt ownership correct"


echo "\n🔍 Checking Task 3: File Search"
[ -f conf_list.txt ] && echo "✅ conf_list.txt exists"
find /var/log -name "*.log" | wc -l


echo "\n🔍 Checking Task 4: Networking"
ip a | grep -q "192.168.100.50" && echo "✅ IP address assigned"
grep -q "test.local" /etc/hosts && echo "✅ test.local added to /etc/hosts"
nmcli con show lab-connection &>/dev/null && echo "✅ lab-connection exists"


echo "\n🔍 Checking Task 6: Scripting"
[ -f sysinfo.sh ] && [ -x sysinfo.sh ] && echo "✅ sysinfo.sh exists and is executable"


# Note: Task 5 (Partitioning & LVM) requires manual verification
# Bonus tasks can be checked as below:
echo "\n🔍 Checking Bonus Tasks"
[ -L ~/Desktop/script.sh ] && echo "✅ Symbolic link exists on Desktop"
du -sh /home
```

> 🔐 **Note:** Ensure the script runs as root or with appropriate permissions where needed.



## Run the Script 
``` bash
bash testscript.sh
```
