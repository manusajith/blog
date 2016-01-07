---
layout: post
title: "Git fatal: remote origin already exists"
date: 2016-01-08 00:48:17 +0530
comments: true
categories: Git
---

One of my colleagues was facing an issue with git, trying to add a remote to the git repo.

```
➜  repo_name git:(master) git remote add origin git@github.com:username/repo_name.git

fatal: remote origin already exists.
```

As the error message indicates, there is already a remote configured with the name `origin`. So you can either add the new remote with a different name say `github` or update the existing one if you don't need it:

To add a new remote with an alternate name, called for example github instead of origin (which obviously already exists in your system), do the following:

```
$ git remote add github git@github.com:username/repo_name.git
```

Alternatively, you can update the existing remote `origin` using the following command:

```
$ git remote set-url origin git@github.com:username/repo_name.git
```

If you want to list the current remotes, you can check the same  using

```
git remote -v
```
