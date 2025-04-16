# Static IP Configuration for Node1 and Node2

This guide provides the steps to configure static IP addresses, DNS, gateway, and hostnames on two Linux host machines using `nmcli`. It also includes how to update `/etc/hosts` for proper name resolution.

---

## 🧾 Configuration Table

| Field             | Node 1                          | Node 2                          |
|------------------|----------------------------------|----------------------------------|
| Connection Name  | lab                              | lab                              |
| IP Address       | 192.168.1.10/24                  | 192.168.1.11/24                  |
| DNS              | 192.168.1.15                     | 192.168.1.15                     |
| Gateway          | 192.168.1.1                      | 192.168.1.1                      |
| Autoconnect      | yes                              | yes                              |
| Hostname         | node1.example.com                | node2.example.com                |

---

## ⚙️ Steps for Configuration. 
📌 Notes
Replace eth0 with your actual network interface name if it differs.

### 🔹 On Node 1

```bash
nmcli con add type ethernet con-name lab ifname eth0 ipv4.addresses 192.168.1.10/24 ipv4.gateway 192.168.1.1 ipv4.dns 192.168.1.15 ipv4.method manual autoconnect yes
nmcli con up lab
hostnamectl set-hostname node1.example.com
```
Verify hostname and ipaddress on node1.

```bash
bash
cat /etc/hostname
hostname
```

### 🔹 On Node 2
```bash
nmcli con add type ethernet con-name lab ifname eth0 ipv4.addresses 192.168.1.11/24 ipv4.gateway 192.168.1.1 ipv4.dns 192.168.1.15 ipv4.method manual autoconnect yes
nmcli con up lab
hostnamectl set-hostname node2.example.com
```
Verify hostname and ipaddress on node2.
```bash
bash
cat /etc/hostname
hostname
```
### 🧩 Edit /etc/hosts on Both Nodes
Append the following lines to the /etc/hosts file on both Node1 and Node2:
```bash
192.168.1.10 node1.example.com node1
192.168.1.11 node2.example.com node2
```
