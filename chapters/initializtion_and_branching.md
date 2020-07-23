# Initialization and Branching  

*git initializtion at local directory*
\
> `$ git init`  
the directory in which git is initialized is the same as the repository name if cloned, [assumption]

\
*add remote origin to local repository*  
> `$ git remote add origin <origin_url>`  
this will add remote origin to url specified at origin_url  
cloned repository from remote location automatically sets remote origin to git.  

\
*set upstream branch*  
> `$ git branch --set-upstream-to=origin/<remote_branch_name> <local_branch_name>`  
>
> `$ git branch -u origin <remote_branch_name>`  
sets currently checked-out branch's upstream to remote_branch_name from origin

only works if upstream remote branch already exists  
if it doesn't we need to push that newly created local branch to remote by the following command,

\
*set upstream branch at specified origin at push event*  
*or push a local branch to remote origin and set local branch's upstream*  
> `$ git push --set-upstream-to=origin/remote_branch <local_branch>`  
> `$ git push -u <origin> <remote_branch>`  
or,  
> `$ git push origin HEAD`  
Upstream indicates where commits will be pushed, [but there must be some commit before doing so]  

\
*show information about remote*  
> `$ git remote -v`  
> `$ git remote -vv`  
\
_to check upstream branch from any checked-out branch_  
> `$ git push -u`  
  
\
*create a branch*  
> `$ git branch <branch_name>`  

\
*create a branch from other branch*  
> `$ git checkout -b <target_branch> <branch_name>`  
or,  
> `git checkout <source_branch>`  
> `git branch <new_target_branch>`  

\
*switch to a barnch*  
> `$ git checkout <branch_name>`  

\
*create a new branch and switch to that at once*  
> `$ git checkout -b <branch_name>`  

\
*show all branches from remote and local*  
> `$ git branch -a`  

\
*show branch from local*  
> `$ git branch`  

\
*show branch tree*  
> `$ git log --graph`  

\
_branch merging_  
checkout branch where you intend to merge another branch  
> `$ git checkout master`  
checked out to master branch  
> `$ git branch --merged`  
lists branches that are merged to master  
> `$ git merge <source/feature_branch_name>`  

\
[Index][index]

[index]: ../index.md
