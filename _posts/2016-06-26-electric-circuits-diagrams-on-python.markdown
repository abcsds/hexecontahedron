---
layout: post
title: "Electric Circuits Diagrams on Python"
date: "2016-06-26 08:05:50 -0500"
comments: true
tags: python , electric circuits
image: "{{ site.static_folder }}/img/circuits/example.png"
---


Recently I found the need to draw electrical circuits to show the relation of neural models to them. For this I found a tool within python that lets you draw most common circuits by defining them line by line. It's called SchemDraw, and you can find it [here](http://cdelker.bitbucket.org/SchemDraw.html).


```python
%matplotlib inline
import SchemDraw as schem
import SchemDraw.elements as e
d = schem.Drawing()
V1 = d.add( e.SOURCE_V, label='10V' )
d.add( e.RES, d='right', label='100K$\Omega$' )
d.add( e.CAP, d='down', botlabel='0.1$\mu$F' )
d.add( e.LINE, to=V1.start )
d.add( e.GND )
d.draw()

```


![circuit]({{ site.static_folder }}/img/circuits/example.png)


As you can see, you add elements to the circuit one by one. The standard elements are contained in the module SchemDraw.elements, and the position of every element is given by a start and end point:


```python
print(V1.start,V1.end)
```

    [ 0.  0.] [  1.83697020e-16   3.00000000e+00]
