
Just a bunch of reminders


## Commands
```bash
git log --follow -p -- file
```

# ADB stuff
```bash
 $ adb logcat | grep `adb shell ps | grep com.example.package | cut -c10-15`
```

Colors: http://jsharkey.org/blog/2009/04/22/modifying-the-android-logcat-stream-for-full-color-debugging/
```bash
 $ adb logcat | grep `adb shell ps | grep com.example.package | cut -c10-15` | ~/coloredlogcat.py
```

## Capistrano
### Deployment user
```bash
adduser --group --shell /bin/bash --disabled-password UserName
groupadd deployers
usermod -a -G deployers UserName
```
Add ~/.ssh/authorized_keys
Add user and group to /etc/ssh/sshd_config (AllowUsers AllowGroups)
Restart sshd (service ssh restart)


