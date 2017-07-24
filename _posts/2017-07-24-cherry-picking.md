---
layout: post
visible: true
title: Cherry-Picking
categories: git cherry-pick
tags: git cherry-pick cherry-picking cherry pick picking
comments: true
author: nipanga
---
So, you want to cherry-pick, but don't know how things work? Don't be sad, nobody knows...
  
## Things to know BEFORE doing a cherry-pick
  
You Googled "git cherry pick" and thought, "It's so easy. Nice!". So you did it, and then after a couple of merges, your 
code base is screwed. "Wwwhhhyyyy?" you think. Maybe because you didn't know these things before cherry-picking:

#### Remember the Commit basics
  
The most basic knowledge about commits is: **A Commit is not editable**, and, **You always commit into the project tree, 
_not inside a branch_**.  
Many people tend to forget these two basic rules before cherry-picking.  
  
Why is this so important? Well, when you cherry-pick, basically, you're "using" these two rules, and, if you're not 
paying attention to that, you can screw up your code base after a cherry-pick and a few merges.  

#### What happens when I cherry-pick
  
Cherry-pick applies the changes from one commit to "_here_".
"here" means whatever pointer you're pointing, i.e. the HEAD pointer, a branch, etc, etc, etc.
  
`cherry-pick` creates a new commit with the same code changes as the source commit, and applies this new commit into
the branch you're on. Some people think that it is the same commit, **but it's not**.
It's a **new** commit, applied into the destination branch. This misconception can lead to lots of errors after a 
couple of merges.

## Cherry-Picking

#### Situations which you'll probably need a cherry-pick
  
First of all, don't use `cherry-pick` deliberatedly. 
Many times you think you want a `cherry-pick` it's better to solve it with a simple `merge`.
  
You'll want a cherry-pick when you just want a particular change in the project into another branch - for example, 
fixing a particular bug into a release branch.  

Don't `cherry-pick` when you want a change from another developer into your branch. Later you both may merge the same 
changes into a master branch, and you can screw up your code. In these cases consider using a simple `merge`, most of 
the time it'll be sufficient.

#### How to `cherry-pick`
  
First, find the commit you want to `cherry-pick` from another branch. 
You can do this using the `git lg` command we configured in the [First Step - Configure your Git](https://nipanga.github.io/git/configuration/2017/04/03/config.html)
post.  
Take the commit hash and store it in your clipboard (i.e. ctrl+C) or a temporary text file.
  
Then, make sure your working directory is clean - i.e. type `git status` and it should be empty, and you are in the
branch you want to apply the `cherry-picked` commit.  

Now, the easy part. Type `git cherry-pick` followed by the commit hash, and it's done:

``` bash
$ git cherry-pick <hash>
```

A real world example, with the Git response:
  
``` bash
$ git cherry-pick c9e4764d4
[branch-cherry-pick-example 9a921d7fb] Fix some bug with a Service class
 Date: Mon Jul 24 04:36:39 2017 -0300
 3 files changed, 39 insertions(+), 9 deletions(-)
```

Pay attention to what we discussed in the first section of this post: `cherry-pick` creates a new commit with the same 
changes from the source commit.  
See that the `c9e4764d4` commit hash changed to `9a921d7fb`. It a new commit, but with the same code changes, in another 
branch.  
If, in the future, these two branches - the one that has the `c9e4764d4` and the `branch-cherry-pick` are merged into a 
master branch, you may undo some changes applied after the `c9e4764d4`, depending on how these branches were merged.
  
The best way to avoid that is not merging one of these two branches. Most of the time, it will be the "source" branch - 
because, if you cherry-picked a commit to a new branch, looks like it's the one you want to keep.  
  
If you really need to merge this two branches, pay attention to the code changes to the files inside the `c9e4764d4` commit.
There is no "rule of thumb" to do this. Every case is a different case, and you should study multiple approaches to solve
the problem before merging the branches.

That's pretty much it. If you have any doubts or suggestions, please comment below.

Bye ::]
