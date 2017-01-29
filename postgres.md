# Postgres
## Install
```bash
wget –quiet https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add ACCC4CF8.asc
echo “deb http://apt.postgresql.org/pub/repos/apt/ $(lsb_release -cs)-pgdg main” >> /etc/apt/sources.list
apt-get update && apt-get upgrade
apt-get install postgresql-9.5

### libpg-dev for pg gem
apt-get install postgresql-server-dev-9.5
```
For mint rosa use "trusty-pgdg"

Version 9.6 on Ubuntu 16.04 LTS
```bash
deb http://apt.postgresql.org/pub/repos/apt/ xenial-pgdg main
wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | \
  sudo apt-key add -
sudo apt-get update
apt-get install postgresql-9.6
```

## Configure
```bash
su - postgres
psql
```
### Create super user (if needed)
```psql
CREATE USER root WITH SUPERUSER CREATEDB CREATEROLE PASSWORD 'secretAccountPassword';
```
Add 
 local   all             root                                md5
to "/etc/postgresql/9.5/main/pg_hba.conf"
and connect via
 psql -U root -h localhost postgres
 
### Create new database and related user
```psql
# Create a role (user) with password
CREATE USER userName PASSWORD 'secretPassword';
CREATE DATABASE dbName WITH OWNER userName;
\connect dbName userName;
CREATE SCHEMA schemaName;
# Grant all privileges
GRANT ALL ON DATABASE dbName TO userName;
# Grant privileges (like the ability to create tables) on new schema to new role
GRANT ALL ON SCHEMA schemaName TO userName;
# Grant privileges (like the ability to insert) to tables in the new schema to the new role
GRANT ALL ON ALL TABLES IN SCHEMA schemaName TO userName;

# If needed grant permission to create a new database
ALTER ROLE userName WITH CREATEDB;
```

## Extensions
### PostGIS
```bash
 $ apt-get install postgis
 $ apt-get install postgis-doc
 $ apt-get install postgresql-9.5-postgis-2.2
 
 su postgres
 psql
```
```psql
 \connet DATABASE_NAME;
 CREATE EXTENSION postgis;
 
```

## psql commands
```psql
\l list databases
\dt list tables
\dn list schemas
\du list roles/users
\dx list extensions

\dt SchemaName. # Show tables for named schema
SET search_path TO SchemaName, public; # Set search_path
SHOW search_path; # Show current schema priority
```
