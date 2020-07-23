# Stashing and Applying changes  

## Stashing

stash is available globally in all barnches

\
_stashing changes_

> `$ git stash save <stash_message>`  

\
_stash list_

> `$ git stash list`  

\
_apply stash_

> `$ git stash apply stash{id}`  
  
applies stashed changes to checked-out branch from stashes identified with "id", does not delete the stash  

\
_pop stash_

> `$ git stash pop`  
  
applies first stash from top of the stash stack to checked out branch and deletes it  

\
_drop stash_

> `$ git stash drop stash{id}`  
  
drops stash which is identified by id  

\
_clear all stash_

> `$ git stash clear`  
  
deletes all stahes  

\
[Index][index]

[index]: ../index.md