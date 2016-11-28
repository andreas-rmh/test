# Configure MySQL
Create a database user which Crowd will connect as (e.g. crowduser).
Create a database for Crowd to store data in (e.g. crowd). For a UTF-8 encoded database:

- Create user
```SQL
create database <DB_NAME> character set utf8 collate utf8_bin;

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
