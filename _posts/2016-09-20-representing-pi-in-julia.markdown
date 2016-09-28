---
layout: post
title: "Representing pi in Julia"
date: "2016-09-20 12:37:52 -0500"
comments: true
tags: julia , pi
image: "{{ site.static_folder }}/img/julia/logo.png"
---

Julia excels as a numeric computation language. It is even [faster than C](https://www.ibm.com/developerworks/community/blogs/jfp/entry/A_Comparison_Of_C_Julia_Python_Numba_Cython_Scipy_and_BLAS_on_LU_Factorization?lang=en) for certain tasks, but has a syntax almost as simple as that of python.
Although, at the beginning, Julia syntax might seem similar to python, things start to change when you want the best performance, or specific numerical functionalities.
This is the case of precision specification. When it comes to numerical computing you must be able to have as much precession as you want. Let's say you have the geeky goal of memorizing the first hundred digits of pi. Just printing it to the console won't cut it, since pi is an irrational number (represented in julia by the type `::Irrational{:π}`):

```julia
π
```

    π = 3.1415926535897...

If you want to print pi with more precession you have to unse it's BigFloat representation:


```julia
BigFloat(π)
```

    3.141592653589793238462643383279502884197169399375105820974944592307816406286198

Notice that it's no longer an irrational representation (no dots at the end). This new representation of pi has a specific precession. Default precision is 256 bits:

```julia
precision(BigFloat)
```

    256

This is the equivalent of four double values. Let's try printing pi as represented by 1024 bits. This is done with the `setprecision()` function within a do block.

```julia
setprecision(2^10) do
    println(precision(BigFloat))
    println(BigFloat(π))
end
```

    1024
    3.141592653589793238462643383279502884197169399375105820974944592307816406286208998628034825342117067982148086513282306647093844609550582231725359408128481117450284102701938521105559644622948954930381964428810975665933446128475648233786783165271201909145648566923460348610454326648213393607260249141273724586997

As you can see, high precision floating numbers are a powerful tool in Julia. I suggest you try playing around with φ, the golden ratio.
