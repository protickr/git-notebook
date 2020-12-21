# Interactive Rebase  
"Git interactive rebase" is completely different from "Git rebase". Interactive rebase allows user to change commit message (reword), delete commits (drop), combines commits into 1 (fixup/squash), reorder commits (By reordering them in Interactive window), splitting commits by providing an interactive window.   

"Git rebase" re-bases one branch onto another. 

**Select commits for interactive rebase**
> `$ git rebase -i HEAD~n`  
> (operates on n commits from head to latest n commits; n = 1,2,3...)  
> - in interactive mode select operation by typing keyword beside individual commit e.g.,   
> - "reword" to change commit message  
> 
> - "drop" to delete a commit  
> 
> - "fixup/squash" to squash a number of commits into single commit. Squashes all commits marked with squash or fixup keyword into the latest commit.  
> 
> - "edit" to go to an "interactive branch" and operate on them;  
    `$ git reset HEAD^`  
    modify, stage and commit them into different commits to "split" single commits into multiple. Then, 
    `$ git rebase --continue`  
    to transfer those new commits to original branch from interactive branch.  
> 
> - Reorder commit entries to "reorder" them

[Index][index]

[index]: ../index.md
    