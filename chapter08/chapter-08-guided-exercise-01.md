## Chaper 8 - Package management in Linux - Guided Exercise 1


1. Mount the RHEL DVD to Node1 machine.
2. Check the Mounted DVD with DF command.
```bash
df -h
```
2. Create the `/dvd` folder and copy the `Appstream` and `BasesOS` directories into /dvd.

Note:- Dont copy paste the RHEL-9-5-0 directories from below output, instead copy it from `df` command executed in 2nd step and provide in below command. 
```bash
mkdir /dvd
cp -rv /run/media/root/RHEL-9-5-0-BaseOS-x86_64/AppStream /dvd
cp -rv /run/media/root/RHEL-9-5-0-BaseOS-x86_64/BaseOS /dvd
```
3. Create the appstream repo file.
```bash
vim /etc/yum.repos.d/appstream.repo
[AppStream]
name=AppStream
baseurl=file:///dvd/AppStream
enabled=1
gpgcheck=0
```
4. Create the baseos repo file.
```bash
vim /etc/yum.repos.d/baseos.repo
[BaseOS]
name=BaseOS
baseurl=file:///dvd/BaseOS
enabled=1
gpgcheck=0
```
5. Now check that repositories are working and showing the packages properly.
```bash
yum clean all
yum repolist
yum repolist -v
```
6. Try to install the httpd package.
```bash
yum install httpd
```
7. Try to remove the httpd package
```bash
yum remove httpd
```
8. Try to update the kernel package.
```bash
yum update kernel
```
9. Check info about a package.
```bash
yum info kernel
```
