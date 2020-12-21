## Git Rebase

Rebases one branch onto another.  
Generally when we create a new branch from antoher the new branch has all the updates upto its parent branch but in case after branch creation parent branch is updated with some resources that we need in our newly created branch what should we do ?  
1. Checkout to its parent branch and pull updates.
   > `$ git checkout master`  
   > `$ git pull origin master`  
2. Checkout to new branch and rebase it onto its parent.  
   > `$ git checkout feature-branch`  
   > `$ git pull origin feature-branch`  
   > `$ git rebase master`  
        Feature branch will have latest updates commits as master branch.

