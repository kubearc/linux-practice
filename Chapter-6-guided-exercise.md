## Linux Network Configuration

Perform static network configuration as per below configuration.

The following table outlines the static network configuration settings for a Linux machine using tools like `nmcli`, `nmtui`, or by editing connection files directly.

| Setting           | Value               |
|------------------|---------------------|
| IP Address        | `192.168.0.15/24`   |
| Gateway           | `192.168.0.1`       |
| DNS Server        | `192.168.0.99`      |
| Domain            | `example.com`       |
| Hostname          | `test.example.com`  |
| Autoconnect       | `yes`               |
| Connection Name   | `test`              |

---

Run below command to set the IP, DNS and Gateway

```bash
nmcli con add con-name test ifname ens* type ethernet ipv4.address 192.168.0.15/24 ipv4.gateway 192.168.0.1 ipv4.dns 192.168.0.99 autoconnect yes
```
Activate the test connection
```bash
nmcli conn up test
```
Check IP and DNS configuration
```bash
nmcli conn show
nmcli conn show test
ifconfig
cat /etc/resolv.conf
```
Set hostname with below command
```bash
hostnamectl set-hostname test.example.com
```
Close the terminal and then open again
```bash
exit
```
Now open the terminal and check the hostname configuration
```bash
hostname
cat /etc/hostname
```
Check the DNS configuration
```bash
cat /etc/resolv.conf
```
Now create 1 more network connection with following configuration.

## DHCP with Domain and Hostname (`test3`)

| Setting           | Value               |
|------------------|---------------------|
| Connection Name   | `test2`             |
| IP Method         | `auto` (DHCP)       |
| Domain            | `example.com`       |
| Autoconnect       | `yes`               |

Create the connection and then activate the connection
```bash
nmcli conn add con-name test2 ifname ens* type ethernet autoconnect yes ipv4.method auto
nmcli conn up test2
```
Check the IP address configuration
```bash
nmcli conn show
nmcli conn show test2
ifconfig
```
Check the DNS configuration
```bash
cat /etc/resolv.conf
```
Now check which connection is activated.
```bash
nmcli conn show
```
If test2 is activated now activate the test connection
```bash
nmcli conn up test
```
Now check the IP address changes
```
ifconfig
cat /etc/resolv.conf
```
