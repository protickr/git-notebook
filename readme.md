# git notebook to future-self

Result of personal practice on Git to understand and experience it hands-on, using a terminal.  
Tried to document what I have learned through practice and tutorials.  
This is not an exhaustive list of commands or descriptions of version control systems.  


# What is git

Git is a distributed version control system that enables us to control versions of a project by tracking different versions of it.
It generally keeps track of all the commits (snapshot or, a package of changes) that we made to a project and lets us traverse through them and also move backward or forward at will.

Distributed version control system is different from Centralized version control system as DVCS allows user to have an updated copy of the whole repository and CVCS allows user to have only a version of the project.

# Git configuration

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


_**help/doc of any command**_
>`$ git help <command_verb>`  
or  
>`$ git <command_verb> --help`  
>`$ git <command_verb> -h`  
(shows short help doc)
>

_**Ignore files**_  
Add files, directories and wild-card entries to .gitignore file, files/directories listed in it will be ignored by git.

_**Configure how git should handle end of line(EOL)**_  
Different for windows and Unix, e.g.,
> `$ git config --global core.autocrlf true` (for windows)  
> `$ git config --global core.autocrlf input` (for UNIX)

_**Set default config editor for git**_  
First set intended app's path in your environment variables.
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
(shows differences graphically in meld app)

_mergetool_
> `$ git config --global merge.tool meld`  
> `$ git config --global mergetool.meld.path "C:\Program Files (x86)\Meld\Meld.exe"`  
(or set application path in environment variable and skip previous line)  
> `$ git config --global mergetool.meld.cmd 'meld "$LOCAL" "$MERGED" "$REMOTE" --output "$MERGED"'`  
> `$ git config --global mergetool.prompt true`  
If a conflict occurs during a merge it can be resolved graphically by,
> `$ git mergetool`

_**Colorful informative git**_
>use posh-git for windows or zsh for unix  

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
> `$ git checkout -b <source_branch> <branch_name>`  
or,  
> `git checkout <source_branch>`  
> `git branch <new_branch>`

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

**Branch merging**  
checkout branch where you intend to merge another branch
> `$ git checkout master`  
checked out to master branch
>
> `$ git branch --merged`  
>lists branches that are merged to master
>
> `$ git merge <feature_branch_name>`  
> or  
>  `$ git merge --squash <source/feature_branch_name>`  
> to squash commits from source branch into single commit

> Octopus merge  
> `$ git merge master feature-branch`  
> merges master with feature-branch and apply merges with currently checked out branch.  

> in case of conflict while merging use,  
> `$ git mergetool`  
> to resolve conflict graphically using mergetool.  
> then  
> `$ git merge --continue`
>
> Or you can just simply abort the merge.  
> `$ git merge --abort`

**Branch Deleting**  
From local `$ git branch -d branch_name`  
From remote `$ git push origin --delete branch_name`  

# Staging, committing and pushing changes

## Tracking and Staging


**show modified flies and newly created files or directory**

> `$ git status`
>
> or short status by,  
> `$ git status -s`


**add files to staging area**
> `$ git add -A`  
or  
> `$ git add --all`
>
>adds files/folders to staging area from everywhere inside git initialized directory
>
> `$ git add -p`  
> Add to staging area part by part.


>_add files to staging area from current directory and its subdirectories_
> `$ git add .`

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

**List of files in staging area**
> `$ git ls-files`

**show changes made**
>`$ git diff`  
> Difference between working directory vs staging.  
> Shows changes that are not staged. Will not show newly added files or untracked files.
>
> `$ git diff --staged`  
> Difference between Staged vs last_commit   
> Review staged changes.
>
>`$ git diff HEAD`  
Shows incoming changes to parent, in this case HEAD, both staged and untracked changes.
>
> `$ git diff branch_name`  
Changes made to a branch
>
>`$ git diff <file_name>`  
Show changes made to file since previous commit
>
>`$ git diff commit_hash_1 commit_hash_2`  
Shows change between commit_1 and commit_2

## Committing to local branch

**Commit staged changes**
>`$ git commit -m "commit message"`

**show git commit log**
> `$ git log`  
> `$ git log --stat`    
> `$ git log --graph`  
> `$ git log --all --oneline --decorate --graph`  
> as a tree


## Push commit to remote repo
>first take a pull then push  
>`$ git pull origin branch`  
>`$ git push origin branch`  
>or  
> `$ git pull`  
> `$ git push`  
> if remote upstream branch is already set or set upstream branch first.  


# How to fix mistakes


> Undo uncommitted changes that has been made to <a_file>  
> `$ git checkout <a_file>`
>
> Restore tracked but deleted folder  
> `git reset -- path/to/folder`  
> `git checkout -- path/to/folder`

## Commit not pushed yet

**re-writes git history**

>Change previous commit message  
> `$ git commit --amend -m "changed message"`

>add new files to previous commit  
> `$ git add .`  
> or  
>`$ git add <file_name>`  
> `$ git commit --amend`

## Transfer commit to other branch

> find out commit hash of a commit to be transferred to other branch  
> `$ git log`  
> `$ git checkout <target_branch>`  
> `$ git cherry-pick <commit_hash_that_need_to_be_cherry_picked>`

## Delete commit, git Reset

**there are 3 types of git reset**

### Soft reset

> no changes are lost, changes remain in staging area  
> `$ git reset --soft <commit_hash_to_where_head_will_be_resetted_to>`

### Mixed/default reset

> no changes are lost, changes are unstaged  
> `$ git reset <commit_hash_to_where_head_will_be_resetted_to>`

### Hard reset

> changes are discarded from tracked files but does not do anything to untracked files, resets back to fresh
>
> `$ git reset --hard <commit_hash_to_where_head_will_be_resetted_to>`

> **removes all untracked directory and files**  
> `$ git clean -df`

> *Remove from staging part by part*  
> `$ git reset -p`

## retrieve changes after a hard reset

> Execute the following command and grab hash of commit that was discarded  
> `$ git reflog`  
> then  
> `$ git checkout <hash>`
>
> This is not a branch, we are in a detached-head state, so we need to create a branch here,  
> `$ git branch <new-commit-restored-branch>`

## Revert a pushed commit
> `$ git revert <commit_hash_that_to_be_undone>`   
> creates a new commit and does not re-write history

## Remove or Rename files and directory
> `$ git rm <path_to_file>`  
> `$ git rm -r <path_to_directory>`  
> removes file or directory from staging and working directory (/project)
>
> `$ git mv <path_to/source_file_name> <path_to/target_file_name>`  
> rename or move file

**Remove file/directory from staging which is recently been ignored by GIT but tracked earlier**
>`$ git rm --cached file.txt`  
>`$ git rm --cached -r bin/`


#### Never Ever edit or reset commit that has been already pushed.  


# Stashing and Applying changes

## Stashing

stash is available globally in all branches
>_stashing changes_  
> `$ git stash save <stash_message>`

>_stash list_  
> `$ git stash list`

>_apply stash_  
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

## Git Rebase

Rebases one branch onto another.  
Generally when we create a new branch from another the new branch has all the updates as its parent branch but in case after branch creation, parent branch is updated with some resources that we need in our newly created branch what should we do ?
1. Checkout to its parent branch and pull updates.
   > `$ git checkout master`  
   > `$ git pull origin master`
2. Checkout to new branch and rebase it onto its parent.
   > `$ git checkout feature-branch`  
   > `$ git pull origin feature-branch`  
   > `$ git rebase master`  
   Feature branch will have the latest updates/commits as master branch.
3. If any conflict occurs while you are rebasing you will be switched to an intermediate rebase branch automatically by Git. Resolve all the conflicts there and continue rebasing,
   > `$ git mergetool`  
   > then  
   > `$ git rebase --continue`
   >
   > alternatively you can abort the rebase operation by  
   > `$ git rebase --abort`

### Rebase
This operation works by going to the common ancestor of the two branches (the one you’re on and the one you’re rebasing onto), getting the diff introduced by each commit of the branch you’re on, saving those diffs to temporary files, resetting the current branch to the same commit as the branch you are rebasing onto, and finally applying each change in turn. [Source](https://git-scm.com/book/en/v2/Git-Branching-Rebasing)

#### Best practice:
1. Rebase your local branch onto origin/source_branch
2. Fix all conflicts if any.
3. Create a Pull request and ask for testing.
4. Do a --ff merge with origin/source_branch.

#### DO NOT:
1. DO NOT Rebase if your commits have already been pushed and someone else has based their work off of yours.

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

###### Fast Forward Merge

If it detects that your current HEAD is an ancestor of the commit you're trying to merge. A fast-forward is when, instead of constructing a merge commit, git just moves your branch pointer to point at the incoming commit. This commonly occurs when doing a git pull without any local changes. [source](https://stackoverflow.com/questions/9069061/what-is-the-difference-between-git-merge-and-git-merge-no-ff)

If you want to preserve branch topology and merge history you should pass in --no-ff flag with merge command.  

# Interactive Rebase
"Git interactive rebase" is completely different from "Git rebase". Interactive rebase allows user to change commit message (reword), delete commits (drop), combines commits into 1 (fixup/squash), reorder commits (By reordering them in Interactive window), splitting commits by providing an interactive window.

"Git rebase" re-bases one branch onto another.

**Select commits for interactive rebase**
> `$ git rebase -i HEAD~n`  
> (operates on n commits from head to latest n commits; n = 1,2,3...)
> - in interactive mode select operation by typing keyword beside individual commit e.g.,
> - "reword" to change commit message
>
> - "drop" to delete a commit
>
> - "fixup/squash" to squash a number of commits into single commit. Squashes all commits marked with squash or fixup keyword into the latest commit.
>
> - "edit" to go to an "interactive branch" and operate on them;  
    `$ git reset HEAD^`  
    modify, stage and commit them into different commits to "split" single commits into multiple. Then,
    `$ git rebase --continue`  
    to transfer those new commits to original branch from interactive branch.
>
> - Reorder commit entries to "reorder" them


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


# ReReRe Reuse Recorded Resolution

It is a merge conflict resolving automation feature offered by Git, to resolve same merge conflict that occurs multiple times we can record conflict resolving steps and reuse them again.

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
> 
> `$ git rerere forget <recorded_resolution_name>`  
> to forget specific resolution  
> 


[Index][index]

[index]: index.md