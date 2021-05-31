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
  
### GIT structure  
There are three distinct compartments that are used by GIT to operate i.e.,  
_**Working Directory / Tree**_ > ( `$ git add` )> _**Staging Area / Index**_ >  
( `$ git commit -m "msg"` ) > _**Repository**_ > (`$ git push` ) > _**Remote Repository**_  
Repository always has a commit hash that points to latest commit which is labeled as HEAD  
But working directory and staging area do not,  
Instead staging area keeps a virtual reference to latest commit or HEAD.  
Meaning as if Staging Area is as updated as latest commit of the repository.  
  
  
## Git configuration

\
_**Retrieve installed git version**_
>`$ git --version`

_**Set git author's username and email**_
>`$ git config --global user.name "user_name"`  
>`$ git config --global user.email "email"`

_**all configuration list**_
>`$ git config --list`  
>`$ git config --local --list`  
>`$ git config --global --list`  
>`$ git config --system --list`  
local config, lists applicable config for current repository.  

_**help/doc of any command**_
>`$ git help <command_verb>`  
or  
>`$ git <command_verb> --help`  
> 
>`$ git <command_verb> -h`  
(shows short help doc)  
>

**Ignore files**  
Add files, directories and wild-card entries to .gitignore file, files/directories listed in it will be ignored by git.

_**Configure how git should handle end of line(EOL)**_  
Different for windows and Unix, e.g.,
> `$ git config --global core.autocrlf true` (for windows)  
> `$ git config --global core.autocrlf input` (for UNIX)  

_**Set default config editor for git**_  
First set the intended app's path in your environment variables.
> `$ git config --global core.editor "app --wait"`  
(Open config file in "app" and edit global-config by,)  
> `$ git config --global -e`

_**git diff and mergetool**_  
Set diff and merge tool as it is helpful while viewing differences and resolving merge conflicts graphically.  In this example we will be using "meld"  

_difftool_
> `$ git config --global diff.tool meld`  
> `$ git config --global difftool.meld.path "C:\Program Files (x86)\Meld\Meld.exe"`  
(or set application path in environment variable and skip previous line)  
> `$ git config --global difftool.meld.cmd 'meld "$LOCAL" "$REMOTE"'`  
> `$ git config --global difftool.prompt true`  
> `$ git difftool`  
(shows differences graphically in meld app by using "git difftool" instead of "git diff" )

_mergetool_
> `$ git config --global merge.tool meld`  
> `$ git config --global mergetool.meld.path "C:\Program Files (x86)\Meld\Meld.exe"`  
(or set application path in environment variable and skip previous line)  
> `$ git config --global mergetool.meld.cmd 'meld "$LOCAL" "$MERGED" "$REMOTE" --output "$MERGED"'`  
> `$ git config --global mergetool.prompt true`  
If a conflict occurs during a merge it can be resolved graphically by,
> `$ git mergetool`

_**Colorful informative git**_
> use posh-git for windows or zsh for unix  

## Initialization and Branching

*git initialization at a local directory*
> go to the root of the project directory and,   
> `$ git init`  

if cloned from remote repository then,  
Project directory will be named as repository-name if cloning destination not specified  
And git is already initialized in it, no need to initialize it again.  
  
*add remote origin (where commits will be pushed) to a local repository*
> `$ git remote add origin <origin_address>`  
this will add a remote named "origin" which will point to URL specified by origin_address.  
Cloning a repository from remote location automatically sets the remote origin and origin_address.

*Set upstream branch*
> `$ git branch --set-upstream-to=origin/<remote_branch_name> <local_branch_name>`
>
> `$ git branch -u origin <remote_branch_name>`  
sets currently checked-out branch's upstream to remote_branch_name from origin
>
**Only works if upstream remote branch already exists**  
  
If it doesn't we need to push that newly created local-branch to remote and set upstream branch for that by following command,
> `$ git push --set-upstream-to=origin/remote_branch <local_branch>`  
> `$ git push -u <origin> <remote_branch>`  
or,  
> `$ git push origin HEAD`  
Upstream indicates where commits will be pushed, [but there must be some commit before doing so]  

*Show information about remote*  
> `$ git remote -v`  

_To check upstream branch from any checked-out branch_
> `$ git push -u`

*Create a branch*
> `$ git branch <branch_name>`

*Create and switch to a branch from other branch at once*
> `$ git checkout -b <new_branch_name> <source_branch>`  
or,  
> `git checkout <source_branch>`  
> `git branch <new_branch>`  

*Switch to a branch*
> `$ git checkout <branch_name>`

*Create a new branch and switch to that at once*
> `$ git checkout -b <branch_name>`

*Rename a local branch*
> `$ git branch -m <old_name> <new_name>`

*Show branch from local*
> `$ git branch`  
  
*Show all branches from remote and local*
> `$ git branch -a`

*Show branch tree*
> `$ git log --graph`  
> `git log --graph --pretty=oneline --abbrev-commit`

**Branch merging**  
checkout branch where you intend to merge another branch
> `$ git checkout master`  
checked out to master branch

> `$ git branch --merged`  
lists branches that are merged to current branch  

> `$ git merge <feature_branch_name>`  
> or  
>  `$ git merge --squash <source/feature_branch_name>`  
To squash commits from source branch into single commit  

**Octopus merge**  
> `$ git merge master feature-branch`  
merges master with feature-branch and currently checked out branch.  

in case of conflict while merging use,  
> `$ git mergetool`  
to resolve conflict graphically using mergetool.  
  
>then  
> `$ git merge --continue`
  
Or you can just simply abort the merge.  
> `$ git merge --abort`

**Branch Deleting**  
From local `$ git branch -d <branch_name_1> <branch_name_2> <branch_name_2> <branch_name_n>`  
From remote `$ git push origin --delete <branch_name_1> <branch_name_2> <branch_name_n>`  

## Staging Committing Pushing

### Tracking and Staging

**show modified flies and newly created files or directory**  
> `$ git status`  
> or short status by,  
> `$ git status -s`  
  
**add files to staging area**
> `$ git add -A`  
> or  
> `$ git add --all`  

--all is default behaviour of git add, if no other option is specified such as -u -i -p  
adds all files/folders to staging area from everywhere inside git initialized directory  
  
> `$ git add -p`  
> Add to staging area part by part (patch by patch).  
  
> `$ git add -i`  
> Add to staging area using interactive mode.  
  
>_add files to staging area from the current directory and its subdirectories_  
> `$ git add .`  
> is same as,  
> `$ git add --all .`  
>  
>_add modified files only_  
> `$ git add -u`  
or  
> `$ git add --update`  

**improper way to stage**
> `$ git add *`  
"*" is a shell command, so whatever returned by shell is added to staging area,  
it is imprecise and inconsistent across multiple operating system and environments  
so avoid using it.  
  
> While  
> `$ git add *.txt`  
> adds all files with txt extension to staging area.
  
### Show changes made

>`$ git diff`   
Difference between working directory vs staging area / index.  
Shows changes that are not staged. Will not show newly added files or untracked files.  
  
> `$ git diff [<options>] --no-index [--] <path> <path>`  
compare between two file paths  
  
if --staged or --cached option is used then diffs between index v/s commit_hash    
> `$ git diff --staged <commit_hash>`  
> or,  
> `$ git diff --cached <commit_hash>`  
> or,  
> `$ git diff --staged`  
The commit_hash section default to HEAD if left empty while --staged or --cached flag is used.  
Review staged changes.  
  
> `$ git diff <options> <commit_hash> <file_name>`  
>  
>`$ git diff HEAD`   
Shows changes that you have in your working directory compared to commit_hash.  
  
> `$ git diff branch_name`  
Changes made to a branch  
it will check for differences between "working directory" and "branch_name"  
as branch_name is also a pointer to a commit hash.  
  
>`$ git diff <path/file_name>`  
Shows changes made to a file compared to the index that are not staged or in working directory.  
  
>`$ git diff commit_hash_1..commit_hash_2`  
>  
>`$ git diff commit_hash_1 commit_hash_2`  
>  
>`$ git diff commit_hash_1...commit_hash_2`  
>  
Shows changes between commit_hash_1 and commit_hash_2  
  
>`$ git diff <options> <commit_hash_1>  <commit_hash_2> <path/file_name.txt>`    
Shows differences from file_name.txt between commit_hash_1 and commit_hash_2  
  
>`$ git diff --stat`  
Shows difference in short form.  
  
>`$ git diff --color-words`  
Shows difference in color, e.g., added changes in green and removed changes in red.  
  
### Committing to local branch

**Commit staged changes**  
>`$ git commit -m "commit message"`  
  
**View a commit**  
> `$ git show <commit_hash>`  
> `$ git show <commit_hash:directory/file>`  
  
**show git commit log**  
> `$ git log`  
> `$ git log --stat`    
> `$ git log --graph`  
> `$ git log --all --oneline --decorate --graph --abbrev-commit`  
> as a tree  
  
  
### Push commit to remote repo  
> First take a pull then push  
>`$ git pull origin branch`  
>`$ git push origin branch`  
> or  
> `$ git pull`  
> `$ git push`  
> If the remote upstream branch is already set or set upstream branch first.  
  
## Stashing and Applying changes  
  
**Stashes all changes from working directory and index is available globally in all branches**  
>_stashing changes_  
> `$ git stash save <stash_message>`  
  
>_stash list_  
> `$ git stash list`  
  
>_applying a stash_  
> `$ git stash apply stash@{id}`  
> applies stashed changes to checked-out branch from stashes identified with "id", does not delete the stash  
  
> _pop stash_  
> `$ git stash pop`  
> applies first stash from top of the stash stack to checked out branch and deletes it  
  
> _drop stash_  
> `$ git stash drop stash@{id}`  
> drops stash which is identified by id  
  
> _clear all stash_  
> `$ git stash clear`  
> deletes all stashes  
  
  
## How to fix mistakes  

### Repository restoration  

#### Modify previous commit, --amend  
**re-writes git history**  
  
> Change previous commit's commit message  
> `$ git commit --amend -m "changed message"`  
  
> Add new files to previous commit  
> `$ git add .`  
> or  
>`$ git add <file_name>`  
> `$ git commit --amend`  

**Commit Message is also a part of the Commit, changing it changes history**
  
#### Undo commit(s) locally by Git Reset  
  
**Changes where or which commit branch is pointing to, does not directly Moves HEAD**  
**there are 3 types of git reset**  
  
#### Soft reset  
  
> `$ git reset --soft <commit_hash_where_tip_of_the_branch_will_be_resetted_to>`  
> no changes are lost, changes remain in staging area  
>  
> Moves branch-pointer to specified commit and stops.  
  
#### Mixed/default reset  
  
> `$ git reset <commit_hash_where_tip_of_the_branch_will_be_resetted_to>`  
> no changes are lost, changes are unstaged  
>  
> Moves branch-pointer to specified commit and,  
> Updates the index/staging area with content from HEAD to make it identical to HEAD.  
  
#### Hard reset  
  
> `$ git reset --hard <commit_hash_where_tip_of_the_branch_will_be_resetted_to>`  
> changes are discarded from tracked files and staging area but does not do anything to untracked files,  
> resets back to fresh  
>  
> Moves branch-pointer to specified commit,  
> Updates the index/staging area with content from HEAD and,  
> Copies all content from Index and overwrites Working Directory with them.  

**GIT Reset Defaults**
> `$ git reset`  
> is same as,  
> `$ git reset --mixed HEAD`  

### Recover commit after hard reset using reflog    

> Execute the following command and grab hash of the commit that was discarded  
> `$ git reflog`  
> git reflog is actually a notebook that records commit traversal history / travel diary of HEAD.  
>  
> then,  
> `$ git checkout <hash>`  
> This is not a branch, we are in a "detached-head state", so we need to create a branch here,  
> Detached HEAD i.e., the HEAD is pointing to a commit that is not a tip of any branch.  

> `$ git branch <new-commit-restored-branch>`  
> and then merge your "new-commit-restored-branch" with your desired branch.  
> or reset --mixed and then stash changes and pop them in your branch.  
> or cherry-pick commits to another branch.  
  
### Transfer commit to another branch (Cherry Pick)  
  
> find out commit hash of a commit to be transferred to other branch  
> `$ git log`  
> `$ git checkout <target_branch>`  
> `$ git cherry-pick <commit_hash_that_need_to_be_cherry_picked>`  

**Never Ever edit or reset commit that has already been pushed.**  
  
### Undo pushed changes using revert  
> `$ git revert <commit_hash_of_the_changes_to_undo>`  
> **creates a new commit and does not re-write history**  
  
### Index / Staging Area , Working Directory / Working Tree  restoration with checkout, reset and restore  

**Restore file and direcotry using,**  

#### Checkout

> Note: git checkout moves HEAD to point to target branch but with "pathspec" it does not. 
> Rather it updates index and overwrites Working Directory with  
> content from the commit specified.  
  
> a double dash (--) is used in most Bash built-in commands and many other commands to signify the end of command options,  
> after which only positional arguments are accepted.  
  
> `$ git checkout <a_file>`  
> `$ git checkout -- file1 file2`  
> Undo unstaged changes that has been made to <a_file>  
> Unlike reset it doesn't default the <tree-ish> parameter to HEAD rather defaults to --staged iplicitly  
> Meaning, overwrites specified files in working tree with content from the respective files in index.  
  
> `$ git checkout -- .`  
> Makes Working Directory identical to Index.  
  
> `git checkout HEAD -- .`  
> Makes index and working tree identical to HEAD  
> HEAD -> Index -> Working Directory.  
> (git reset --hard HEAD)
  
> `git checkout HEAD -- <file.ext>`  
> Updates file.ext in index and then working tree with the same version as HEAD.  
> HEAD -> Index -> Working Directory.
> (git rest --hard HEAD file.ext) which is not allowed by git reset.   
  
> `git checkout <commit_hash> -- <file1.ext file2.ext>`  
> `git checkout <branch> -- <file1.ext file2.ext>`  
> Updates file1.ext, file2.ext in index and then working tree with the same version as commit_hash.  
> Commit -> Index -> Working Directory.   

> Restore tracked but deleted folder from index to working tree  
> `git checkout -- path/to/folder`  
  
> Resolve merge conflict by checking out --ours or --theirs version of file that caused a merge conflict  
> `git checkout filename.ext --ours`  
> Note: In a merge conflict git splits index area into 3 areas; result, your version, remote version.  
  
> There is also a patch option available if using "pathspec"  
> `git checkout . -p`  
> press s to split a large chunk of change in smaller chunks while in this mode.  
  
#### Reset

Remove file/directory from staging area using git reset  
> `$ git reset file.txt`  
> `$ git reset HEAD -- file.txt`  
> `$ git reset HEAD -- directory`  

Remove chunk of change from staging area  
> `$ git reset -p`  

> Restore tracked but deleted folder  
> `git reset -- path/to/folder`  

#### Restore

> Restores file in working tree and index  
>  
> `$ git restore --staged file1 file2 *.extension .`  
> restores/removes files from index/staging to working tree/directory  
>  
> `$ git restore file1 file2 *.extension .`  
>  restores/removes changes from working tree/directory  
>  
> `$ git restore --source <commit_hash> files .`  
> restores file from a commit using provided commit_hash as source  
  
> **removes all untracked directory and files**  
> `$ git clean -df`  
  
> *Remove from staging area part by part (patch by patch)*  
> `$ git reset -p`  
  
#### Rename/Move file/directory and stage them

**Remove files and directory**  
> `$ git rm <path_to_file>`  
> `$ git rm -r <path_to_directory>`  
> removes file or directory from staging and working directory (project)  

**Rename or move files and directory**
> `$ git mv <path_to/source_file_name> <path_to/target_file_name>`  
> rename or move file  

**Remove file/directory from tracking list which is recently been ignored by GIT but tracked earlier**  
>`$ git rm --cached file.txt`  
>`$ git rm --cached -r bin/`  


## Git Rebase  
  
Rebases one branch onto another.  
Generally when we create a new branch from another the new branch has all the updates as its parent branch but in case after branch creation, parent branch is updated with some commits that we need in our newly created branch then what should we do ?
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

   
#### Rebase
This operation works by going to the common ancestor of the two branches (the one you’re on and the one you’re rebasing onto), getting the diff introduced by each commit of the branch you’re on, saving those diffs to temporary files, resetting the current branch to the same commit as the branch you are rebasing onto, and finally applying each change in turn. [Source](https://git-scm.com/book/en/v2/Git-Branching-Rebasing)

#### Best practice:
1. Rebase your local branch onto origin/source_branch  
2. Fix all conflicts if any.  
3. Create a Pull request and ask for testing.  
4. Do a --ff merge with origin/source_branch.  
  
#### DO NOT:
1. DO NOT Rebase if your commits have already been pushed and someone else has based their work off of yours.  
  
#### Rebase pushed branch  
**Do this only when you are the only person working on this branch**  
1. Rebase your local topic branch on top of your desired local branch  
2. Then force push the local branch (override remote topic branch with local topic branch).  
   > `$ git push --force origin feature-branch`  
   > or  
   > `$ git push --force-with-lease`  
   > It is a safer option that checks for any incoming changes from remote which conflicts with local that you are not  
   > aware of. Does not overwrite teammates code.  
   
#### Advanced Rebasing:
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
> in case of a rebase disaster.  
  
##### Fast Forward Merge  

If it detects that your current HEAD is an ancestor of the commit you're trying to merge. A fast-forward is when, instead of constructing a merge commit, git just moves your branch pointer to point at the incoming commit. This commonly occurs when doing a git pull without any local changes. [source](https://stackoverflow.com/questions/9069061/what-is-the-difference-between-git-merge-and-git-merge-no-ff)  

If you want to preserve branch topology and merge history you should pass in --no-ff flag with merge command.  

## Interactive Rebase
"Git interactive rebase" is different from "Git rebase". Interactive rebase allows user to change commit message (reword), delete commits (drop), combines commits into 1 (fixup/squash), reorder commits (By reordering them in Interactive window), splitting commits by providing an interactive window.

"Git rebase" re-bases one branch onto another.

**Select commits for interactive rebase**
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
> 
> _Splitting a commit:_  
> - "edit" to go to an "interactive branch" and operate on it;  
    `$ git reset HEAD^`  
    modify, stage and commit them into different commits to "split" single commits into multiple. Then,  
    `$ git rebase --continue`  
    to transfer those new commits to original branch from the intermediate interactive branch.  
>  
  
## Git Bisect
git-bisect - Use binary search to find a commit that introduced a bug  


> `$ git bisect start`  
> starts bisecting mode  
> `$ git bisect good <commit_hash>`  ( select earlier commit when the bug was not introduced yet)  
> `$ git bisect bad HEAD` ( select commit where things are broken)  
> `$ git bisect visualize` (where am I at, at this moment while bisecting)  
>  
> In this point we will need a testing script that will check the existence of files and such   
> the testing script should output 0 if intended functionality is working properly or 1 if not.  
> Also, the script should not be source-controlled i.e., not tracked by Git.  
>  
> `$ git bisect run ./script.ext`  
> now Git bisect will run that script against every commit and report bad-commit based on  
> the script's output.  
> `$ git bisect reset`  (when bisecting is finished, or you found the bad commit)  
>  
> What git bisect really does is, checkout commit hashes in a binary search fashion and waits for your instruction.  
> if you do not want to use a test script then you should mark commit as good or bad depending on your manual testing.  
> As Git will checkout a commit hash, you can run and test the project as if you were in a branch. If it's behaviour is  
> okay then mark it good or bad otherwise.  
> `$ git bisect good`  
> `$ git bisect bad`  
> then git will automatically select the next commit hash.  
> Finally after Git bisect reset you will be checked out to HEAD, the latest commit of the branch you were working on.  
  
  
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
>  
> if you forgot to use recurse when cloning you can also use,   
> `$ git submodule update --init`  
>  
> or to make it foolproof,  
> `$ git submodule update --init --recursive`  


## ReReRe Reuse Recorded Resolution

It is an automation feature that resolves merge conflicts automatically based on how you resolved the same conflict last time, to resolve same merge conflict that occurs multiple times we can record conflict resolving steps and reuse them again.

> `$ git config --global rerere.enabled true`  
> you should enable this feature before resolving conflicts in order to record them.
>  
> `$ git rerere status`  
> to show recorded resolutions  
>  
> `$ git config --global rerere.enabled false`  
> to turn this feature off  
>  
> delete .git/rr-cache directory to delete recorded resolution.  
> or  
> `$ git rerere forget <recorded_resolution_name>`  
> to forget specific resolution  
>  


[Index][index]

[index]: index.md
