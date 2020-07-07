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

### mixed/default reset

no changes are lost, changes are unstaged  

### hard reset

changes are discarded, resets back to fresh  

\
[Index][index]

[index]: ../index.md
