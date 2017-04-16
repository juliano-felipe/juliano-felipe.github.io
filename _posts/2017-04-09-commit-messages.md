---
layout: post
title: Commit Messages
categories: git commit
tags: git commit message
comments: true
author: nipanga
---
People often don't pay the proper attention to commit messages, but it is something so important that I feel like I need to write about it.
  
Commit messages are not just texts that you type and forget. It is used by almost everyone in the team, including yourself!  
Next month, when you need to know how/why a bug was introduced in the code, these commit messages will help to solve the problem.  

### Rules

```
First line, 50 characters maximum
[Second line blank. Always.]
Third and next lines will be a text, and can have 72 characters maximum.
You need to explain:

- Why you did it: why this change was necessary? 
    Please don't write "Because it has a task on Redmine".
    If it's a bug, explain what was the problem. If not, write
    why it was necessary for the project.
- How you've done it: how did you solve the problem?
    "With...ahn...code...I guess". No. PLEASE DON'T.
    If it's a bug, explain the approach to solve the problem. If not 
    explain the steps you took to make this functionality work.
- Useful Information: can it has some side effects?
    "No, my code ALWAYS works with no bugs". Yeah, we've all been there.
    write down some useful information, like "this will not work if the 
    User has no phone number". --poor example, I know...--

Don't be afraid to write a long text about the code inside it, but try 
to be succinct and explicit. Sometimes a commit's message is bigger 
than the code inside it, and that's ok.

You can finish your message with a sign-off.
```

### Tips

**1. Try to be as short and explicit as possible on the first line.**
> _Example: "change menu color" can be written as "Change Menu Color from White to Black".
It is very explicit about the work done in this commit, and it is the "50 chars" rule._

**2. Try not to go beyond 72 chars in the message text.**
> _Most Git servers and project management softwares follow that rule to show the Git messages, following this rule make the message reading a so less heavy job._

**3. Include a full URL to the Issue.**
> _It's easier to go to the issue that this commit is linked. Also, some bug/issue trackers systems have a particular way to link commits to issues. I, personally, like to include the full URL and this particular way together.
Example:_
>
> ---
>> Generic Commit Message Summary  
>>  
>> Generic commit text.  
>>  
>> https://redmine.org/project/issues/123456  
>> \#123456 done @4h  
>
> ---
> _This links the commit to the Issue, and you can easily "travel" from the commit's message to the Issue without having to search it.
It also makes it easier to track CI builds and deploys to the code._

**4. ++_NEVER_++ use `git commit -m "shortest message ever"**
> _It encourages to write short commit messages with almost to no meaning at all. Try to avoid that, as commit messages should be meaningful._

**5. Use imperative mood**
> _Imagine that will are continuing the phrase `This commit will...`.
"**Fix**" not "Fixing" or "Fixed". This commit will FIX a bug, it is not "fixing", nor it "fixed" the problem.
"**Add**" not "Adding" or "Added". This commit will ADD a new class to the project. It is not "Adding", nor it has "Added".
"**Change**" not "Changing" or "Changed". This commit will CHANGE something. It is not "Changing" it, not it "Changed"._
> 
> _Let's say the commit you just pushed is reverted. It is NOT doing something, nor it did. If this commit is applied, it will FIX a bug, and, if not, it will NOT fix the bug. Simple as that.
But in the message text you can not use imperative mood. This rule is just for the first line._

**6. Make small changes per commit**
> _Making commits with small changes tend to be less error prone and are easier to manage in case of a cherry-pick or rebase. Just keep in mind that every commit should not "break" the project (e.g. it has to compile, at least)._

### A Real World Example

A message like, `$ git commit -m "fix login bug"`, can be better written as this:
  
```
Fix login bug when it's not an email

This login bug happens when a User types his login number, and not an 
email, at any login input. Some older Users - from the legacy system, 
has a login number, instead of an email.

Refactored the LoginController and LoginService to accept not only 
e-mails, but also numbers, and  tweaked the LoginValidator to throw an 
exception when a number with less than 6 chars is passed to it.

https://redmine.org/project/issues/123456
#123456 resolved @4h

Signed-off-by: A Good Developer <best.dev@host.com>
```

Commit messages are a very wide topic, it this post is a little off my "time to read limit", but I think this is the minimum rules to write good commit messages.

Next post will be about merges (and maybe conflicts).


Bye ::]