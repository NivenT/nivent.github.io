---
layout: post
title: "Euler's Formula"
modified: 
categories: blog
excerpt: The above equation is known as [Euler's identity](https://www.wikiwand.com/en/Euler%27s_identity). It's often described as one of the most [beautiful equations](http://www.bbc.com/earth/story/20160120-the-most-beautiful-equation-is-eulers-identity) in all of mathematics, since it makes use of 5 important constants.
tags: [calculus, math]
date: 2016-12-24 20:18:00
---

>$$e^{i\pi}+1=0$$
{: style="font-size: 200%;"}

The above equation is known as [Euler's identity](https://www.wikiwand.com/en/Euler%27s_identity). It's often described as one of the most [beautiful equations](http://www.bbc.com/earth/story/20160120-the-most-beautiful-equation-is-eulers-identity) in all of mathematics, since it makes use of 5 important constants. The identity is a direct consequence from this post's [titular](https://www.wikiwand.com/en/Euler's_formula) formula, which is arguably more beautiful for its increased generality and the surprising connection it reveals.

>$$e^{ix}=\cos(x)+i\sin(x)$$

This formula ties exponentiation to trigonmetric functions, and can be used to show that complex multiplication corresponds to rotations in the plane. It also shows that exponentiation is periodic, with period $$2\pi i$$. It can be used to proof [De Moivre's formula](https://www.wikiwand.com/en/De_Moivre's_formula), and can be used to derive many trigonometric identites. It's quite a formula. However, while it is generally well-received, its usual derivation is often seen as unenlightening and/or unmotivated.

# Standard Approach
The standard approach for deriving Euler's formula is to look at the Taylor series for $$\sin$$, $$\cos$$, and $$e^x$$. You then observe that by placing $$i$$'s in the right places, things start to match up, leading you to Euler's famed equation. If I am not mistaken [^1], this is the method Euler himself used to derive the formula. I won't go into the details [^2], but just mention that it is the usual approach.

Luckily, this is not the only way to arrive at this formula. There are more geometric ways of thinking that give good intuition for why this formula is true, and that can be turned into rigorous arguments. My favorite such method, is to consider a particle moving along the path $$f(t)=e^{it}$$. Then, note that this particle's instantaneous velocity at any point along the path is $$f'(t)=ie^{it}=if(t)$$. Complex numbers have nice geometric correspondences. Even without knowing Euler's formula, it can be shown that multiplication by $$i$$ corresponds to rotating a complex number $$90^\circ$$. In fact, if you are willing to accept that $$(a,b)$$ rotated $$90^\circ$$ (counter-clockwise) is $$(-b,a)$$, then all we have to do to show this is realize that $$i(a,b)=i(a+bi)=-b+ai=(-b,a)$$ where we identify the complex number $$a+bi$$ with the point $$(a,b)$$ in the plane! So we have a particle moving along a path $$f(t)$$ with velocity $$if(t)$$ perpendicular to its position. Anyone familar with multivariable calculus can tell you that any path with velocity always perpendicular to position must be a circle!

> Quick Proof<br>
Consider any path $$p:\mathbb R\rightarrow\mathbb R^n$$ such that $$p(t)$$ is perpendicular to $$p'(t)$$ (i.e. $$p(t)\cdot p'(t)=0$$) for all $$t$$. Then,
$$\begin{align*}
\frac d{dt}\|p(t)\|^2=\frac d{dt} p(t)\cdot p(t)=p(t)\cdot p'(t)+p'(t)\cdot p(t)=0+0=0
\end{align*}$$
and so $$\|p(t)\|^2$$ is a constant. Since the path is always a constant distance from the origin, it must be a circle (or part of a circle)

This means that the path described by $$e^{it}$$ must be a circle. What's its radius? Well, plug in $$t=0$$ to get $$e^{i0}=e^0=1$$, so the circle has radius $$1$$. From trigonometry, we know that the unit circle can be parameterized by $$(\cos(t), \sin(t))$$, so we have that $$e^{it}=\cos(t)+i\sin(t)$$ and we have recovered Euler's formula[^3].

# A different approach
The method I just described is good for geometric intuition, but I would argue that it has one flaw: it still feels unmotivated. Sure, if you know Euler's formula already, then the approach makes sense, but if you do not, investigating the derivative of $$e^{it}$$ does not seem like an obvious thing to do in order to gain some insight into something. Because of this, I want to suggest a final method of arriving at Euler's formula that I believe is fairly motivated [^4].

It starts with the observation that $$f(x)=e^x$$ is the unique solution (upto constant factor) of the differential equation $$\frac d{dx}f(x)=f(x)$$. This means that if we find another solution to this equation (and it agrees with $$e^x$$ at some point), then they must be equal! To this end, we remark that $$\frac d{dx}\cos(x)=-\sin(x)$$ and $$\frac d{dx}\sin(x)=\cos(x)$$. Taken together, this seems to suggest that there might be a way to combine these two and get a function that is invariant under differentiation. Let's try and find such a combination. Let $$g(x)=a\cos(bx)+c\sin(dx)$$. We want to find choices of $$a,b,c,d$$ such that $$\frac d{dx}g(x)=g(x)$$. We also need this equation to agree with $$f(x)$$ at some point, so let's consider $$x=0$$ since $$0$$ is nice and simple. $$g(0)=a=1=f(0)$$, so we already have a value of $$a$$ and we can write $$g(x)=\cos(bx)+c\sin(dx)$$.

To figure out the rest of the constants, we differentiate to get $$g'(x)=-b\sin(bx)+cd\cos(dx)$$. To make this equal to $$g(x)$$, we are going to take a leap of faith at stipulate that $$g(x)=g'(x)$$ iff their corresponding parts (coefficients) all equal to each other [^5]. This gives the following three equations.

$$\begin{align*}
-b=c & & b=d & & cd=1
\end{align*}$$

These equations are fairly simple at very little algebra shows that their unique solution is $$(b,c,d)=(i,-i,i)$$ and so $$g(x)=\cos(ix)-i\sin(ix)$$. Plugging in $$x=0$$ and differentiating verify that in fact $$g(0)=f(0)$$ and $$g'(x)=g(x)$$ as desired, and so it must be that $$f(x)=g(x)$$. We have just shown that $$e^x=\cos(ix)-i\sin(ix)$$! This is not in exactly the same form as Euler's formula, and if you are unfamiliar with complex analysis, this formula likely seems sketchy since you are taking $$\sin/\cos$$ of imaginary numbers. Despite this, we're going to trust that things make sense, and try to alleviate our worries by getting rid of those pesky imaginaries in our trig functions. To do this, we blug $$ix$$ into $$g$$ in order to get $$g(ix)=\cos(-x)-i\sin(-x)=\cos(x)+i\sin(x)$$. Since $$g$$ and $$f$$ are supposed to be the same function, we use this as justification to say that $$e^{ix}=\cos(x)+i\sin(x)$$.

This approach to deriving Euler's formula is one that I believe a curious student could find by just experimenting with ways of finding functions that equal their derivatives.

[^1]: and I could be. Math history is not one of my stronger suits
[^2]: partially because I don't like this method. Partially because carrying it out is simple enough that I don't really need to say more.
[^3]: to make this more rigorous, we should make sure that we are moving around the circle at the correct rate. I do not think that we haven't ruled out the case that e^{it}=cos(3t)+isin(3t) for example, but this argument still provides good intuition
[^4]: I will admit that it is not as intuitive as the last one, but still less magic than the first
[^5]: This part may seem not completely justified, but I think it makes intuitive sense that this would be the case. At the very list, if this is the case, then g and g' are equal, so let's hope that this can be the case.