# GIT Notebook

Result of personal practice on Git to understand and experience it hands-on, using a terminal.  
Tried to document what I have learned through practice and tutorials.  
This is not an exhaustive list of commands or descriptions of version control systems.  

## What is git

Git is a distributed version control system that enables us to control versions of a project by tracking different versions of it.  
It generally keeps track of all the commits (snapshot or, a package of changes) that we made to our project and enables us to traverse through them.  
  
The Distributed version control system is different from The Centralized version control system as  
DVCS allows all users to have an updated copy of the whole repository offline  
CVCS allows user to have only a version of the project and they commit their changes to remote central repository directly.  

&nbsp;    
### GIT structure  
There are three distinct compartments that are used by GIT to operate i.e.,  
_**Working Directory / Tree**_ > ( `$ git add` )> _**Staging Area / Index**_ >  
( `$ git commit -m "msg"` ) > _**Repository**_ > (`$ git push` ) > _**Remote Repository**_  
Repository always has a commit hash that points to latest commit which is labeled as HEAD  
But working directory and staging area do not,  
Instead staging area keeps a virtual reference to latest commit or HEAD.  
Meaning as if Staging Area is as updated as latest commit of the repository.  
  
&nbsp;    
## Git configuration

&nbsp;  
>_**Retrieve installed git version**_  
>`$ git --version`

&nbsp;  
> _**Set git author's username and email**_  
>`$ git config --global user.name "user_name"`  
>`$ git config --global user.email "email"`

&nbsp;  
> _**all configuration list**_  
>`$ git config --list`  
>`$ git config --local --list`  
>`$ git config --global --list`  
>`$ git config --system --list`  
local config, lists applicable config for current repository.  

&nbsp;  
> _**help/doc of any command**_  
>`$ git help <command_verb>`  
or  
>`$ git <command_verb> --help`  
> 
>`$ git <command_verb> -h`  
(shows short help doc)  
>

&nbsp;  
> **Ignore files**  
> Add files, directories and wild-card entries to .gitignore file, files/directories listed in it will be ignored by git.
  
&nbsp;  
> _**Configure how git should handle end of line(EOL)**_  
> Different for windows and Unix, e.g.,  
> `$ git config --global core.autocrlf true` (for windows)  
> `$ git config --global core.autocrlf input` (for UNIX)  

&nbsp;  
> _**Set default config editor for git**_  
> First set the intended app's path in your environment variables.  
>  
> `$ git config --global core.editor "app --wait"`  
>  
> (Open config file in "app" and edit global-config by,)  
> `$ git config --global -e`  

&nbsp;  
> _**Add an Alias for git commands**_  
> `$ git config --global alias.grph "log --all --oneline --decorate --graph --abbrev-commit"`  
  
&nbsp;  
> _**git diff and mergetool**_  
Set diff and merge tool as it is helpful while viewing differences and resolving merge conflicts graphically.  In this example we will be using "meld"  

&nbsp;  
_difftool_  
> `$ git config --global diff.tool meld`  
> `$ git config --global difftool.meld.path "C:\Program Files (x86)\Meld\Meld.exe"`  
(or set application path in environment variable and skip previous line)  
> `$ git config --global difftool.meld.cmd 'meld "$LOCAL" "$REMOTE"'`  
> `$ git config --global difftool.prompt true`  
> `$ git difftool`  
(shows differences graphically in meld app by using "git difftool" instead of "git diff" )

&nbsp;  

_mergetool_
> `$ git config --global merge.tool meld`  
> `$ git config --global mergetool.meld.path "C:\Program Files (x86)\Meld\Meld.exe"`  
(or set application path in environment variable and skip previous line)  
> `$ git config --global mergetool.meld.cmd 'meld "$LOCAL" "$MERGED" "$REMOTE" --output "$MERGED"'`  
> `$ git config --global mergetool.prompt true`  
If a conflict occurs during a merge it can be resolved graphically by,  
> `$ git mergetool`  

&nbsp;  
> _**Colorful informative git**_  
> use posh-git for windows or zsh for unix  

&nbsp;  

## Bare repositories -- Central remote repository
> 
> `$ git init --bare project.git`  
>  
Initializes a bare repository called project.git where developers will be able to push and pull from  
It _dose not have a working directory,_ making changes and committing directly to it is impossible.  
It is a storage facility rather than a development environment.  

&nbsp;  
    
## Initialization and Branching
  
> *git initialization at a local directory*  
> go to the root of the project directory and,   
> `$ git init`

&nbsp;  
> if cloned from remote repository then,  
> Project directory will be named as repository-name if cloning destination not specified  
> or,  
> `$ git clone <repository/source> <target/directory/path>`  
>  And git is already initialized in it, no need to initialize it again.  

&nbsp;  
> *add remote origin (where commits will be pushed) to a local repository*  
> `$ git remote add origin <origin_address>`  
this will add a remote named "origin" which will point to URL specified by origin_address.  
Cloning a repository from remote location automatically sets the remote origin and origin_address.  

&nbsp;  
> *Show information about remote*  
> `$ git remote -v`  

&nbsp;  
> _To check upstream branch from any checked-out branch_  
> `$ git push -u`

&nbsp;  
> *Create a branch from HEAD as the source*  
> `$ git branch <branch_name>`

&nbsp;  
> *Create a new branch from HEAD and switch to that at once*  
> `$ git checkout -b <branch_name>`  
> or,  
> `$ git switch -c <branch_name>`  

&nbsp;  
> *Create and switch to a branch from other branch at once*  
> `$ git checkout -b <new_branch_name> <source_branch>`  
> or,  
> `$ git switch -c <new_branch_name> <source_branch>`  
or,  
> `$ git checkout <source_branch>`  
> `$ git branch <new_branch>`  
> `$ git checkout <new_branch>`  

&nbsp;  
> *Switch to a branch*  
> `$ git checkout <branch_name>`  
> or,  
> `$ git switch <branch_name>`  

&nbsp;  
> *Switch back to previous branch*  
> `$ git switch -`  

&nbsp;  
> *Switch to a branch in detach head state to carry on expermient*  
> `$ git checkout branch_name@{0}`  
> or,  
> `$ git checkout "branch_name@{0}"`  
> in powershell,  
> or,  
> `$ git switch --detach <commit_hash>`  

&nbsp;  
> *Rename a local branch*  
> `$ git branch -m <old_name> <new_name>`

&nbsp;  
> *Show branch from local*  
> `$ git branch`  

&nbsp;  
> *Show all branches from remote and local*  
> `$ git branch -a`

&nbsp;  
> *Show branch tree*  
> `$ git log --graph`  
> `$ git log --graph --pretty=oneline --abbrev-commit`  

&nbsp;  
> *Set upstream branch*  
> `$ git branch --set-upstream-to=origin/<remote_branch_name> <local_branch_name>`  
>  
> `$ git branch -u origin <remote_branch_name>`  
sets currently checked-out branch's upstream to remote_branch_name from origin  
>
> **Only works if upstream remote branch already exists**  
>  
> If it doesn't we need to push that newly created local-branch to remote and set upstream branch for that by following command,  
> `$ git push --set-upstream-to=origin/remote_branch <local_branch>`  
> `$ git push -u <origin> <remote_branch>`  
> or,  
> `$ git push origin HEAD`  
> Upstream indicates where commits will be pushed, [but there must be some commit before doing so]  

&nbsp;  
> **Branch merging**  
> 
> checkout branch where you intend to merge another branch  
> `$ git checkout master`  
> checked out to master branch  

> `$ git branch --merged`  
lists branches that are merged to current branch  

> `$ git merge <feature_branch_name>`  
> or  
>  `$ git merge --squash <source/feature_branch_name>`  
To squash commits from source branch into single commit  

&nbsp;  
> **Octopus merge**  
> `$ git merge master feature-branch`  
merges master with feature-branch and currently checked out branch.  

&nbsp;  
> in case of conflict while merging use,  
> `$ git mergetool`  
>to resolve conflict graphically using mergetool.  
>   
>then  
> `$ git merge --continue`
  
&nbsp;  
> Or you can just simply abort the merge.  
> `$ git merge --abort`

&nbsp;  
> **Branch Deleting**  
> From local  
> `$ git branch -d <branch_name_1> <branch_name_2> <branch_name_3> <branch_name_n>`  
>  
> From remote  
>`$ git push origin --delete <branch_name_1> <branch_name_2> <branch_name_n>`
    
&nbsp;  
## Staging, Committing and Pushing
&nbsp;  
### Tracking and Staging  

> **show modified flies and newly created files or directory**  
> `$ git status`  
> `$ git status -v -v`  
> `$ git status -vv`  
>  
> or short status by,  
> `$ git status -s`  
  
&nbsp;  
> **add files to staging area**  
> `$ git add -A`  
> or  
> `$ git add --all`  

&nbsp;  
> --all is default behaviour of git add, if no other option is specified such as -u or --update  
>adds all files/folders to staging area from everywhere inside git initialized directory  

&nbsp;    
> `$ git add -p`  
> Add to staging area part by part (patch by patch).  

&nbsp;  
> `$ git add -i`  
> Add to staging area using interactive mode.  

&nbsp;  
>_add files to staging area from the current directory and its subdirectories_  
> `$ git add .`  
> is same as,  
> `$ git add --all .`  
>  
&nbsp;  
>_add modified files only_  
> `$ git add -u`  
or  
> `$ git add --update`  
>  
&nbsp;  
>_do not add deleted files to staging area_  
> `$ git add --no-all`  
or  
> `$ git add --ignore-removal`  

&nbsp;  
> **improper way to stage**  
> `$ git add *`  
"*" is a shell command, so whatever returned by shell is added to staging area,  
it is imprecise and inconsistent across multiple operating system and environments  
so avoid using it.

&nbsp;  
> While  
> `$ git add *.txt`  
> adds all files with txt extension to staging area.

&nbsp;  
### Show changes made

>`$ git diff`   
Difference between working directory vs staging area / index.  
Shows changes that are not staged. Will not show newly added files or untracked files.  

&nbsp;    
> `$ git diff [<options>] --no-index [--] <path> <path>`  
compare between two file paths  

&nbsp;  
> if --staged or --cached option is used then diffs between index v/s commit_hash    
> `$ git diff --staged <commit_hash>`  
> or,  
> `$ git diff --cached <commit_hash>`  
> or,  
> `$ git diff --staged`  
The commit_hash section default to HEAD if left empty while --staged or --cached flag is used.  
Review staged changes.  

&nbsp;  
> `$ git diff <options> <commit_hash> <file_name>`  
>  
>`$ git diff HEAD`   
Shows changes that you have in your working directory compared to commit_hash.  
  
&nbsp;  
> `$ git diff branch_name`  
Changes made to a branch  
it will check for differences between "working directory" and "branch_name"  
as branch_name is also a pointer to a commit hash.  

&nbsp;  
>`$ git diff <path/file_name>`  
Shows changes made to a file compared to the index that are not staged or in working directory.  

&nbsp;  
>`$ git diff commit_hash_1..commit_hash_2`  
>  
>`$ git diff commit_hash_1 commit_hash_2`  
>  
>`$ git diff commit_hash_1...commit_hash_2`  
>  
> Shows changes between commit_hash_1 and commit_hash_2  

&nbsp;    
>`$ git diff <options> <commit_hash_1>  <commit_hash_2> <path/file_name.txt>`    
> e.g.,  
> `$ git diff --color-words HEAD~2 HEAD`  
>  or,  
> `$ git diff --color-words <parent_commit> <latest_commit>`  
> 
> Shows differences from file_name.txt between commit_hash_1 and commit_hash_2  
  
&nbsp;  
>`$ git diff --stat`  
> Shows difference in short form.  
  
&nbsp;   
>`$ git diff --color-words`  
Shows difference in color, e.g., added changes in green and removed changes in red.
    
&nbsp;  

#### Custom Diff category and coverter tools

1. Add and edit .gitattributes file in your repository, append the following, 
   > `*.odt diff = odt`  
   > Now all files with odt extension will be diffed in odt category  

2. Set file mode for categories that doesn't make sense while being diffed to binary so git will stop showing diff results.  
   > `$ git config --local diff.odt.binary true`  

3. You can also set a text converter to show diff results in text format  
   > `$ git config --local diff.odt.textconv = odt2text`  
  
&nbsp;  
    
### Committing to local branch

> **Commit staged changes**  
>`$ git commit -m "commit message"`  

&nbsp;  
> **Stage all modified changes and commit**  
>`$ git commit -a -m "commit message"`  
> or,  
>`$ git commit -am "commit message"`  

&nbsp;  
> **View a commit**  
> `$ git show <commit_hash>`  
> `$ git show <commit_hash:directory/file>`  

&nbsp;  
> **show git commit log**  
> `$ git log`  
> `$ git log --stat`    
> `$ git log --graph`  
> `$ git log --all --oneline --decorate --graph --abbrev-commit`  
> as a tree  

&nbsp;  
> **show commit that are not pushed to remote**  
> `$ git log origin/master..master`  

&nbsp;  
> **show all commits that changed a specific file**  
> `$ git log -p filename`  
> `$ git log --follow -- filename`  
> `$ git log -- path/to/filename`  
> `$ git log --all --first-parent --remotes --reflog --author-date-order -- filename`

&nbsp;  
**show total number of commits made**  
> `$ git rev-list --count HEAD`  

&nbsp;  
### Push commit to remote repo  
> First take a pull then push  
>`$ git pull origin branch`  
>`$ git push origin branch`  
> or  
> `$ git pull`  
> `$ git push`  
> If the remote upstream branch is already set or set upstream branch first.  

&nbsp;  
## Stashing and Applying changes  
  
**Stashes all changes from working directory and index is available globally in all branches**  

&nbsp;  
>_stashing changes_  
> `$ git stash save <stash_message>`  

&nbsp;  
>_stash list_  
> `$ git stash list`  

&nbsp;  
>_applying a stash_  
> `$ git stash apply stash@{id}`  
> applies stashed changes to checked-out branch from stashes identified with "id", does not delete the stash  

&nbsp;  
> _pop stash_  
> `$ git stash pop`  
> applies first stash from top of the stash stack to checked out branch and deletes it  

&nbsp;  
> _drop stash_  
> `$ git stash drop stash@{id}`  
> drops stash which is identified by id  

&nbsp;  
> _clear all stash_  
> `$ git stash clear`  
> deletes all stashes  
  
&nbsp;  
  
## How to fix mistakes

&nbsp;  
#### Modify previous commit, --amend  

> Change previous commit's commit message  
> `$ git commit --amend -m "changed message"`  
**Commit Message is also a part of the Commit, changing it changes history** 

&nbsp; 
> Add new files to previous commit  
> `$ git add .`  
> or  
>`$ git add <file_name>`  
> `$ git commit --amend`  

&nbsp; 
### Repository restoration  
&nbsp;
## Git Reset    
  
_**Undo commit(s) locally; changes where or which commit, branch is pointing to, does not directly Moves HEAD, there are 3 types of git reset**_  
  
&nbsp;
### Soft reset  
  
> `$ git reset --soft <commit_hash>`  
> no changes from previous commits are lost, changes remain in staging area  
>  
> 1. Moves branch-pointer to specified commit and stops.  

&nbsp;    
### Mixed/default reset  
  
> `$ git reset <commit_hash>`  
> `$ git reset --mixed <commit_hash>`  
> no changes are lost, changes are unstaged  
>  
> 1. Moves branch-pointer to specified commit and,  
> 2. Updates the index/staging area with content from HEAD to make it identical to HEAD and stops.  

&nbsp;  
### Hard reset  
  
> `$ git reset --hard <commit_hash>`  
> changes are discarded from tracked files and staging area but does not do anything to untracked files,  
> resets back to fresh  
>  
> 1. Moves branch-pointer to specified commit,  
> 2. Updates the index/staging area with content from HEAD and,  
> 3. Copies all content from Index and overwrites Working Directory with them and stops.  
  
&nbsp;  
_GIT Reset Defaults_
> `$ git reset`  
> is same as,  
> `$ git reset --mixed HEAD`  
  
**git reset manipulates all three trees; working tree, index, repository**

&nbsp;  
### Recover commit after hard reset using reflog    

> Execute the following command and grab hash of the commit that was discarded  
> `$ git reflog`  
> git reflog is actually a notebook that records commit traversal history / travel diary of HEAD.  
>  
> then,  
> `$ git checkout <hash>`  
> This is not a branch, we are in a "detached-head state", so we need to create a branch here,  
> Detached HEAD i.e., the HEAD is pointing to a commit that is not a tip of any branch.  
>
> `$ git branch <new-commit-restored-branch>`  
> and then merge your "new-commit-restored-branch" with your desired branch.  
> or cherry-pick commits to another branch.  

&nbsp;  
### Transfer commit to another branch (Cherry Pick)  
  
> find out commit hash of a commit to be transferred to other branch  
> `$ git log`  
> `$ git checkout <target_branch>`  
> `$ git cherry-pick <commit_hash>`  

 &nbsp;  
**Never Ever edit or reset commit that has already been pushed.**  
### Undo pushed changes using revert  
> `$ git revert <commit_hash>`  
> creates a new commit and does not re-write history  
  
&nbsp;  
    
### Index, Working Directory restoration with checkout, reset and restore 

&nbsp;  

### Checkout

> Switching branches or cloning goes through a similar process.  
> When you checkout a branch, 
> 1. it changes HEAD to point to the new branch ref,  
> 2. populates your index with the snapshot of that commit,  
> 3. then copies the contents of the index into your working directory. 

&nbsp;  
> **Note: git checkout <branch_name/commit_hash> -- "pathspec" does not move HEAD.**  
> Rather it skips step 1 then  
> 2. updates index identical to commit_hash   
> 3. overwrites Working Directory with content from the commit specified.  
> _it is not working direcotry safe_  

&nbsp;  
> a double dash (--) is used in most Bash built-in commands and many other commands to signify the end of command options,  
> after which only positional arguments are accepted.  

&nbsp;  

> Undo unstaged changes that has been made to a < file >  
> `$ git checkout <file>`  
> `$ git checkout -- file1 file2`  
>    
> Unlike reset it doesn't default the < tree-ish > parameter to HEAD rather defaults to --staged iplicitly  
> Meaning, overwrites specified files in working tree with content from the respective files in index.  

&nbsp;  
> Make Working Directory identical to Index.  
> `$ git checkout -- .`  
> Index -> Working Directory.(tested)  

&nbsp;  
> Make Index and working tree identical to HEAD  
> `$ git checkout HEAD -- .`  
> or,  
> HEAD -> Index -> Working Directory.  
> (git reset --hard HEAD)  

&nbsp;  
> Update file.ext in index and then working tree with the same version as HEAD.  
> `$ git checkout HEAD -- <file.ext>`  
> HEAD -> Index -> Working Directory.  
>  
  
&nbsp;  
> Restore file1.ext, file2.ext in index and then working tree with the same version as commit_hash.  
> `$ git checkout <commit_hash> -- <file1.ext file2.ext>`  
> `$ git checkout <branch> -- <file1.ext file2.ext>`  
> Commit -> Index -> Working Directory.  
  
&nbsp;  
> Restore tracked but deleted and the deletion not yet staged folder from index to working tree  
> `$ git checkout -- path/to/folder`  

&nbsp;  
>Restore tracked but deleted and staged folder from HEAD to index and then to working tree  
> `$ git checkout HEAD -- path/to/folder`  

&nbsp;  
> Resolve merge conflict by checking out --ours or --theirs version of file that caused a merge conflict  
> `$ git checkout filename.ext --ours`  
> Note: In a merge conflict git splits index area into 3 areas; result, your version, remote version.  

&nbsp;  
> There is also a patch option available  
> `$ git checkout . -p`  
> press s to split a large chunk of change in smaller chunks while in this mode.  
  
&nbsp;  
  
### Reset

> Note: git reset moves branch to a specified commit    
> but with "pathspec" it does not move branch to a specific commit, rather it updates only index (in --mixed mode) with content from the commit specified or HEAD.  
>  
> it could also update working directory but "--hard" option is not permitted with pathspec/file/directories

&nbsp;  
> Remove file/directory from staging area using git reset  
> `$ git reset --mixed HEAD -- file.txt`  
> `$ git reset --mixed HEAD -- directory`  
> or shorthand as,  
> `$ git reset file.txt`  
> `$ git reset directory`  

&nbsp;  
> Unstage everything from index  
> `$ git reset `  
> or,  
> `$ git reset --mixed HEAD`  

&nbsp;  
> Restore tracked and previously committed folder which is deleted and staged.  
> `$ git reset -- path/to/folder`  
> `$ git reset --mixed HEAD -- path/to/folder`  
> Previous command will restore the folder into index from HEAD.  
>  
> Now restore the folder into working directory by the following,  
> `$ git checkout -- path/to/folder`  

&nbsp;  
> Restore tracked and previously committed but deleted file  
> same as folder/directory but with a filename istead.  

&nbsp;  
> Restore a file/directory from earlier version/commit/branch and directly stage to Index.  
> `$ git reset --mixed <commit_hash> -- <pathspec/file/directory/.>`  
> `$ git reset --mixed <branch_name> -- <pathspec/file/directory/.>`  
> this command is powerful and working directory safe.  

&nbsp;  
> Remove chunk of change from staging area  
> `$ git reset -p`  

#### reset v/s checkout summary

reset  
> Undo commits  
> `$ git reset <commit_hash>`
>   
> unstage  
> `$ git reset <file_name>`  

checkout  
> change branch  
> `$ git checkout <commit_hash>`
>   
> copy file contents from index/staging area to working directory  
> `$ git checkout <file_name>`
>   
> copy file contents from other commits into staging/index and working directory  
> `$ git checkout <commit_hash> -- <file_name>`  


&nbsp;  
[Reset Demystified](https://git-scm.com/book/en/v2/Git-Tools-Reset-Demystified)

&nbsp;  
  
**GIT RESET vs CHECKOUT _when used with -- pathspec_**  
> `$ git reset --soft commit_hash -- file.ext`  
> doesn't make sense, as $ git reset with --soft flag and
>  
> 1. Without pathspec, it only moves branch pointer and does not manipulates index and working directory,
>   
> 2. With pathspec reset doesn't even move branch to point to specified commit hash.  
>  
> `$ git reset --hard commit_hash -- file.ext`  
> [_which is not allowed by git reset._]  
>  
> so,  
> `$ git reset --mixed commit_hash -- file.ext`  
> or,  
> `$ git reset commit_hash file.ext`  
> can update the file.ext in **INDEX ONLY**, identical to commit_hash's version.  
>  
> while,  
> `$ git checkout commit_hash -- file.ext`  
> can update the file.ext both in **INDEX and WORKING DIRECTORY**, identical to commit_hash's version  
>  


&nbsp;  

## Restore
  
1. Restore specified paths in the working tree with contents from a restore source.  
2. If a path is tracked but does not exist in the restore source, it will be removed to match the source.  
  
3. The command can also be used to restore the content (tree) in the index with --staged, or restore both the working tree and the index with --worktree and --staged respectively.  

&nbsp;  
_**By default, the restore sources for working tree and index are index and HEAD respectively, --source could be used to specify a commit as the restore source.**_  

&nbsp;  
> Restore file in the worktree from the Index or discard unstaged local changes    
> `$ git restore file1 file2 *.extension .`  
> `$ git restore .`
> is same as,  
> `$ git restore --worktree .`  
> if --staged flag is not passed then it defaults to --worktree and use the Index as source.(Tested)  

&nbsp;  
> Restore file in the Index or unstage changes  
> `$ git restore --staged file1 file2 *.extension .`  
> is same as,  
> `$ git restore --source=HEAD --staged file1 file2 *.extension .`  
> restores files in index/staging area from HEAD.  
> restoring file from HEAD to Index effectively unstages changes.  

&nbsp;  
> Restore file/directory in the Worktree from a commit using provided commit_hash as source  
> `$ git restore --source <commit_hash> directory/files`  

&nbsp;  
> Restore file/directory in the Index from a commit using provided commit_hash as source  
> `$ git restore  --source <commit_hash> --staged directory/files`  

&nbsp;  
> Restore file/directory in the Index and in the Worktree from a commit as source  
> `$ git restore  --source <commit_hash> --staged --worktree directory/files`  
  
&nbsp;  
### Rename/Move file/directory and stage them

&nbsp;  
> Remove files and directory  
> `$ git rm <path_to_file>` 
>  
> `$ git rm -r <path_to_directory>`  
> removes file or directory from staging and working directory (project)  

&nbsp;  
> Rename or move files and directory  
> `$ git mv <path_to/source_file_name> <path_to/target_file_name>`  

&nbsp;  
> Remove file/directory from tracking list which is recently been added to .gitignore but was being tracked by git.  
>`$ git rm --cached file.txt`  
>`$ git rm --cached -r bin/`  

&nbsp;  
#### Remove untracked files

> Remove all untracked directory and files  
> `$ git clean -df`  
  
&nbsp;  
## Git Rebase  
  
Rebases one branch onto another.  
Generally when we create a new branch from another the new branch has all the updates as its parent branch but in case after branch creation, parent branch is updated with some commits that we need in our newly created branch then what should we do ?
&nbsp;  
1. Checkout to its parent branch and pull updates.
   > _Assuming feature-branch was branched off of master branch earlier_  
   >   
   > `$ git checkout master`  
   > `$ git pull origin master`  
2. Checkout to new branch and rebase it onto its parent.
   > `$ git checkout feature-branch`  
   > `$ git pull origin feature-branch`  
   > `$ git rebase master`  
   Feature branch will have the latest updates/commits from master branch, also the base of feature-branch will be moved to the tip of master branch.  
3. If any conflict occurs while you are rebasing you will be switched to an intermediate rebase branch automatically by Git. Resolve all the conflicts there and continue rebasing,
   > `$ git mergetool`  
   > then  
   > `$ git rebase --continue`  
   >  
   > alternatively you can abort the rebase operation by  
   > `$ git rebase --abort`  
   > 
4. Undo a rebase operation by,
   > Actually, rebase saves your starting point to ORIG_HEAD so this is usually as simple as:  
   > `$ git reset --hard ORIG_HEAD`  
   > However, the reset, rebase and merge all save your original HEAD pointer into ORIG_HEAD 
   > so, if you've done any of those commands since the rebase you're trying to undo then you'll have to use the reflog.  
   > [source](https://stackoverflow.com/questions/134882/undoing-a-git-rebase)  

&nbsp;  
### Rebase

This operation works by going to the common ancestor of the two branches (the one you’re on and the one you’re rebasing onto), getting the diff introduced by each commit of the branch you’re on, saving those diffs to temporary files, resetting the current branch to the same commit as the branch you are rebasing onto, and finally applying each change in turn. [Source](https://git-scm.com/book/en/v2/Git-Branching-Rebasing)  

&nbsp;  
#### Best practice:
1. Rebase your local branch onto origin/source_branch  
2. Fix all conflicts if any.  
3. Create a Pull request and ask for testing.  
4. Do a --ff merge with origin/source_branch.  

&nbsp;  
#### DO NOT:
1. DO NOT Rebase if your commits have already been pushed and someone else has based their work off of yours.  

&nbsp;  
#### Rebase pushed branch  

**Do this only when you are the only person working on this branch**  
1. Rebase your local topic branch on top of your desired local branch  
2. Then force push the local branch (override remote topic branch with local topic branch).  
   > `$ git push --force origin feature-branch`  
   > or  
   > `$ git push --force-with-lease`  
   > It is a safer option that checks for any incoming changes from remote which conflicts with local that you are not aware of.  
   > Does not overwrite teammates code.  

&nbsp;  
#### Advanced Rebasing:
&nbsp;  
You can also have your rebase replay on something other than the rebase target branch. Take a history like A history with a topic branch off another topic branch, for example. You branched a topic branch (server) to add some server-side functionality to your project, and made a commit. Then, you branched off that to make the client-side changes (client) and committed a few times. Finally, you went back to your server branch and did a few more commits.  
Suppose you decide that you want to merge your client-side changes into your mainline for a release, but you want to hold off on the server-side changes until it’s tested further. You can take the changes on client that aren’t on server (C8 and C9) and replay them on your master branch by using the --onto option of git rebase:  
> `$ git rebase --onto master server client`  
  
This basically says, “Take the client branch, figure out the patches since it diverged from the server branch, and replay these patches in the client branch as if it was based directly off the master branch instead.” It’s a bit complex, but the result is pretty cool.  
Now you can fast-forward your master branch (see Fast-forwarding your master branch to include the client branch changes):  
  
> `$ git checkout master`  
> `$ git merge client`  
  
Let’s say you decide to pull in your server branch as well. You can rebase the server branch onto the master branch without having to check it out first by running git rebase <basebranch> <topicbranch> which checks out the topic branch (in this case, server) for you and replays it onto the base branch (master):
  
> `$ git rebase master server`  
  
This replays your server work on top of your master work, as shown in Rebasing your server branch on top of your master branch.
Then, you can fast-forward the base branch (master):
  
> `$ git checkout master`  
> `$ git merge server`  
[source](https://git-scm.com/book/en/v2/Git-Branching-Rebasing)  
  
> `$ git pull --rebase`  
> or,  
> `$ git fetch`  
> `$ git rebase remote/branch`  
> in case of a rebase disaster, i.e., someone else overwrote commit that you based your work on and force pushed that.  
  
**You can get the best of both worlds: rebase local changes before pushing to clean up your work, but never rebase anything that you’ve pushed somewhere.**  
  
&nbsp;  
  
#### Fast Forward Merge  
&nbsp;  
If it detects that your current HEAD is an ancestor of the commit you're trying to merge. A fast-forward is when, instead of constructing a merge commit, git just moves your branch pointer to point at the incoming commit. This commonly occurs when doing a git pull without any local changes. [source](https://stackoverflow.com/questions/9069061/what-is-the-difference-between-git-merge-and-git-merge-no-ff)  

If you want to preserve branch topology and merge history you should pass in --no-ff flag with merge command.  

&nbsp;  

## Interactive Rebase
&nbsp;  
"Git interactive rebase" is different from "Git rebase". Interactive rebase allows user to change commit message (reword), delete commits (drop), combines commits into 1 (fixup/squash), reorder commits (By reordering them in Interactive window), commit splitting by providing an interactive window.

"Git rebase" re-bases one branch onto another.

&nbsp;  
> _Select commits for interactive rebase_  
> `$ git rebase -i HEAD~n`  
> (operates on n commits from head to latest n commits; n = 1,2,3...)  
> - in the interactive mode, choose preferred operation for a commit by typing keyword beside that individual commit e.g.,  
> - "reword" to change commit message  
>  
> - "drop" to delete a commit  
>  
> - "fixup/squash" to squash a number of commits into single commit. Squashes all commits marked with squash or fixup keyword into the latest commit.  
>
> - "Reorder" commit entries to "reorder" them.  

&nbsp;  
> _Splitting a commit:_  
>  
> "edit" to go to an "interactive branch" and operate on it;  
> &nbsp;    
   `$ git reset HEAD^`  
    modify, stage and commit them into different commits to "split" single commits into multiple. Then,  
    &nbsp;  
    `$ git rebase --continue`  
    to transfer those new commits to original branch from the intermediate interactive branch.  
>  
>  &nbsp;  

&nbsp;  

## Git Bisect
git-bisect - Use binary search to find a commit that introduced a bug  

&nbsp;  
> `$ git bisect start`  
> starts bisecting mode  

> `$ git bisect good <commit_hash>`  
> select earlier commit when the bug was not introduced yet.  
  
> `$ git bisect bad HEAD`  
> select commit where things are broken.  
    
> `$ git bisect visualize`  
> where am I at, at this moment while bisecting    
  
> In this point we will need a testing script that will check the existence of files and such.   
> the testing script should output 0 if intended functionality is working properly or 1 if not.  
> _Also, the script should not be source-controlled i.e., not tracked by Git._  
  
> `$ git bisect run ./script.ext`  
> now Git bisect will run that script against every commit and report bad-commit based on the script's output.  

> `$ git bisect reset`  
> when bisecting is finished, or you found the bad commit  
  
> What git bisect really does is, checkout commit hashes in a binary search fashion and waits for your instruction.  
> if you do not want to use a test script then you should mark commit as good or bad depending on your manual testing.  

> As Git will checkout a commit hash, you can run and test the project as if you were in a branch.  
> If it's behaviour is okay then mark it good or bad otherwise.  
> `$ git bisect good`  
> `$ git bisect bad`  
> then git will automatically select the next commit hash.  
> Finally after Git bisect reset you will be checked out to HEAD, the latest commit of the branch you were working on.  
  
&nbsp;  
  
## Git Submodules
  
It is a way to use another module (source controlled project i.e., repository) within a parent project  
The benefit of using another repository as your dependency library is, you can always get the latest update  
without getting into useless hassles such as, copying the new source code again and again.  
Making any changes to that submodule will be available to all other parent projects who are using it.  

&nbsp;  
**When you do not want your library to be available publicly but also need it to be source-controlled and used within 
other projects easily, use submodules**  
  
>_Add submodules to your main project_  
> `$ git submodule add <submodule_source> <directory_name>`  
> previous command must be run from root of parent project directory.  

> then in the parent project directory run the following,  
> `$ git commit -m "added a submodules called "`  

> from within the submodule's directory modify your library and commit and push changes from there  
> 
> Now from the parent directory run the following command to get the changes in submodule,  
> `$ git submodule update`  
>  

&nbsp;  

**If you clone a project that has submodule dependency in it, run the following**  
> `$ git submodule init` (to initialize submodule)  
> `$ git submodule update` (to get the latest changes in submodule)  
> or  
> `$ git clone --recurse-submodules <main_project_link>`  
>  
> if you forgot to use recurse when cloning you can also use,   
> `$ git submodule update --init`  
>  
> or to make it foolproof,  
> `$ git submodule update --init --recursive`  

&nbsp;  
## ReReRe Reuse Recorded Resolution

It is an automation feature that resolves merge conflicts automatically based on how you resolved the same conflict last time, to resolve same merge conflict that occurs multiple times we can record conflict resolving steps and reuse them again.

&nbsp;  
> `$ git config --global rerere.enabled true`  
> you should enable this feature before resolving conflicts in order to record them.

&nbsp;  
> `$ git rerere status`  
> to show recorded resolutions  

&nbsp;  
> `$ git config --global rerere.enabled false`  
> to turn this feature off  

&nbsp;  
> delete .git/rr-cache directory to delete recorded resolution.  
> or  
> `$ git rerere forget <recorded_resolution_name>`  
> to forget specific resolution  
>  

&nbsp;  

## Tagging

Git supports two types of tags: lightweight and annotated.  

&nbsp;  
_Annotated tags_ stored as full objects in the Git database. 
They’re checksummed; contain the tagger name, email, and date; have a tagging message;  
and can be signed and verified with GNU Privacy Guard (GPG). It’s generally recommended that  
you create annotated tags so you can have all this information; but if you want a temporary tag  
or for some reason don’t want to keep the other information, lightweight tags are available too  
  
> `$ git tag -a <tag_name> -m <tag_message> <commit_hash or defaults to HEAD>`  
> here -a , -m stands for annotated and message respectively.  

&nbsp;  
> _A lightweight tag_ is very much like a branch that doesn’t change — it’s just a pointer to a specific commit.  
> to create a lightweight tag do not supply -a -s or -m  
> `$ git tag <tag_name> <commit_hash or defaults to HEAD>`  
  
&nbsp;  
>_List of tags_  
> `$ git tag`  

&nbsp;   
>_Search for tags_    
> `$ git tag -l "v1.0.1*"`  
> `$ git tag --list "v1.0.1*"`  

&nbsp;    
>_Sharing Tags_  
By default, the git push command doesn’t transfer tags to remote servers.  
You will have to explicitly push tags to a shared server after you have created them.  
> This process is just like sharing remote branches — you can run   
> `$ git push origin <tagname>`  
> or,  
> `$ git push origin --tags`  
> to push all tags to remote  

&nbsp;  
> _Deleting Tags_  
> To delete a tag on your local repository, you can use  
> `$ git tag -d <tagname>`  

&nbsp;  
> To delete a tag from remote server,  
> `$ git push origin --delete <tag_name>`  

&nbsp;  
> _Checking out Tags_  
> If you want to view the versions of files a tag is pointing to, you can do a git checkout of that tag, although this puts your repository in “detached HEAD” state, which has some ill side effects:  
> `$ git checkout <tag_name>`  

&nbsp;    
## HEAD ~ vs ^ 

HEAD~2 : 2 commits older than HEAD  

HEAD^2 : the second parent of HEAD, if HEAD was a merge, otherwise illegal  

HEAD@{2} : refers to the 3rd listing in the overview of git reflog  

HEAD~~ : 2 commits older than HEAD  

HEAD^^ : 2 commits older than HEAD  

> If HEAD was a merge, then,  
> first parent is the branch into which we merged,  
> second parent is the branch we merged.  

&nbsp;  
## git filter-branch and filter-repo  
> Removing a File from Every Commit  
> `$ git filter-branch --tree-filter 'rm -f passwords.txt' HEAD`  
> To run filter-branch on all your branches, you can pass --all to the command.  

&nbsp;
> Making a Subdirectory the New Root  
> `$ git filter-branch --subdirectory-filter subdirectory_name HEAD`  

&nbsp;  
> Changing Email Addresses Globally  
> ```$ git filter-branch --commit-filter '
>        if [ "$GIT_AUTHOR_EMAIL" = "schacon@localhost" ];  
>        then  
>                GIT_AUTHOR_NAME="Scott Chacon";  
>                GIT_AUTHOR_EMAIL="schacon@example.com";  
>                git commit-tree "$@";  
>        else  
>                git commit-tree "$@";  
>        fi' HEAD`  
>```  
>  &nbsp;

[Index][index]
  
[index]: index.md
