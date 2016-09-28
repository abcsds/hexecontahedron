---
layout: post
title: "Fresnel Integrals"
date: "2016-03-25 00:47:00 -0600"
comments: true
tags: physics , visualization
image: "{{ site.static_folder }}/img/notebooks/fresnel-integral.png"
---
Named after [Augustin-Jean Fresnel](https://en.wikipedia.org/wiki/Augustin-Jean_Fresnel) Fresnel integrals are:

$$ x(t) = C(t) = \int_{0}^{t} cos(\dfrac{\pi}{2}s^2) ds $$

$$ y(t) = S(t) = \int_{0}^{t} sin(\dfrac{\pi}{2}s^2) ds $$

You can read more about them [here](https://en.wikipedia.org/wiki/Fresnel_integral).


```python
%matplotlib inline
from scipy.special import fresnel
from scipy import linspace
import matplotlib.pyplot as plt
```


```python
t = linspace(0, 5, 1000)
y, x = fresnel(t)
plt.figure(figsize=(10,10))
plt.plot(t, x, t, y)
plt.show()
```

![Fresnel Integral]({{ site.static_folder }}/img/notebooks/fresnel-integral.png)


## Euler spiral
The parametric plot of these functions is called the Euler spiral.


```python
t = linspace(0, 10, 1000)
y, x = fresnel(t)
plt.figure(figsize=(10,10))
plt.plot(x, y)
plt.show()
```


![Half Euler Spiral]({{ site.static_folder }}/img/notebooks/half-eulers-spiral.png)


```python
t = linspace(-10, 10, 1000)
y, x = fresnel(t)
plt.figure(figsize=(10,10))
plt.plot(x, y)
plt.show()
```


![Euler Spiral]({{ site.static_folder }}/img/notebooks/eulers-spiral.png)
