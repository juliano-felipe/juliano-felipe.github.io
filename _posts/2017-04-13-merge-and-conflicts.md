---
layout: post
title: Merge, and Conflicts
categories: git merge conflict
tags: git merge merging conflict conflicts
comments: true
author: nipanga
---
Merge... A 7 headed monster that no one wants to deal with...
Actually, it's not that bad. It just has two heads. And I'll explain how to beat each one.

## First Head: A Simple Merge

```bash
$ git merge another-branch
```

That's it. Simple, isn't it? No? Ok, I'll elaborate:

This will merge `another-branch` "inside"  the branch you're on.
Let's say you're already on `branch-1`, and want to merge `branch-2`, just type `git merge branch-2` and that's it.

Lots of new Git users ~~, especially the ones that came from SVN,~~ tend to get confused about that. But it is just that simple. It can't get more simple than that.

## Second Head: A Conflicted Merge

So... you tried to merge two branches and Git told you "Ahn... pal... I'm afraid I can't do that... You need to solve this conflict here". Before you start to cry, let me help you.

The "thing" that confuses many people here is that Git pauses the merge, and you need to solve it. So, keep in mind that you need to "deal with Git" a little bit different.

There is, basically, two methods to solve a conflict:

## 1. Choosing a Strategy: our side or their side

Taking our side of the conflict is easy. The caveat here is that you need to see for yourself, checking ALL the files, if our side of the conflict is the correct one to use. 
After you checked, I repeat, ALL conflicted files and you're sure that our side of the conflict is the correct one, you need to abort the current merge, then merge 
again with the parameter `-X ours` and it's done. Like this:

```bash
$ git merge --abort
$ git merge -X ours another-branch
```

Here you're telling Git: "Dude, thanks for your concerns. I already checked all the files and if you take MY side of the code we're good."

Another thing to keep in mind that, if you use this approach before trying to merge, and before checking the files, Git will merge your side of the CONFLICTED code. If it's not the correct one, it's your fault.

To take their side of the conflict you need to use `-X theirs`. This will take their side of the conflict for all the conflicted files:

```bash
$ git merge --abort
$ git merge -X theirs another-branch
```

_**Important Note: In case there is no conflict, Git will not just take your side of the code. The command is different, and we'll cover this in another post.**_

## 2. Solving it yourself.

Solving it yourself needs a little more work, but there's is some cases that you need to take our side of the conflict, and another file their side of the conflict, and sometimes you need both sides of the conflict.
There's is no built-in strategy to take both sides of the conflict.

_Keep in mind that, in case you want to solve the conflict yourself, you don't need to abort the current merge._

When you run the command `git merge another-branch` Git will tell you what file are conflicted. You also can `git status` - or our alias `git st` to show you what files are conflicted.

When you open a conflicted file, you'll see something like this:

```bash
++ File.code ++

/* some code */
/* another line of code */
/* more code */

<<<<<<< HEAD
/* ahn.. I guess MY code is the correct one */
=======
/* no, MY code is right, not yours */
>>>>>>> another-branch
```

All you need to to is identify the code you want to stay in the file, and delete the lines you do not want, including the `<<<<<<< HEAD`, `=======`, and `>>>>>>> another-branch`.

The tricky part here is identifying which one is the correct one to stay in the code. Sometimes it's your side, something is their side, and sometimes it's both sides.

AFTER you decided what code is right, and deleted the lines Git created to show you the conflict, for ALL the files, you just need to add these files to the stage and commit. 
Like this (in this example, both sides should stay in the file):

```bash
++ File.code ++

/* some code */
/* another line of code */
/* more code */


/* ahn.. I guess MY code is the correct one */
/* no, MY code is right, not yours */
```

And then:

```bash
$ git add File.code
$ git add AnotherFileWithConflict.code
$ git add OneMoreFiileWithConflict.code
$ git commit
```

Git will fill the commit message automatically, you don't need to change that. (Actually, it is a good practice not to change that message, unless there's is some rules about that in your project).

You only finish the merge when you `git commit`. Lots of new Git users get this wrong and think that after you edited the file the merge is done.
**DO NOT FORGET TO `git commit`.**
  
  
  
And that's pretty much it. I told you that it's not that bad. Although it's pretty basic this should cover 98% of your merging needs.

Next post we'll talk about branches and tips about creating new ones.

Bye ::]