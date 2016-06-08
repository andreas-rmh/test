# Git config

```bash
 $ git config --global user.name "John Doe"
 $ git config --global user.email johndoe@example.com

 $ git config --global core.autocrlf input
 $ git config --global core.editor vim -f
 $ git config --global core.whitespace nowarn

 $ git config --global alias.co checkout
 $ git config --global alias.br branch
 $ git config --global alias.ci commit
 $ git config --global alias.st status
 $ git config --global alias.unstage 'reset HEAD --'
 $ git config --global alias.last 'log -1 HEAD'

 $ git config --global alias.lgg 'log --graph --oneline --all'
 $ git config --global alias.df 'diff-tree --no-commit-id --name-only -r'
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
\connect dbName;
CREATE SCHEMA schemaName;
# Grant privileges (like the ability to create tables) on new schema to new role
GRANT ALL ON SCHEMA schemaName TO userName;
# Grant privileges (like the ability to insert) to tables in the new schema to the new role
GRANT ALL ON ALL TABLES IN SCHEMA schemaName TO userName;

#### psql commands
```psql
\l list databases
\dt list tables
\dn list schemas
\du list roles/users
```
