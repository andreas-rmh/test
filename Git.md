# Git

## Commands
```bash
$ git log --follow -p -- file

$ git fetch -p # Prunes all stale references
```

## Config

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

 git config --global alias.lgga 'log --graph --decorate --oneline --all' # --all, will show all the branches instead of just the current one
 git config --global alias.lgg 'log --graph --decorate --oneline' 
 
 git config --global alias.ls 'log --pretty=format:"%C(yellow)%h%Cred%d\\ %Creset%s%Cblue\\ [%cn]" --decorate'
 git config --global alias.ll 'log --pretty=format:"%C(yellow)%h%Cred%d\\ %Creset%s%Cblue\\ [%cn]" --decorate --numstat'
 git config --global alias.lds 'log --pretty=format:"%C(yellow)%h\\ %ad%Cred%d\\ %Creset%s%Cblue\\ [%cn]" --decorate --date=short'
 git config --global alias.ld 'log --pretty=format:"%C(yellow)%h\\ %ad%Cred%d\\ %Creset%s%Cblue\\ [%cn]" --decorate --date=relative'
 
 git config --global alias.publish '!git push -u origin $(git branch-name)'
 git config --global alias.unpublish '!git push origin :$(git branch-name)'
 
 git config --global alias.df 'diff-tree --no-commit-id --name-only -r'
 git config --global alias.bra 'branch -a'
 
# Find file
git config --global alias.f '!git ls-files | grep -i'
git config --global alias.grep 'grep -Ii'
 
 git config -l
```


