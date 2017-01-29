
# ADB stuff
```bash
 $ adb logcat | grep `adb shell ps | grep com.example.package | cut -c10-15`
```

Colors: http://jsharkey.org/blog/2009/04/22/modifying-the-android-logcat-stream-for-full-color-debugging/
```bash
 $ adb logcat | grep `adb shell ps | grep com.example.package | cut -c10-15` | ~/coloredlogcat.py
```
