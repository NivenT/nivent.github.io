---
layout: post
title: "Absolute Values and p-adics"
modified:
categories: blog
excerpt:
tags: [math, p-adic, absolute value]
date: 2018-09-19
---

A potentially better title for this post might be "A Brief Introduction to Local Fields." In it, I plan to introduce absolute values, proving some surprising facts about non-archimedean absolute values, and ending with a characterization of so-called local fields in characteristic 0. I'll try to focus more on topological/analytic aspects [^5], so this post will be less algebraic than most of my others.

# Absolute Values
<div class="definition">
    Let $D$ be an integral domain. An <b>absolute value</b> $\nabs:D\to\R_{\ge0}$ is a function satisfying
    <ol>
        <li> $\abs x=0\iff x=0$ </li>
        <li> $\abs{xy}=\abs x\abs y$ </li>
        <li> $\abs{x+y}\le\abs x+\abs y$ </li>
    </ol>
    3. above is called the <b>triangle inequality</b>.
</div>
<div class="remark">
    What I called an absolute value is sometimes instead called a "norm," and an "absolute value" is usually then a function satisfying 1. and 2., but 3. is replaced by the condition that $\abs{x+y}\le c\max(\abs x,\abs y)$ for some $c\ge1$.
</div>

Absolute values gives us a way of measuring the size of elements of our ring. While I defined the notion for general integral domains, we usually only consider absolute values on fields. In fact, for $D$ a domain with fraction field $F$, any absolute value $\nabs:D\to\R_{\ge0}$ extends to one on $F$ via

$$\abs{\frac xy}=\frac{\abs x}{\abs y}$$

This is easily checked to satisfy 1., 2., and 3. In addition, there are other immediate properties of absolute values.
<div class="proposition">
    Let $\nabs:D\to\R_{\ge0}$ be an absolute value. Then,
    <ul>
        <li> $\abs{\pm1}=1$. More generally, $\abs\zeta=1$ whenever $\zeta\in D$ is a root of unity. </li>
        <li> $\abs n\le n$ for all $n\in\Z_{\ge0}$ </li>
    </ul>
</div>

So, what should we keep in mind as our goto examples of absolute values? Well, one obvious choice is the normal absolute value on $\Q$ where $\|x\|=x$ if $x\ge0$ and $\|x\|=-x$ otherwise. We will denote this absolute value by $\nabs_\infty:\Q\to\R_{\ge0}$. In addition to this, there is always a trivial absolute value where $\|x\|=1$ for all $x\in D$. Both of these examples are kinda boring [^9], so another good one is

<div class="example">
    Fix a prime $p$. The <b>$p$-adic absolute value</b> $\nabs_p:\Q\to\R$ is given by
    $$\abs{\frac xy}_p=\frac1{p^{v_p(x)-v_p(y)}}$$
    when $x,y\neq0$ (where $v_p(x)$ is the exponent of the largest power of $p$ dividing $x$), and $\abs0_p=0$.
</div>

For example, when $p=3$, we have $\abs{75/19}_ 3=1/3$ since $3\nmid19$ and $3\mid75$ but $9\nmid75$. This may seem like a weird way to measure size at first, but if you stop and think about it, this is saying, for example, that $n\in\Z$ is really small whenever its divisible by a large power of $p$; in other words, if we can write $n\equiv0\pmod{p^e}$ for $e$ large, then $n$ is small. In essence, this absolute value gives us an analytic way to study congruence relations. Speaking of analysis, absolute values turn rings into metric spaces.

<div class="definition">
    Fix a set $X$. A function $d:X\by X\to\R_{\ge0}$ is called a <b>metric</b> if it satisfies
    <ol>
        <li> $d(x,y)=0\iff x=y$ </li>
        <li> $d(x,y)=d(y,x)$ </li>
        <li> $d(x,y)+d(y,z)\ge d(x,z)$ </li>
    </ol>
    When $d$ is a metric, the pair $(X,d)$ is called a <b>metric space</b>.
</div>
<div class="theorem">
    Let $\nabs:D\to\R_{\ge0}$ be an absolute value. Then, we can define a metric $d:D\by D\to\R_{\ge0}$ on $D$ via
    $$d(x,y)=\abs{x-y}$$
</div>
<div class="proof4">
    First, 
    $$d(x,y)=0\iff\abs{x-y}=0\iff x-y=0\iff x=y$$ 
    For 2.,
    $$d(x,y)=|x-y|=|-1||x-y|=|y-x|=d(y,x)$$
    Finally,
    $$d(x,y)+d(y,z)=|x-y|+|y-z|\ge|(x-y)+(y-z)|=|x-z|=d(x,z)$$
    so we win.
</div>
<div class="remark">
    Just a reminder: in the $p$-adic metric on $\Z$, two integers $x,y$ are close (i.e. $d(x,y)$ is small) whenever $x\equiv y\pmod{p^e}$ for $e$ large.
</div>

Having a metric is great for many reasons; one of them is that a metric induces the metric topology [^1]. Given a metric space $(X,d)$, the metric topology has a basis consisting of open balls $B(x,r)=\brackets{y\in X\mid d(x,y)< r}$. Our primary application of this induced topology is the following definition.

<div class="exercise">
    Let $(X,d)$ be a metric space. Show that the (closed) ball $\bar B(x,r)=\brackets{y\in X:d(x,y)\le r}$ is a closed subset of $X$ (i.e. its complement is a union of open balls)
</div>
{::options parse_block_html="true" /}
<span class="exercise">
    Let $\nabs:D\to\R_{\ge0}$ be an absolute value on a domain $D$. Given $D$ the topology induced by $\nabs$. Prove that $\nabs$ is a continuous function to $\R_{\ge0}$ with the Euclidean topology. [^2]
</span>

{::options parse_block_html="false" /}
<div class="definition">
    Let $\nabs,\nabs':D\to\R_{\ge0}$ be two absolute values on a domain $D$. We say that they are <b>equivalent</b>, denote $\nabs\sim\nabs'$ if the topologies they induce on $D$ coincide. i.e. they are not just homeomorphic, but are literally the same as sets.
</div>
<div class="theorem">
    Let $\nabs,\nabs':F\to\R_{\ge0}$ be two absolute values on a field $F$. Then, they are equivalent if and only if there exists some $t>0$ s.t. $\nabs^t=\nabs'$.
</div>
<div class="proof4">
    $(\impliedby)$ It suffices to show that every open ball of one is an oben ball of the other and vice versa. This is the case since
    $$B(x,r)=\brackets{y\in F:|x-y|< r}=\brackets{y\in F:|x-y|'< r^t}=B'(x,r^t)$$

    $(\implies)$ Note that while every open subset of $F$ w.r.t $\nabs$ is open w.r.t $\nabs'$, a priori not every open ball w.r.t $\nabs$ is an open ball w.r.t $\nabs'$. We will first show that $\abs x<1\iff\abs x'<1$. Fix $x\in F$ s.t. $\abs x<1$. Then, $\lim|x^n|=0$, so every open set $U\subset F$ containing $0$ contains a tail of (the primage of) this sequence (e.g. $\exists N\ge1$ such that $n\ge N\implies x^n\in U$). However, $\nabs,\nabs'$ share the same open sets, so we get that $\lim x^n=0\in F$ in the $\nabs'$ topology as well. By continuity of $\nabs'$, this means that $\lim\abs{x^n}'=0$ so clearly $\abs{x}'<1$. By considering inverses, we immediately get $\abs x>1\iff\abs x'>1$ as well. Similarly, we have $\abs x=1\iff\abs x'=1$. To finish, for any $x\in F$ with $\abs x>1$, let
    $$t(x)=\frac{\log{\abs x'}}{\log{\abs x}}$$
    By construction, $\abs x^{t(x)}=\abs x'$. We claim that $t(x)=t(y)$ for all $x,y\in F$ with $\abs x,\abs y>1$. Suppose otherwise. Fix such $x,y$ with $t(x)\neq t(y)$. We can find $m,n\in\Z$ such that
    $$\frac{\log{\abs x'}}{\log{\abs y'}}<\frac mn<\frac{\log{\abs x}}{\log{\abs y}}$$
    where $m,n\in\Z$. However, this implies that
    $$\abs{\frac{x^n}{y^m}}'<1\text{ and }\abs{\frac{x^n}{y^m}}>1$$
    which is impossible. Thus, $t=t(x)$ is independent of $x$. For $0<|x|<1$, we have
    $$\frac1{\abs x^t}=\abs{\frac1x}^t=\abs{\frac1x}'=\frac1{\abs x'}\implies\abs x^t=\abs x'$$
    so the claim holds.
</div>
<div class="definition">
    A <b>place</b> on a field $F$ is an equivalence class of absolute values on $F$.
</div>

The point of the above definition is that we shouldn't focus on individual absolute values, but instead on places. With that said, what types of properties (of absolute values) are well-defined on places? Perhaps unsurprisingly, one of the most important such properties is Archimedeaness.

<div class="definition">
    Let $\nabs:D\to\R_{\ge0}$ be an absolute value (i.e. a representative of a place). Then, we say $\nabs$ is <b>archimedean</b> if $\abs{\Z}\subset\R$ is unbounded, and we call it <b>non-archimedean</b> otherwise.
</div>
<div class="theorem">
    An absolute value $\nabs:D\to\R_{\ge0}$ is non-archimedean if and only if it satisfies the <b>ultrametric inequality</b>: $\abs{x+y}\le\max(\abs x,\abs y)$.
</div>
<div class="proof4">
    $(\impliedby)$ this direction is obvious.<br>
    $(\implies)$ Let $\nabs$ be a non-archimedean absolute value on a domain $D$. Fix $C\in\Z$ large enough so that $\abs n< C$ for all $n\in\Z$. Then, for any $n\in\Z$, we have
    $$\begin{align*}
        \abs{x+y}^n &=\abs{\sum_{k=0}^n\binom nkx^ky^{n-k}}\\
        &\le\sum_{k=0}^nC\max(\abs x,\abs y)^n\\
        &= nC\max(\abs x,\abs y)^n\\
        \abs{x+y} &\le (nC)^{1/n}\max(\abs x,\abs y)
    \end{align*}$$
    The bottom inequality holds for all $n$, so taking the limit as $n\to\infty$ gives the desired result.
</div>
<div class="corollary">
    In a non-archimedean absolute value, $\abs n\le1$ for all $n\in\Z$.
</div>
<div class="exercise">
    Prove that two equivalent absolute values are either both archimedean or both not.
</div>
<div class="example">
    The Euclidean absolute value $\nabs_\infty:\Q\to\R$ is archimedean, while the $p$-adic absolute values $\nabs_p:\Q\to\R$ are not.
</div>

# Non-Archimedean Geometry
In this section, we'll explore some properties of non-archimedean places. We will see that, in some ways, non-archimedean places are much nicer than their archimedean counterparts. Throughout the section, fix a field $F$ with a non-archimedean place represented by $\nabs:F\to\R_{\ge0}$.

<div class="theorem">
    Every triangle in $F$ is isosceles.
</div>
<div class="proof4">
    Consider a triangle with points at $0,x,y\in F$. It has side lengths $\abs x,\abs y,\abs{x-y}$. Our goal is to show that two of these are equal. Suppose that $\abs x>\abs y$. We claim that, in this case, $\abs x=\abs{x-y}$. This is because
    $$\abs x=\abs{(x-y)+y}\le\max\parens{\abs{x-y},\abs y}\implies\abs x\le\abs{x-y}$$
    where the implication comes from the assumption that $\abs x>\abs y$. Furthermore,
    $$\abs{x-y}\le\max\parens{\abs x,\abs y}=\abs x$$
    so we have $\abs x=\abs{x-y}$ as claimed.
</div>
If you look at the proof, we actually proved something slightly stronger. Not only is every triangle isosceles, but its always the longest side length that appears (at least) twice.
<div class="theorem">
    Every point of a circle in $F$ is the center.
</div>
<div class="proof4">
    Consider a circle $B=B(x,r)\subset F$, and fix any $y\in B$. Our goal is to show that $B(x,r)=B(y,r)$. For any $z\in F$ with $\abs{x-z}< r$, we have
    $$\abs{y-z}=\abs{(y-x)+(x-z)}\le\max(\abs{y-x},\abs{x-z})< r$$
    so $z\in B(y,r)$. Since $x\in B(y,r)$, by symmetry this shows that $B(x,r)=B(y,r)$.
</div>
<div class="corollary">
    The (closed) ball $\bar B(x,r)=\brackets{y\in F:\abs{x-y}\le r}$ is open.
</div>
<div class="proof4">
    For any $y\in\bar B(x,r)$, we have $B(y,r)=B(x,r)\subset\bar B(x,r)$.
</div>
However, not everything is better in non-archimedean land. Non-archimedean fields have weird topological properties.
<div class="theorem">
    The topology on $F$ is totally disconnected. i.e. the only connected nonempty sets are points.
</div>
<div class="proof4">
    Let $C\subset F$ be a set with two distinct points $x,y\in C$. Fix some $0 < r < \abs{x-y}$ and write
    $$C=\parens{C\cap\brackets{z\in F:\abs{x-z}\le r}}\sqcup\parens{C\cap\brackets{z\in F:\abs{x-z}>r}}$$
    as the union of two nonempty open (in $C$) sets. This means that $C$ is not connected.
</div>
For the last theorem, I'll need to introduce the notion of a complete metric space. This is a metric space "without any holes." The idea is that any sequence that looks like it should have a limit [^3] actually does have a limit.
<div class="definition">
    Let $(X,d)$ be a metric space. A sequence $\brackets{a_n}\subset X$ in $X$ is called <b>Cauchy</b> if for any $\eps>0$, there exists some $N\in\N$ such that
    $$d(a_n,a_m)<\eps$$
    whenever $n,m\ge N$. 
</div>
<div class="exercise">
    Show that any convergent sequence is Cauchy.
</div>
<div class="example">
    Consider the sequence $(3,3.1,3.14,3.141,3.1415,\dots)$ consisting of truncations of the digits of $\pi$. As a sequence in $\Q$, it is Cauchy but not convergent. 
</div>
<div class="definition">
    A metric space $(X,d)$ is called <b>complete</b> if every Cauchy sequence converges.
</div>
Cauchy sequences look like they should converge; in the tail of the sequence, there's barely any difference between one term and the next so you would expect that it eventually converges to some point. As the example above shows, this isn't true in general, so complete spaces are extra nice. In particular, complete spaces coming from a non-Archimedean norm has a very simple criterion for convergence. 
<div class="lemma">
    $\abs{x+y}\ge\abs{x}-\abs{y}$
</div>
<div class="proof4">
    $\abs x=\abs{(x+y)-y}\le\abs{x+y}+\abs y$
</div>
<div class="theorem">
    Assume that $F$ is complete as a metric space with the metric induced by $\nabs$. Let $\brackets{a_n}_{n\ge1}\subset F$ be a sequence in $F$. Then,
    $$\sum_{n\ge1}a_n\text{ converges}\iff\lim\abs{a_n}=0$$
</div>
<div class="proof4">
    $(\implies)$ Assume that $\sum_{n\ge1}a_n=L$. Then, for any $\eps>0$, there's some $N_{\eps}$ such that $\abs{\sum_{n\ge k}a_n}=\abs{L-\sum_{n=1}^ka_n}<\eps$ whenever $k\ge N_{\eps}$. Now, suppose that $\lim\abs{a_n}\neq0$, so there exists some $\delta>0$ such $\abs{a_n}>\delta$ infinitely often. Now, fix some $k\ge N_{\frac\delta2}$ such that $\abs{a_k}>\delta$. Then, $\abs{\sum_{n\ge k}a_n},\abs{\sum_{n>k}a_n}<\frac\delta2$, but
    $$\abs{\sum_{n\ge k}a_n}\ge\abs{a_k}-\abs{\sum_{n>k}a_n}>\delta-\frac\delta2=\frac\delta2$$
    where the first inequality above comes from the lemma. This is a contradiction, so we win.<br>

    $(\impliedby)$ Now, assume instead that $\lim\abs{a_n}=0$, and let $S_n=\sum_{k=1}^na_k$ denote the $n$th partial sum. We will show that the sequence $S_n$ is Cauchy. This is because, assuming WLOG that $n\ge m$,
    $$\abs{S_n-S_m}=\abs{\sum_{k=m+1}^na_k}\le\max\parens{\abs{a_{m+1}},\dots,\abs{a_n}}\longrightarrow0$$
    Hence, in the tail of the sequence (of paritial sums), the terms become arbitarily close together, so the sequence is Cauchy. This gives the claim. 
</div>
<div class="remark">
    I'm not that strong in analysis, so there's probably a better proof of the $\implies$ direction than what I was able to come up with.
</div>
Compared to the mess of convergence tests for series in $\R$, this is quite nice. However, the question still remains: where do these complete fields come from?

# Constructing Complete Fields
In this section, we will give the idea behind the construction of complete fields such as $\Q_p$, the $p$-adic numbers. After that, we will show one way of writing down elements of $\Q_p$.
<div class="theorem">
    Let $\nabs:F\to\R_{\ge0}$ be an absolute value on a field $F$. Then there exists an isometry $\iota:F\to\wh F$ into a field $\wh F$ complete with respect to an absolute value $\wh\nabs:\wh F\to\R_{\ge0}$ such that any isometry $\iota':F\to K$ into a complete field factors through $\iota$. Furthermore, $\iota(F)\subset\wh F$ is dense, and $\wh F$ is unique upto (unique) isomorphism.
</div>
The idea is to construct $\wh F$ as the set of Cauchy sequences $\brackets{a_n}$ in $F$ modulo the relation $\brackets{a_n}\sim\brackets{b_n}\iff\lim\abs{a_n-b_n}=0$. You then define multiplication, addition, subtraction, and division in the obvious ways [^4], and endow it with the absolute value

$$\abs{\brackets{a_n}}'=\lim\abs{a_n}$$

<div class="definition">
    The field $\wh F$ in the above theorem is called the <b>completion</b> of $F$ w.r.t $\nabs$.
</div>
<div class="remark">
    You can use this theorem to construct $\R$ from $\Q$ via $\nabs_\infty$, but you cannot use this theorem to define $\R$. That is because this theorem (and even the notion of an absolute value) relies on preexisting construction of $\R$.
</div>
We can, however, use this theorem to define the <b>$p$-adic numbers</b> $\Q_p$ which are the completion of $\Q$ with respect to the $p$-adic absolute value $\nabs_p$. We still use $\nabs_p$ to denote its extention to an absolute value on $\Q_p$.

The rest of this section will be devoted to constructing a canonical choice of representatives of elements of $\Q_p$. We first make the observation that passing from $\Q$ to $\Q_p$ does not change the image of $\nabs_p$. Formally,
<div class="theorem">
    Let $\brackets{a_n}\subset\Q$ be Cauchy. Then, the sequence $\abs{a_n}_p$ is eventually constant or $\lim a_n=0$.
</div> 
<div class="proof4">
    Suppose that $\lim a_n\neq0$, so there exists some $\eps>0$ such that $\abs{a_n}_p>\eps$ infinitely often. Furthermore, there is some $N\in\N$ such that
    $$\abs{a_n-a_m}_p<\eps$$
    whenever $n,m\ge N$. Fix an index $n\ge N$ such that $\abs{a_n}>\eps$. Then, for any $m\ge n$, because all triangles are isosceles (with largest side length appearing twice) and $\abs{a_n-a_m}_p<\eps$, we get that $\abs{a_n}_p=\abs{a_m}_p$, showing that $\abs{a_n}_p$ is eventually constant.
</div>
<div class="corollary">
    $\abs{\Q_p}_p=\abs{\Q_p}$. That is, for all $x\in\Q_p$, $\abs x_p=p^n$ for some $n\in\Z$.
</div>
<div class="remark">
    The above theorem (and corollary) hold anytime you complete a field with respect to a non-archimedean absolute value. Passing to the completion does not affect the set of possible absolute values. This is in contrast to, for example, the archimedean place $\nabs_\infty$ on $\Q$ since $\R$ has more possible absolute values than $\Q$.
</div>
This fact will allow us to simply things slightly by shifting focus from $\Q_p$ to $\Z_p$ without losing too much information.
<div class="definition">
    For a prime $p$, the <b>$p$-adic integers</b> form the ring
    $$\Z_p:=\brackets{q\in\Q_p:\abs q_p\le 1}$$
</div>
<div class="remark">
    $\Z_p\sqbracks{\frac1p}=\Q_p$. Given some $q\in\Q_p$, we can write $\abs{q}_p=p^n$ for some $n\in\Z$. If $n\le0$, then $\abs{p^nq}_p=1$, so $a:=p^nq\in\Z_p$, and we can write
    $$q=\frac a{p^n}\in\Z_p\sqbracks{\frac1p}$$ 
</div>
The above remark is what I meant by not losing too much information; you only have to invert a single element to get from $\Z_p$ to $\Q_p$. Now, our goal is to show that

$$\Z_p=\brackets{\sum_{k\ge0}a_kp^k:0\le a_k< p}$$

Since $\abs{a_kp^k}_ p=\abs{p^k}_ p\to0$, we know that any such series converges, so we need to show that every element of $\Z_p$ admits such a series representation. I'll leave it as an exercise to show that these representations are unique. We'll call a sum of the above form a <b>power series representation</b> of $x\in\Z_p$.

To do this [^6], we'll need to do some algebra. First, note that $p\Z_p=\brackets{n\in\Z_p:\abs n_p<1}=\Z_p\sm\units\Z_p$ is the unique maximal ideal of $\Z_p$. Furthermore, given some $x=\sum_{k\ge0}a_kp^k$, we can look at it $\bmod{p^n}$ to get the approximation $\sum_{k=0}^{n-1}a_kp^k$ which is just some integer in the set $\{0,1,\dots,p^n-1\}$. By making successive approximations like this, we can obtain power series representations for any element of $\Z_p$. To make this idea formal, we first need... [^7]

<div class="theorem">
    Fix a positive integer $n\in\N$. Then, $\Z_p/p^n\Z_p\simeq\Z/p^n\Z$.
</div>
<div class="proof4">
    We will actually show instead that $\Z_p/p^n\Z_p\simeq\Z_{(p)}/p^n\Z_{(p)}$. We leave it as an exercise to the reader to show that $\Z_{(p)}/p^n\Z_{(p)}\simeq\zmod{p^n}$.<br>
    Note that $\Z_{(p)}=\brackets{q\in\Q:\abs q_p\le1}$. Furthermore, $\Z_{(p)}\hookrightarrow\Z_p$ and $p^n\Z_{(p)}\hookrightarrow p^n\Z_p$, so this inclusion descends to a map $f:\Z_{(p)}/p^n\Z_{(p)}\to\Z_p/p^n\Z_p$ which we claim is an isomorphism. Injectivity of $f$ is equivalent to the statement $p^n\Z_p\cap\Z_{(p)}=p^n\Z_{(p)}$. To show this, consider some $x\in p^n\Z_p\cap\Z_{(p)}$ so $\log_p\abs x_p\le-n$. Write $x=a/s$ where $p\nmid s$, so $\abs x_p=p^{-v_p(a)}$. Hence, $v_p(a)\ge n$ which is precisely the statement that $x\in p^n\Z_{(p)}$. Hence $f$ is injective. <br>
    For surjectivity, fix any $y\in\Z_p$. We will constuct an $x\in\Z_{(p)}$ such that $x\equiv y\pmod{p^n\Z_p}$. Recall that $\Q$ is a dense subset of $\Z_p$, so we can choose some $q\in\Q$ with $\abs{q-y}_p< p^{-n}$. Note that
    $$\abs x_p\le\max(\abs{q-y}_p,\abs y_p)\le1$$
    so $x\in\Z_{(p)}$. Furthermore, since $\Z_p=\brackets{\nabs_p\le1}$, we have $p^n\Z_p=\brackets{\nabs_p\le\abs{p^n}_p}=\brackets{\nabs_p\le p^{-n}}$, so $x-y\in p^n\Z_p$. Thus, $x\equiv y\pmod{p^n\Z_p}$, proving surjectivity.
</div>
<div class="theorem">
    Every element of $\Z_p$ has a power series representation.
</div>
<div class="proof4">
    Fix some $x\in\Z_p$. We will inductively define the $\{a_n\}_{n\ge0}$ so that
    $$x=\sum_{n\ge0}a_np^n$$
    First, $a_0$ is the unique integer $0\le a_0< p$ such that $x\equiv a_0\pmod p$. Now, suppose we have defined $a_0,\dots,a_k\in\brackets{0,\dots,p-1}$ such that
    $$x\equiv\sum_{n=0}^ka_np^n\pmod{p^{k+1}}$$
    We want to define $a_{k+1}$. Then, let
    $$x'=\frac1{p^{k+1}}\sqbracks{x-\sum_{n=0}^ka_np^n}\in\Z_p$$
    Define $a_{k+1}$ to be the unique element of $\{0,\dots,p-1\}$ such that $x'\equiv a_{k+1}\pmod p$. Then,
    $$\sum_{n=0}^{k+1}a_np^n\equiv\sum_{n=0}^ka_np^n+a_{k+1}p^{k+1}\equiv\sum_{n=0}^ka_np^n+x'p^{k+1}\equiv x\pmod{p^{k+2}}$$
    so the theorem follows by induction.
</div>
Since $\Q_p=\Z_p[1/p]$, as a corollary, we get that any $x\in\Q_p$ can be written

$$x=\sum_{n\ge-m}a_np^n\text{ where }0\le a_n< p\text{ and }m\in\Z$$

<div class="remark">
    Since I didn't give all of the details of constructing completions in general. One could take the above as the definition of $\Q_p$ (i.e. as a set (or even a multiplicative monoid) $\Q_p\simeq\Q((p))$, the field of Laurent series in $p$). You would need to give formulas for addition and multiplication, and also say that
    $$\abs{\sum_{n\ge-m}a_np^n}_p=p^m\text{ if }a_{-m}\neq0$$
    This would be very ad hoc so one shouldn't do this, but one could.
</div>
Note that, since the coefficients $a_n$ are all that matter in writing down an element of $\Q_p$, we can take a cue from how we usually write real numbers and define the notation

$$\sqbracks{\dots a_2a_1a_0.a_{-1}a_{-2}\dots a_{-m}}_p:=\sum_{n\ge-m}a_np^n\in\Q_p$$

where the square brackets are unneeded when writing actual digits instead of $a_n$. Note that a $p$-adic expansions can be infinite to the left and must be finite to the right; this is the reverse of decimal expansions in $\R$.
<div class="example">
    For concreteness, let's write down some $p$-adic numbers.
    <ul>
        <li> $-1\in\Q_2$
            $$\begin{align*}
                -1 &= 1+1(2)+1(2)^2+1(2)^3+1(2)^4+\dots\\
                &= \dots11111_2
            \end{align*}$$
        </li>
        <li> $\sqrt{-1}\in\Q_5$
            $$\begin{align*}
                \sqrt{-1} &= 2+1(5)+2(5)^2+1(5)^3+3(5)^4\\
                &= \dots31212_5
            \end{align*}$$
        </li>
        <li> $\sqrt 2\in\Q_7$
            $$\begin{align*}
                \sqrt 2 &= 3+1(7)+2(7)^2+6(7)^3+1(7)^4+\dots\\
                &= \dots16213_7
            \end{align*}$$
        </li>
    </ul>
</div>
I might explain how to calculate these expansions in a future post. For now, if you're curious, look up [Hensel's lemma](https://www.wikiwand.com/en/Hensel%27s_lemma).

# Ostrowski's Theorem
To end, I'll prove a theorem due to Ostrowski and state (but not prove) the characterization of so-called local fields in characterisitc 0. Ostrowski's theorem states that the only completions of $\Q$ are the real numbers $\R$ and the $p$-adic numbers $\Q_p$.

<div class="theorem" name="Ostrowski">
    Let $\nabs:\Q\to\R_{\ge0}$ be a nontrivial absolute value. Then, $\nabs\sim\nabs_\infty$ or $\nabs\sim\nabs_p$ for some prime $p$.
</div>
<div class="proof4">
    We'll start with the non-Archimedean case. Suppose that $\nabs n\le1$ for all integers $n\in\Z$. Fix a positive integer $n$ with $\abs n< 1$ and factor
    $$n=\prod_{k=1}^gp_k^{e_k}$$
    for some finite set of primes $\{p_k\}$. Clearly $\abs{p_k}< 1$ for some prime dividing $n$. We claim this is the case for exactly one prime. Suppose that $p,q$ are both primes with absolute value (strictly) less than 1. Well, fix exponents $e,f$ such that $\abs p^e,\abs q^f<\frac12$. Since they are coprime, we can find $x,y\in\Z$ such that $xp^e+yq^f=1$. However,
    $$1=\abs1=\abs{xp^3+yq^f}\le\abs{p^e}+\abs{q^f}< 1$$
    a contradiction. Hence, only one prime $p$ has absolute value less than one. Thus, in general, $\abs n=\abs p^{v_p(n)}$. Letting $t=-\frac{\log\abs p}{\log p}$, we see that $\nabs=\nabs_p^t$.<br>

    Now for the Archimedean case. Suppose that $\abs{\Z}$ is unbounded. Let $a,b$ and $n$ be natural numbers with $a,b>1$. Write $b^n$ in base $a$
    $$b^n=\sum_{k=0}^mc_ka^k\text{ where }c_k\in\{0,\dots,a-1\}$$
    and $m\le n\log_ba+1$. Then,
    $$\abs b^n\le am\max\parens{\abs a^{m-1},1}\le a(n\log_ab+1)\max\parens{\abs a^{n\log_ab},1}$$
    Since this holds for all $n$, taking the $n$th root and the limit as $n\to\infty$ shows that
    $$\abs b\le\max\parens{\abs a^{\log_ab},1}$$
    Note that if $\abs b>1$, then $\abs a>1$ since otherwise we would have $\abs b\le1$. Thus, for any choice of $a,b>1$ we get $\abs b\le\abs a^{\log_ab}$. In other words,
    $$\frac{\log\abs b}{\log b}\le\frac{\log\abs a}{\log a}$$
    By symmetry, this is actually an equality, so there's some constant $t\in\R$ such that $\log\abs n=\lambda\log n$ for all $n\in\Z$. This means that $\abs n=n^\lambda=\abs n_\infty^\lambda$, so we win.
</div>
So, despite the fact that we're more accustomed to the Archimedean place $\nabs_\infty$ on $\Q$, the typical place on $\Q$ is non-Archimedean. With that said, what's a local field?

<div class="definition">
    A <b>local field</b> is a field $F$ complete with respect to a nontrival absolute value $\nabs:F\to\R_{\ge0}$ such that the resulting topology is locally compact.
</div>
<div class="theorem">
    Let $F$ be a local field and assume that $\Char(F)=0$. Then, $F$ is isomorphic (as a topological field) to one of the following:
    <ul>
        <li> The real numbers $\R$ </li>
        <li> The complex numbers $\C$ </li>
        <li> A finite extension of the $p$-adics $\Q_p$ for some prime $p$. </li>
    </ul>
</div>
The idea behind the proof is that $\Q\subset F$ since $F$ has characterisitc zero. Then, $\nabs$ restricts to an absolute value on $\Q$, so by Ostrowski it is either $\nabs_\infty$ or $\nabs_p$ for some prime $p$. Since $F$ is complete, it then must contain either $\R$ or $\Q_p$. After this, you need to show that $F/\R$ (or $F/\Q_p$) is a finite extension. 

The actual last thing I'll do is mention another definition of local fields in the non-Archimedean case.
<div class="definition">
    We say an absolute value $\nabs:F\to\R_{\ge0}$ is <b>discretely-valued</b> if $\abs F\subset\R$ is a discrete subgroup.
</div>
For example, $\nabs_p$ is discretely valued for all primes $p$, since $\abs{\Q_p}_p=\abs{\Q}_p=p^{\Z}$ is isomorphic to the integers (as a topological group).
<div class="definitoin">
    Let $F$ be a field with a discrete absolute value $\nabs:F\to\R_{\ge0}$. Then, $A=\{x\in F:\abs x\le1\}$ is $F$'s <b>valuation ring</b>. It is a local ring whose unique maximal ideal is $\mfm=\{x\in F:\abs x< 1\}$. The field $k=A/\mfm$ is call the <b>residue field</b> of $F$.
</div>
<div class="exercise">
    Let $\nabs:F\to\R_{\ge0}$ be an absolute value on a field $F$. Show that this makes $F$ a local field if and only if $\nabs$ is discretely valued with a finite residue field (and, of course, $F$ is complete w.r.t $\nabs$).
</div>

[^1]: If you don't know what a topology is, don't worry.
[^2]: This means that the inverse image of any open interval in R is a union of open balls in D.
[^3]: In the sense that its points get arbitrarily close to one another.
[^4]: i.e. termwise but you have to be careful with division because of zeros in your sequence (just choose a representation without any).
[^5]: It will be hard for me to stop myself from doing algebra, but I don't want this post to become unreasonably long.
[^6]: At least, to do it the way I'll do it...
[^7]: If you haven't seen the Z_{(p)} notation before, check out my [localization post](../ufd-localization)
[^9]: I'll probably forget to mention this when needed, so just always assume that I'm only considering nontrivial absolute values.