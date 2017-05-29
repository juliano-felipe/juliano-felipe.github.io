---
layout: post
visible: true
title: Creating Branches
categories: git branch
tags: git branch
comments: true
author: nipanga
---
Many developers tend to think that branches are cumbersome. Plot twist; they're not!

## Create a branch: easy-peasy

```bash
$ git branch feature-something
```

It creates a new branch named `feature-something`, and that's pretty much it.
But there are some times that you don't want to just create a branch, you want to work on it, 
and you need to do a `git checkout feature-something`. What about just type one simple command that
does it all? Here's that command:

```bash
$ git checkout -b feature-something
```

Just as simple as the first one. But this one does a little more.
The parameter `-b` on the `git checkout` command creates
a new branch and changes the `HEAD` to this new branch.
Let's say that it 'copies' the current branch you're on to a new one.
It is the same as

```bash
$ git branch feature-something
$ git checkout feature-something
```

Now, what about creating a new branch from the `origin` or `upstream` current state?
Or, in other words, create a new branch with the updated code from the project main repos?

`git checkout -b` can accept two parameters. The first one is the name of the new branch you want to create.
The second one is the starting point for that new branch. This starting point is any git pointer: it can be another branch,
a commit (hash), or another pointer like `HEAD`(default), `FETCH_HEAD` and so on.  

So, to create a new branch with the `master` branch new updates, you just need to fetch the `master` branch,
and pass it as the starting point to `git checkout -b`, like this:

```bash
$ git fetch <origin|upstream> master:master
$ git checkout -b feature-something master
```

_**Important Note: Keep in mind that `git fetch <remote> any-branch:any-branch` throws an error if you're on `any-branch`.
So, you need to run that command from another branch that's not the branch you want to fetch.**_

The trick here is better to create a branch from `master` and not from its remote tracking counter-part `origin/master`,
because your new branch will be 'attached' to `origin/master`, and if you do a `git push` without any parameters, 
you can screw up your `master` branch pretty nice.  
And, in many projects out there, you (barely) won't push code directly into `master`, so it's better to not 'touch' it in
any way, it is just there to help you create new branches.

With that trick you won't need to fetch all project's branches and won't see a thousand lines when typing `git branch -a`,
and a hundred branches on your `git log`.
This will keep you local repos clean and neat. Just like your code, right?... RIGHT? (I hope so...)


Next post will be about the `git cherry-pick` command, and how to not explode your git repos.

Bye ::]
