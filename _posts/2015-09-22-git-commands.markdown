---
layout:     post
title:      "Git commands"
subtitle:   "Tổng hợp git commands"
date:       2015-09-22 12:00:00
author:     "tientm"
header-img: "img/git.jpg"
---

# Git diff
---

`git diff` shows unstaged differences since last commit.

Use `git diff --staged` to view staged differences.

# Unstage
---

Use `git reset HEAD <file>` to unstage.

> HEAD refers to last commit on the current branch.

`git checkout -- <file>` blows away all changes since last commit.

# Skip tracking and commit
---

`git commit -a -m "Message"` adds changes from all tracked files.

# Undoing a commit
---

We forgot something on commit.

`git reset --soft HEAD^` resets all changes into staging. `^` moves all changes to the commit before HEAD.

Maybe we forgot to add a file.

`git commit --amend -m "New message"`. `--amend` adds new tracked changes to the last commit.

# Useful command
---

|Commands|Meaning|
|--|--|
|`git reset --soft HEAD^`|Undo last commit, put changes into staging|
|`git commit --amend -m "New message"`|Change the last commit|
|`git reset --hard HEAD^`|Undo last commit, blow away all changes|
|`git reset --hard HEAD^^`|Under last 2 commits and all changes|

__Dont do these after pushing__

# Adding a remote
---

> Origin refers canonical repository, our official repository that most of people use for their project.

`git remove add origin http://github.com/Gregg/git-real.git`

- `add` new remote
- `origin` our name for this remote
- `http://...` address

`git remote -v` shows all remotes.

# Pushing to remote
---

`git push -u origin master`

- `origin`: remote repository name
- `master`: local branch to push

# Pulling from remote
---

`git pull`: pull down all changes from remote repository and sync up your local repository.

# Working with remotes
---

|Commands|Meaning|
|--|--|
|`git remote add <name> <address>`|Add new remote|
|`git remote rm <name>`|Remove remote|
|`git push -u <name> <branch>`|Push to remote|

`-u` means that you don't have to specify the name and branch in the next pushing, just run `git push`.
