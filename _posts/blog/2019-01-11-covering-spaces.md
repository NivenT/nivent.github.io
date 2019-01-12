---
layout: post
title: "Covering Spaces"
modified:
categories: blog
excerpt:
tags: [math, topology, homotopy]
date: 2019-01-11
---

This post is more for me than it is for you. I wanna make sure I still understand the theory of covering spaces after not thinking about them for a while. It's possible you'll get something out of this as well. Throughout this post, every space is assumed path-connected and locally path-connected unless stated otherwise. Furthermore, every map is continuous.

# The Basics
<p class="definition">
    A <b>covering map</b> is a surjective map $p:\wt X\to X$ such that every $x\in X$ has a <b>fundamental</b> (or <b>elementary</b>) <b>neighborhood</b> $U$, meaning each connected component of $\inv p(U)$ is mapped homeomorphically onto $U$ by $p$. The connected components of $\inv p(U)$ are called <b>lifts</b> of $U$. Given $x\in X$, the set $\inv p(x)$ is called the <b>fiber</b> above $x$ and an inpidual $\tilde x\in\inv p(x)$ is called a <b>lift</b> of $x$. The pair $(\wt X,p)$ is called a <b>covering space</b> of $X$, and we will often abuse notation by referring to $\wt X$ alone as a covering space. We will sometimes refer to $X$ as the <b>base space</b>. 
</p>

Covering spaces are neat because they have simpler topologies (read: "simpler" fundamental groups [^1]) than the base space, allowing us to "lift" certain arguments from a base space to (one of) its coverings, and because a space's coverings have a "Galois correspondence" with its fundamental group.

We will begin by showing the existence of lifts of maps $f:Y\to X$. By this, we mean a map $f:Y\to\wt X$ such that the following diagram is commutative
<center>
    <img src="{{ site.url }}/images/blog/covering-spaces/lift.png" width="200" height="100">
</center>
where the dashed line is meant to signify that $\tilde f$ exists given some (sufficiently nice) $f:Y\to X$. This is easiest to see in the case of paths.

For the remainder of this section, fix some base space $X$ and a covering space $(\wt X,p)$.

<p class="lemma" name="unique path lifting">
    Given a path $f:I\to X$ and a lift $\tilde x\in\inv p(f(0))$, there exists a unique path $\tilde f:I\to\wt X$ such that $\tilde f(0)=\tilde x$ and $p\tilde f=f$.
</p>
<p class="proof4">
    By covering $X$ by fundamental neighborhoods, pulling them back to $I$ via $f$, and appealing to compactness of $I$, we obtain some finite cover $\{U_i\}_{i=1}^n$ of $I$ such that $f(U_i)$ is contained in some elementary neighborhood. By possibly refining this cover, this means there's some $m\in\N$ such that $I_j:=[j/m,(j+1)/m]$ gets mapped into a fundamental neighborhood by $f$ for $j=0,\dots,m-1$. We can now lift $f$ piece-by-piece. Let $\tilde U_0\subseteq\tilde X$ be the unique path component of $\inv p\parens{f(I_0)}$ containing $\tilde x$. Since $p:\tilde U_0\to f(I_0)$ is a homeomorphism, we define $\tilde f$ on $I_0$ by $\tilde f(x)=\inv p(f(x))$ where we consider $p$ a function $\tilde U_0\to f(I_0)$. We now proceed inductively. Given $f$ defined on $I_0\cup\cdots\cup I_{j-1}$, we define it on $I_j$ by letting $U_j$ be the path component of $\inv p(f(I_j))$ containing $\tilde f(j/m)$, and then lifting $f$ on $I_j$ the only way possible.
</p>
<p class="theorem">
    Given a covering space $p:\tilde X\to X$, a homotopy $f_t:Y\to X$, and a map $\st{f_0}:Y\to\tilde X$ lifting $f_0$, there exists a unique homotopy $\tilde f_t:Y\to\tilde X$ of $\tilde f_0$ that lifts $f_t$.
</p>
<p class="proof4">
    We first constrct a lift locally around each point. Let $F:Y\by I\to X,(y,t)\mapsto f_t(y)$. Given some $y\in Y$ and $t\in[0,1]$, we can find a basic neighborhood $B_t=N_t\by(a_t,b_t)$ such that $F(B_t)$ is contained in some fundamental neighborhood. Using compactness of $I$ and varying $t$, we see that finitely many such $B_t$ are sufficient for covering $\{y\}\by I$. Intersecting the $N_t$ and choosing a suitably large $m\in\N$, we can find a single neighborhood $N_y$ of $y$ such that $F(N\by[j/m,(j+1)/j])$ is contained in a fundamental neighborhood for each $j=0,\cdots,m-1$. Repeating the inductive procedure from last time, this let's us construct a lift $\st f_t^y:I\to\tilde X$ of $f_t$.<br>
    Finally, consider some $y,y'\in Y$. Note that the lifts $\st f_t^y,\st f_t^{y'}$ must agree on $N_y\cap N_{y'}$ since for any $y_0\in N_y\cap N_{y'}$, $t\mapsto\st f_t^y\mid_{\{y_0\}\by I}$ and $t\mapsto\st f_t^{y'}\mid_{\{y_0\}\by I}$ are both lifts of the path $t\mapsto f_t(y_0)$ and hence are equal by the above lemma. Thus, our various local lifts stitch together to give a global lift $\tilde f_t:Y\to\tilde X$ which is continuous since it's continuous on each $N_y$ and these cover $Y$. It's unique because it's unique of each "slice" $\{y\}\by I$.
</p>
<p class="remark">
    If $f_t:I\to X$ is a homotopy of paths (i.e. it fixes endpoints), then any lift $\st{f_t}:I\to X$ also fixes endpoints because $\st{f_0}:I\to X$ lifts a constant path as does $\st{f_1}:I\to X$ (and $\inv p(x)$ is discrete for all $x\in X$).
</p>

This has some immediate applications. Note that when we write a map $f:(X,x)\to(Y,y)$ we mean that $f:X\to Y$ is a map with $f(x)=y$ (more generally, given $A\subseteq X$ and $B\subseteq Y$, $f:(X,A)\to(Y,B)$ means $f(A)\subseteq B$).
<p class="proposition">
    The map $\push p:\pi_1(\wt X,\st x_0)\to\pi_1(X, x_0)$ induced by the covering $p:(\wt X,\st x_0)\to(X,x_0)$ is injective. Furthermore, the its image $\push p\pi_1(\wt X,\st x_0)$ in $\pi_1(X,x_0)$ consists of (homotopy classes of) loops in $X$ based at $x_0$ whose lifts to $\wt X$ starting at $\wt x_0$ are loops.
</p>
<p class="proof4">
    Suppose that $\st f\in\pi_1(\wt X,\st x_0)$ has a nulhomotopic image, so there's some homotopy $h_t:I\to X$ with $h_0=p\tilde f$ and $h_1(t)=x_0$ for all $t$. Since $\tilde f$ clearly lifts $h_0$, we can lift this homotopy to $\st{h_t}:I\to\wt X$ where $\st{h_0}=\st f$. Then, $\st{h_1}$ lifts $h_1$, a constant path, so $\st{h_1}$ must be constant as well. Hence, $\tilde f$ is nulhomotopic, so $\push p$ is injective. The second part of the proposition is obvious.
</p>
<p class="proposition">
    The size of the fiber $\inv p(x)$ over any $x\in X$ is equal to the index of $\push p\pi_1(\wt X,\st x_0)$ in $\pi_1(X, x_0)$.
</p>
<p class="proof4">
    Let $G=\pi_1(X, x_0)$, $H=\push p\pi_1(\wt X,\st x_0)$, and $G/H=\{Hg:g\in G\}$ be the set of cosets of $H$. We define a function $\phi:G/H\to\inv p(x_0)$ by letting $\phi(Hg)$ be $\tilde g(1)$ where $\tilde g$ is the lift of $g$ starting at $\st x_0$. This is well-defined since elements of $H$ lift to loops, so $hg$ has the same endpoint as $g$ for any $h\in H$. Note that $\phi$ is surjective since $\wt X$ is path-connected, and $\phi$ is injective because $\phi(Hg)=\phi(Hk)\implies \st g\inv{\st k}\in\pi_1(\wt X,\st x_0)$, so $g\inv k\in H$.
</p>
<p class="corollary">
    Every fiber of $p:\wt X\to X$ has the same size, and $\wt X$ is a fiber bundle over $X$.
</p>

# More Lifts

We've seen how to lift homotopies given a starting point, but what about more general maps? Fix a covering space $p:(\wt X,\st x_0)\to(X,x_0)$.
<p class="proposition">
    Given a map $f:(Y,y_0)\to(X,x_0)$ this lifts to a map $\st f:(Y,y_0)\to(\wt X,\st x_0)$ iff $\push f\pi_1(Y,y_0)\subseteq\push p\pi_1(\wt X,\st x_0)$.
</p>
<p class="proof4">
    The "only if" direction is obvious since $f=p\tilde f$, so we focus on the "if" direction. Given some $y\in Y$, let $g$ be a path from $y_0$ to $y$, so $\push fg$ is a path from $x_0$ to $f(y)$. This lifts to a path $\wt{\push fg}$ starting at $\st x_0$; call the other endpoint of this lift $\st f(y)$, i.e. $\st f(y)=\wt{\push fg}(1)$. This is well-defined since given another path $h$ from $y_0$ to $y$, we have $g\inv h\in\pi_1(Y, y_0)$ so $\push f(g\inv h)\in\push p\pi_1(\wt X,\st x_0)$ meaning that $(\push fg)\inv{(\push fh)}$ lifts to a loop based at $\tilde x_0$ which is possible iff $\wt{\push fg}(1)=\wt{\push fh}(1)$. Thus, we only need to show that $\st f$ is continuous. For this, let $U\subset X$ be an open neighborhood of $f(y)$ with a lift $\wt U\subseteq\wt X$ containing $\st f(y)$ such that $p:\wt U\to U$ is a homeomorphism. Choose a path-connected open neighborhood $V$ of $y$ with $f(V)\subseteq U$. Then, $\st f(V)\subseteq\wt U$ (since $V$ path-connected) and $\tilde f\mid_V=\inv pf$ so $\st f$ is continuous at $y$.
</p>
{::options parse_block_html="true" /}
<p class="cor">
    For $n\ge2$ (really, $n\ge1$), let $\pi_n(X, x_0):=[(S^n, s_0),(X, x_0)]$ be the set (really group) of homotopy classes of maps $(S^n, s_0)\to(X, x_0)$ [^2]. Then, for $n\ge2$ (this time actually $n\ge2$), $\pi_n(X,x_0)\simeq\pi_n(\wt X,\st x_0)$.
</p>
<p class="proof4">
    Using the fact that $S^n$ is simply connected for $n\ge2$ (and the fact that $I$ is simple connected), we can apply to above proposition to lift any map $S^n\to X$ up to a map $S^n\to\wt X$ (giving surjectivity) and lift any homotopy $S^n\by I\to X$ up to a homotopy $S^n\by I\to\wt X$ (giving injectivity).
</p>
<p class="proposition">
    Let $Y$ be connected (but not necessarily path-connected or locally path-connected), and fix a map $f:Y\to X$ with lifts $\st{f_1},\st{f_2}:Y\to\wt X$. If these lifts agree at one point of $Y$, then they agree on all of $Y$.
</p>
<p class="proof4">
    Let $S=\{y\in Y:\st{f_1}(y)=\st{f_2}(y)\}$, and fix some $y\in Y$. Let $U$ be a fundamental neighborhood of $f(y)$. Let $\wt U_1,\wt U_2\subseteq\wt X$ be such that $p$ maps both of them homeomorphically onto $U$, $\st f_1(y)\in\wt U_1$, and $\st f_2(y)\in\wt U_2$. Then, $N=\inv f(U)$ is a neighborhood of $y$ mapped into $\wt U_i$ by $\st{f_i}$, $i=1,2$. If $y\in S$, then $N\subseteq S$ since $\st f_1(y'),\st f_2(y')\in\wt U_1$ both lift $f(y)\in U$; hence, $S$ is open. If $y\not\in S$, then $N\subseteq Y\sm S$ since $\wt U_1\cap\wt U_2=\emptyset$; hence, $Y\sm S$ is open. Since $Y$ is connected, this means that $S=Y$ or $S=\emptyset$, but $S$ is nonempty by assumption, so $S=Y$.
</p>

# Galois Correspondence

<p class="definition">
    Let $(\wt X_1,p)$ and $(\wt X_2,q)$ both be covers of $X$. A map $\phi:\wt X_1\to\wt X_2$ is called a <b>homomorphism</b> if $q\phi=p$. The group of isomorphisms $\wt{X_1}\to\wt{X_1}$ is denoted $\Aut(\wt{X_1},p)$.
</p>
<p class="remark">
    Any $\phi\in\Aut(\wt X,p)$ is a lift of the covering map $p:\wt X\to p$ and so it is determined by its action on any single point.
</p>
<p class="lemma">
    Let $(\wt X_1,\wt x_1)$ and $(\wt X_2, \st x_2)$ be covers of $X$ (with covering maps $p,q$ respectively). Then, $(\wt X_1, p)\simeq(\wt X_2, q)$ iff $\push p\pi_1(\wt{X_1},\st x_1)=\push q\pi_1(\wt{X_2},\st x_2)$.
</p>
<p class="proof4">
    Note this is literal equality as sets, and note just isomorphism as groups. The $\to$ direction is easy, so we'll only do the $\leftarrow$ direction. Suppose that $\push p\pi_1(\wt{X_1},\st x_1)=\push q\pi_1(\wt{X_2},\st x_2)$, and fix any $\st x_1'\in\wt{X_1}$. Now we do the only thing we can do in this situation. Pick a path $g$ from $\st x_1$ to $\st x_1'$, push it down to $X$, lift it up to $\wt{X_2}$ starting at $\st x_2$, and call its right endpoint $f(\st x_1)$. We then show this construction is well-defined and gives an isomorphism of covering spaces, which it is (since the push-forward of loops in $\wt{X_1}$ lift to loops in $\wt{X_2}$) and it does (because you can define the inverse in the same way).
</p>

<p class="definition">
    Let $(\wt X, \st x_0)$ be a covering of $(X, x_0)$. We call it a <b>universal covering (space)</b> if $\pi_1(\wt X,\st x_0)=0$.
</p>
The name is justified by the following theorem.
<p class="theorem">
    Let $(\wt X,\st x_0)$ be the universal cover of $(X,x_0)$ (with covering map $p$). Then, for any subgroup $H\leq\pi_1(X,x_0)$, there exists a cover $(\wt X_H, \st x_h)$ (with covering map $q$) of $(X,x_0)$ that $(\wt X,\st x_0)$ covers with $\push q\pi_1(\wt X_h, \st x_h)=H$.
</p>
<p class="proof4">
    Fix a subgroup $H\le\pi_1(X, x_0)$. Note that $\pi_1(X,x_0)$ acts on $\wt X$ (on the right!) via the map (secretly an isomorphism) $\pi_1(X, x_0)\to\Aut(\wt X,\st x_0)\op$ given by sending $f\in\pi_1(X,x_0)$ to the (unique!) automorphism sending $\st x_0$ to $\st f(1)$ where $\st f$ lifts $x_0$ beginning at $\st x_0$. Let $\wt{X_H}= X/H$, the orbit space of this action restricted to $H$, and define $q:\wt{X_H}\to X$ via $q(\st xH)=p(\st x)$. This is well defined since $H$ preserves the fibers of $p$. <br>
    So, we want to show that $q$ is a covering map, that the quotient map $h:\wt X\to\wt{X_H}$ is a covering map, and that $\push q\pi_1(\wt{X_H},\st x_H)=H$ where $\st x_H=h(\wt x_0)$. I was more concerned with the lifting properties of covering spaces when I began this post, so I'll leave all of this as an exercise.
</p>
<p class="corollary">
    Let $(\wt X, \st x_0)$ be a universal cover of $(X, x_0)$, and let $(X', x_0')$ be a cover of $(X, x_0)$. Then, $(\wt X, \st x_0)$ also covers $(X', x_0')$.
</p> 

[^1]: read: their fundamental groups are subgroups of the base group.
[^2]: this obviously does not depend on the choice of $s_0$ upto isomorphism in the relevant category (i.e. pointed sets with basepoint the homotopy class of maps into $x_0$ or groups)
