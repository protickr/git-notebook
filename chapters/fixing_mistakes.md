# How to fix mistakes


> Undo uncommitted changes that has been made to <a_file>  
> `$ git checkout <a_file>`  
> 
> Restore tracked but deleted folder  
> `git reset -- path/to/folder`  
> `git checkout -- path/to/folder`   

## Commit not pushed yet

**re-writes git history**

>Change previous commit message  
> `$ git commit --amend -m "changed message"`  

>add new files to previous commit  
> `$ git add .`  
> or  
>`$ git add <file_name>`  
> `$ git commit --amend`

## Revert a Pushed commit
> creates a new commit and does not re-writes git history  
> `$ git revert "commit_hash_that_need_to_be_reverted"`  

## Transfer commit to other branch

> find out commit hash of a commit to be transferred to other branch  
> `$ git log`  
> `$ git checkout <target_branch>`  
> `$ git cherry-pick <commit_hash_that_need_to_be_cherry_picked>`  

## Delete commit, git Reset

**there are 3 types of git reset**  

### Soft reset

> no changes are lost, changes remain in staging area  
> `$ git reset --soft <commit_hash_to_where_head_will_be_resetted_to>`  

### Mixed/default reset

> no changes are lost, changes are unstaged  
> `$ git reset <commit_hash_to_where_head_will_be_resetted_to>`  

### Hard reset

> changes are discarded from tracked files but does not do anything to untracked files, resets back to fresh  
> `$ git reset --hard <commit_hash_to_where_head_will_be_resetted_to>`  

>removes all untracked directory and files  
> `$ git clean -df`  

## retrieve changes after a hard reset

> Execute the following command and grab hash of commit that was discarded  
> `$ git reflog`  
> then  
> `$ git checkout <hash>`  
>
> This is not a branch, we are in a detached-head state, so we need to create a branch here,  
> `$ git branch <new-commit-restored-branch>`  

## Remove or Rename files and directory  
> `$ git rm <path_to_file>`  
> `$ git rm -r <path_to_directory>`  
> removes file or directory from staging and working directory (/project)  
> 
> `$ git mv <path_to/source_file_name> <path_to/target_file_name>`  
> rename or move file  

**Remove file/directory from staging which is recently been ignored by GIT but tracked earlier**
>`$ git rm --cached file.txt`  
>`$ git rm --cached -r bin/`  

[Index][index]

[index]: ../index.md
