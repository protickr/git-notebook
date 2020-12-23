## Git Bisect  
git-bisect - Use binary search to find the commit that introduced a bug  


> `$ git bisect start`  
> starts bisecting mode  
> `$ git bisect good <commit_hash>`  (earlier commit when the bug was not introduced yet)  
> `$ git bisect bad HEAD` (things are broken in the latest commit)  
> `$ git bisect visualize` (where am I at, at this moment while bisecting)  
> 
>In this point we will need a testing script that will check the existence of files and such   
> the testing script should output yes (0) /  good or no (1) / bad.  
> Also, the script should not be source controlled i.e., not tracked by Git.  
>
> `$ git bisect run ./script.ext`  
> now Git bisect will run that script against every commit and report bad-commit based on  
> the script's output.  
> `$ git bisect reset`  
> 
> What git bisect really does is, checkout commit hash in a binary search fashion and waits for your instruction.  
> if you do not want to use a test script then you should mark commit as good or bad depending on your manual testing.
> As Git will checkout a commit hash, you can run and test the project as if you were in a branch. If it's behaviour is 
> okay then mark it good or bad otherwise.  
> `$ git bisect good`  
> `$ git bisect bad`  
> then git will automatically select the next commit hash.  
> Finally after Git bisect reset you will be checked out to HEAD, latest commit of the branch you were working on.  


[Index][index]

[index]: ../index.md