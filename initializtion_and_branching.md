# Initialization and Branching  

*git initializtion at local directory*  
`$ git init`  
the directory in which git is initialized is the same as the repository name if cloned, [assumption]

\
*add remote origin to local repository*  
`$ git remote add origin <origin_url>`  
this will add remote origin to url specified at origin_url  
cloned repository from remote location automatically sets remote origin to git.  

\
*set upstream branch*  
`$ git branch --set-upstream-to=origin/<remote_branch_name> <local_branch_name>`  

`$ git branch -u origin <remote_branch_name>`  
sets currently checked-out branch's upstream to remote_branch_name from origin

\
*set upstream branch at specified origin at push event*  
*or push a local branch to remote origin and set local branch's upstream*  
`$ git push --set-upstream-to=origin/remote_branch <local_branch>`  
`$ git push -u <origin> <remote_branch>`  
Upstream indicates where commits will be pushed

\
*show information about remote*  
`$ git remote -v`  
`$ git remote -vv`  

\
*create a branch*  
`$ git branch <branch_name>`  

\
*switch to a barnch*  
`$ git checkout <branch_name>`  

\
*create a new branch and switch to that at once*  
`$ git checkout -b <branch_name>`  

\
*show all branches from remote and local*  
`$ git branch -a`  

\
*show branch from local*  
`$ git branch`  

\
*show branch tree*  
`$ git log --graph`  

\
_branch merging_  
checkout branch where you intend to merge another branch  
`$ git checkout master`  
checked out to master branch  

`$ git branch --merged`  
lists branches that are merged to master  

`$ git merge <source/feature_branch_name>`  
