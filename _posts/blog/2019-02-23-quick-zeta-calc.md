---
layout: post
title: "A Quick Note on Values of the Riemann Zeta Function"
modified:
categories: blog
excerpt:
tags: [math, riemann zeta, quick, zeta, bernoulli number, bernoulli polynomial]
date: 2019-02-23 00:01:00
---

I don't know how much you'll enjoy this post, but calculating values of the zeta function is one of those things that struck high-school me as being incredibly difficult and requiring mastery over the arcane arts of mathematics, so it's pretty cool to know that I can do this now [^1]. Without further ado, let's find a formula for $\zeta(2k)\dots$ [^2]

Let's start with Parseval. Recall that we have a nice theory of Fourier analysis on the circle $S^1$ for the space $C^2(S^1)$ of twice differentiable (with continuous second derivative) functions. Note furthermore that viewing circle functions as functions $f:[0,1]\to\C$ with $f(0)=f(1)$ gives an embedding $C^2(S^1)\into C^2([0,1])$. Note that the set $\bracks{e_n}_{n\in\Z}$ where $e_n(x)=e^{-2\pi inx}$ is orthonormal with respect to the following inner product on $C^2([0,1])$:

$$\angles{f,g}=\int_0^1f(x)\conj{g(x)}\dx.$$

We claim (without proof) that the (linear) span of $\bracks{e_n}$ is dense in $C^2([0,1])$, letting us make a limit argument to show that for any $f\in C^2([0,1])$, one has [^7]

$$\sum_{n=-\infty}^\infty\abs{\angles{f,e_n}}^2=\|f\|^2:=\int_0^1\abs{f(x)}^2\dx.$$

The comment about embedding $C^2(S^1)$ into $C^2([0,1])$ is meant to help you recognize that $\angles{f,e_n}$ is exactly the $n$th Fourier coefficient of $f$. Our strategy for calculating $\zeta(2k)$ will be to find some function $f\in C^2([0,1])$ whose Fourier series has coefficients (roughly) of the form $c_n=\frac1{n^k}$ and then apply Parseval's above identity.

The functions we'll use are the <b>(Jacob) Bernoulli polynomials</b> $B_k(x)$ defined by the following identity [^4]

$$\int_x^{x+1}B_k(u)\d u=x^k.$$

In particular, $\int_0^1B_k(x)\dx=0^k$ (Here, $0^0=1$). Note that one can show that $B_k'(x)=kB_{k-1}(x)$ [^3], and for good measure, one can calculate

$$\begin{align*}
    B_0(x) &= 1\\
    B_1(x) &= x - \frac12\\
    B_2(x) &= x^2 - x + \frac16,
\end{align*}$$

and so on. Note that this derivative relation gives

$$B_k(1)-B_k(0)=\int_0^1B_k'(x)\dx=k\int_0^1B_{k-1}(x)\dx=0$$

for $k>1$ whereas $B_1(1)-B_1(0)=1$. Let the $k$th <b>Bernoulli number</b> $B_k$ be $B_k(0)$ (some authors use $B_k(1)$ instead). With this, we've done enough set up, so let's get to the zeta stuff. [^5]

Define $c_k(n):=\int_0^1B_k(x)e^{-2\pi inx}\dx$, the $n$th Fourier coefficient of $B_k(x)$, and calculate

$$c_k(n)=\int_0^1B_k(x)e^{-2\pi inx}\dx=\frac{-1}{2\pi in}\sqbracks{\left.B_k(x)e^{-2\pi inx}\right|_0^1-\int_0^1 B_k'(x)e^{-2\pi inx}\dx}=\frac{k c_{k-1}(n)}{2\pi in}$$

for $k>1$ (since the product vanishes) while $c_1(n)=-1/(2\pi in)$ (since the integral vanishes). This gives

$$c_k(n) = \frac{k c_{k-1}(n)}{2\pi i n}=\frac{k(k-1)c_{k-2}(n)}{(2\pi in)^2}=\cdots=\frac{k!c_1(n)}{(2\pi in)^{k-1}}=-\frac{k!}{(2\pi in)^k}$$

where the $\cdots$ indicates that an induction argument is taking place behind the scenes. Now, the careful reader should be up in arms with the above equalities because they only hold for $n\neq0$ (this is needed for the integration by parts to work as claimed). By definition of the Bernoulli polynomials, we have $c_k(0)=0$. At this point, Parseval says

$$\sum_{\substack{n=-\infty\\n\neq0}}^\infty \abs{c_k(n)}^2=\int_0^1B_k(x)^2\dx.$$

The left hand side simplifies as

$$\sum_{\substack{n=-\infty\\n\neq0}}^\infty \abs{c_k(n)}^2=2\sum_{n=1}^\infty\frac{(k!)^2}{(2\pi n)^{2k}}=\frac{2(k!)^2}{(2\pi)^{2k}}\zeta(2k),$$

so our fabled $\zeta$ finally appears. To calculate the right hand side, integrate by parts (and induct) some more:

$$\begin{align*}
    \int_0^1B_k(x)^2\dx 
    &= \frac1{k+1}\sqbracks{\left.B_k(x)B_{k+1}(x)\right|_0^1-k\int_0^1B_{k-1}(x)B_{k+1}(x)\dx}\\
    &= -\frac k{k+1}\int_0^1B_{k-1}(x)B_{k+1}(x)\dx\\
    &= -\frac k{(k+1)(k+2)}\sqbracks{\left.B_{k-1}(x)B_{k+2}(x)\right|_0^1-(k-1)\int_0^1B_{k-2}(x)B_{k+2}(x)\dx}\\
    &= \frac{k(k-1)}{(k+1)(k+2)}\int_0^1B_{k-2}(x)B_{k+2}(x)\dx\\
    &=\cdots\\
    &= (-1)^{k-1}\frac{(k!)^2}{(2k-1)!}\int_0^1B_1(x)B_{2k-1}(x)\dx\\
    &= (-1)^{k-1}\frac{(k!)^2}{(2k)!}\sqbracks{\left.B_1(x)B_{2k-1}(x)\right|_0^1-\int_0^1B_{2k}(x)\dx}\\
    &= (-1)^{k-1}B_{2k}\frac{(k!)^2}{(2k)!}.
\end{align*}$$

Putting these two sides together gives

$$\begin{align*}
    \sum_{n=-\infty}^\infty\abs{\angles{B_k(x),e^{-2\pi inx}}}^2 &= \int_0^1B_k(x)^2\dx\\
    \frac{2(k!)^2}{(2\pi)^{2k}}\zeta(2k) &= (-1)^{k-1}\frac{B_{2k}(k!)^2}{(2k)!}\\
    \zeta(2k) &= (-1)^{k-1}B_{2k}\frac{(2\pi)^{2k}}{2(2k)!}
\end{align*}$$

In particular, plugging in $k=1$ recovers the classic

$$\zeta(2)=(-1)^{1-1}B_2\frac{(2\pi)^2}{2(2!)}=\frac{\pi^2}6$$

which is a good sign [^6]. Furthermore, I haven't actually checked this myself yet, but I'm pretty sure that using the functional equation for the $\zeta$ function along with this calculation let's you show that $\zeta(1-2k)\in\Q$ for all $k$ (and so $\zeta(1-k)\in\Q$ for all $k$ since it's 0 even $k$ is odd) which is quite surprising. To end, I'll really indulge a high-school fantasy by "proving" everyone's favorite "theorem."

<div class="theorem" name="The Best One">
    The sum of the naturals is $-1/12$. That is,
    $$\sum_{n=1}^\infty n=-\frac1{12}.$$
</div> 
<div class="proof4">
    Recall the functional equation for $\zeta(s)$ which is
    $$\zeta(s)=\frac{\pi^s\Gamma\parens{\frac{1-s}2}\zeta(1-s)}{\Gamma\parens{\frac s2}\sqrt\pi}$$
    Thus (using $\Gamma(-1/2)=-2\sqrt\pi$ and $\Gamma(1)=1$),
    $$\zeta(-1)=\frac{\Gamma(1)\zeta(2)}{\Gamma(-1/2)\pi\sqrt\pi}=\frac{\pi^2}{-12\pi^2}=-\frac1{12}.$$
    Now recall that the Riemman zeta function is originally defined as
    $$\zeta(s)=\sum_{n=1}^\infty\frac1{n^s},$$
    and that $\frac1{n^{-1}}=n$, so 
    $$-\frac1{12}=\zeta(-1)=\sum_{n=1}^\infty n.$$
    Boom! There you have it: the sum of the naturals is negative one twelfth. Checkmate, mathematicians; the internet wins this one.
</div>

[^1]: And also nice to know that I didn't have to master any arcane arts to do so
[^2]: using an argument that's rigorous modulo me playing fast-and-loose with the definition of Bernoulli numbers/polynomials and with proving Parseval's identity
[^3]: A perhaps suggestive observation is that this relation is held by the polynomials B_k(x)=x^k
[^4]: Exercise: prove that this defines a unique (degree k) polynomial
[^5]: Read: Let's do some GRE prep by integrating by parts
[^6]: A better sign is that the general formula we calculated here is the same one appearing in Wikipedia
