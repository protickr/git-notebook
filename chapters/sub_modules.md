## Git Submodules

It is a way to use another module (source controlled project i.e., repository) within a parent project  
The benefit of using another repository as your dependency library is, you can always get the latest update  
without getting into useless hassles such as, copying the new source code again and again. 
Making any changes to that submodule will be available to all other parent projects who are using it.

**When you do not want your library to be available publicly but also need it to be source-controlled and used within 
other projects easily, use submodules**

>_Add submodules to your main project_  
> `$ git submodule add <submodule_source> <directory_name>`      
> previous command must be run from root of parent project directory.  
>
> then in the parent project directory run the following,  
> `$ git commit -m "added a submodules called "`
> 
> from within the submodule's directory modify your library and commit and push changes from there  
>
> Now from the parent directory run the following command to get the changes in submodule,  
> `$ git submodule update`  
> 

**If you clone a project that has submodule dependency in it, run the following**
> `$ git submodule init` (to initialize submodule)  
> `$ git submodule update` (to get the latest changes in submodule)  
> or  
> `$ git clone --recurse-submodules <main_project_link>`  
> if you forgot to use recurse when cloning you can also use,    
> 
> `$ git submodule update --init`  
> 
> or to make it foolproof,  
> `$ git submodule update --init --recursive`  






[Index][index]

[index]: ../index.md