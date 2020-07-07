# Staging, committing and pushing changes  

## Tracking and Staging

\
_show modified flies and newly created files or directory_

> `$ git status`  

\
_add files to staging area_
> `$ git add -A`  

or  

> `$ git add --all`  

adds files/folders to staging area from everywhere inside git initialized directory  

\
_add files to staging area from current directory and its subdirectories_  

> `$ git add .`

\
_add modified files only_  
> `$ git add -u`  

or  

> `$ git add --update`  

\
_improper way to stage_  
> `$ git add *`  

"*" is a shell command, so whatever returned by shell is added to staging area,  
its imprecise and inconsistent accross multiple operating system and environments  
so avoid using it.  

## Committing to local branch

\
_Commit staged changes_  
>`$ git commit -m "commit message"`  

\
_change commit message_
>`$ git commit --amend -m "changed commit message"`  

\
_add leftout files to previous commit_
>`$ git add <file_name>`  
> `git commit --amend`  

\
_show git commit log_
>`$ git log`

as a tree  
> `$ git log --graph`  

\
_push commit to remote repo_
first take a pull then push
>`$ git pull origin branch`  
>`$ git push origin branch`  

\
_show changes made between commits_  
>`$ git diff <file_name>`  

shows changes made to file since previous commit

>`$ git diff commit_hash_1 commit_hash_2`  

shows changes between commit_1 and commit_2  

\
[Index][index]

[index]: ../index.md
