# Git
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

 git config --global alias.lgg 'log --graph --oneline --all'
 git config --global alias.df 'diff-tree --no-commit-id --name-only -r'
 
 git config -l
```