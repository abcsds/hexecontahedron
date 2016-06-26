---
layout: post
title: "Model of RC circuit"
date: "2016-06-26 09:05:54 -0500"
comments: true
tags: python, electric circuits, capacitor, rc
image: "{{ site.static_folder }}/img/circuits/rc.png"
---

The RC circuit will be important for later posts so I have decided to create a small one about it. It is also a good chance to try out [SchemDraw](/2016/06/26/electric-circuits-diagrams-on-python.html), a circuit diagram drawer for python.

The voltage of an RC circuit is described with the next equation:

$$ V(t) = V_0  (1-e^{-\frac{t}{\tau_0}}) $$

Where $\tau$ is the capacitance constant of the capacitor, given by RC.


```python
# Importing necesary libraries
%matplotlib inline
import numpy as np
import matplotlib.pyplot as plt
```

For this simulation we will use a 10K resistance, a 10mF capacitor, and a 10V source. The curcuit will then look like this:


```python
import SchemDraw as schem
import SchemDraw.elements as e
d = schem.Drawing()
V1 = d.add( e.SOURCE_V, label='10V' )
d.add( e.RES, d='right', label='10K$\Omega$' )
d.add( e.CAP, d='down', botlabel='10mF' )
d.add( e.LINE, to=V1.start )
d.add( e.GND )
d.draw()
```


![RC Circuit]({{ site.static_folder }}/img/circuits/rc.png)


We input the constants for our model:


```python
R = 10e3
C = 10e-3
tau = R*C
maxTime = 500
v0 = 10
```

And finally run our model through time to plot it's voltage over time.


```python
t = np.arange(0,maxTime,0.01)
V = v0*(1-np.e**(-t/tau))
plt.figure(figsize=(16,5))
plt.title('Voltage of an RC Circuit')
plt.ylabel('Voltage')
plt.xlabel('Time')
plt.plot(t,V)
plt.show()
```


![Voltage of RC circuit]({{ site.static_folder }}/img/circuits/rc_plot.png)
