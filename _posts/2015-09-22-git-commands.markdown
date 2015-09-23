---
layout:     post
title:      "Git commands"
subtitle:   "Tổng hợp git commands"
date:       2015-09-22 12:00:00
author:     "tientm"
header-img: "img/git.jpg"
---

# Staging and Remotes
---

## Git diff

`git diff` shows unstaged differences since last commit.

Use `git diff --staged` to view staged differences.

## Unstage

Use `git reset HEAD <file>` to unstage.

> HEAD refers to last commit on the current branch.

`git checkout -- <file>` blows away all changes since last commit.

## Skip tracking and commit

`git commit -a -m "Message"` adds changes from all tracked files.

## Undoing a commit

We forgot something on commit.

`git reset --soft HEAD^` resets all changes into staging. `^` moves all changes to the commit before HEAD.

Maybe we forgot to add a file.

`git commit --amend -m "New message"`. `--amend` adds new tracked changes to the last commit.

## Useful command

|Commands|Meaning|
|--|--|
|`git reset --soft HEAD^`|Undoes last commit, put changes into staging|
|`git commit --amend -m "New message"`|Changes the last commit|
|`git reset --hard HEAD^`|Undoes last commit, blow away all changes|
|`git reset --hard HEAD^^`|Undoes last 2 commits and all changes|

__Dont do these after pushing__

## Adding a remote

> Origin refers canonical repository, our official repository that most of people use for their project.

`git remove add origin http://github.com/Gregg/git-real.git`

- `add` new remote
- `origin` our name for this remote
- `http://...` address

`git remote -v` shows all remotes.

## Pushing to remote

`git push -u origin master`

- `origin`: remote repository name
- `master`: local branch to push

## Pulling from remote

`git pull` pulls down all changes from remote repository and sync up your local repository.

## Working with remotes

|Commands|Meaning|
|--|--|
|`git remote add <name> <address>`|Adds new remote|
|`git remote rm <name>`|Removes remote|
|`git push -u <name> <branch>`|Pushes to remote|

`-u` means that you don't have to specify the name and branch in the next pushing, just run `git push`.

# Cloning and Branching
---

## Cloning a repository

~~~
$ git clone https://github.com/codeschool/git-real.git
Cloning into 'git-real'...
~~~

~~~
$ git clone https://github.com/codeschool/git-real.git git-demo
Cloning into 'git-demo'
~~~

- `https://...`: URL of remote repository
- `git-demo`: local folder name

Git Clone operation:

1. Downloads the entire repository into a new git-real directory.
2. Adds the ‘origin’ remote, pointing it to the clone URL.
3. Checks out initial branch (likely master).

## Branching

Need to work on a feature that will take some time? Time to branching out.

|Commands|Meaning|
|--|--|
|`git branch <name>`|Creates new branch. HEAD still on master branch|
|`git checkout <name>`|Switches to branch `<name>`. HEAD is now on `<name>` branch|
|`git checkout -b <name>`|Creates and switch to branch `<name>`|
|`git merge <name>`|Merges `<name>` branch into another|
|`git branch -d <name>`|Safety remove branch `<name>`|

### Fast-forward merge

Fast-forward merge will be used on condition that there is only one branch has commits. If other branch also has commits we wont use fast-forward. Fast-forward is a easy way for git to merge 2 branches. Because there are nothing new in the other branch.

### Recursive merge

If 2 branches have new commits after branching out, we will use recursive merge due to the existence of conflicts.

# Collaboration Basics
---

## Git push rejected

__Situation:__ Jane committed some new files (product.rb and store.rb) and pushed them to Github. Gregg updated, committed his README file and try to push it to Github but he failed. What happened?

~~~
gregg $ git push
To https://github.com/codeschool/git-real.git
! [rejected] master -> master (non-fast-forward)  # Cannot write over Jane’s commit
error: failed to push some refs to 'https://github.com/codeschool/git-real.git'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. Merge the remote changes (e.g. 'git pull')
hint: before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
$ git pull # Uses git pull to get Jane code before push
$ git push
...
...
Success!
~~~

## What does `git pull` do?

1. Fetches (or Sync) our local repository with the remote one. It corresponds with `git fetch`. Fetch doesn't actually update any of our local code. It fetches master branch from github to origin/master branch on our local repo.
2. After that it merges the origin/master with master branch. `git merge origin/master`.

## Merge conflicts

__Situation:__ Both Jane and Gregg updated and committed on the same files. Jane pushed her commit to Github. Gregg pulled down the Github code and he got the conflicts. So, what happened?

~~~
gregg $ git pull
remote: Counting objects: 5, done.
remote: Compressing objects: 100% (1/1), done.
remote: Total 3 (delta 1), reused 3 (delta 1)
Unpacking objects: 100% (3/3), done.
From https://github.com/Gregg/git-real
 ee47baa..4e76d35 master -> origin/master
Auto-merging README.txt
CONFLICT (content): Merge conflict in README.txt
Automatic merge failed; fix conflicts and then commit the result.
~~~

You need to edit conflict files and correct they.

~~~
here is my readme
<<<<<<< HEAD # Our local version
the cake is a lie.
=======
the cake is telling the truth! # Jane's version
>>>>>>>
4e76d3542a7eee02ec516a47600002a90a4e4b48
~~~

After correcting, Gregg might push his code.

# Remote branches and Tags
---

Why create a remote branch?

- When you need other people to work on your branch.
- Any branch that will last more than a day

|Commands|Meaning|
|--|--|
|`git checkout -b <shopping_cart>`|Creates and switches to new branch|
|`git push <origin> <shopping_cart>`|Links local branch to remote branch (tracking)|
|`git fetch`|Fetches new branches|
|`git branch`|Lists all local branches|
|`git branch -r`|Lists all remote branches|
|` git remote show <origin>`|Shows all remote branches and local branches|
|` git push <origin> :<shopping_cart>`|Deletes remote branch|
|`git branch -d <shopping_cart>`|Deletes local branch|
|`git branch -D <shopping_cart>`|Forces to delete local branch|
|`git remote prune <origin>`|Cleans up deleted remote branches|

A tag is a reference to a commit (used mostly for release versioning).

|Commands|Meaning|
|--|--|
|`git tag`|Lists all tags|
|`git checkout v0.0.1`|Checks out code at commit|
|`git tag -a <v0.0.3> -m <"version 0.0.3">`|Adds a new tag|
|`git push --tags`|Pushes new tag|
