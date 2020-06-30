# Initialization and Branching  

*git initializtion local directory*  
`$ git init`  
the directory in which git is initialized is the same as the repository name if cloned, [assumption]

*add remote origin to local repository*  
`$ git remote add origin <origin_url>`  
this will add remote origin to url specified at origin_url  
cloned repository from remote location automatically sets remote origin to git.  

*set upstream branch at specified origin*  
`$ git push --set-upstream <origin> <branch>`  
`$ git push -u <origin> <branch>`  
Upstream indicates where commits will be pushed

*show information about remote*  
`$ git remote -v`  
`$ git remote -vv`  

*create a branch*  
`$ git branch <branch_name>`  

*switch to a barnch*  
`$ git checkout <branch_name>`  

*create a new branch and switch to that at once*  
`$ git checkout -b <branch_name>`  

*show all branches from remote and local*  
`$ git branch -a`  

*show branch from local*  
`$ git branch`  
