
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

Remove Unused Network-Facing Services
```bash
 $ netstat -tulpn
```
