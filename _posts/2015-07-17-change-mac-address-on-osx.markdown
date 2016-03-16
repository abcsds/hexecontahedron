---
layout: post
title: "Change MAC address on OSx"
date: "2015-07-17"
tags: mac osx networks english
---
Changeing your MAC address is important before doing any pentesting work. MacOSX offers a way of doing it with the default networking tool `ifconfig`. We will need super user access, though:

```
sudo ifconfig en1 ether 00:11:22:33:44:55
```

Here the new MAC `00:11:22:33:44:55` could be any valid MAC address you want, and the interface can be either `en1` for the wireless adapter, or `en0` for the ethernet adapter.
