# Run script as below on particular nodes.
```bash
bash script.sh node1
bash script.sh node2
```
- Belos is the script.

```bash
#!/bin/bash

NODE="$1"
RESULTS=()
TOTAL=0
PASSED=0

check() {
  DESC="$1"
  CMD="$2"
  EXPECTED="$3"
  
  OUTPUT=$(eval "$CMD" 2>/dev/null)
  
  ((TOTAL++))
  
  if echo "$OUTPUT" | grep -q "$EXPECTED"; then
    RESULTS+=("$(tput setaf 2)[PASS]$(tput sgr0) $DESC")
    ((PASSED++))
  else
    RESULTS+=("$(tput setaf 1)[FAIL]$(tput sgr0) $DESC")
  fi
}

check_node1() {
  echo "Running checks for Node1..."

  # SECTION A: Users and Groups
  check "Group 'devops' exists" "getent group devops" "devops"
  check "User 'john' exists" "id john" "john"
  check "User 'john' is in 'devops'" "id john" "devops"
  check "User 'admin' exists with /bin/bash" "getent passwd admin" "/bin/bash"
  check "User 'admin' home is /data/admin" "getent passwd admin" "/data/admin"

  # SECTION B: Permissions
  check "/shared/devops exists" "[ -d /shared/devops ] && ls -ld /shared/devops" "devops"
  check "Setgid on /shared/devops" "stat -c %A /shared/devops" "s"
  check "readme.txt permission is 600" "stat -c %a /shared/devops/readme.txt" "600"

  # SECTION C: systemctl
  check "sshd service is active" "systemctl is-active sshd" "active"
  check "sshd is disabled at boot" "systemctl is-enabled sshd" "disabled"   # Modified to PASS when disabled
  check "chronyd is masked" "systemctl is-enabled chronyd" "masked"

  # SECTION D: YUM
  check "httpd is installed" "rpm -q httpd" "httpd"
  check "wget is removed" "! rpm -q wget" "not installed"
  check "yum cache is cleared" "test ! -d /var/cache/yum" ""

  # SECTION E (part): Networking
  check "IP is 192.168.10.11" "ip a | grep inet" "192.168.10.11"
  check "Default route via 192.168.10.12" "ip route" "default via 192.168.10.12"
  check "Ping to Node2" "ping -c 1 192.168.10.12" "1 received"

  # SECTION F: File transfer (only verify file exists on Node1)
  check "File testfile.txt exists" "[ -f /home/john/testfile.txt ] && echo OK" "OK"

  # SECTION G: tar
  check "Archive exists" "[ -f /tmp/devops_backup.tar.gz ] && echo OK" "OK"
  check "Extracted directory exists" "[ -d /restore/devops ] && echo OK" "OK"

  # SECTION H: Hostname
  check "Hostname is training-node1" "hostname" "training-node1"
}

check_node2() {
  echo "Running checks for Node2..."

  # SECTION E (part): Networking
  check "IP is 192.168.10.12" "ip a | grep inet" "192.168.10.12"
  check "Default route via 192.168.10.11" "ip route" "default via 192.168.10.11"

  # SECTION F: File transfer verification (only on Node2)
  check "testfile.txt exists in /tmp" "[ -f /tmp/testfile.txt ] && echo OK" "OK"

  # SECTION H: Hostname
  check "Hostname is training-node2" "hostname" "training-node2"
}

if [[ "$NODE" == "node1" ]]; then
  check_node1
elif [[ "$NODE" == "node2" ]]; then
  check_node2
else
  echo "Usage: $0 node1|node2"
  exit 1
fi

echo
echo "==== Test Results for $NODE ===="
for r in "${RESULTS[@]}"; do
  echo "$r"
done

# Calculate score
SCORE=$((PASSED * 100 / TOTAL))
echo
echo "==== Overall Score: $SCORE% ===="

```
