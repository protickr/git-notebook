# Initialization and Branching  

*git initialization at local directory*  
>go to the root of the project directory and,   
> `$ git init`  
if cloned from remote then project directory will be named as repository-name and git is already initialized in it, no need to initialize it again.

*add remote origin (where commits will be pushed) to local repository*  
> `$ git remote add origin <origin_address>`  
this will set remote "origin" to url specified at origin_url  
cloned repository from remote location automatically sets remote origin to git.  

*Set upstream branch*  
> `$ git branch --set-upstream-to=origin/<remote_branch_name> <local_branch_name>`  
>
> `$ git branch -u origin <remote_branch_name>`  
sets currently checked-out branch's upstream to remote_branch_name from origin

**Only works if upstream remote branch already exists**  
  
If it doesn't we need to push that newly created local branch to remote and set upstream branch for that by following command,
> `$ git push --set-upstream-to=origin/remote_branch <local_branch>`  
> `$ git push -u <origin> <remote_branch>`  
or,  
> `$ git push origin HEAD`  
Upstream indicates where commits will be pushed, [but there must be some commit before doing so]  

*Show information about remote*  
> `$ git remote -v`  
> `$ git remote -vv`  

_To check upstream branch from any checked-out branch_  
> `$ git push -u`  

*Create a branch*  
> `$ git branch <branch_name>`  

*Create a branch from other branch*  
> `$ git checkout -b <target_branch> <branch_name>`  
or,  
> `git checkout <source_branch>`  
> `git branch <new_target_branch>`  

*Switch to a barnch*  
> `$ git checkout <branch_name>`  

*Create a new branch and switch to that at once*  
> `$ git checkout -b <branch_name>`  

*Show all branches from remote and local*  
> `$ git branch -a`  

*Show branch from local*  
> `$ git branch`  

*Show branch tree*  
> `$ git log --graph`  
> `git log --graph --pretty=oneline --abbrev-commit`  

_Branch merging_  
checkout branch where you intend to merge another branch  
> `$ git checkout master`  
checked out to master branch  
> `$ git branch --merged`  
lists branches that are merged to master  
> `$ git merge <source/feature_branch_name>`  
> in case of conflict while merging use,  
> `$ git mergetool`  
> to resolve conflict graphically using mergetool.

_Branch Deleting_  
From local `$ git branch -d branch_name`  
From remote `$ git push origin --delete branch_name`  

[Index][index]

[index]: ../index.md
