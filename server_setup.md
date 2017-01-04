
# SSH server config

```bash
 $ vim /etc/ssh/sshd_config
```
* Change port  
  **Port 2200**
  
* Only use protocol 2  
  **Protocol 2**
  
* Disable root login  
  **PermitRootLogin no**

* Disable password authentication (Upload public key before!)  
  **PasswordAuthentication no**
  
* Specify network interface for ssh connections  
  **ListenAddress 192.168.1.20**
  
* Reduce login grace timeout  
  **LoginGraceTime 60**

* Set maximum number of concurrent connections  
  **MaxStartups 2**

* Disable forwarding  
  **X11Forwarding no**
  
* Disable empty passwords  
  **PermitEmptyPasswords no**
  
* Optional
  * Change log level for more information about e.g. failed attempts  
    **LogLevel VERBOSE**
  * Hide last login  
    **PrintLastLog no**

# Remove Unused Network-Facing Services
```bash
 $ netstat -tulpn
```

# Secure SSH using IPTables
To allow SSH connections only from 192.168.0.20
```bash
 $ sudo iptables -A INPUT -p tcp -m state --state NEW --source 192.168.0.20 --dport 22 -j ACCEPT
```
To allow SSH connections from certain IP range
```bash
 $ iptables -A INPUT -i eth0 -s 192.168.0.0/16 -j ACCEPT
```
Disable SSH connection from all other hosts
```bash
 $ sudo iptables -A INPUT -p tcp --dport 22 -j DROP
```
Save new rules
```bash
 $ sudo iptables-save > /etc/iptables/rules.v4
```
