---
layout: post
title: "Change MAC address on OSx"
date: "2015-07-17"
categories: mac osx networks
---
# How to change your MAC address on MacOSx
Changeing your MAC address is important before doing any pentesting work. Mac offers a way of doing it with the default tool `ifconfig`. We will need super user access, though:

```
sudo ifconfig en1 ether 00:11:22:33:44:55
```

Here the new MAC `00:11:22:33:44:55` could be any valid MAC address you want, and the interface can be either `en1` for the wireless adapter, or `en0` for the ethernet adapter.
