---
layout: post
title: "An Interesting Equation II"
modified:
categories: blog
excerpt:
tags: [math, number theory, dedekind domain]
date: 2019-01-01
---

This will be another post analyzing a particular diophantine equation. Like the [last time](../interesting-equation), this equation will be quadratic. Unlike last time, this time there will actually be some integral solutions. The equation in question is

$$x^2 - 5y^2 = 4$$

where, of course, $x,y\in\Z$. In other words, we want to know which integers $y$ make $5y^2+4$ a perfect square. The answer may surprise you.

Note: I'm gonna use some facts about Dedekind domains that I haven't proved anywhere on this blog (i.e. unique factorization of ideals into prime ideals). If I'm going to keep doing posts like this one, at some point I will write a post introducing the theory of Dedekind domains and proving that rings of integers are always Dedekind.

# The Answer
The first thing to realize is that working in $K=\Q(\sqrt 5)$ allows us to rewrite our equation as

$$\knorm(x+y\sqrt5)=(x+y\sqrt5)(x-y\sqrt5)=x^2-5y^2=4,$$

where $\knorm:K\to\Q$ is the standard relative norm, so we are looking for elements of $K$ (integral coefficients and) with norm $4$. Since we only want elements with integer coefficients, we may be tempted to work in the ring $\Z[\sqrt 5]$. However, this ring isn't super nice. Instead, the proper setting for this problem is the ring of integers $\ints K=\Z[\phi]$ where $\phi$'s satisfies $x^2-x-1=0$ (notice that $-\inv\phi$ also satisfies this polynomial). 

Hence, our goal is to find elements of $\ints K$ with norm $4$. Well, technically our goal is to find elements of $\Z[\sqrt5]$ with norm $4$, but since $\Z[\sqrt 5]\subseteq\ints K$, our only concern is that $\ints K\sm\Z[\sqrt 5]$ might have some norm $4$ elements, but this will turn out to be a non-issue.

Fix $x,y\in\Z$ such that $x+y\phi$ has norm $4$. That is,

$$\knorm(x+y\phi)=\parens{x+y\phi}\parens{x-y\frac1\phi}=4.$$

This shows that $x+y\phi$ is a factor of $4$, so the natural thing to do would be to invoke unique factorization somehow. We are in luck because $\ints K$ turns out to be a UFD. However, this is non-trivial to prove, so we won't rely on this fact. We'll instead rely on the slightly-easier-to-prove facts [^1] about general Dedekind domains. In particular, that they recover unique factorizations on ideals. In terms of ideals, we have

$$(x+y\phi)(x-y\inv\phi)=(4)=(2)^2.$$

Note that $(2)$ is prime as

$$\begin{align*}
    \ints K/(2)
    \simeq \frac{\Z[X]}{(2,X^2-X-1)}
    \simeq \frac{\F_2[X]}{(X^2-X-1)}
    \simeq \F_4.
\end{align*}$$

This makes $(2)^2$ the (unique) factorization of $(4)$ into prime ideals. Because $x+y\phi$ and $x-y\inv\phi$ are not units (as they have non-unit norms), this means we must have

$$(x+y\phi)=(2)=(x-y\inv\phi).$$

Thus, $x+y\phi=2u$ for some unit $u\in\units{\ints K}$ [^2]. Now, we have [previously shown](../solving-pell) that $\units{\ints K}=\pm\eps^{\Z}$ for some fundamental unit $\eps\in\ints K$. It's not too hard to show furthermore that one can take $\eps=\phi$ as such a fundamental unit. This means we have shown that every norm $4$ element of $\ints K$ is of the form $\pm2\phi^n$ for some $n\in\Z$. 

We can actually say more. Because $\knorm(x+y\phi)=\knorm(2)$, we must have $\knorm(u)=1$; however, $\knorm(\phi)=-1$, so $u$ must be an even power of $\phi$. That is, the norm $4$ elements of $\ints K$ are exactly those of the form $\pm2\phi^{2n}$ for some $n\in\Z$.

Since we are looking for solutions to $x^2-5y^2=4$ and squaring erases signs, we'll ignore the $\pm$, and define sequences $a_n,b_n\in\Z$ by $a_n+b_n\phi=2\phi^{2n}$. Using that $\phi^2=1+\phi$, we see that

$$a_{n+1}+b_{n+1}\phi=2\phi^{2n}\phi^2=(a_n+b_n\phi)(1+\phi)=(a_n+b_n)+(a_n+2b_n)\phi$$

so $a_{n+1}=a_n+b_n$ and $b_{n+1}=a_n+2b_n$. At this point, it is worthwhile to remark that $a_0=2$ and $b_0=0$, so induction shows that $a_n,b_n$ are both even for all $n$. This means that $a_n+b_n\phi\in2\ints K\subseteq\Z[\sqrt5]$, so the norm $4$ elements are really in 1-1 correspondence with the solutions we seek. 

Now, we want "integers $y$ such that $5y^2+4$ is perfect" so we really only care about $b_n$. With this in mind, note that $a_n=b_{n+1}-2b_n$ so $a_{n+1}=b_{n+2}-2b_{n+1}$. Thus, $b_{n+2}-2b_{n+1}=b_{n+1}-b_n$ which we rearrange to read

$$b_{n+2} = 3b_{n+1}-b_n,\,b_0=0,\,b_1=2$$

We could get an explicit formula for this [^3], but we'll cheat a little instead. If you form a table of the first few values of $b_n$,

$$\begin{array}{| c | c | c |}\hline
n & 0 & 1 & 2 & 3 & 4 & 5\\\hline
b_n & 0 & 2 & 6 & 16 & 42 & 68\\\hline
\end{array}$$

and stare at them for long enough, you may notice that it looks a lot like $b_n=2F_{2n}$ where $F_n$ is the $n$th Fibonacci number. Indeed, defining $\ast b_n:=2F_{2n}$ we see this sequence satisfies

$$\ast b_{n+2} = 2F_{2n+4} = 2F_{2n+3} + 2F_{2n+2} = 4F_{2n+2} + 2F_{2n+1} = 6F_{2n+2} - 2F_{2n} = 3\ast b_{n+1} - \ast b_n.$$

Since we also have $\ast b_0=2F_0=0$ and $\ast b_1=2F_2=2$, this shows that $b_n=\ast b_n=2F_{2n}$. Returning to our original question (and noting that $\phi=(1+\sqrt5)/2$), we can write $a_n+b_n\phi=x_n+y_n\sqrt5$ where

$$x_n=a_n+F_{2n}\text{ and }y_n=F_{2n}.$$

Thus, the (positive) integers $y$ such that $5y^2+4$ exactly make up every other Fibonacci number! This is a very surprising fact on first glance, but it came fairly naturally from our analysis of the equation $x^2-5y^2=4$. The fibonacci numbers showed up since we worked in the ring $\ints K=\Z[\phi]$ where $\phi$ is the golden ratio, and it's every other fibonacci number because $\knorm(\phi)=-1$ so you switch between $5y^2+4$ being a square and $5y^2-4$ being a square as you consider consecutive powers of $\phi$ (consecutive Fibonacci numbers).

[^1]: that I'm still not proving here
[^2]: We could have reached this conclusion earlier if we had used unique factorization at the level of elements, but the detour through ideals was a short one, so no biggy
[^3]: using e.g. generating functions or linear algebra
