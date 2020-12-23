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

[Index][index]

[index]: ../index.md