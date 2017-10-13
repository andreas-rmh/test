# Configure MySQL
Create a database user which Crowd will connect as (e.g. crowduser).
Create a database for Crowd to store data in (e.g. crowd). For a UTF-8 encoded database:

- Create user
```SQL
CREATE DATABASE <DB_NAME> CHARACTER SET utf8 COLLATE utf8_bin;

# 5.7.6 and above
CREATE USER IF NOT EXISTS 'user'@'localhost' IDENTIFIED BY 'password';

# Version below 5.7.6)
GRANT ALL ON `<DB_NAME>`.* TO 'user'@'localhost' IDENTIFIED BY 'password';

---
CREATE USER 'newuser'@'localhost' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON * . * TO 'newuser'@'localhost';
FLUSH PRIVILEGES;

```

- Edit the /etc/mysql/mysql.conf.d/my.cnf file

```CONFIG
[mysqld]
character-set-server=utf8
collation-server=utf8_bin

[mysqld]
default-storage-engine=INNODB

[mysqld]
transaction-isolation = READ-COMMITTED
```
