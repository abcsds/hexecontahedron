---
layout: post
title: "Octave Serial Connection"
date: "2015-07-17"
tags: octave matlab snippet
---
# How to open a serial connection from Octave
Small snippet to open a serial connection from [Octave][Octave] on Unix.

```MATLAB
fid = fopen("/dev/ttyUSB0", "r+")
fwrite(fid, your_data)
out = fread(fid)
```
[Octave]: http://www.gnu.org/software/octave/
