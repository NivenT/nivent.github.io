---
layout: post
title: "Classification of (Complex) Elliptic Surfaces without Multiple Fibers"
modified:
categories: blog
excerpt:
tags: [math, for me, elliptic surfaces, complex surfaces, complex geometry, algebraic geometry, monodromy]
date: 2020-07-26
hidden: true
---

To some extent, every post I write is written for me moreso than for you, the proverbial reader. However, this post is especially written for me. I want to understand the construction of complex elliptic surfaces with prescribed global monodromy, but don't want to type up the details of the parts of this story that are needed for this construction (e.g. the local classification of elliptic surfaces), so here we are. I'll start by recalling the local picture [^1], and then we'll look at the global picture (only constructing these surfaces; no calculating numerical invariants or whatnot) [^2].

1. TOC
{:toc}

# Local Theory of Complex Elliptic Surfaces (No Proofs)

What are our objects of study?
<div class="definition">
    An <b>elliptic surface</b> is a $2$-dimensional complex manifold (i.e. a surface) $X$ equipped with a fibration (i.e. a proper, surjective (flat) holomorphic map) $\pi:X\to C$ to a $1$-dimensional complex manifold (i.e. a curve) such that the general fiber $X_c:=\inv\pi(c)$ (for $c\in C$) is a smooth connected curve of genus $1$.
</div>

An elliptic surface $\pi:X\to C$ captures the notion of a "holomorphically varying family of elliptic curves." The elements of this family are the fibers $X_c=\inv\pi(c)$ for $c\in C$. While almost all of these are smooth, there will be some finite number of <b>singular fibers</b>, fibers $X_c=\inv\pi(c)$ which are not smooth. Letting $c_1,\dots,c_n\in C$ denote the <b>critical values</b> (i.e. the points above which $X$ is not smooth), letting $\ast C=C\sm\bracks{c_1,\dots,c_n}$, and letting $\ast X=X\sm\bigcup_{i=1}^nX_{c_i}$, the restriction

$$\pi\vert_{\ast X}:\ast X\to\ast C$$

is a topological fiber bundle. Thus, via path lifting, is comes equipped with a <b>global monodromy map</b>

$$\pi_1(\ast C, c)\to\Aut(\hom_1(X_c;\Z))\simeq\GL_2(\Z)$$

for any fixed $c\in\ast C$. Before saying more about this, we want to look at its local counterpart. Fix any $c_i\in\bracks{c_1,\dots,c_n}$. Since $C$ is a smooth curve, we can find some neighborhood $U\subset C$ around $c_i$ such that $U\cong\Delta=\bracks{z\in\C:\abs z<1}$ with $c_i\in U$ corresponding to the origin $0\in\Delta$. Thus, locally $\pi:X\to C$ looks like an elliptic surface [^3]

$$f:S\to\Delta$$

with a single singular fiber, lying above $0\in\Delta$. Hence, $\ast\Delta=\Delta\sm\bracks0$ is homotopy equivalent to a circle $S^1$, so, fixing a nonzero basepoint $c\in\Delta$, its fundamental group is $\pi_1(\ast\Delta,c)\cong\Z$. As in the global case, the map $S\sm S_0\xto f\ast\Delta$ is a topological fiber bundle, so comes equipped with a <b>local monodromy map</b>

$$\Z\cong\pi_1(\ast\Delta,c)\to\Aut(\hom_1(X_c;\Z))\simeq\GL_2(\Z).$$

This map is clearly determined by what it does to the generator $\gamma\in\pi_1(\ast\Delta,c)$ circling the origin once counterclockwise, and so, after choosing a basis for $\hom_1(X_c;\Z)$, is identifiable with a matrix $T\in\GL_2(\Z)$, called the <b>local monodromy matrix</b>. This matrix $T$ is not arbitrary. In fact, up to conjugation (i.e. change of basis), it belongs to one of "finitely many" [^4] possible monodromy matrices. Furthermore, this local monodromy matrix $T$ actually determines the singular fiber $S_0=\inv f(0)$ up to isomorphism! Thus, elliptic fibrations are locally classified by a single invariant, the monodromy matrix.

# The Main Result

With that very brief overview done, let's get into the meet of things. Consider an elliptic surface $\pi:X\to C$ with critical values $c_1,\dots,c_n\in C$. As before, let $\ast C=C\sm\bracks{c_1,\dots,c_n}$ and let $\ast X=\inv\pi(\ast C)$.

Recall that $\ast X\xto\pi\ast C$ is a topological fiber bundle. The means that $L=\derpush1\pi\Z_X$ is a locally constant sheaf [^5] on $\ast C$ with stalks/fibers

$$L_c=\hom^1(X_c;\Z)\simeq\Z\oplus\Z.$$

As mentioned earlier, this situation gives rise to a global monodromy action $\pi_1(\ast C)\to\GL_2(\Z)$. 

[^1]: The first lecture of Miranda's [Basic Theory of Elliptic Surfaces](https://www.math.colostate.edu/~miranda/) is a good reference for this.
[^2]: For this, I am using [Compact Complex Surfaces](https://link.springer.com/book/10.1007/978-3-642-96754-2) by Barth et al.
[^3]: We changed notation to make the global and local cases more visually distinguishable. You should think $S=\inv\pi(U)$, $\Delta=U$, $U\subset C$ was taken small enough that $c_j\not\in U$ if $j\neq i$, and $f=\pi\vert_S$.
[^4]: Two infinite families, and six exceptional matrices
[^5]: Topologically, $\pi:\ast X\to\ast C$ locally looks like the natural projection $p:T\by U\to U$ where $T\cong(S^1)^2$ is a torus. On these trivial pieces. $\derpush1p\Z_X$ is the sheafification of the presheaf $U\supset V\mapsto\hom^1(\inv p(V);\Z)\simeq\hom^1(T;\Z)$ so $\derpush1p\Z_X$ is the constant sheaf $\hom^1(T;\Z)_ U$. Thus, $\derpush1\pi\Z_X$ is locally constant with stalks isomorphic to $\hom^1(T;\Z)$.
