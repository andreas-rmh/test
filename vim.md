
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

set encoding=utf-8
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
