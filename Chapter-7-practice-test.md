Login with root user on the system
Run following commands

List running services
```bash
# systemctl -list --type=service
```
List all Services 
``` bash
# systemctl list-units --type=service --all
```
Lists units that are both loaded and active
```bash
# systemctl
```
View Service State os sshd.serviec
```bash
# systemctl status sshd.service
```
Verify the Status of a sshd.service is active or not 
```bash
# systemctl is-active sshd.service
```
Verify the Status of a sshd.service is enable or not
```bash
# systemctl is-enabled sshd.service
```
Verify the Status of a sshd.service is failed or not
```bash
# systemctl is-failed sshd.service
```
Check the state of your System 
```bash
# systemctl get-default
```
Change the state to the cli mode
```bash
# systemctl isolate multi-user.target
```
Change the state to the graphical mode
```bash
# systemctl isolate grraphicaly.target
```
Change the state permanently to the cli mode
```bash
# systemctl set-default multi-user.target
```
start Service sshd.service temporary
```bash
# systemctl start sshd.service
```
start Service sshd.service permanently
```bash
# systemctl enable sshd.service
```
reload Service sshd.service
```bash
# systemctl reload sshd.service
```
stop Service sshd.service temporary
```bash
# systemctl stop sshd.service
```
stop Service sshd.service permanently
```bash
# systemctl desable sshd.service
```
