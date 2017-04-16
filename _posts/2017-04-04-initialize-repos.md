---
layout: post
title: Initialize a Repos
categories: git initialize
tags: git init initialize remote fetch
comments: true
author: nipanga
---
### Bare Repos (server)

To start using Git you need to set your Server. I can be a github, gitlab or whatever you want. If you want to set a Git Server on your machine, the simplest way to do that is creating a folder in you computer, and run the following commands:

_For example purposes, let's say we have a /git-server in our computer_

```` bash
$ cd /git-server
$ git init --bare project.git
````

This will create a `project.git` directory inside the `/git-server` folder.
If you don't specify the project name, Git will initialize the bare repos where you are.

Bare repositories don't have a working tree, so you can't work from there. You need to `git push` to that repos.
I won't get too deep on this command, because this should be a quick tip, and most of the time initialing a Git repos like this is sufficient. You can read the git oficial documentation (below) if you want to do something more.

A good practice when creating a bare Git repos is putting the suffix ".git" in the directory, it explicits it is a Git repos.


### Local Repos (development)

Now you need to create a local repos before start coding you project (or after, doesn't really matter).

Create a folder that will have your project, let's call it `project` (so creative, right?!). You need to `git init` in this repository, and "link" it to the Git server repos, so you can upload your code:

``` bash
$ cd /project
$ git init
```

"Hey, Git, I have a project I need to work on, and this the the folder I'll be using." - That's what `git init` means.
This will do nothing more than creating a `.git` directory inside `/project`.

### Setting up your Local Repos

Now that you have a Git Server repos, let's download it. It is called "clone". It's trivial:

``` bash
$ git clone -url-
```

This will create a folder with the same name as the project, download it inside the directory you're on.
You'll have all data inside the project: files (and folders), branches, tags, and so on.

I personally don't like this approach, because you will not work with all those branches at once.
So, you'll want to wipe all the branches that are not in use at the moment, which is annoying.

One thing I always do is configure the remote alias/url and fetch the specific branches I want. Like this:

``` bash
$ git remote add origin -url-
$ git fetch origin -branch-
```

This will create a remote called `-origin-`, and then fetch only the `-branch-`, and not all branches that everyone in the team pushed.
Another thing I like in this approach is that you can or cannot download all the branches, depending on your decision (just don't pass the branch when fetching); everytime you need to download the same, or another, branch, you'll do the same way; and you have some branches that you won't need in the working directory, so you can keep it in the remote tracking area (like origin/master).

To finish, a real world example:

``` bash
$ cd /project
$ git init
$ git remote add origin git@github.com:nipanga/nipanga.github.io.git
$ git fetch origin master
$ git checkout master
```

It's done, now you can start working!

Next post will be about git status, add and commit.

Bye :]