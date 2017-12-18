---
layout: post
title: "An interesting equation"
modified:
categories: blog
excerpt:
tags: [math, number theory, algebraic number theory]
date: 2017-12-17 20:39:00
---

One day I will return to writing posts that are not always very algebraic in nature, but this is not that day. I want to talk today about an example of a peculiar equation, but first a little background... In my mind, number theory (at least on the algebraic side) is ultimately about solving diophantine equations and not much more. This is what originally got me interested in the subject because trying to solve these equations can often feel like some sort of puzzle or exploratory game; there's a common set of tricks one can apply, but not much of a single path or algorithm that always gets you the solution. Among the most basic/fundamental of tricks is to use congruences. If you seek (integer) solutions to $x^2+y^2=3$, then a natural thing to do is consider this equation (mod $4$) and note that there are no solutions to $x^2+y^2\equiv3\pmod4$ [^1], so there are no integer solutions to the original equation; easy. In fact, you can state this principal in general.

>Fact<br>
Let $p(x,y)$ be some polynomial with integer coefficients. If $p(x,y)\equiv0\pmod m$ has no solutions for some $m$, then $p(x,y)$ has no integer solutions.

It's not far fetched to imagine that this is the only thing preventing polynomials from having integer solutions. That is, it's natural to consider if any polynomial that can be solved$\pmod m$ for all $m\in\Z_{>0}$ must be solvable by integers. However, it turns out that this is not the case, and the subject of this post is a single counterexample

$$\begin{align*}
x^2-82y^2=2
\end{align*}$$

For conveince, let's let $q(x,y)=x^2-82y^2-2$. I haven't thought too much about this, but for understanding this post, probably [these](../number-theory) [two](../solving-pell) posts on number theory, and some [ring theory](../ring-intro) should be sufficient; if you don't feel like reading those, then just stick with this post and if anything doesn't make sense, you can refer back to those posts to figure it out or leave a comment, asking a question.

# Solutions in $\Q$ and $\zmod m$
We'll first establish that this equation has solutions both in $\Q$ and in $\zmod m$ for all $m$. For $\Q$, we'll actually do one better and show that it has infinitely many solutions. We will first search for a single rational solution, so let $x=a/b$ and $y=c/d$ where $a,b,c,d\in\Z$. In order to keep things simple, we'll assume $b=d$ so we can rewrite our equation as

$$\begin{align*}
x^2-82y^2=2\iff(a/b)^2-82(c/d)^2=2\iff a^2-82c^2=2b^2\iff a^2=2b^2+82c^2
\end{align*}$$

This suggests one way of finding a solution. We just need to search for integers $b,c$ such that $2b^2+82c^2$ is a perfect square. If you were to try some examples by hand or write a computer program to search, you'd eventually come across $2(3)^2+82(1)^2=10^2$ which gives $(x,y)=(10/3,1/3)$ as a solution to $q(x,y)\in\Q[x,y]$. This is one solution, but far from the only one.

>Exercise<br>
Show that $q(x,y)\in\Q[x,y]$ has infinitely many rational solutions [^2].

To show that this equation has solutions in $\zmod m$, it'll be sufficient to show that it can be solved for $m$ a prime power. This is a consequence of the [Chinese Remainder Theorem](https://www.wikiwand.com/en/Chinese_remainder_theorem).

>Theorem<br>
Let $p\neq3$ be a prime. Then, $q(x,y)$ has a solution viewed as a polynomial $q(x,y)\in\zmod{p^r}[x,y]$ for all $r$. That is, there exists integers $a,b$ s.t. <center>$q(a,b)=a^2-82b^2\equiv2\pmod{p^r}$</center>

<div class="proof2">
Pf: Fix any positive integer $r$, and note that $\gcd(3,p^r)=\gcd(3,p)=1$, which means $3$ is a unit in $\zmod{p^r}$. Fix some $b$ s.t. $3b\equiv1\pmod{p^r}$ and note that $(x,y)=(10b,b)$ is a solution to $q(x,y)\in\zmod{p^r}[x,y]$ as <center>$$100b^2-82b^2=18b^2\equiv2(3b)(3b)\equiv2\pmod{p^r}$$</center>$\square$
</div>

This just leaves the case of powers of $3$. This isn't actually a special case, and can be handled much in the same way as all the others. We begin by noting that $(66/13,-7/13)$ is a rational solution to $q(x,y)$. Since $3$ does not divide $13$, we say that they are coprime, and so $13$ is a unit in $\zmod{3^r}$ for all $r$. Hence, $(66/13,-7/13)$ still makes sense as a solution in $\zmod{3^r}$. This will give away one solution to the exercise, but in case you're curious where this point came from [^3].

Thus, we've shown $q(x,y)$ has solutions (mod $p^r$) for all prime powers $p^r$, and hence it has solutions (mod $m$) for all integers $m$.

# Chinese Remainder Theorem
This section can be skipped, but I wanted to give a statement and proof of CRT for completeness. 

>Chinese Remainder Theorem<br>
Let $R$ be a ring, and $I_1,\dots,I_n$ be a collection of pairwise coprime two-sided ideals (i.e. $I_i+I_j=R$ for all $i\neq j$). Then, we have a ring isomorphism 
<center>$$\Large\begin{matrix}
\frac R{I_1\cap I_2\cap\dots\cap I_n} &\longrightarrow& \frac R{I_1}\oplus\frac R{I_2}\oplus\dots\oplus\frac R{I_n}\\
r+I_1\cap I_2\cap\dots\cap I_n &\longmapsto& \left(r+I_1,r+I_2,\dots,r+I_n\right)
\end{matrix}$$</center>

<div class="proof2">
Pf: We will prove this by induction on $n$, starting with the case of two ideals and the map $\phi:(r+I_1\cap I_2)\mapsto(r+I_1,r+I_2)$. We first need to confirm that this map is well-defined. Pick some $r,s\in R$ in the same coset so $r-s\in I_1\cap I_2$. Practically by definition, this means that $r+I_1=s+I_1$ and $r+I_2=s+I_2$ so $\phi$ is well-defined. From the behavior of cosets, it's clear that $\phi$ is a homomorphism so we only need to verify injectivity and surjectivity. Now, pick some $r+I_1\cap I_2\in\ker\phi$ so $r\in I_1\cap I_2$. Then, $\phi(r)=(r+I_1,r+I_2)=(I_1,I_2)$ is the identity so $\phi$ has trivial kernel which only leaves surjectivity. Fix some $x\in I_1$ and $y\in I_2$ such that $x+y=1$ which we get from coprimality. Then, $(r+I_1,s+I_2)$ has $sx+ry$ as a preimage, so $\phi$ is surjective. Now that we've established the case of two ideals, the general case will follow if we can show that $I_1$ and $I_2\cap\dots\cap I_n$ are coprime. To this end, for each $2\le j\le n$ pick $x_j\in I_1$ and $y_j\in I_j$ s.t. $x_j+y_j=1$. Then, <center>$$1=(x_2+y_2)(x_3+y_3)\dots(x_n+y_n)=\sum_{S\subseteq\{2,\dots,n\}}\left(\prod_{i\in S}x_i\right)\left(\prod_{j\not\in S}y_j\right)=X+\left(\prod_{j=2}^ny_j\right)$$</center>
where $X\in I_1$ is some linear combination of terms that contain $x_i$ for some $i\in\{2,\dots,k\}$ and $\prod y_j\in I_2\cap\dots\cap I_n$. Thus, $1\in I_1+(I_2\cap\dots\cap I_n)$ so $I_1+(I_2\cap\dots\cap I_n)=R$ which means these ideals are coprime as claimed. $\square$
</div>

>Corollary<br>
Fix an integer $m$ and factor it as $m=p_1^{r_1}p_2^{r_2}\dots p_n^{r_n}$ where each $p_i$ is a different prime. Then, <center>$\zmod m\simeq\zmod{p_1^{r_1}}\oplus\zmod{p_2^{r_2}}\oplus\dots\oplus\zmod{p_n^{r_n}}$</center>

<div class="proof2">
Pf: Exercise to reader
</div>

For our purposes, we only need the corollary and not the full CRT. We want to confirm that $x^2-82y^2=2$ has solutions (mod $m$) for all $m$. Well, given any $m$, we factor it into prime powers to see that $\zmod m\simeq\zmod{p_1^{r_1}}\oplus\zmod{p_2^{r_2}}\oplus\dots\oplus\zmod{p_n^{r_n}}$. In the previous section, we found solutions in each of these factors so let $(x_j,y_j)$ satisfy $x_j^2-82y_j^2\equiv2\pmod{p_j^{r_j}}$. Then, CRT guarantees the existence of some $$x^*,y^*\in\zmod m$$ such that $$x^*\equiv x_j\pmod{p_j^{r_j}}$$ and $$y^*\equiv y_j\pmod{p_j^{r_j}}$$ for all $j$. Thus, $$(x^*)^2-82(y^*)^2\equiv2\pmod{p_j^{r_j}}$$ for all $j$. Since $$(x^*,y^*)$$ satisfy $q(x,y)$ in each factor of $\zmod m$ (i.e. in each $\zmod{p_j^{r_j}}$), they must satisfy it in $\zmod m$ itself, so $q(x,y)$ does indeed have solutions modulo any integer.

# No Solutions in $\Z$
To finish things off, we'll show that there are no integer solutions to $x^2-82y^2=2$. This section will use some of the ideas previously touched upon in my [pell's post](../solving-pell). Our first observation is that the right setting to analyze this equation is in $\zadjs{82}$, which, using terminology from that pell's post, is the ring of integers for $K=\qadjs{82}$. We see that solutions to this equation correspond exactly to elements of $\zadj{82}$ with norm $2$. As it turns out, understanding which numbers have norm $2$ is related to understanding how $2$ factors in $\ints K=\zadj{82}$. More specifically, we wish to factor $(2)$ into prime ideals:

$$(2)=(2,\sqrt{82})^2$$

This equality is easily verified as $(2,\sqrt{82})^2=(4,2\sqrt{82},82)=(2)(2,\sqrt{82},41)=(2)$ since $(2,\sqrt{82},41)=(1)$ as $41-2(20)=1$. Now, suppose $z=x+y\sqrt{82}$ ($x,y\in\Z$) has norm 2. i.e. assume that $=x^2-82y^2=2$. It is a fact that I will not prove that this is possible only if $(x+y\sqrt{82})=(2,\sqrt{82})$. Given this, we see that $(z^2)=(z)^2=(2)$ so $z^2=2u$ for some unit $u\in\ints K^\times$. Taking norms of both sides gives

$$4\knorm(u)=\knorm(2)\knorm(u)=\knorm(2u)=\knorm(z^2)=\knorm(z)^2=4\implies\knorm(u)=1$$

Now, note that $\zadj{82}$ has fundamental unit $$\eps=9+\sqrt{82}$$ and that $$\knorm(\eps)=-1$$. Since every unit is $\pm$ a power of $\eps$, this means we can write $u=\pm\eps^{2k}$ for some $k$. Thus, we can rewrite $z^2=2u$ as $(\eps^{-k}z)^2=\pm2$. To finish things off, we will show that neither of $\pm2$ is a square in $\ints K$, giving a contradiction. This is easily seen by observing that given any $a,b\in\Z$, we have

$$(a+b\sqrt{82})^2=(a^2+82b^2)+2ab\sqrt{82}$$

This can't be $-2$ because the non-$\sqrt{82}$ is always positive, and it can't be $+2$ since that would require $b=0$ and $2$ is not a square in the normal integers. Thus, $\pm2$ are no squres in $\ints K$ so there's no element of norm $2$ which means that $x^2-82y^2=2$ has no integer solutions.

# Further Work
So we've shown that $x^2-82y^2=2$ has infinitely many rational solutions, and solutions in $\zmod m$ for all $m$, but no integer solutions. This means congruential obstructions are not the only things that can prevent a polynomial from being solved in the integers. We might still be interested in asking questions about better understanding congruential obstructions though. For example, in our analysis of this equation, the fact that we has solutions in $\zmod m$ for all $m$ was very related to the fact that we had (infinitely) many rational solutions, which begs the question

>Conjecture<br>
Let $p$ be a polynomial with integer coefficients. Then, $p$ has solutions in $\zmod m$ for all $m\iff p$ has infinitely many rational solutions.

It actually turns out that this conjecture if false, and one counterexample is the polynomial

$$p(x) = (x^2-2)(x^2-17)(x^2-34)$$

This has solutions (mod $m$) for all $m$ [^4], but there are visibly no rational solutions. This breaks one direction of the iff above, but it's still possible that the other direction holds, and I encourage you to investigate this.

[^1]: Just try all 16 possible pairs of values for x,y
[^2]: [hint](../number-theory)
[^3]: I used the (10/3,1/3) solution to project the line y=0 onto the curve defined by x^2-82y^2=2. Under this projection/correspondence, the point (4,0) on this line gets mapped to (66/13,-7/13) on this curve
[^4]: The easiest way to convince yourself of this claim is via [quadratic reciprocity](https://www.wikiwand.com/en/Quadratic_reciprocity)