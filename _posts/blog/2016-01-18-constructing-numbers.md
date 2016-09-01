---
layout: post
title: "Constructing Numbers"
modified: 2016-09-01
categories: blog
excerpt:
tags: [math, sets, first]
image: 
  feature: blog/feature/post-bg-01.jpg
  credit: 123RF
  creditlink: https://www.123rf.com/photo_24386233_red-brickwork-the-number-1961-on-background-white-bricks.html
date: 2016-01-18 19:17:00
---

This first post will serve as an introduction to constructing (the rational) numbers. For the sake of keeping this post short(ish) and accesible, this will not be a rigorous treatment of the subject. Explanations will be short and claims will be stated without proof.

Naturals
---------------
---------------
Before we begin the construction, we need to address the question of what it is we are trying to construct. We will begin with the natural numbers, but what are the naturals numbers? They are the set $$ \mathbb N=\{0,1,2,3,\dots\} $$ (in usual parlance), but more simply, they are a collection of objects where each object has a successor (you can always add 1) and there is an object that is no other object's successor (there is a starting point).

So, calling the set we are going to construct $$N$$ and letting $$S:N\rightarrow N$$ be our successor function, we want the following the be true:

* There is an element $$0\in N$$ such that $$S(a)=0$$ for no $$a\in N$$
* $$S(a)\in N$$ for all $$a\in N$$
* Nothing else is in $$N$$

There may be a few different candidates for elements of  $$N$$ that come to mind, but you have to remember that we are constructing these numbers. At this point, we do not even know what a 5 is; that is what we are trying to figure out. As such, the elements of $$N$$ need to be fundamental objects, something that is mathematically sound and does no depend on prexistence of numbers. Our choice of elements (and the usual choice) is sets [^1].

We begin by defining $$0\equiv\{\}$$ (the empty set). Next, we need a successor function, so we define $$S(a)\equiv a\cup\{a\}$$ [^2]. From this, we have 

$$\begin{align*}
0 &= \{\} \\
S(0) &= \{\}\cup\{\{\}\}=\{\{\}\}=\{0\}\equiv1 \\
S(1) &= \{0\}\cup\{\{0\}\}=\{0,\{0\}\}=\{0,1\}\equiv2 \\
&\vdots
\end{align*}$$

As you can see, every natural number is the set of all natural numbers preceding it. Using this definition of $$0$$ and $$S$$, we can define (construct) the set of natural numbers by stating that $$N$$ is the smallest set containing $$0$$ that is closed under $$S$$ [^3].

To finish the discussion on naturals, the following give definitions of addition and multiplication that behave as you would expect:\\
$$\begin{align*}
a + 0 &= a \\ 					
a + S(b) &= S(a + b) \\
a * 0 &= 0 \\
a * S(b) &= a + (a*b)
\end{align*}$$


Integers
---------------
---------------
So, now that we know what $$0,1,2,\dots$$ are, the next thing we desire are negative numbers. This, and the following construction, will be length than the previous one. The idea here is to form ordered pairs $$(a,b)$$ of natural numbers. These pairs will (in a sense) represent the integer $$a-b$$ [^4].

The first thing you might realize is that, if $$(a,b)$$ represents $$a-b$$ then $$(1,3)=(0,2)$$. This seems to suggest that are multiple -2's that are different (as ordered pairs), but equal in value. This is an issue and will be dealt with by effectively "sweeping it under the rug". We begin by defining and equivalence relation $$\sim$$ on pairs of natural numbers (An equivalence relation is just a way of saying two objects are equivalent [^5]). Motivated by the idea that $$(a,b)$$ represents $$a-b$$, we say $$(a,b)\sim(c,d)$$ iff $$a+d=c+b$$ [^6].

Finally, we define the set of integers $$Z$$ to be the set of all equivalence classes of pairs of naturals under the relation $$\sim$$ [^7]. Note that we now need to define addition, multiplication, and even subtraction on integers (pairs of naturals). I'll leave this as an exercise for the reader [^8].


Rationals
---------------
---------------
Now that we have all integers (positive and negative [^9]), our next step is to construct the rational numbers. These numbers, more commonly known as fractions, are ratios of integers (Ex. $$\frac12$$, $$\frac58$$, $$\frac94$$). The idea here is similar to the one above. We start by forming ordred pairs of integers and then say what it means for two ordered pairs to be equivalent. 

Our definition of equivalence here will be motivated by the idea that $$(a,b)$$ should represent $$\frac a b$$. You may remember from elementary school that two fractions are equivalent if you can cross multiply and get the same number twice. With this in mind, we define the equivalence relation $$\sim$$ s.t. [^10] $$(a,b)\sim(c,d)$$ iff $$ad=bc$$. Now, the set of rationals $$Q$$ is just the set of all equivalence classes of pairs of integers under $$\sim$$. 

Again, we still need to define addition, multiplication, subtraction, and now division as well before we can be satisfied that this construction lines up with our intuition of the natural numbers. And again, this is left as an exercise for the reader.


Notes
---------------
---------------
* You may be wondering why I said nothing about constructing the reals. This is because the construction of the real numbers (that I am most familiar with) involves taking [infinite sets of rational numbers](https://en.wikipedia.org/wiki/Dedekind_cut) and is more messy and less intuitive than what I presented here. Basically, it is beyond the scope of this blog post [^11].
* One annoyance with this route of constructing numbers (going from set to set) is that many numbers end up with multiple representations. As an example, consider $$0$$. As a natural number $$0=\{\}$$, as an integer $$0=[(0,0)]=[(\{\},\{\})]$$, and as a rational number $$0=[(0,1)]=[([(\{\},\{\})],[(\{\{\}\},\{\})])]$$ [^12]. One construction of numbers [^13] that avoids this annoyance is the construction of Conway's [surreal numbers](https://en.wikipedia.org/wiki/Surreal_number).
* The astute reader will notice that our construction of rational numbers does not rule out $$\frac00$$ and is therefore technically incorrect. This is simply because I intended to present a fairly simple introduction to the construction with the hope that it would prepare the reader for a more rigorous look at it. Explicitly mentioning that $$(0,0)$$ should not be one of the considered pairs of integers would not have, in my opinion, made the construction any more intuitive.

[^1]: Informally, a set is a collection of objects. Although this is not necessary, these objects are often restricted to being sets themselves.
[^2]: Set union: the set containing all elements of a and all elements of b.
[^3]: This just means that if you apply S to a member of N, you get a member of N as a result.
[^4]: Remember that we have not definied subtraction of natural numbers, so a-b does not make formal sense. It is, however, intuitively what these pairs represent.
[^5]: It is any symmetric, transitive, and reflexive relation.
[^6]: iff is short for "if and only if".
[^7]: An equivalence class is just a set where everything in it is equivalent.
[^8]: I have always wanted to say that.
[^9]: and zero
[^10]: s.t. is short for "such that".
[^11]: I have always wanted to say that.
[^12]: [x] is the equivalence class containing x.
[^13]: naturals, integers, rationals, reals, and more