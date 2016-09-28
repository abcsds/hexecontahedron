---
layout: post
title: "Estimate Pi in one line with Julia"
date: "2016-08-20 14:45:49 -0500"
comments: true
tags: julia , montecarlo , pi
image: "{{ site.static_folder }}/img/favicon.png"
---

A montecarlo aproximation relies on large random sampling to obtain numeric results. This is, guiven a known distribution of data, can you aproximate a numeric value? You can read more about it [here](https://en.wikipedia.org/wiki/Monte_Carlo_method).

A simple demonstration of this is finding pi: Guiven a circle of radius \(r\) inside a square of sides length \(2r\), if you throw a large number of random points inside the square, and knowing the equations for the area of both the circle and the square you can find pi with the following equation:

$$ \pi = 4 * \frac{\text{(Number of Darts in Circle)}}{\text{(Number of Darts in Square)}} $$

I acctually learned it from [this source](http://polymer.bu.edu/java/java/montepi/MontePi.html), if you are interested in learning to deduce it by yourself. For some years now I have learned by coding. It is easier to grasp a complex process if you can instruct a computer to do it. Programming is an organized language thinking tool. So, to understand how the Montecarlo aproximation of pi works, I made this oneliner in julia:


```julia
function compute_pi(x) return 4 * sum([1 for _ in filter(_ -> rand()^2 + rand()^2 < 1, 1:x)]) / x end
```




    compute_pi (generic function with 1 method)



Lets decompose this function:

The innermost function is a filter function: `filter(_ -> rand()^2 + rand()^2 < 1, 1:x)` this is the way of doing conditional comprehention lists in julia, since, up to version 0.4 it does not accept the `[for in if]` syntax, so a list must be created using the filter function. This receives a finction and an iterable as arguments. The function we are sending in this case is an annonymus function, created by mapping a value `_` (a trow away value in this case) into a function: `rand()^2 + rand()^2 < 1`. We do the same for all values between 1 and x (the number of trials in the simulation). The filter function will only return a value for those items between 1 and x where the annonymus function return a true value.
The second part of our function is adding a one for every true value in our filtered list, multiply it by four and divide it by the number of trials in our simulation (x).
As you can see, this is quite a fast way to find an aproximate pi:


```julia
@time print(compute_pi(10^3))
```

    3.168  0.159191 seconds (56.82 k allocations: 2.614 MB)


And with increasing trials we should get a better aproximation:


```julia
S = map(x -> 10^x, 1:6)
@time map(x -> 4 * sum([1 for _ in filter(w -> rand()^2 + rand()^2 < 1, 1:x)]) / x, S)
```

      1.664543 seconds (12.93 M allocations: 258.194 MB, 4.84% gc time)





    6-element Array{Float64,1}:
     4.0    
     3.26   
     3.212  
     3.1604
     3.13612
     3.13942
