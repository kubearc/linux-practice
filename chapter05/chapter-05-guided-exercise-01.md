1. Login with root user on the system
2. Create a user kubearc with password 123
3. Run following commands
```bash
id
echo $HOME
echo $PATH
whoami
```
4. Login with test user
```bash
su test
```
5. Run following commands
```bash
id
```
6. Now logout from test user and get back to root user
```bash
exit
```
7. Create a group named poet with ID 15000
```bash
groupadd -g 15000 poet
```
8. Create another group called artist
```bash
groupadd artist
```
9. Create a user `sam` with password `123`
```bash
useradd sam
passwd sam
```

10. Create a user `dean` with password `123`
```bash
useradd dean
passwd dean
```

11. Create a user `bob` with password `123`
```bash
useradd bob
passwd bob
```

12. Create a user `alice` with password `123`
```bash
useradd alice
passwd alice
```

13. Add `sam` user to `poet` group as a supplementary group
```bash
usermod -aG poet sam
```

14. Add `dean` user to `poet` group as a primary group
```bash
usermod -g poet dean
```

15. Add `bob` user to `artist` group as a secondary group
```bash
usermod -aG artist bob
```

16. Add `alice` user to `artist` group as a secondary group
```bash
usermod -aG artist alice
```

17. Check the group configuration file and view group entries
```bash
cat /etc/group
```

18. Modify the home directory of `bob` to `/home/poet`
```bash
usermod -d /home/poet bob
```

19. Modify the home directory of `alice` to `/home/artist`
```bash
usermod -d /home/artist alice
```

20. Lock the `alice` user account
```bash
usermod -L alice
```

21. Change the password policy for `dean` so that the password expires every 60 days
```bash
chage -M 60 dean
```

22. Force password change for `bob` on first login
```bash
chage -d 0 bob
```


22. Force password change for bob user on very first login.
```bash
chage -d 0 bob
```
23. Login with bob user and set the password to linux
24. All newly created users must change the password every 45 days. Modify the PASS_MAC_DAYS to 45
```bash
vim /etc/login.defs

PASS_MAX_DAYS 45
PASS_MIN_DAYS 0
PASS_MIN_LEN 5
PASS_WARN_AGE 7
```
25. Test user should be able to run all super user commands without providing the password. Edit sudoers file and add line at end
```bash
vim /etc/sudoers
test ALL=(ALL) NOPASSWD:ALL
```
27. Bob dean user should be able to run fdisk -l command, but bob should be asked password before running this command with sudo.
```bash
vi /etc/sudoers
bob  ALL=(ALL) PASSWD: /sbin/fdisk -l
```
28. Now login with dean user and try to run the fdisk -l command and then logout
```bash
su dean
sudo fdisk -l
exit
```
29. Add alice user to wheel account so that it can run all admin commands. 
```bash
usermod -aG wheel alice
```
30. Now login with alice user and try to run the admin commands and then logout
```bash
su alice
sudo useradd new
exit
```
31. Users which are part of poet group should be able to run all the super user commands.
```bash
vi /etc/sudoers
%poet ALL=(ALL) ALL
```
32. Try to run the admin commands with sam user which is part of poet group and then logout.
```bash
su sam
sudo useradd new1
exit
```
