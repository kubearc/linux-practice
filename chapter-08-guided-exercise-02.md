## Chapter 08 - Package management in Linux -  Guided Exercise 02

1. List all the available packages with yum
```bash
yum list available
```
2. List all the installed packages with yum
```bash
yum list installed
```
3. List installed and available packages with yum
```bash
yum list all
```
4. To list a particular package, replace httpd with package name
```bash
yum list httpd
```
5. To list all packages groups.
```bash
yum grouplist
```
6. To install a package group
```bash
yum groupinstall group-name
```
7. To check info about a package group
```bash
yum groupinfo "Compatibility Libraries"
```
4. Check yum history and get info about a history transaction.
```bash
yum history
yum history info 3
```
5. Undo yum history
```bash
yum history undo 6
```
6. Check package info with rpm command. First grep the kernel package vesion which is installed on the system.
```bash
rpm -qa|grep kernel
kernel-tools-libs-5.14.0-503.11.1.el9_5.aarch64
kernel-modules-core-5.14.0-503.11.1.el9_5.aarch64
kernel-core-5.14.0-503.11.1.el9_5.aarch64
kernel-modules-5.14.0-503.11.1.el9_5.aarch64
kernel-tools-5.14.0-503.11.1.el9_5.aarch64
kernel-5.14.0-503.11.1.el9_5.aarch64
```
7. Now provide the package version in below command
```bash
rpm -qi kernel-5.14.0-503.11.1.el9_5.aarch64
```
8. List all files included in a package.
```bash
rpm -ql kernel-5.14.0-503.11.1.el9_5.aarch64
```
9. Install a single package `zsh` with rpm command. Go to /dvd/BaseOS/Packages directory. Find the zsh package.
```bash
cd /dvd/BaseOS/Package
ll|grep zsh
-r--r--r--. 1 root root   3374533 Apr 24 16:03 zsh-5.8-9.el9.aarch64.rpm
```
10. Now install it with rpm command.
```bash
rpm -ivh  zsh-5.8-9.el9.aarch64.rpm
```
11. Now check with info about zsh package with rpm command.
```bash
# rpm -qi zsh
Name        : zsh
Version     : 5.8
Release     : 9.el9
Architecture: aarch64
Install Date: Fri 25 Apr 2025 03:52:21 PM IST
Group       : Unspecified
Size        : 9442011
License     : MIT
Signature   : RSA/SHA256, Thu 24 Feb 2022 09:29:13 PM IST, Key ID 199e2f91fd431d51
Source RPM  : zsh-5.8-9.el9.src.rpm
Build Date  : Wed 23 Feb 2022 08:37:31 PM IST
Build Host  : arm64-034.build.eng.bos.redhat.com
Packager    : Red Hat, Inc. <http://bugzilla.redhat.com/bugzilla>
Vendor      : Red Hat, Inc.
URL         : http://zsh.sourceforge.net/
Summary     : Powerful interactive shell
Description :
```
12. Now remove the zsh package with rpm command. First list all the packages and grep the zsh package.
```bash
rpm -qa|grep zsh
zsh-5.8-9.el9.aarch64
```
13. Now remove the zsh by providing the package name.
```bash
rpm -evh zsh-5.8-9.el9.aarch64
```
