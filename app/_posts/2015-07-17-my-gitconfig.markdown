---
layout: post
title: "My gitconfig"
date: "2015-07-17"
tags: git config linux mac
---
# My .gitconfig
This file belongs to the user home folder, adds a password cache, and a small alias for pretty log print.

```
[user]
	name = Alberto Barradas
	email = myEmail@gmail.com
[push]
	default = simple
[alias]
	lg = log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit
[credential]
	helper = cache --timeout 2678400
# LINUX
#	helper = /usr/share/doc/git/contrib/credential/gnome-keyring/git-credential-gnome-keyring
# MAC
#	helper = osxkeychain
```
