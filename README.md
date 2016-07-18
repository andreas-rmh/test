# Git config

```bash
 git config --global user.name "John Doe"
 git config --global user.email johndoe@example.com

 git config --global core.autocrlf input
 git config --global core.editor vim -f
 git config --global core.whitespace nowarn

 git config --global alias.co checkout
 git config --global alias.br branch
 git config --global alias.ci commit
 git config --global alias.st status
 git config --global alias.unstage 'reset HEAD --'
 git config --global alias.last 'log -1 HEAD'

 git config --global alias.lgg 'log --graph --oneline --all'
 git config --global alias.df 'diff-tree --no-commit-id --name-only -r'
 
 git config -l
```

# ADB stuff
```bash
 $ adb logcat | grep `adb shell ps | grep com.example.package | cut -c10-15`
```

Colors: http://jsharkey.org/blog/2009/04/22/modifying-the-android-logcat-stream-for-full-color-debugging/
```bash
 $ adb logcat | grep `adb shell ps | grep com.example.package | cut -c10-15` | ~/coloredlogcat.py
```

# VIM
## Default config
File: ~/.vimrc
```
set nocompatible " use vim defaults.  MUST BE FIRST LINE

set noexpandtab " Make sure that every file uses real tabs, not spaces
set shiftround  " Round indent to multiple of 'shiftwidth'
set smartindent " Do smart indenting when starting a new line
set autoindent  " Copy indent from current line, over to the new line

" Set the tab width
let s:tabwidth=2
exec 'set tabstop='    .s:tabwidth
exec 'set shiftwidth=' .s:tabwidth
exec 'set softtabstop='.s:tabwidth

colorscheme ron

set encoding=utf-8

" Backup files
set backupdir=~/.vim/backup//
set directory=~/.vim/swap//
set undodir=~/.vim/undo//
" Using double trailing slashes in the path tells vim to enable a feature
" where it avoids name collisions

set title           " show title of the file in vim title bar
set ls=2            " show status bar with file path and name
set showcmd         " displays an incomplete command in the lower right of the window
set ruler           " show the cursor vertical and horiz position in the lower right corner, or right status line
set nowrap          " don't wrap lines
set showmode        " show the current mode of the editor
set history=1000    " keep the last 1000 commands and last 1000 search patterns
" set background=dark " make background dark, i.e black
" set mouse=a         " enable mouse usage
set virtualedit=onemore    " allow cursor one line beyond last line
set hlsearch        " highlight searches. All valid search results are highlighted in color.
set incsearch       " do searching as characters are typed in the search pattern
set ignorecase      " ignore case when searching
set number                                      " Show line numbers
set sm                " show matchin braces
set hidden                                      " any buffer can be hidden (keeping its changes) without first writing the buffer to a file
syntax on            " syntax highlighting

set splitright
set splitbelow
```

## Shortcuts
```
=       In visual mode, typing = will fix indentation of the current section. 
gg=G    In normal mode, typing gg=G will reindent the entire file
```

## nginx syntax
```bash
#!/bin/sh
mkdir -p ~/.vim/syntax/
cd ~/.vim/syntax/
wget -O nginx.vim http://www.vim.org/scripts/download_script.php?src_id=19394
cat > ~/.vim/filetype.vim <<EOF
au BufRead,BufNewFile /etc/nginx/*,/usr/local/nginx/conf/* if &ft == '' | setfiletype nginx | endif
EOF
```

## Postgres
### Install
```bash
wget –quiet https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add ACCC4CF8.asc
echo “deb http://apt.postgresql.org/pub/repos/apt/ $(lsb_release -cs)-pgdg main” >> /etc/apt/sources.list
apt-get update && apt-get upgrade
apt-get install postgresql-9.5

# libpg-dev for pg gem
apt-get install postgresql-server-dev-9.5
```
For mint rosa use "trusty-pgdg"

### Configure
```bash
su - postgres
psql
```
#### Create super user (if needed)
```psql
CREATE USER root WITH SUPERUSER CREATEDB CREATEROLE PASSWORD 'secretAccountPassword';
```
Add 
 local   all             root                                md5
to "/etc/postgresql/9.5/main/pg_hba.conf"
and connect via
 psql -U root -h localhost postgres
 
#### Create new database and related user
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

### Extensions
#### PostGIS
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

### psql commands
```psql
\l list databases
\dt list tables
\dn list schemas
\du list roles/users
```

## Ruby
### Install
```bash
apt-get install git-core curl zlib1g-dev build-essential libssl-dev libreadline-dev libyaml-dev libsqlite3-dev sqlite3 libxml2-dev libxslt1-dev libcurl4-openssl-dev python-software-properties libffi-dev

# From source
- Download sources
./configure 
make && make install

cd ext/zlib
ruby extconf.rb
make && make install

- Same for ext/openssl


# Install with ruby-install
wget -O ruby-install-0.6.0.tar.gz https://github.com/postmodern/ruby-install/archive/v0.6.0.tar.gz
tar -xzvf ruby-install-0.6.0.tar.gz
cd ruby-install-0.6.0/
sudo make install

mkdir /opt/rubies
ruby-install --rubies-dir /opt/rubies --latest ruby 2.3.1

# Use with chruby
wget -O chruby-0.3.9.tar.gz https://github.com/postmodern/chruby/archive/v0.3.9.tar.gz
tar -xzvf chruby-0.3.9.tar.gz
cd chruby-0.3.9/
make install

cat >> ~/.$(basename $SHELL)rc <<EOF
source /usr/local/share/chruby/chruby.sh
source /usr/local/share/chruby/auto.sh
EOF

exec $SHELL 

## Rails 
### Install (rails-5.0.0.rc1)
gem install rails --pre --no-ri --no-rdoc

### Create project
rails new myapp --database=postgresql
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

## PostGIS support
Add 
 gem 'activerecord-postgis-adapter'
to Gemfile
Change adapter in config/database.yml to
 adapter: postgis
 postgis_extension: postgis # default is postgis
 postgis_schema: public     # default is public
 schema_search_path: public,postgis
 
Use in existing project
```bash
bin/rails db:gis:setup
```

### Config


