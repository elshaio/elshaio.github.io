---
layout: post
title: "Setting up multiple SSH github accounts"
date: 2025-12-24 20:00:28 -0600
categories: []
tags: []
---

First post, setting up this blog using my own account instead of one that I was using for a side project make me realize it is a little headache to push to multiple github accounts with different ssh keys, so basically my fix was to setup something like this:

Imagine you have two cows, one is called personal-cow and the second one is project-cow.
Each of them are setting up two different ssh keys on each github account, so at the end you will have a configuration like this on your `~/.ssh/config` file.

```sshconfig
Host github.com-personal-cow
  HostName github.com
  User git
  IdentitiesOnly yes
  IdentityFile ~/.ssh/github-personal-cow

Host github.com-project-cow
  HostName github.com
  User git
  IdentitiesOnly yes
  IdentityFile ~/.ssh/github-personal-cow
```

each of them should work when you call any of them like:
```bash
ssh -T github.com-personal-cow
ssh -T github.com-project-cow
```

Anyways, the trick for it is to setup the origin url per project with a little trick, like me setting up this new blog, the url was something like `git@github.com:<username>/<username>.github.io.git`

so the trick is to change the text in between @ and :  for the `Host` entry of the ssh key you want to use per push, so:
```bash
# personal cow
git@github.com-personal-cow:<username>/<username>.github.io.git
# project cow
git@github.com-project-cow:<username>/<username>.github.io.git
```
If by any chance you already setup that, you could change it with:
```bash
git remote set-url origin <your-changed-url>
```

