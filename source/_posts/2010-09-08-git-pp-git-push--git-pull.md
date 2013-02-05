---
layout: post
title: git pp (git pull && git push)
tags:
- git
- alias
- config
---
I am addicted to committing (not commitment).

I make small, distinct commits all the time.

But the consequence of this is

``` bash
$ git push origin master

To git@myServer:myRepo.git
  ! [rejected]        master -> master (non-fast-forward)
  error: failed to push some refs to ‘git@myServer:myRepo.git’

To prevent you from losing history, non-fast-forward updates were rejected

Merge the remote changes (e.g. ‘git pull’) before pushing again.  See the
‘Note about fast-forwards’ section of ‘git push —help’ for details.
```

I hate getting push failures.

But I don’t trust myself to do a pull beforehand.

Enter a git alias!

``` bash
$ cat ~/.gitconfig
[alias]
    pp = !sh -c ‘git pull $0 $1 && git push $0 $1’
```

Now I am free to “git pp origin master” as much as I want.

``` bash
$ git pp origin master

From myServer:myRepo
 * branch            master     -> FETCH_HEAD
Already up-to-date.
Everything up-to-date
```

SAFE!