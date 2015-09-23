---
layout:     post
title:      "Git commands"
subtitle:   "Tổng hợp git commands"
date:       2015-09-22 12:00:00
author:     "tientm"
header-img: "img/git.jpg"
---

# Staging and Remotes

## Git diff
---

`git diff` shows unstaged differences since last commit.

Use `git diff --staged` to view staged differences.

## Unstage
---

Use `git reset HEAD <file>` to unstage.

> HEAD refers to last commit on the current branch.

`git checkout -- <file>` blows away all changes since last commit.

## Skip tracking and commit
---

`git commit -a -m "Message"` adds changes from all tracked files.

## Undoing a commit
---

We forgot something on commit.

`git reset --soft HEAD^` resets all changes into staging. `^` moves all changes to the commit before HEAD.

Maybe we forgot to add a file.

`git commit --amend -m "New message"`. `--amend` adds new tracked changes to the last commit.

## Useful command
---

|Commands|Meaning|
|--|--|
|`git reset --soft HEAD^`|Undo last commit, put changes into staging|
|`git commit --amend -m "New message"`|Change the last commit|
|`git reset --hard HEAD^`|Undo last commit, blow away all changes|
|`git reset --hard HEAD^^`|Under last 2 commits and all changes|

__Dont do these after pushing__

## Adding a remote
---

> Origin refers canonical repository, our official repository that most of people use for their project.

`git remove add origin http://github.com/Gregg/git-real.git`

- `add` new remote
- `origin` our name for this remote
- `http://...` address

`git remote -v` shows all remotes.

## Pushing to remote
---

`git push -u origin master`

- `origin`: remote repository name
- `master`: local branch to push

## Pulling from remote
---

`git pull`: pull down all changes from remote repository and sync up your local repository.

## Working with remotes
---

|Commands|Meaning|
|--|--|
|`git remote add <name> <address>`|Add new remote|
|`git remote rm <name>`|Remove remote|
|`git push -u <name> <branch>`|Push to remote|

`-u` means that you don't have to specify the name and branch in the next pushing, just run `git push`.

# Cloning and Branching

## Cloning a repository
---

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
---

Need to work on a feature that will take some time? Time to branching out.

|Commands|Meaning|
|--|--|
|`git branch <name>`|Create new branch. HEAD still on master branch|
|`git checkout <name>`|Switch to branch `<name>`. HEAD is now on `<name>` branch|
|`git merge <name>`|Merge `<name>` branch into another|
|`git branch -d <name>`|Safety remove branch `<name>`|

### Fast-forward merge

Fast-forward merge will be used on condition that only one branch has commits. If other branch also has commits we wont use fast-forward. Fast-forward is a easy way for git to merge 2 branches. Because there are nothing new in the other branch.

### Recursive merge

If 2 branches have new commits after branching out, we will use recursive merge due to the existence of conflicts.
