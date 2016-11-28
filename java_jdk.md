
# Java

[source](https://wiki.ubuntuusers.de/Java/Installation/Oracle_Java/Java_8/)

- Create directory /opt/java
- Download current [Java JDK from Oracle](http://www.oracle.com/technetwork/java/javase/downloads)
- Extract and copy JDK to /opt/java/<JDK_VERSION>/
- Add JAVA_HOME to /ets/environemt or /etc/profile

```bash
$ sudo update-alternatives --install "/usr/bin/java" "java" "/opt/java/<JDK_VERSION>/bin/java" 1
$ sudo update-alternatives --install "/usr/bin/javac" "javac" "/opt/java/<JDK_VERSION>/bin/javac" 1
$ sudo update-alternatives --install "/usr/bin/javaws" "javaws" "/opt/java/<JDK_VERSION>/bin/javaws" 1
$ sudo update-alternatives --install "/usr/bin/jar" "jar" "/opt/java/<JDK_VERSION>/bin/jar" 1 
 
$ sudo update-alternatives --set "java" "/opt/java/<JDK_VERSION>/bin/java"
$ sudo update-alternatives --set "javac" "/opt/java/<JDK_VERSION>/bin/javac"
$ sudo update-alternatives --set "javaws" "/opt/java/<JDK_VERSION>/bin/javaws"
$ sudo update-alternatives --set "jar" "/opt/java/<JDK_VERSION>/bin/jar" 
```

