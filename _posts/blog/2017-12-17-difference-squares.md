---
layout: post
title: "Difference of squares"
modified:
categories: blog
excerpt:
tags: [math, number theory, galois theory, thoughts, problem]
date: 2017-12-17 21:55:00
---

Two new posts in one day? It must be Christmas. I think this post will be relatively short. I want to talk about a problem that popped in my head while I was working on the last post, and then mention some thoughts that this problem sparked which I hope are worth writing down before I forget.

# Which numbers can be written as the difference of two squares?
Let's just jump right into things. One natural place to start tackling this questions is with the primes. With that said, let $p$ be a prime number and suppose we can write $p=x^2-y^2$ for some $x,y\in\Z_{\ge0}$. This gives[^1]

$$p=x^2-y^2=(x-y)(x+y)\implies p=x+y\text{ and }x-y=1$$

which means we require that $p$ is the sum of two consecutive numbers! Now, this took me longer than I'd like to admit to realize while I was working on this, but this is equivalent to saying that $p$ is odd. In other words, all primes $p\neq2$ can be written as the difference of two squares, namely $p=\lceil p/2\rceil^2-\lfloor p/2\rfloor^2$. 

Since we've completely characterized which primes are differences of squares, we really hope that the product of differences of squares is also a difference of squares. I claim that a natural way of reaching this conclusion is to make use of the ring $\Z[\eps]\simeq\Z[x]/(x^2-1)$ where $\eps^2=1$. Using this ring let's us factor $x^2-y^2=(x+\eps y)(x-\eps y)$, and while we could factor things before, this factorization is for useful since we can easily calculate

$$(a+b\eps)(c+d\eps)=(ac+bd)+\eps(ad+bc)$$

which is enough to see that $(a^2-b^2)(c^2-d^2)=(ac+bd)^2-(ad+bd)^2$ so being a difference of squares is preserved by multiplication. Since all odd primes are differences of squares, this get's us that all odd numbers are differences of squares[^2].

Now, let $z=n^2m$ where $m=x^2-y^2$. Then, $z=n^2(x^2-y^2)=(nx)^2-(ny)^2$ is also a difference of squares. Hence, any number that $2$ divides an even number of times is a difference of squares. At this point, I was tempted to think that I was done, but then I realized that $8=3^2-1^2$ is also a difference of squares. Since $4=2^2-0^2$, we know that $2^2$ and $2^3$ are differences of squares, so $2^{2a+3b}$ is also a difference of squares where $a,b\in\Z_{\ge0}$. It's not hard to see that every integer can be written as $2a+3b$ execept for 1 [^3], so $2^1=2$ is the only power of two that cannot be written as a difference of squares. 

Since every odd prime is a difference of squares, and all but one power of $2$ is also a difference of squares, we've shown that the only number that might not be difference of squares are those that $2$ divides exactly once. Another way of characterizing these "bad" numbers is that they are the $n\in\Z$ for which $n\equiv2\pmod4$. Now, the equation $x^2-y^2\equiv2\pmod4$ has no solutions as one can verify by checking all 16 possible assignments of $x,y$. Thus, we've completely characterized the numbers that can be written as differences of squares; they are all the integers that are not $2\pmod4$! This is a surprisingly simple and nice outcome if you ask me.

# Thoughts[^5]
With that question resolved, I wanna mention some thoughts it motivated. In the process of answering the question, it was helpful to consider the ring $\Z[\eps]$ which morally felt like the ring of integers of the number field $K=\Q(\eps)$ [^4]. However, this is technically wrong since $K$ isn't a number field; it's not a field at all (or even just a domain since $(1-\eps)(1+\eps)=0$). Despite this, we still have a natural notion of a "relative norm" on $K$ over $\Q$ given by $\knorm(x+y\eps)=x^2-y^2$, which made me wonder how much of algebraic number theory can be recovered if we study ring extensions of $\Q$ like this one [^7].

Taking a step back to a slightly more general setting, my curiosity shifted away from number theory specifically to wonder what happens if you do Galois theory in a more general setting like this. The "ring extension" $K/\Q$ morally feels like degree 2 Galois extension with non-trivial autmorphism given by $\sigma(x+y\eps)=\sigma(x-y\eps)$. After having this in the back of my mind all day, this is what I've discovered so far as the possible beginnings of a formalism... 

Fix some field $\F$. We want to study (commutative) rings [^6] containing this field, so let $R$ be such a ring. $R$ is still an $\F$-vector space, so we can still define the degree of the extension $R/\F$ as $[R:\F]:=\deg_{\F}R$. However, if we think on this more, it might make more sense to think of $R$ less an some sort of extension ring, and more as an $\F$-algebra. I don't know how beneficial this algebra viewpoint is compared to thinking in terms of ring extensions, but it does at least suggest that the true object of interest of this hypothetical generalized Galois theory should be $R$-algebras where we require that $R$ is a $k$-algebra for some field $k$ (or equivalently, that $R$ is a vector space).

The first major issue I see with recovering Galois theory in this setting is the behavior of towers of extensions. Classically, if we have $L/K/F$ a tower of field extensions, then we get that $[L:F]=[L:K][K:F]$ and this allows one to perform induction arguments [^8]. This fact basically follows from the niceness of vector spaces, but since generally for a ring $R$, non-free $R$-modules exist, we face some issues with studying towers of ring extensions. It's possible that $R$ being a $k$-algebra (for $k$ a field) is a strong enough restriction to force all $R$-algebras to be free $R$-modules, but I don't know enough algebra to think of a proof or counterexample to that claim off the top of my head (although it's almost certainly false), so this issue remains unresolved. Despite this, if one could find away to get around this issue of towers of extensions, then[^9] I think you can manage to recover at least a few gems from Galois theory. I'm a hopeful enough person to think that this might be possible in some nice settings, so

>Conjecture<br>
Let $\F$ be a field, and fix some $f(x)\in\F[x]$. Let $R$ be the "splitting ring" of $f(x)$ [^10]. Then, the number of automorphisms $\sigma:R\rightarrow R$ fixing $\F$ is at most $\deg_{\F}R$.

I obviously don't know if this conjecture is true, but I feel that something like it should be true. I suspect I won't do a lot of thinking about this anytime soon, so I leave this here to one day return to it and continue my thoughts.

[^1]: It's technically also possible that x-y=-1, but without loss of generality, assume x>y
[^2]: This didn't hit me until after I'd done all the work that went into this post, but the difference between the nth square and the (n+1)th square is the nth odd number (i.e. (n+1)^2-n^2=2n+1) so this conclusion is trivial
[^3]: If n=2k is even, then take a=k and b=0. If n=2k+1 is odd, then take a=k-1 and b=1 (this fails only if k=0, i.e. if n=1)
[^4]: I'm pretty sure this notation technically makes no sense, but by it, I mean the ring Q(e)={a+be|a,b are fractions} where e^2=1
[^5]: of a Programmer
[^6]: I'm hesistant to require commutativty because the quaternions also feel morally like an extension that should be considered in this more general theory, albeit not a Galois one
[^7]: One immediate question I haven't thought about the answer two is "does the traditional definition of the ring of integers still work?" In this example, one would expect that the integer ring of Q(e) should be Z[e], but I haven't varified that this is what you get from just applying the standard definition of an integer ring.
[^8]: If you're studying an extenion K/F, you might start by picking a in K-F so you get the tower K/F(a)/F. Prove your statement for F(a)/F, get the same thing for K/F(a) by induction of degrees and then use these to together to conclude something about K/F
[^9]: Don't quote me on this; I haven't thought about it too deeply
[^10]: i.e. the smallest ring (containing F) in which f splits