---
layout:     post
title:      "Square Triangles"
subtitle:   "1 + 2 + 3 + ... + m = n^2"
date:       2016-07-24 03:06:00
author:     "NivenT"
header-img: "img/blog/header/post-bg-04.jpg"
thumbnail:  /img/blog/thumbs/empty.png
tags: [math, number theory, algebra]
category: [math]
comments: true
---

<script src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"></script>

I recently came across [this](https://www.youtube.com/watch?v=Gh8h8MJFFdI) youtube video, where [Matt Parker](http://standupmaths.com) asks whether 36 is the only triangle-square number or not. Immediately after seeing this, I decided to tackle the problem, and after some early results, I decided to chronicle my efforts thus far [^1].
{: style="font-size: 60%;"}

The Problem
------------
------------
Before detailing my attempt to tackle this problem, it's probably a good idea to specify what it is. We are trying to find all triangle-square numbers. A triangle-square number is a number that is both a triangle number and a square number [^2]. So, it is a number $$x$$ such that $$x=n^2$$ and $$x=m(m+1)/2$$ where $$m,n$$ are natural numbers. Therefore, we will find such $$x$$ by investigating solutions to the following equation:
{: style="font-size: 60%;"}

<center>
$$\begin{equation}
n^2=\frac{m(m+1)}2
\end{equation}$$
</center>
{: style="font-size: 80%;"}

We are looking for pairs of natural number $$m, n$$ that make the above true.
{: style="font-size: 60%;"}

First Steps
----------------
----------------
Before I started trying to solve this problem, I thought about what I expected the solution to be. Initially, I figured 36 was probably the only triangle-square number [^3]. At the very least, I could not immediately think of any other such number, or an obvious connection between triangle and square numbers. When I started working on the problem, I expected a nice solution to appear "in plain sight" after a bit of algebra that would show that the only possible solution was 36 [^4].
{: style="font-size: 60%;"}

Finally beginning to work, the very first thing I did was rewrite the equation. Division is much messier than multiplication, so I had to get rid of that divide by 2. I also thought it might be a good idea to distribute the $$m$$.
{: style="font-size: 60%;"}

<center>
$$2n^2=m^2 + m$$
</center>
{: style="font-size: 80%;"}

Before I continued, I thought it might be helpful to write down the one solution I had so far. A quick calculation showed that the triangle-square 36 corresponds to the solution $$(m,n)=(8,6)$$. Now that I could return to the problem at hand, one approach to solving diophantine equations [^5] that is often helpful is looking for restrictions on the variables. This basically involves using algebra and properties of integers to show that the variables must behave a certain way or follow a certain pattern. Since this problem deals with squares, the first trick that came to mind was to consider the equation $$\pmod 4$$. Perfect squares are always congruent to 0 or 1 $$\pmod 4$$ [^6], so since there are two squares in the equation, this can be used to find 4 (hopefully not distinct) possible values of $$m\pmod 4$$.
{: style="font-size: 60%;"}

$$n^2\pmod 4$$  | $$m^2\pmod 4$$ | equation $$\pmod 4$$ | $$m\pmod 4$$
-------|---------
0 | 0 | $$0\equiv0+m$$ | 0
0 | 1 | $$0\equiv1+m$$ | 3
1 | 0 | $$2\equiv0+m$$ | 2
1 | 1 | $$2\equiv1+m$$ | 1
{: style="font-size: 60%;"}

As you can see from looking at the rightmost column $$m$$ could potentially be congruent to anything $$\pmod 4$$. In other words, that was a waste of effort because it told us nothing.
{: style="font-size: 60%;"}

A Breakthrough
-------------------
-------------------
After my initial attempt proved less than fruitful, I decided I needed to tackle this problem from a different angle. My first thought was to refactor the right hand side of the equation, because multiplication is nice.
{: style="font-size: 60%;"}

<center>
$$2n^2 = m(m+1)$$
</center>
{: style="font-size: 80%;"}

After staring at this equation for some time, and idea popped into my head: I should consider the prime factorizations of these numbers. The left hand side is twice a square. In the prime factorization of a square number, every prime has an even exponent. This means that if $$n^2=p_1^{a_1}p_2^{a_2}\dots p_k^{a_k}$$ where each $$p_i$$ is a prime number, then every $$a_i$$ is even. Therefore, in the prime factorization of the left hand side, every prime has an even exponent, except for 2, which has an odd exponent. Now we're getting somewhere. This must also be the case on the right hand side [^7], but how can we use that information? Here, I remembered that every number is coprime to its successor [^8], so for any given prime $$p$$, its exponent in the prime factorization of $$2n^2$$ is equal to its exponent in the prime factorization of $$m$$ or to its exponent in the prime factorization of $$m+1$$. Therefore, every prime in the prime factorization of $$m$$ must have an even exponent. The same holds for $$m+1$$. The only exception is 2, which has an odd exponent in one of $$m$$ and $$m+1$$. This means that $$m$$ is twice a square and $$m+1$$ is a square, or vice versa! I then decided to continue my investigation by looking at each case separately.
{: style="font-size: 60%;"}

The First Case: $$m=2k^2$$
-----------------------------
-----------------------------
At this point, I just did a little algebra.
{: style="font-size: 60%;"}

<center>
$$
\begin{align*}
m(m+1) &= 2k^2(2k^2 + 1) \\
&= 4k^4+2k^2\\
&= 2n^2\\
\end{align*}
$$
</center>
{: style="font-size: 60%;"}

<center>
$$
\begin{align*}
&n^2 = 2k^4+k^2
\end{align*}
$$
</center>
{: style="font-size: 60%;"}

Here was another equation to investigate. Like with the first, my initial thought was modular arithmetic. Once again, we are dealing with squares so I looked at the equation $$\pmod 4$$. I'll spare you the details, but it turns out that $$k$$ must be congruent to 0 or 2 $$\pmod 4$$. In other words, $$k$$ is even. When I reached this point, I was out of ideas, and returned to the classic stare at the problem until inspiration hits approach. Luckily, it did. I hadn't yet used the fact that $$m+1$$ was a square. This realization led to the following bit of algebra.
{: style="font-size: 60%;"}

<center>
$$
\begin{equation}
2k^2 + 1 = q^2\\
2k^2 = (q-1)(q+1)
\end{equation}
$$
</center>
{: style="font-size: 60%;"}

This looked promising. I tried some more mod stuff, tried thinking about what properties of $$q$$ I could derive from this, and considered where using the fact that 2 must divide $$(q-1)$$ or $$(q+1)$$ could get me. All of this was to no avail, however. Eventually, after some more staring, I realized that $$(q-1)$$ and $$(q+1)$$ have the same parity, and so since the left hand side is even, they must both be even as well so $$q$$ is odd [^9]. Naturally, this led to another equation, and even more algebra.
{: style="font-size: 60%;"}

<center>
$$
\begin{equation}
q = 2t+1\\
2k^2 = 2t(2t+2)\\
k^2 = 2t(t+1)\\
n^2 = 2t(t+1)(2t+1)^2
\end{equation}
$$
</center>
{: style="font-size: 60%;"}

At this point, I had stumbled onto a gem, although I didn't realize it at first. Looking at that final equation, I didn't expect more modular arithmetic to be helpful, but I had no other ideas so I tried the standard look at things $$\pmod 4$$ approach, and learned nothing useful. After some consideration, I returned to the idea that had gotten me this far: considering prime factorizations. The left hand side is a perfect square, so all of its prime factors have even exponents. The same must be true of the right hand side. The rightmost factor is a perfect square, so its primes obviously have even exponents. So, what remains (i.e. $$2t(t+1)$$ must also have primes with all even exponents. This meant that $$2t(t+1)$$ must be a perfect square. Symbolically,
{: style="font-size: 60%;"}

<center>
$$2t(t+1)=s^2$$
</center>
{: style="font-size: 80%;"}

This was exciting. If you look long enough, this equation should start to look familiar. It's very similar to the equation this problem began with [^10]. In case you don't remember, the equation I'm referring to is this one:
{: style="font-size: 60%;"}

<center>
$$2n^2=m(m+1)$$
</center>
{: style="font-size: 80%;"}

Very similar indeed. This gave me an idea: could solutions to the original equation lead to solutions from this equation? The answer is, luckily, yes. If $$t$$ is a solution to the original equation ($$t(t+1)=2p^2$$ is twice a perfect square), the it is also a solution to this latest equation ($$2t(t+1)=4p^2=(2p)^2$$ is a perfect square). This was exciting! Recall that we derived this equation for $$t$$ by investigation solutions to the original equation. Values for $$t$$ that satisfy this equation [^11] can be used to generate solutions to the original equation. Since we have just shown that solutions to the original equation also solve this $$t$$-equation, we have shown that they also generate new solutions to the original equation! Therefore, not only is 36 not the only triangle-square number, but there are infinitely many such numbers, and once you know one of them, you know infinitely many of them! As an example, remember that $$(m,n)=(8,6)$$ is the solution to the original equation, so if we let $$t=8$$, then we can generate a new solution. The corresponding solution is $$(m,n)=(288,204)$$, and indeed the 288th triangle number is $$204^2$$.
{: style="font-size: 60%;"}

As exciting as this news is, our work here is not done. We still do not know if this process gives all solutions or not. At this point, I thought it would. It was a really nice pattern (old solutions giving rise to new ones), and so I figured it was probably all there was to it. Still, I continued to investigate further just to make sure.
{: style="font-size: 60%;"}

The Second Case: $$m+1=2k^2$$
-----------------------------
-----------------------------
This case went by more quickly than the last, because it involved applying the same ideas. As always, I started with algebra.
{: style="font-size: 60%;"}

<center>
$$
\begin{align*}
m(m+1) &= 2k^2(2k^2 - 1) \\
&= 2n^2\\
\end{align*}
$$
</center>
{: style="font-size: 60%;"}

<center>
$$
\begin{align*}
n^2 = k^2(2k^2-1)
\end{align*}
$$
</center>
{: style="font-size: 60%;"}

I tried to find a restriction on the value of $$k\pmod 4$$ from that equation, but found none. Oh well. Modular arithmetic had not been the most useful tool during this venture, so I didn't expect it to be very helpful here either. I then used the fact that $$m$$ was a perfect square to do the following.
{: style="font-size: 60%;"}

<center>
$$
\begin{equation}
2k^2-1=q^2\\
q=2t+1\\
2k^2=2t+2\\
k^2=t+1\\
n^2=2(t+1)(2t+1)
\end{equation}
$$
</center>
{: style="font-size: 60%;"}

Here, I returned to my good old friend prime factorizations. $$n^2$$, and hence $$2(t+1)(2t+1)$$, must only have primes with even exponents in its prime factorization. So, the exponent of 2 in the prime factorization of $$(t+1)(2t+1)$$ must be odd. $$(2t+1)$$ is odd, so 2 has an exponent of 0 in its factorization, and so the exponent of 2 must be odd in the prime factorization of $$(t+1)$$. Since $$(t+1)$$ and $$(2t+1)$$ are coprime, they share no prime factors. This means that the exponent of every prime (except 2) in the prime factorization of $$(t+1)$$ must be even. Thus $$(t+1)$$ is twice a square, so
{: style="font-size: 60%;"}

<center>
$$
\begin{equation}
t+1=2s^2\\
n^2=4s^2(4s^2-1)
\end{equation}
$$
</center>
{: style="font-size: 60%;"}

This progressed nicely from here. $$4s^2$$ is a square, so $$(4s^2-1)$$ must be a square too. However, $$4s^2-1=4(s^2-1)+3$$, so its remainder is 3 when divided by 4 (i.e. $$4s^2-1\equiv3\pmod4$$). However, a perfect square will always have remainder 0 or 1 when divided by 4. Therefore, $$(4s^2-1)$$ cannot be a square! This means that there is no solution to the original equation where $$m+1=2k^2$$.
{: style="font-size: 60%;"}

Final Thoughts
-------------------
-------------------
At this point, I had found a method for generating infinitely many solutions where $$m$$ is twice a square, and had shown that no solutions exist when $$m+1$$ is twice a square. This seemed to lend evidence to the idea that all the solutions could be found by starting with a valid $$m$$ value (Ex. $$m=1$$), plugging it in for $$t$$ to generate a new valid $$m$$ value, and repeating. However, it still did not 
{: style="font-size: 60%;"}

Things were looking good, until I came across the solution $$(m,n)=(49,35)$$ [^12]. This was an issue for two reasons. One, you cannot find this solution by starting with $$m=1$$ and using $$t$$ to generate new solutions. Two, $$m+1=50$$ is twice a perfect square. The first issue I can deal with. All it means is that my iteration idea does not generate all solutions; it still generates valid solution, so that doesn't bother me too much. The second issue is much more disturbing. I thought I had shown that there was no solution where $$m+1$$ is twice a square. This means that there must have been some flaw in my reasoning somewhere, and I need to reconsider my approach to this problem.
{: style="font-size: 60%;"}

Once I realized I had flaws, I decided I had done enough math for one night [^13], and would continue my investigation some other time. Thus, I leave you on a bit of a cliffhanger [^14].
{: style="font-size: 60%;"}

[^1]: This post will try to show my entire approach to this problem, and not just where it worked. There will be places where my reasoning was more complicated than it needed to be. I will not point these out, because they seem obvious in hindsight.
[^2]: duh
[^3]: Aside from 1, which is a boring (read "trivial") answer.
[^4]: Perhaps, there would be a bound on the possible values of m or n, and so all the solutions could be found by checking every possible value for the bounded variable.
[^5]: Equations where you are only interested in integer solutions.
[^6]: In English, if you divide a perfect square by 4, the remainder is 0 or 1 (Ex. 9/4 = 2 R 1 and 64/4 = 16 R 0).
[^7]: They are equal, after all.
[^8]: n and (n+1) do not share any prime factors
[^9]: If I were good at math, I would have realized this sooner
[^10]: Oh yeah, this problem had a beginning. At this point, I was beginning to think it was a neverending sequence of equation manipulation with no origin and no end.
[^11]: Values such that 2t(t+1) is a perfect square.
[^12]: Just when I think I had done good math for once, a counterexample ruins everything.
[^13]: I had almost filled a page, and turning to the next page in my notebook would have been too much trouble.
[^14]: In case anyone is curious, the problem was that I forgot to square q after writing q=2t+1, so I had 2k^2=q+1 instead of 2k^2=q^2+1. Also, I don't plan on writing another post about what I did after finding the error.