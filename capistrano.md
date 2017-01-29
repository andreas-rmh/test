# Capistrano
## Deployment user
```bash
 adduser --group --shell /bin/bash --disabled-password UserName
 groupadd deployers
 usermod -a -G deployers UserName
```

Add ~/.ssh/authorized_keys
Add user and group to /etc/ssh/sshd_config (AllowUsers AllowGroups)
Restart sshd (service ssh restart)
