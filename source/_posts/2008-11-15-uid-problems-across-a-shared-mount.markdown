---
layout: post
title: UID problems across a shared mount?
tags:
- uniq
- linux
- sysadmin
- uid
- usermod
alias: [/post/59819490,/post/59819490/uid-problems-across-a-shared-mount]
---
We just moved to new Ubuntu servers.

We use file-column (with some modifications) to deal with our file
uploads.

```
deploy@jgp-web01:/var/www/oursite$ ls -l public/uploaded_file/file_name/000/000/051/585/ total 4-rw-r--r-- 1 gerhard www-data 2670 2008-11-15 05:09 MatthewJacobsCV.txtdeploy@jgp-web02:/var/www/oursite$ ls -l public/uploaded_file/file_name/000/000/051/585/ total 4-rw-r--r-- 1 deploy www-data 2670 2008-11-15 05:09 MatthewJacobsCV.txt
```

If you look carefully, you’ll see one is owned by ```deploy``` and the other
by ```gerhard```.

These are mounted by NFS, shared across the two computers.

So these are actually the same file, but with different permissions on
each.

A quick use of the ```id``` command confirmed this;

```
deploy@jgp-web01:~$ id deployuid=1004(deploy) gid=33(www-data) groups=33(www-data),1005(aspire)deploy@jgp-web02:~$ id deployuid=1002(deploy) gid=33(www-data) groups=33(www-data),1003(aspire)
```

The answer is;

```
root@jgp-web01:~# usermod -u 10000 deployroot@jgp-web02:~# usermod -u 10000 deploy
```

boom!

Now this is resolved, but you’ll have to chown all the existing files,
back to ```deploy```, else they’ll still be attached to the old uid.
