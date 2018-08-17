---
layout: post
title: "Orbit-Stabilizer for Finite Group Representations"
modified:
categories: blog
excerpt:
tags: [math, representation theory, group actions, group theory, algebra]
date: 2018-06-06 00:19:00
---

One of my professors covered the main result of this post during a class that I missed awhile ago. Using some notes from a friend who attended that class, I want to try to reconstruct the theorem [^1]. Experience with representation theory will be useful for this post, but I'll try to cover enough of the basics so that previous exposure isn't strictly required.

# Orbit-Stabalizer

We will begin by continuing our discussion of group actions from [last post](../geo-group). Recall the definition
<div class="definition">
    Let $G$ be a group and let $X$ be a set. A <b>(left) group action</b> of $G$ on $X$ is a map $\phi:G\times X\rightarrow X$ satisfying
    <ul>
        <li> $1\cdot x=x$ for all $x\in X$ where $1\in G$ is the identity</li>
        <li> $g\cdot(h\cdot x)=(gh)\cdot x$ for all $x\in X$ and $g,h\in G$</li>
    </ul>
    where $g\cdot x$ denotes $\phi(g,x)$.
</div>

We sometimes write $G\curvearrowright X$ to denote that $G$ acts on $X$. If $X$ has additional structure (e.g. if $X$ is a vector space), then we require our group action to respect $X$'s structure. In general, a group action $G\curvearrowright X$ is a map $G\rightarrow\Aut(X)$ where the automorphisms of $X$ depend on the context [^2].

Now, in order to (state and) prove Orbit-Stabalizer, we'll need to know what those words mean.
<div class="definition">
    Let $G$ be a group acting on a set $X$. Given some $x\in X$, its <b>orbit</b> is
    $$G\cdot x=\{g\cdot x\mid g\in G\}$$
    Furthermore, its <b>stabalizer</b> is
    $$\Stab(x)=G_x=\{g\in G\mid g\cdot x=x\}$$
</div>

Note that the stabalizer of $x\in X$ is a subgroup of $G$ since $g,h\in G_x\implies(g\inv h)\cdot x=g\cdot x=x$. Furthermore, if $G\cdot x=X$ for some $x\in X$, then we say $G$ acts <b>transitively</b> on $X$.

Finally, if $G\curvearrowright X$, then we call $X$ a <b>$G$-set</b>. Naturally, these spaces have their own notion of homomorphisms.
<div class="definition">
    Let $X,Y$ be two $G$-sets. A <b>$G$-map</b> (or <b>$G$-equivariant map</b> or <b>$G$-morphisms</b>) is a map $f:X\rightarrow Y$ s.t. $f(g\cdot x)=g\cdot f(x)$ for all $g\in G$ and $x\in X$. We say $f$ is a <b>$G$-isomorphism</b> if it is bijective.
</div>
<div class="exercise">
    Show that if $f$ is a $G$-isomorphism, then $\inv f$ is $G$-equivariant.
</div>

With our definitions set up, we come to
<div class="theorem" name="Orbit-Stabilizer">
    Let $X$ be a $G$-set. Fix any $Y\subseteq X$ s.t. $g\cdot Y\cap Y\in\{Y,\emptyset\}$ for all $g\in G$ and $G\cdot Y=\{g\cdot y\mid g\in G,y\in Y\}=X$. Finally, let $H=\Stab(Y)=\{g\in G\mid\forall y\in Y:g\cdot y\in Y\}$. Then,
    $$X\simeq\bigsqcup_{\sigma_i\in G/H}\sigma_iY$$
    as $G$-sets where the union is taken over coset representatives of $G/H$ and $\sigma_iY=\{\sigma_i y\mid y\in Y\}$ (note: $\sigma_iy$ is just a formal symbol) and $G$ acts on it via $g\cdot(\sigma_iy)=\sigma_j(h\cdot y)$ for the unique $\sigma_j,h$ s.t. $g\sigma_i=h\sigma_j$.
</div>
<div class="proof4">
    Let $f:\bigsqcup_{\sigma_i\in G/H}\sigma_iY\to X$ be the map $f(\sigma_iy)=\sigma_i\cdot y$. This map is $G$-equivariant since 
    $$f(g\cdot\sigma_iy)=f(\sigma_j(h\cdot y))=\sigma_j\cdot(h\cdot y)=(\sigma_jh)\cdot y=(g\sigma_i)\cdot y=g\cdot(\sigma_i\cdot y)=g\cdot f(\sigma_iy)$$
    where $g\sigma_i=\sigma_jh$. For injectivity, if $\sigma_i\cdot y=\sigma_j\cdot y'$, then 
    $$(\inv\sigma_j\sigma_i)\cdot y=y'\implies\inv\sigma_j\sigma_i\in H\implies\sigma_iH=\sigma_jH\implies\sigma_i=\sigma_j\implies y=y'$$
    where the second-to-last implication comes from the fact that we fixed our coset representatives ahead of time. Finally, for surjectivity, fix any $x\in X$. Since $G\cdot Y=X$, there exists $g\in G$ and $y\in Y$ s.t. $g\cdot y=x$. Thus, writing $g=\sigma_jh$, we have that $f(\sigma_j(h\cdot y))=x$.
</div>
<div class="cor">
    Let $X$ be a $G$-set, and fix any $x\in X$. Then, $|G\cdot x|=|G:G_x|=|G|/|G_x|$
</div>
<div class="proof4">
    Apply the above theorem to the $G$-set $G\cdot x$ where $Y=\{x\}$.
</div>

It's worth noting that Orbit-Stabilizer usually only refers to the corollary above, but this stronger version is closer to our main theorem.

# A Quick Intro to Representations of Finite Groups

Now that we've seen Orbit-Stabilizer, we'll need to introduce some definitions from representation theory.
<div class="definition">
    Fix a group $G$ and a vector space $V$ over a field $\F$. A <b>(linear) representation of $G$</b> is a map $\rho:G\rightarrow\GL_{\F}(V)$. Given such a map, we call $V$ a <b>$G$-rep</b>, and morphisms of $G$-reps are $G$-equivariant linear maps. Finally $\theta:G\to\GL_{\F}(U)$ is a <b>subrepresentation</b> if $U\subseteq V$ and $\theta(g)=\rho(g)\mid_U$ for all $g\in G$.
</div>

When studying linear representations of groups, there are two main perspectives one can take. Everything can be done in terms of an explicit representation (i.e. the map $\rho$ above) or in terms of modules over the group ring. Since I haven't talked about modules on this blog before [^4], I'll stick to the explicit representation approach and leave exercises to translate things into statements about modules for the interested reader.

{::options parse_block_html="true" /}
<span class="exercise">
    Prove that a linear representation of $G$ is the same thing as an $\F[G]$-module. [^5]
</span>

Thankfully, we don't need a lot of representation theory for the main result of this post. We only need to know a few different types of linear representations. Also, in case I ever forget to mention this, for the rest of this post, assume all vector spaces are finite-dimensional and assume that all groups are finite.

{::options parse_block_html="false" /}
<div class="definition">
    A <b>permutation representation</b> of $G$ on a finite-dimensional $\F$-vector space $V$ is a linear representation $\rho:G\rightarrow\GL(V)$ in which the elements of $G$ act by permuting some basis $B=\{b_1,\dots,b_n\}$ for $V$.
</div>
<div class="example">
    Consider the symmetric group $S_n$ acting on $\C^n=\bigoplus_{i=1}^n\C e_i$ via $\sigma\cdot e_i=e_{\sigma(i)}$. 
</div>
<div class="example">
    Let $G$ be any finite group, and consider $\C[G]\simeq\bigoplus_{g\in G}\C g$ as vector spaces. This is the <b>regular representation</b> when $G$ acts via $h\cdot g=hg$ on the basis.
</div>

Finally, we need the notion of induced representations. This let's you take a representation of a group $H$ and canoncially construct a representation of a larger group $G\supseteq H$. The construction is very reminiscent of the Orbit-Stabilizer theorem.

<div class="construction">
    Let $H\le G$ be a subgroup of $G$, and let $V$ be an $H$-rep. Fix a complete set of coset representatives $\sigma_1=e,\dots,\sigma_n\in G$ s.t. $G/H=\{\sigma_iH:0\le i\le n\}$ and $n=|G/H|$. Then, as a vector space, the <b>induced representation</b> from $H$ to $G$ is
    $$\Ind_H^GV=\bigoplus_{i=1}^n\sigma_iV$$
    where $\sigma_iV=\{\sigma_iv\mid v\in V\}$ is a space of formal symbols. This is given a $G$-action as follows: given some $\sigma_iv\in\Ind_H^GV$, there's a unique $\sigma_j$ and $h\in H$ s.t. $g\sigma_i=\sigma_jh$. We define $g\cdot\sigma_iv=\sigma_j(h\cdot v)$.
</div>
<div class="exercise">
    Prove that, as $\F[G]$-modules, we have
    $$\Ind_H^GV\simeq\F[G]\otimes_{\F[H]}V$$
    so induction is really just extension of scalars.
</div>
<div class="example">
    The regular representation is $\Ind_1^G\F$ where $1$ denotes the trivial group and $G$ acts trivially (i.e. by the identity) on $\F$.
</div> 

# Orbit-Stabilizer v2
This is where we'll prove the main result, which roughly says that (almost-)permutation representations are induced representations.
<div class="theorem" name="Orbit-Stabilizer Variation">
    Let $V$ be a $G$-rep with a decomposition $V\simeq\bigoplus_{i=0}^nV_i$ as a vector space s.t. for all $i,j\in\{0,\dots,n\}$, there exists a $g\in G$ s.t. $g\cdot V_i=V_j$, and let $H=\Stab(V_0)$. Then,
    $$V\simeq\Ind_H^GV_0$$
</div>
<div class="proof4">
    We will show this by constructing an explicit isomorphism. Let $f:\Ind_H^GV_0\rightarrow V$ be the map given by
    $$f(\sigma_iv_0)=\sigma_i\cdot v_0$$
    This is easily seen to be $G$-equivariant, and it is linear by construction. For surjectivity, it suffices to find preimages for elements of the form $v_i\in V_i$. Given such an element, there exists some $g_i\in G$ and $w_i\in V_0$ s.t. $g_i\cdot w_i=v_i$. Now, we can write $g_i=h_i\ith\sigma_j$ for a unique $h_i\in H$ and coset representative $\ith\sigma_j$. Doing so gives us that $f(\ith\sigma_j(h_i\cdot w_i))=v_i$ so $f$ is surjective as claimed. Finally, we need to show that $f$ is injective, so fix some $w=\sum_{\sigma_i\in G/H}\sigma_i\ith v_0\in\ker f$. This means that $\sum_{\sigma_i\in G/H}\sigma_i\cdot\ith v_0=0$, but we claim that $\sigma_i\cdot\ith v_0$ and $\sigma_j\cdot\Ith vj_0$ belong to different summands (i.e. different $V_i$'s) which forces $\sigma_i\cdot\ith v_0=0\implies\ith v_0=0$ for all $i$ so $w=0$. To prove the claim, suppose that $\sigma_i\cdot\ith v_0,\sigma_j\cdot\Ith vj_0\in V_k$ for some $k$. Then,
    $$\inv\sigma_j\sigma_i\cdot\ith v_0\in V_0\implies\inv\sigma_j\sigma_i\in H\implies\sigma_j=\sigma_i$$
    and we win.
</div>
This wasn't the proof I had in mind. I imagined (and still do) that it was possible to directly apply the original orbit-stabilizer by letting $X$ be a (well-chosen) basis for $V$ and $Y$ be a (well-chosen) basis for $V_0$. However, in trying to make this work, I ran in to issues getting a well-defined action of $G$ on $B$. Basically, $H=\Stab(V_0)$ can act nontrivially so it's possible that $h\cdot B_0\not\subseteq B$ which is troublesome. I still hold out hope that this idea can be salvaged in general[^6], so  
<div class="exercise">
    See if you can come up with a proof of the above that applies the original Orbit-Stabilizer theorem (e.g. apply it to a basis of V and then extend linearly). If you can, let me know.
</div>
Even though the proof is a little unsatisfying, we have proven what we set out to prove, so let's end with a couple examples. $\newcommand{\trv}{\underline{\text{Trv}}}\newcommand{\alt}{\underline{\text{Alt}}}$
<div class="example">
    Consider $S_n\curvearrowright\Sym^2\C^n$ where $\C^n=\bigoplus\C e_i$ and $S_n$ acts by permuting the $e_i$. Restricting this action to the basis $B=\{e_ie_j:i,j\in\{1,\dots,n\}\}$, we see there are two $S_n$-orbits
    $$\begin{matrix}
        B_0 &=& \brackets{e_ie_j:i\neq j} && \Stab(\C e_1e_2) &=& S_2\times S_{n-2}\\
        B_1 &=& \brackets{e_1^2,\dots,e_n^2} && \Stab(\C e_1^2) &=& S_{n-1}
    \end{matrix}$$
    Thus we can write $\Sym^2\C^n=V\oplus W$ where $V=\C B_0=\bigoplus_{i\neq j}\C e_ie_j$ and $W=\C B_1=\bigoplus_{i=1}^n\C e_i^2$. Furthermore, $S^n$ acts transitively on these decompositions of $V,W$ so applying our theorem ($V_0=\C e_1e_2$ and $W_0=\C e_1^2$) yields
    $$\Sym^2\C^n\simeq\parens{\Ind_{S_2\times S_{n-2}}^{S_n}\trv\otimes\trv}\oplus\parens{\Ind_{S_{n-1}}^{S_n}\trv}$$
    where $\trv$ is the trivial 1-dimensional $S_k$ representation sending each element to the number 1.
</div>
<div class="example">
    This time, let's look at $S_n\curvearrowright\parens{\Wedge^2\C^n}\otimes\C^n$ where $\C^n=\bigoplus e_i$ and $S_n$ again acts by permuting the $e_i$. We have a basis $B=\{(e_i\wedge e_j)\otimes e_k:i,j,k\in\{1,\dots,n\},i< j\}$ but it's not fixed by $S_n$ (e.g. $(12)\cdot(e_1\wedge e_2)\otimes e_3=(e_2\wedge e_1)\otimes e_3\not\in B$), so we'll look instead at the spanning set $B'=\{(e_i\wedge e_j)\otimes e_k:i,j,k\in\{1,\dots,n\},i\neq j\}$ which is fixed by $S_n$. This has the following orbits
    $$\begin{matrix}
        B_0 &=& \brackets{(e_i\wedge e_j)\otimes e_k:i\neq j\neq k} && \Stab(\C (e_1\wedge e_2\otimes e_3)) &=& S_2\times S_{n-3}\\
        B_1 &=& \brackets{(e_i\wedge e_j)\otimes e_k:i\neq j,k\in\{i,j\}} && \Stab(\C(e_1\wedge e_2\otimes e_1)) &=& S_{n-2}
    \end{matrix}$$
    It's worth noting that $(12)\cdot(e_1\wedge e_2)\otimes e_1=-(e_1\wedge e_2)\otimes e_2$ so we can switch whether $k=i$ or $k=j$ in $B_1$ above. Applying our theorem to (the span of) each orbit and summing them up, we get that
    $$\Wedge^2\C^n\otimes\C^n\simeq\parens{\Ind_{S_2\times S_{n-3}}^{S_n}\alt\otimes\trv}\oplus\parens{\Ind_{S_{n-2}}^{S_n}\trv}$$
    where $\alt$ is the alternating 1-dimensional $S_k$ representation sending each element to its sign.
</div>

[^1]: which, unsurprisingly, is a version of Orbit-stabilizer for representations of finite groups
[^2]: for X a set, they are (self) bijections
[^3]: these are formal symbols
[^4]: but really should at some point
[^5]: This includes proving that $\F[G]$-linear maps are $G$-equivariant and that submodules correspond to subrepresentations
[^6]: It certainly can be in the case that H does indeed act trivially (or at least stabalizes the basis)... Question: is there always a basis B_0 s.t. Stab(V_0) is contained in Stab(B_0)?