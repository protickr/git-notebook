# How to fix mistakes

\
_undo uncommitted changes that has been made to <a_file>_
> `$ git checkout <a_file>`  

## Commit not pushed yet

\
_re-writes git history_

\
_amend previous commit message or add new files to previous commit_
> `$ git commit --amend -m "changed message"`  

\
_add new files to previous commit_
> `$ git add .`  
> `$ git commit --amend`  

## Revert a Pushed commit

\
_creates a new commit and does not re-writes git history_

> `$ git revert "commit_hash_that_need_to_be_reverted"`  

## cherry pick commit to other branch

\
> `$ git log`  
find out commit hash of a commit to be cherry picked to other branch  
> `$ git checkout <target_branch>`  
> `$ git cherry-pick <commit_hash_that_need_to_be_cherry_picked>`  

## delete commit from a branch, git Reset

there are 3 types of git reset  

### soft reset

no changes are lost, changes remain in staging area  
> `$ git reset --soft <commit_hash_to_where_head_will_be_resetted_to>`  

### mixed/default reset

no changes are lost, changes are unstaged  
> `$ git reset <commit_hash_to_where_head_will_be_resetted_to>`  

### hard reset

changes are discarded from tracked files but does not do anything to untracked files, resets back to fresh  
> `$ git reset --hard <commit_hash_to_where_head_will_be_resetted_to>`  

removes all untracked directory and files  
> `$ git clean -df`  

## retrieve changes after a hard reset

execute the following command and grab hash of commit that was discarded  
> `$ git reflog`  

then  
>`$ git checkout <hash>`  

this is not a branch, we are in a detached-head state, so we need to create a branch here,  
> `$ git branch <new-commit-restored-branch>`  

\
[Index][index]

[index]: ../index.md
