Quick tools for generating polynomial approximations to arbitrary functions
==============================

So, frequently, on graphics twitter, a discussion will come up about finding a "good" approximation
to some function like 

$$cos(acos(t)/3)$$

or

$$f(x) = \over{x}{x+1}$$

on some range, usually $[0,1]$.

What does "good" mean?
---------------------------------------

Well, there are entire families of methods to cook up polynomial approximations to functions.

In this notebook, we focus on a technique that minimizes mean squared error (MSE).

It's not the only thing we can minimize.

But it's one of the easiest things to minimize.

And we can do it in almost closed form for surprisingly arbitrary choices of functions to approximate.

So, how do we do it?
--------------------------------

Imagine you have a function $f(x)$ and you want to cook up a $g(x) = \sum_{i=0}^n \alpha_i x^i$ that minimizes
$ \int_a^b (f(x) - g(x))^2 dx$ over some interval $(a,b)$.

Now, if you write that whole thing out, you get

$$\sum_{i=0}^n \sum_{j=0}^n \int_a^b \alpha_i \alpha_j x^{j+i}dx -
\sum_{i=0}^n 2 \int_a^b \alpha_i x^i f(x) dx +
\int_a^b f(x)^2 dx
$$

That looks messy, but it turns out the whole thing can be written as a matrix expression that expresses the MSE
of our approximation function in terms of the sequence of $\alpha_i, i \in 0..n$

It kind of looks like

$$ MSE(\alpha) = \alpha^T A \alpha - 2 B \alpha + C$$

where $\alpha$ is the vector of $\alpha_i$, 
$A_{i,j} = \int_a^b x^{j+i}dx = {{(b^{j+i+1} - a^{j+1+1})}\over{j+i+1}}$,
$B_i = \int_a^b f(x) x^i dx$ (often has to be computed numerically)
and $C = \int_a^b f(x)^2 dx$

We can minimize it by using the standard least-squares trick of setting the gradient to zero, and solving

$A \alpha - B = 0$ or $A \alpha = B$ 

Where do I learn more?
------------------------------------

I've been told that this is a standard technique, but, having stumbled upon it by re-inventing the wheel,
I don't know what the standard name for it is.

It's closely related to least-squares regression.  Maybe it's just called "least squares regression".  Or maybe
it's called something like "least squares regression with (word for one of the tricks being used here)"
