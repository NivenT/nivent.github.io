---
layout: post
title: "Characteristic Classes"
modified:
categories: blog
excerpt:
tags: [math, topology, homotopy theory, cohomology, classifying spaces, chern classes, euler class, obstruction theory, enumerative geometry]
date: 2020-07-02
---

For a long time I've been telling myself that I should try and get a solid understanding of characteristic classes, so why not do that now?

Before getting into things, as usual, a few remarks about this post. First, by a "characteristic class" I mean a functorial way of attaching a cohomology class to a vector bundle [^3]. There are many of these, but because I care more about algebraic/holomorphic things than I do about smooth things, we will basically just look at Chern classes. I want to be quite detailed in this post, so even just focusing on these will require a lot of work. On the upside, the payoff will be a good amount of interesting/neat applications/calculations. Second, I'm going to try [^1] to make this post be a good one [^30]. I feel like many of my recent posts have either been overall meh or have started off good only for me to fumble the ending, and this is starting to really bother me. Hence, for this post, I'm going to try to prioritize quality/detail [^2] over "just producing a finished product" and see how this feels. Third, this post is titled "Characteristic Classes" but, if possible, I'd like to throw in a few things not strictly related to/requiring characteristic classes, but which are both at least somewhat related to them and things I've been wanting to improve my understanding of. Finally, characteristic classes are one of those things that can be constructed a dozen different ways, and can be given a million different treatments. Throughout this post, I'll try to maintain an unapologetically algebro-topological perspective, so don't expect me to e.g. say the words "connection" or "integration" [^20].
$
\newcommand{\CW}{\mathrm{CW}}
\newcommand{\Top}{\mathrm{Top}}
\newcommand{\Set}{\mathrm{Set}}
\newcommand{\Grp}{\mathrm{Grp}}
\DeclareMathOperator{\Ho}{Ho}
$

Throughout this post, assume the base space of any fibre bundle is Hausdorff and paracompact, so a CW complex or a manifold or a metric space or something like this. [^4] In particular, base spaces will always admit partitions of unity.

1. TOC
{:toc}

# Principal $G$-Bundles

The key example of a characteristic class to keep in mind throughout this post is the first Chern class $c_1(E)$ of a complex (topological) line bundle $E\to X$ which was introduced at the end of [the post on Brown Representability](../brown-rep). This class lives in $X$'s second integral cohomology and actually completely characterizes $E$ up to isomorphism (as a topological, complex line bundle over $X$). We constructed this class as the pullback on the canonical generator $\gamma\in\hom^2(\CP^\infty;\Z)\simeq\Z\gamma$ of the cohomology of $\CP^\infty$ along $E$'s classifying map $X\to BS^1\simeq\CP^\infty$ [^5]. Motivated by this, in order to define cohomology classes for higher rank (complex) vector bundles, we will want to understand the cohomology of $BU(n)$ for all $n$ [^39].

Before calculating $\ast\hom(BU(n);\Z)$, I want to patch up a hole in my introduction to Principal $G$-bundles from the Brown Representability post. In particular, I claimed that such bundles satisfy a homotopy invariance property, but did not proof this. This fact is high-key the starting point to being able to use $G$-bundles productively in homotopy theory, so this is probably actually something worth writing down a proof of. First recall the definition of a principal $G$-bundle.

<div class="definition">
    Fix a topological group $G$. A <b>principal $G$-bundle</b> over a space $B$ is a fiber bundle $\pi:P\to B$ with a free and transitive right action by $G$ on the fibers.
</div>
<div class="definition">
    Let $\pi_1:P_1\to B_1$ and $\pi_2:P_2\to B_2$ be principal $G$-bundles. A <b>morphism of principal $G$-bundles</b> $f=(\phi,\psi):(P_1,B_1)\to(P_2,B_2)$ is a pair of maps $\phi:P_1\to P_2$ and $\psi:B_1\to B_2$ such that the following commutes
    $$\begin{CD}
        P_1 @>\phi>> P_2\\
        @V\pi_1VV @VV\pi_2V\\
        B_1 @>>\psi> B_2
    \end{CD}$$
    and $\phi(p\cdot g)=\phi(p)\cdot g$ for all $g\in G$. We say $\phi$ <b>lies over</b> $\psi$.
</div>

In order to show that homotopic maps induce isomorphic pullback bundles, the following lemma will be useful. In short, it says that $G$-bundle maps lying above the identity are automatically isomorphisms.

<div class="lemma">
    Let $P$ and $P'$ be principal $G$-bundles over $B$, and let $\phi:P\to P'$ be a morphisms lying over the identity $B=B$. Then, $\phi$ is an isomorphism.
</div>
<div class="proof4">
    (Injectivity) We first show $\phi$ injective. Pick $p,q\in P$ such that $\phi(p)=\phi(q)$. Since $\phi$ lies over the identity, $p,q$ must belong to the same fiber of $P\to B$. Because $G$ acts transitively on the fibers, there exists some $g\in G$ such that $p\cdot g=q$. Since $\phi$ is a morphism of $G$-bundles, we get that $\phi(p)\cdot g=\phi(q)$, but $\phi(p)=\phi(q)$ and $G$ acts freely on the fibers. This means we must have $g=e$, the identity of $G$, so $q=p\cdot g=p\cdot e=p$.
    <br>
    (Surjectivity) We now treat surjectivity. Fix some $p'\in P'$ lying over $b\in B$. Let $p\in P$ be any point which also lies over $b$, so $\phi(p)$ and $p'$ belong to the same fiber of $P'$. Hence, by transitivity of the $G$-action, there is some $g\in G$ such that $\phi(p)\cdot g=p'$, and so $p\cdot g\in P$ is a preimage of $p'\in P'$.
    <br>
    (Continuity of $\inv\phi$) Now that we know $\phi$ is bijective, all that remains is to show that it is an open mapping. For this, we work locally. Pick some small open $U\subset B$ such that we have local trivializations $P\vert_U\simeq U\by G$ and $P'\vert_U\simeq U\by G$. Then, in local coordinates, $\phi\vert_U$ must take the form
    $$\phi:(b,g)\mapsto\parens{b,\phi'(b,g)}=\parens{b,\phi'(b,e)g}$$
    for some $\phi':U\by G\to G$ satisfying $\phi'(b,gh)=\phi'(b,g)h$. Thus, $\inv\phi$ is of the form
    $$(b,g)\mapsto(b,\inv{\phi'(b,e)}g)$$
    which is visibly continuous.
</div>
<div class="theorem">
    Let $\pi:P\to B'$ be a principal $G$-bundle, and let $f_0\sim f_1:B\rightrightarrows B'$ be two homotopic maps. Then, the bundles $\pull f_0(P)$ and $\pull f_1(P)$ over $B$ are isomorphic.
</div>
<div class="proof4">
    Let $F:B\by I\to B'$ be a homotopy from $f_0=F(-,0)$ to $f_1=F(-,1)$. We consider the pullback $\pull FP$, a principal $G$-bundle over $B\by I$. Our goal is essentially to show that $\pull FP$ is of the form $\pull f_0P\by I$; we will in fact show that this is the case for any principal $G$-bundle over $B\by I$. With that said, let $p:Q\to B\by I$ be a principal $G$-bundle. We claim that $Q\simeq Q_0\by I$ where $Q_0:=\inv p(B\by\{0\})\to B$ is the restriction of $Q$ to $0\in I$.
    <br>
    We seek an isomorphism $Q_0\by I\iso Q$ (lying over the identity on the base). Note that this amounts to extending the canonical map $Q_0\by\{0\}\iso Q_0\into Q$ into one from $Q_0\by I\to Q$. In other words, we are attempting to solve the following lifting problem.
    <center>
        <img src="{{ site.url }}/images/blog/char-class/lift.png" width="250" height="100">
    </center>
    Now, we're in luck. Since $B\by I$ is paracompact, the map $Q\xto pB\by I$ is a fibration, and so satisfies the homotopy lifting property. This says exactly that we can construct the above dashed map $\phi:Q_0\by I\to Q$ above (so the diagram commutes)! We claim this $\phi$ is an isomorphism. This follows immediately from the lemma.
</div>

With that taken care of, let's return to our goal of understanding characteristic classes. As was noted earlier, the first step in doing so is determining the cohomology (ring) of $BU(n)$ since this space classifies principal $U(n)$-bundles and so classifies rank $n$ complex vector bundles. We will spend a section going over a technical tool useful for performing this calculation (and also useful for proving things about characteristic classes in general), and then after that we will get our cohomology classes.


## Splitting Principle

Our first major goal is to show that

$$\ast\hom(BU(n);\Z)\simeq\Z[c_1,c_2,\dots,c_n]\text{ where }c_i\in\hom^{2i}(BU(n);\Z),$$

and so obtain $n$ different characteristic classes for any rank $n$ vector bundle, the Chern classes. In order to do this, we will carry out an inductive argument, relating the cohomology of $BU(n)$ to that of $BU(n-1)\by BU(1)$. This argument will make use of a general construction that allows one to peel of a single (line bundle) summand from an arbitrary vector bundle.

To see what I mean, let $p:E\to B$ be any rank $n+1$ vector bundle. Implicitly cover $B$ by opens $U_i\subset B$ on which $p$ trivializes, and let $\tau_{ij}:U_i\cap U_j\to U(n+1)\subset\GL_{n+1}(\C)$ be $p$'s transition functions [^6]. Then, we can projectivize $E$ in order to form a $\CP^n$-bundle $\pi:\P(E)\to B$ whose fibers are $\inv\pi(b)\simeq\P(\inv p(b))=\P(E_b)$ (I use $E_b$ to denote $E$'s fiber over $b\in B$), and whose transition functions are the compositions

$$U_i\cap U_j\xto{\tau_{ij}}U(n+1)\into\GL_{n+1}\C\onto\PGL_n\C.$$

This space $\P(E)$, called <b>projectivization of $E$</b> is where we will peel off a summand of $E$. A point $x\in\P(E)$ belongs to the projective space $\P(E)_ {\pi(x)}=\P(E_{\pi(x)})$ and so is identifiable with a line in the fiber $E_{\pi(x)}=\inv p(\pi(x))$. Note that $E$ has a few natural vector bundles. First, there is the pullback bundle $\pull\pi E\to\P(E)$ whose fiber above a point $x\in\P(E)$ is the fiber $E_{\pi(x)}$ of $E\xto pB$ above $\pi(x)\in B$. Inside of $\pull\pi E$, one can find the <b>tautological subbundle</b>

$$L_E:=\bracks{(\l, v)\in\P(E)\by E:v\in\l}\subset\pull\pi E$$

whose fiber above a point $\l\in\P(E)$ is the line $\l\subset E_{\pi(\l)}$ it corresponds to. The <b>tautological quotient bundle</b> $Q_E$ on $\P(E)$ is defined by its place in the following exact sequence:

$$0\too L_E\too\pull\pi E\too Q_E\too0.$$

Note that if we restrict the above sequence to the fiber $\P(E)_ b=\P(E_b)$ above any point $b\in B$, then we recover the normal sequence of tautological bundles on projective space [^7]. The existence of this sequence allows us to write $\pull\pi E\simeq L_E\oplus Q_E$ as the sum of a line bundle and a rank $n$ vector bundle.

<div class="lemma">
    Let $0\too L\too E\too Q\too 0$ be any sequence of complex vector bundles on some base space $B$. Then, $E\simeq L\oplus Q$ as vector bundles.
</div>
<div class="proof4">
    Let $m,n,k$ be the ranks of $L,E,Q$, respectively. Since $B$ is paracompact and Hausdorff by assumption, we can cover it by small opens $U_i\subset B$ such that
    <ol>
        <li> $L,E,Q$ all three trivialize over $U_i$, i.e. $L\vert_{U_i}\simeq U_i\by\C^m$, $E\vert_{U_i}\simeq U_i\by\C^n$, and $Q\vert_{U_i}\simeq U_i\by\C^k$. </li>
        <li> There exists a partition of unity $\rho_i:B\to[0,1]$ subordinate to the $U_i$'s. That is, $\supp\rho_i\subset U_i$ for all $i$ (the cover $\{U_i\}$ assumed locally finite) and
            $$\sum_i\rho_i(x)=1$$
            for all $x\in X$ (all but finitely many terms above are $0$). </li>
    </ol>
    Locally, the exact sequence $0\too L\too E\too Q\too 0$ of vector bundles looks like the sequence $0\too\C^m\too\C^n\too\C^k\too0$ of vector spaces. This sequence splits (say via $s:\C^k\to\C^n$), and so for every $i$, we can construct a local splitting map 
    $$\sigma_i:Q\vert_{U_i}\simeq U_i\by\C^k\xto{(\Id,s)}U_i\by\C^n\simeq E\vert_{U_i}$$
    realizing $E\vert_{U_i}$ as a sum $E\vert_{U_i}\simeq L\vert_{U_i}\oplus Q\vert_{U_i}$. We want to upgrade these into a global splitting map $\sigma:Q\to E$. To do so, we define
    $$\sigma(q)=\sum_i\rho_i(\pi(q))\sigma_i(q)$$
    where $q\in Q$ and $\pi:Q\to B$ is the projection map. The formula above makes sense since $\rho_i(\pi(q))=0$ when $q\not\in Q\vert_{U_i}$, and defines a splitting map because $\sigma\vert_{\inv\pi(U_i)}=\sigma_i$ by construction. Thus, $E\simeq L\oplus Q$ as claimed.
</div>

The above lemma justifies our earlier claim that $\pull\pi E\simeq L_E\oplus Q_E$. 

<div class="exercise">
    Let $EU(n)\to BU(n)$ be the universal rank $n$ vector bundle (really $EU(n)$ should denote the universal principal $U(n)$-bundle, but then you can turn this into a vector bundle by taking the vector bundle associated to the inclusion map $U(n)\into\GL_n\C=\Aut(\C^n)$). By the above discussion, pulling this bundle back to $X:=\P(EU(n))$ splits it into a line bundle and a rank $(n-1)$ vector bundle. Since $X$ splits the universal rank $n$ vector bundle, show that $X\simeq BU(n-1)\by BU(1)$ (they solve the same moduli problem/represent the same functor).
</div>

In order to carry out our induction argument, we still need to be able to relate the cohomology of $\P(E)$ to that of $E$ (e.g. cohomology of $BU(n-1)\by BU(1)$ to that of $BU(n)$ by the exercise above). We do this now. First recall the tautological exact sequence

$$0\too L_E\too\pull\pi E\too Q_E\too0$$

on $\P(E)$, and let $x=c_1(\dual L_E)\in\hom^2(\P(E);\Z)$ ($\dual L_E$ is the dual line bundle). As earlier remarked, this sequence restricts to the normal tautological exact sequence on the fibers $\P(E)_ b\simeq\P^n$; in particular, $L_E\vert_{\P(E)_ b}$ is the usual tautological line bundle [^8], and so the canonical generator for $\hom^2(\P(E)_ b;\Z)$ is precisely $x\vert_{\P(E)_ b}$ (this is the reason for taking the dual of $L_E$ before). Taking self cup-products, this means that $\{1,x,x^2,\dots,x^{n-1},x^n\}\subset\ast\hom(\P(E);\Z)$ are global cohomology classes whose restriction to each fiber $P(E)_ b=\P(E_b)\simeq\P^n$ freely generate the cohomology there (as a module). This allows us to determine the cohomology of $\P(E)$ via the following generalization of the Kunneth formula.

<div class="theorem" name="Leray-Hirsch">
    Let $F\xto\iota E\xto\pi B$ be a fiber bundle sequence, and let $R$ be a commutative ring. Assume that there are global cohomology classes $e_1,\dots,e_r\in\ast\hom(E;R)$ on $E$ which, when restricted to each fiber, freely generate the cohomology of said fiber (i.e. $\ast\hom(F;R)$ is a free (graded) $R$-module with basis $\{e_i\vert_F\}_{i=1}^r$). Let $s:\ast\hom(F;R)\to\ast\hom(E;R)$ be the map determined by these $e_i$ (i.e. $s(e_i\vert_F)=e_i$ and we extend linearly). Then, the map
    $$\mapdesc f{\ast\hom(B;R)\otimes_R\ast\hom(F;R)}{\ast\hom(E;R)}{\alpha\otimes\beta}{\pull\pi(\alpha)\smile s(\beta)}$$
    is an isomorphism of $\ast\hom(B;R)$-modules (not of rings though). Hence, $\ast\hom(E;R)$ is a free $\ast\hom(B;R)$-module with basis $e_1,\dots,e_r$.
</div>
<div class="proof4">
    We use the <a href="../spectral-seq">Serre spectral sequence</a>. First note that $\pull\iota:\ast\hom(E;R)\to\ast\hom(F;\R)$ is surjective, and so $\pi_1(B)$ acts trivially on $\ast\hom(F;R)$. Indeed, for any $\gamma\in\pi_1(B)$, it acts via the map $L_\gamma:F\to F$ given on $f\in F$ by lifting $\gamma$ to a path $\wt\gamma:[0,1]\to E$ starting at $f$ and then setting $L_\gamma(f)=\wt\gamma(1)$. Essentially by definition, this means we have a homotopy $h_t:F\to E$ from $h_0=\iota$ to $h_1=L_\gamma$. Hence, $\iota$ and $\iota\circ L_\gamma$ induce the same map on cohomology. Since $\pull\iota=\pull L_\gamma\circ\pull\iota$ and $\pull\iota$ is surjective, we conclude that $\pull L_\gamma=1$, i.e. that $\pi_1(B)$ acts trivially on the cohomology of the fiber.
    <br>
    This means we are justified in forming the Serre spectral sequence 
    $$E_2^{p,q}=\hom^p(B;\hom^q(F;R))\implies\hom^{p+q}(E;R).$$
    By assumption, $\hom^q(F;R)$ is a free $R$-module (i.e. of the form $R^{\oplus k}$ for some $k$, depending on $q$), so we see immediately that
    $$E_2^{p,q}=\hom^p(B;\hom^q(F;R))\simeq\hom^p(B;R)\otimes_R\hom^q(F;R)\simeq E_2^{p,0}\otimes_RE_2^{0,q}.$$
    Recall the the differential $d_2$ on the $E_2$-page has bidegree $(2,-1)$, i.e. we have
    $$d_2:E_2^{p,q}\simeq E_2^{p,0}\otimes_RE_2^{0,q}\to E_2^{p+2,0}\otimes_RE_2^{0,q-1}\simeq E_2^{p+2,q-1}.$$
    By the Leibniz rule, for $a\in E_2^{p,0}$ and $b\in E_2^{0,q}$, we have
    $$d_2(a\otimes b)=(a\otimes1)d_2(1\otimes b)+(-1)^p(1\otimes b)d_2(a\otimes 1)=(a\otimes1)d_2(1\otimes b)$$
    since $d_2(a\otimes 1)\in E_2^{p+2,-1}=0$. At the same time, $E_\infty^{0,q}=G^0\hom^q(E;R)=\hom^q(E;R)/F^1\hom^q(E;R)$ where $F^1\hom^q(E;R)=\ker(\hom^q(E;R)\to\hom^q(E_0;R))$ where $E_0=F$. In other words,
    $$E_\infty^{0,q}\simeq\im(\hom^q(E;R)\to\hom^q(F;R))=\hom^q(F;R)\simeq E_2^{0,q},$$
    from which we see that $d_2(b)=0$ for all $b\in E_2^{0,q}$ (so $E_2^{0,q}$ survives to the $E_\infty$-page). Thus, $d_2=0$ in all degrees, so the $E_2$-page is the $E_\infty$-page! This is almost enough for us to conclude that
    $$\hom^n(E;R)\simeq\bigoplus_{p+q=n}E_\infty^{p,q}=\bigoplus_{p+q=n}E_2^{p,q}\simeq\bigoplus_{p+q=n}\hom^p(B;R)\otimes_R\hom^q(F;R)$$
    which would exactly give the claim. In orer to actually conclude this claim, recall that $E_\infty^{p,q}\simeq G^p\hom^{p+q}(E;R)$ are successive quotients in a filtration 
    $$0\subset F^{p+q}\hom^{p+q}(E;R)\subset F^{p+q-1}\hom^{p+q}(E;R)\subset\dots\subset F^0\hom^{p+q}(E;R)=\hom^{p+q}(E;R).$$
    of $\hom^{p+q}(E;R)$. In particular, we have exact sequences
    $$0\too F^{k+1}\hom^n(E;R)\too F^k\hom^n(E;R)\too E_\infty^{k,n-k}\too0.$$
    Since $E_{\infty}^{k,n-k}\simeq\hom^k(B;R)\otimes_R\hom^{n-k}(F;R)$, the above sequence splits via the map $\sigma:E_\infty^{k,n-k}\to F^k\hom^n(E;R)$ given by $\sigma(\alpha\otimes\beta)=\pull\pi(\alpha)s(\beta)$ (i.e. $\sigma=f\vert_{E_\infty^{k,n-k}})$, and so
    $$F^k\hom^n(E;R)\simeq F^{k+1}\hom^n(E;R)\oplus E_\infty^{k,n-k}.$$
    Since this holds for all $k$ and $F^{n+1}\hom^n(E;R)=0$, induction shows that indeed
    $$\hom^n(E;R)\simeq\bigoplus_{p+q=n}E_\infty^{p,q}=\bigoplus_{p+q=n}E_2^{p,q}\simeq\bigoplus_{p+q=n}\hom^p(B;R)\otimes_R\hom^q(F;R),$$
    so we win.
</div>
<div class="remark">
    One can rephrase the hypotheses of the above theorem by saying that $\ast\hom(F;R)$ is a finite free $R$-module, and $\pull\iota:\ast\hom(E;R)\to\ast\hom(F;R)$ is surjective.
</div>

Returning to our situation of interest, we have a projective bundle $\P(E)\xto\pi B$ with tautological exact sequence

$$0\too L_E\too\pull\pi E\too Q_E\too0.$$

We observed that, letting $x=c_1(\dual L_E)$, the set $\{1,x,x^2,\dots,x^{n-1},x^n\}\subset\ast\hom(\P(E);\Z)$ freely generates the cohomology of each fiber. Thus, by Leray-Hirsch, $\ast\hom(\P(E);\Z)$ is a free $\ast\hom(B;\Z)$-module with basis $1,x,x^2,\dots,x^{n-1},x^n$. Thus [^10], there must exist some polynomial $p(x)\in\ast\hom(B;\Z)[x]$, say (recall $n+1=\rank E$)

$$p(x)=x^{n+1}+c_1(E)x^n+\dots+c_n(E)x+c_{n+1}(E)$$

such that $\ast\hom(\P(E);\Z)\simeq\ast\hom(B;\Z)[x]/(p(x))$. For now, just think of $c_i(E)\in\hom^{2i}(B;\Z)$ above as notation for the coefficient in this polynomial [^9]. In particular, we have an injection $\ast\hom(B;\Z)\into\ast\hom(\P(E);\Z)$. This gives our link between the cohomology of $B$ and that of $\P(E)$. We saw earlier that if we take $B=BU(n)$ and $E=EU(n)$ (modulo the distinction between a vector bundle and a $U(n)$-bundle), then $\P(E)\simeq BU(n-1)\by BU(1)$, so we are ready to carry out our induction argument.

<div class="remark">
    In this section, there is no reason to stop after only splitting off a single line bundle. Indeed, if you pull $E$ back to not just $\P(E)$ but to $\P(Q_E)$, then the same arguments show that you can split off two line bundles from $E$. Continuing this pattern let's you show that any for any vector bundle $E\to B$, there's some $f:B'\to B$ such that the pullback bundle $E'=\pull fE\to B'$ splits as a sum of $\rank E$ line bundles. Furthermore, inductively applying the cohomology calculation given here shows that we can even form $B'$ such that $\pull f:\ast\hom(B;\Z)\into\ast\hom(B';\Z)$ is an injection.
    <br>
    This phenomenon can be described universally. Let $f:(BU(1))^n\to BU(n)$ be the classifying map for the sum of $n$ copies of the universal line bundle (i.e. the classifying map for the universal sum of $n$ line bundles), and consider any rank $n$ vector bundle $E\to B$. This is pulled back along some classifying map $g:B\to BU(n)$, so we can form the pullback $B'=B\by_{BU(n)}BU(1)^n$.
    $$\begin{CD}
        B' @>h>> B\\
        @Vg'VV @VVgV\\
        BU(1)^n @>>f> BU(n)
    \end{CD}$$
    By construction, the pullback bundle $E'=\pull hE\to B'$ has $g\circ h=f\circ g':B'\to BU(n)$ as its classifying map. Since this map factors through $BU(1)^n$, we see that $E'$ splits as the sum of $n$ line bundles, so we can observe this splitting phenomenon without needing any construction. However, this perspective has the downside that it is potentially harder to see that $B$'s cohomology injects into that of $B'$. This is needed, for example, if you want to reduced proofs of properties of Chern classes of general vector bundles to the case of sums of line bundles.
</div>

## Cohomology of $BU(n)$

Recall that $BU(1)\simeq\CP^\infty$ and so its cohomology ring is $\ast\hom(BU(1);\Z)\simeq\Z[c_1]$ with $c_1\in\hom^2(BU(1);\Z)$ the first Chern class. Also, from the previous section, recall that we have ring isomorphisms

$$\ast\hom(BU(n-1)\by BU(1);\Z)\simeq\ast\hom(BU(n);\Z)[x]/(p_n(x))$$

where $\deg x=2$ (i.e $x\in\hom^2(BU(n-1)\by BU(1);\Z)$) and

$$p_n(x)=x^n+c_1(EU(n))x^{n-1}+\dots+c_{n-1}(EU(n))x+c_n(E)\in\ast\hom(BU(n);\Z)[x]$$

is some polynomial [^11]. Our goal this section is to prove the following.

<div class="theorem">
    $$\ast\hom(BU(n);\Z)\simeq\Z[c_1,c_2,\dots,c_n]$$
    where $c_i=c_i(EU(n))\in\hom^{2i}(BU(n);\Z)$ will be called the <b>$i$th Chern class</b>.
</div>

We already know this in the case $n=1$. Let's see how the argument goes for $n=2$. Here, using Kunneth on the left, we have

$$\Z[c_1,c_1']\simeq\ast\hom(BU(1)\by BU(1);\Z)\simeq\ast\hom(BU(2);\Z)[x]\left./\parens{x^2+c_1(EU(2))x+c_2(EU(2))}\right.$$

with $\deg c_1=\deg c_1'=2=\deg x$. Now, the fibration $\pi:BU(1)\by BU(1)\to BU(2)$ we are using pulls the universal rank $2$ vector bundle $EU(2)$ into a sum $EU(1)\oplus EU(1)$ of two copies of the universal line bundle [^12]. Thus, recalling how we defined $x$ earlier, we see that we can take $x=-c_1\in\hom^2(BU(1);\Z)$ above. That is, $c_1^2-c_1(EU(2))c_1+c_2(EU(2))=0$. Similarly, by symmetry (e.g. the automorphism $BU(1)\by BU(1)\iso BU(1)\by BU(1)$ permuting the factors), we equally see that $(c_1')^2-c_1(EU(2))c_1'+c_2(EU(2))=0$. In other words,

$$x^2+c_1(EU(2))x+c_2(EU(2))=(x+c_1)(x+c_1')=x^2+(c_1+c_2')x+c_1c_1'$$

as polynomials. Matching coefficients, we see that $c_1(EU(2))=c_1+c_1'$ and $c_2(EU(2))=c_1c_1'$ are given by the elementary symmetric polynomials in $c_1,c_1'$. Thus, by Galois theory [^13], $\Z[c_1(EU(2)),c_2(EU(2))]$ gives a polynomial algebra in $\ast\hom(BU(2);\Z)$. We claim this is the whole thing. This follows from a counting argument. We know, from Leray-Hirsch, that

$$\Z[c_1,c_1']\simeq\ast\hom(BU(2);\Z)\otimes\ast\hom(\P^1;\Z)$$

additively (i.e. as graded modules). So, letting $S_k$ denote the degree-$k$ part of a graded ring $S$, (cohomology in odd degrees vanishes)

$$\begin{align*}
k+1
&=\rank_\Z\Z[c_1,c_1']_ {2k}\\
&=\rank_\Z\parens{\ast\hom(BU(2);\Z)\otimes\ast\hom(\P^1;\Z)}_ {2k}\\
&=\rank_\Z\hom^{2k}(BU(2);\Z)+\rank_\Z\hom^{2k-2}(BU(2);\Z)\\
&\ge\rank_\Z\Z[c_1(EU(2)),c_2(EU(2))]_{2k}+\rank_\Z\Z[c_1(EU(2)),c_2(EU(2))]_{2k-2}\\
&=\parens{\floor{\frac k2}+1}+\parens{\floor{\frac{k-1}2}+1}\\
&=k+1.
\end{align*}$$

This shows that $\Z[c_1(EU(2)),c_2(EU(2))]_ n=\hom^n(BU(2);\Z)$ for all $n$, so

$$\ast\hom(BU(2);\Z)\simeq\Z[c_1,c_2]$$

with $c_1=c_1(EU(2))$ and $c_2=c_2(EU(2))$ as desired!

We now handle the general case $n\ge2$. Based on how the $n=2$ case played out, let's update our goal.

<div class="theorem">
    Let $f:BU(1)^n\to BU(n)$ be the classifying map for the sum $EU(1)^{\oplus n}$ of $n$ copies of the universal line bundle. Then, $f$ induces an injection
    $$\pull f:\ast\hom(BU(n);\Z)\into\ast\hom(BU(1)^n;\Z)\iso\Z[\Ith c1_1,\dots,\Ith cn_1]$$
    whose image $\Z[c_1,c_2,\dots,c_n]$ is the polynomial algebra generated by the elementary symmetric polynomials
    $$\begin{matrix}
        c_1(EU(n)) &=& c_1 &=& \Ith c1_1+\Ith c2_1+\dots+\Ith cn_1\\
        c_2(EU(n)) &=& c_2 &=& \Ith c1_1\Ith c2_1+\Ith c1_1\Ith c3_1+\dots+\Ith c{n-1}_1\Ith cn_1\\
        &&\vdots\\
        c_n(EU(n)) &=& c_n &=& \Ith c1_1\Ith c2_1\cdots\Ith cn_1
    \end{matrix}$$
    In particular, $\ast\hom(BU(n);\Z)\iso\Z[c_1,c_2,\dots,c_n]$ with $\deg c_i=2i$.
</div>
<div class="proof4">
    The isomorphism $\hom(BU(1)^n;\Z)\iso\Z[\Ith c1_1,\dots,\Ith cn_1]$ is simply the Kunneth formula since $B(U(1)^n)\simeq(BU(1))^n$. By the previous section, we know we also have an isomorphism
    $$\ast\hom(BU(n-1)\by BU(1);\Z)\simeq\ast\hom(BU(n))[x]\left/\parens{x^n+c_1x^{n-1}+\dots+c_{n-1}x+c_n}\right.$$
    where $c_i=c_i(EU(n))\in\hom^{2i}(BU(n);\Z)$. Since we know the theorem already when $n=1$ (and even when $n=2$), we can inductively assume it holds for $n-1$ (and that $n\ge2$) in order to write
    $$\ast\hom(BU(n-1)\by BU(1);\Z)\simeq\ast\hom(BU(n-1);\Z)\otimes\ast\hom(BU(1);\Z)\simeq\Z[c_1',c_2',\dots,c_{n-1}',e_1]$$
    where the notation $e_1=c_1(EU(1))\in\hom^2(BU(1);\Z)$ is used to avoid a clash with the earlier defined $c_1=c_1(EU(n))\in\hom^2(BU(n);\Z)$. The classifying map $f:BU(1)^n\to BU(n)$ in the theorem statement factors as
    $$BU(1)^n\iso BU(1)^{n-1}\by BU(1)\xto{f'\by\Id}BU(n-1)\by BU(1)\to BU(n)$$
    where $f':BU(1)^{n-1}\to BU(n-1)$ is the classifying map for $EU(1)^{\oplus(n-1)}$. Thus, on cohomology, $\pull f:\ast\hom(BU(n);\Z)\to\ast\hom(BU(1)^n;\Z)$, is given by the composition (say $e_1\mapsto\Ith cn_1$)
    $$\ast\hom(BU(n);\Z)\into\ast\hom(BU(n);\Z)[x]/(p_n(x))\into\Z[\Ith c1_1,\dots,\Ith cn_1],$$
    where
    $$p_n(x)=x^n+c_1x^{n-1}+\dots+c_{n-1}x+c_n\in\ast\hom(BU(n);\Z)[x].$$
    This shows that $\pull f$ is injective, so we only need to show its image is generated by the elementary symmetric polynomials in $\Ith c1_1,\dots,\Ith cn_1$. The polynomial $p_n(x)$ makes sense as a function on $\Z[\Ith c1_1,\dots,\Ith cn_1]$. As in the $n=2$ case handled earlier, from the construction of this polynomial, we easily see that $p_n(-\Ith cn_1)=0$ (since this is the negation of the Chern class of the line bundle being split off). Again, as in the $n=2$ case, there are automorphisms $BU(1)^n\iso BU(1)^n$ given by permuting the factors; this allows us to put any $\ith c_1$ in the role of the split off line bundle, so actually $p_n(-\ith c_1)=0$ for all $i$. Thus, after viewing $p_n$ in the larger ring $\Z[\Ith c1_1,\dots,\Ith cn_1]$ instead of merely $\ast\hom(BU(n);\Z)$, we see that
    $$p_n(x)=\prod_{i=1}^n\parens{x+\ith c_n}.$$
    By matching coefficients, this says exactly that $c_i:=c_i(EU(n))$ is the $i$th elementary symmetric polynomial in the $\Ith cj_n$'s. This shows that $\Z[c_1,c_2,\dots,c_n]$ is in the image of $\pull f$. In order to finish, we need to show that this is the entire image. We do this by another counting argument. As before, we have
    $$\begin{align*}
        \Z[c_1',c_2',\dots,c_{n-1}',e_1]
        &\simeq\ast\hom(BU(n-1)\by BU(1);\Z)\\
        &\simeq\ast\hom(BU(n);\Z)\otimes\ast\hom(\P^{n-1};\Z)
        \supset\Z[c_1,c_2,\dots,c_n]\otimes\Z[x]/(x^n)
    \end{align*}$$
    additively. Keep in mind that $\deg c_i'=2i$, $\deg c_i=2i$, $\deg e_1=2=\deg x$, and cohomology above vanishes in odd degree. Now, observe that (for any $k\ge0$)
    $$\begin{align*}
        \sum_{i=0}^\infty\rank_\Z\Z[c_1',c_2',\dots,c_{n-1}']_{2k-2i}
        &=\rank_\Z\Z[c_1',c_2',\dots,c_{n-1}',e_1]_{2k}\\
        &\ge\rank_\Z(\Z[c_1,c_2,\dots,c_{n-1},c_n][x]/(x^n))_{2k}\\
        &=\sum_{i=0}^{n-1}\rank_\Z\Z[c_1,c_2,\dots,c_{n-1},c_n]_{2k-2i}\\
        &=\sum_{i=0}^{n-1}\sum_{j=0}^\infty\rank_\Z\Z[c_1,c_2,\dots,c_{n-1}]_{2k-2i-2nj}\\
        &=\sum_{i=0}^\infty\rank_\Z\Z[c_1,\dots,c_{n-1}]_{2k-2i}
        .
    \end{align*}$$
    where the first equality above comes from conditioning on the exponent of $e_1$ in a monomial, and the second-to-last one comes from condition on the exponent of $c_n$ in a monomial. Since $\deg c_i=\deg c_i'$ for all $i\le n-1$, we see that all expressions above are equal. This can only mean one thing: the theorem statement must be true!
</div>

# Chern Classes

With the conclusion of the previous section, we have obtained our Chern classes, canonical generators of the cohomology ring $\ast\hom(BU(n);\Z)\simeq\Z[c_1,c_2,\dots,c_n]$. In this section, we will collect a few basic properties of these classes. First, for visibility's sake, let's throw in a definition block.

<div class="definition">
    Let $E\to B$ be a vector bundle with classifying map $f:B\to BU(n)$. Then, for $i\in\{0,1,\dots,n\}$, $E$'s <b>$i$th Chern class</b> is the pullback
    $$c_i(E):=\pull fc_i\in\hom^{2i}(B;\Z)$$
    of the cohomology class $c_i\in\ast\hom(BU(n);\Z)$ constructed in the previous section. Above, $c_0=1\in\hom^0(BU(n);\Z)\simeq\Z$. Putting these together, $E$'s <b>total Chern class</b> is
    $$c(E):=\sum_{i=0}^nc_i(E)=1+c_1(E)+c_2(E)+\cdots+c_n(E)\in\ast\hom(B;\Z).$$
    Finally, if $i>n$ or $i<0$, we let $c_i(E)=0$.
</div>

<div class="proposition" name="Properties of Chern classes">
    The main properties of Chern classes are the following.
    <ol>
        <li> They are functorial, i.e. $\pull fc_i(E)=c_i(\pull fE)$ always. </li>
        <li> They vanish in large degree, i.e. $c_i(E)=0$ if $i>\rank_\C(E)$. </li>
        <li> They vanish for trivial bundles, i.e. $c_i(B\otimes\C^n)=0$ unless $i=0$. </li>
        <li> They satisfy a product formula, i.e. $c(E\oplus F)=c(E)c(F)$. </li>
        <li> If $E$ is the tautological line bundle on $\CP^n$, then $c_1(E)\in\hom^2(\CP^n;\Z)$ is a generator. </li>
    </ol>
</div>
<div class="proof4">
    The only thing that really warrants a proof is 4., so we'll prove that. This will be an application of the splitting principal. Note that the formula $c(E\oplus F)=c(E)c(F)$ amounts to some finite number of polynomial relations, i.e. it boils down to the claim that $c_i(E),c_j(F),c_k(E\oplus F)$ satisfy some polynomials 
    $$p_l(x_1,\dots,x_n,y_1,\dots,y_m,z_1,\dots,z_{n+m})$$ 
    with integral coefficients where $n=\rank E$ and $m=\rank F$. Say $B$ is the base space of $E,F$. By the splitting principal, there exists a space $B'\xto fB$ such that $\pull fE,\pull fF$ both split as a sum of line bundles, and $\pull f:\ast\hom(B;\Z)\into\ast\hom(B';\Z)$ is an injection. By functoriality of Chern classes + injectivity of $\pull f$, this means that
    $$\begin{align*}
        &&&0
        &&=p_l(\pull fc_1(E),\dots,\pull fc_n(E),\pull fc_1(F),\dots,\pull fc_m(F),\pull fc_1(E\oplus F),\dots,\pull fc_{n+m}(E\oplus F))\\
        &&&&&=\pull fp_l(c_1(E),\dots,c_n(E),c_1(F),\dots,c_m(F),c_1(E\oplus F),\dots,c_{n+m}(E\oplus F))\\
        &\implies &&0
        &&= p_l(c_1(E),\dots,c_n(E),c_1(F),\dots,c_m(F),c_1(E\oplus F),\dots,c_{n+m}(E\oplus F))
    \end{align*}$$
    Thus, it suffices to prove the claim in the case that $E$ and $F$ (and hence $E\oplus F$) are both sums of line bundles. By induction, it then suffices to prove this in the case that $E,F$ are themselves both line bundles. Let $f:B\to BU(1)$ and $g:B\to BU(1)$ be the classifying maps for $E,F$, respectively. By functoriality of Chern classes, we can use $(f,g):B\to BU(1)^2$ to reduce from $E,F$ themselves to sum $EU(1)\oplus EU(1)$ of two copies of the universal line bundle. Now, we are done. We showed at the end of the last section that the product formula holds in this case. Indeed, the product formula says that the Chern classes of $EU(1)\oplus EU(1)$ are given by the elementary symmetric functions of the Chern classes of each factor, but this was shown in the last theorem of the previous section.
</div>

We also want to show that $c_1(L\otimes L')=c_1(L)+c_1(L')$ when $L,L'$ are both line bundles. For this, [recall](../brown-rep) [^14] that $BU(1)\simeq\CP^\infty$ also represents second integral cohomology. That is, we have natural isomorphisms (of functors)

$$\hom^2(-;\Z)\simeq[-,\CP^\infty]\simeq B(-)$$

where $[X,\CP^\infty]$ is the set of homotopy classes of maps from $X\to\CP^\infty$ and $B(X)$ is the set of isomorphism classes of principal $U(1)$-bundles. Note that $\hom^2(-;\Z)$ is a functor $\Ho(\push\CW)\to\Ab$; that is, it spits about abelian groups, not just sets. As such, we have an "addition natural transformation" $m:\hom^2(-;\Z)\by\hom^2(-;\Z)\to\hom^2(-;\Z)$ such that, for any $X\in\Ho(\push\CW)$ (say $X$ a topological space with the homotopy type of a CW complex [^15])

$$m_X:\hom^2(X;\Z)\by\hom^2(X;\Z)\to\hom^2(X;\Z)$$

is the usual addition map on cohomology. There's similarly an "inversion natural transformation" $i:\hom^2(-;\Z)\to\hom^2(-;\Z)$ which, on any space $X$, simply sends a cohomology class to its negation. We can use the natural isomorphism $\hom^2(-;\Z)\simeq[-,\CP^\infty]$ to translate these into natural transformations

$$m:[-,\CP^\infty]\by[-,\CP^\infty]\to[-,\CP^\infty]\,\text{ and }\, i:[-,\CP^\infty]\to[-,\CP^\infty]$$

giving a (functorial) group structure to $[X,\CP^\infty]$ for all $X\in\Ho(\push\CW)$ [^16] [^17]. By Yoneda, these must arise from some morphisms (i.e. homotopy classes of continuous maps)

$$m:\CP^\infty\by\CP^\infty\to\CP^\infty\,\text{ and }\, i:\CP^\infty\to\CP^\infty$$

giving $\CP^\infty$ the structure of a group object in $\Ho(\push\CW)$ (an $H$-space?). Furthermore, we can run this same game with $B(-)$ in place of $\hom^2(-;\Z)$ since $B(X)$, for varying $X$, also has a (functorial) group structure given by taking the tensor product of line bundles. Thus, we arrive at a second pair of maps

$$m':\CP^\infty\by\CP^\infty\to\CP^\infty\,\text{ and }\, i':\CP^\infty\to\CP^\infty$$

which also give $\CP^\infty$ the structure of a group object in $\Ho(\push\CW)$. We claim that $(m,i)=(m',i')$, so the natural isomorphism $\hom^2(-;\Z)\simeq B(-)$ is an isomorphism of functors $\Ho(\push\CW)\to\Ab$ and not just of functors $\Ho(\push\CW)\to\Set$; put more concretely, our claim gives immediately that $c_1(L\otimes L')=c_1(L)+c_1(L')$. In order to prove that $(m,i)=(m',i')$, we will show that $\CP^\infty$ has a unique structure as a group object in $\Ho(\push\CW)$.

Recall that $\CP^\infty\simeq K(\Z,2)$ [^18], and so a multiplication map $\mu:\CP^\infty\by\CP^\infty\to\CP^\infty$ corresponds to some element of

$$\hom^2(\CP^\infty\by\CP^\infty;\Z)\simeq\hom^2(\CP^\infty;\Z)\oplus\hom^2(\CP^\infty;\Z)\simeq\Z c_1\oplus\Z c_1'.$$

Denote this element by $\mu=ac_1+bc_1'$ with $a,b\in\Z$. Let $e:\bracks{* }\to\CP^\infty$ be the identity morphism of its group object structure (i.e. a choice of identity element), so 

$$\mu\circ(e\by\Id)=\mu\circ(\Id\by e)=\Id:\CP^\infty\to\CP^\infty.$$

In terms of cohomology, these equalities say exactly that $b=a=1$ [^19], which is to say we must have $\mu=c_1+c_1'$. Thus, $\CP^\infty$ has a unique structure as a group object in $\Ho(\push\CW)$, so $(m,i)=(m',i')$, so $c_1(L\otimes L')=c_1(L)+c_1(L')$ ultimately by abstract nonsense + $\CP^\infty$ having simple cohomology.

<div class="exercise">
    Let $E=L_1\oplus L_2\oplus\dots\oplus L_n$ be a sum of $n$ line bundles. Then,
    $$\Wedge^kE=\bigoplus_{1\le i_1<\dots< i_k\le n}L_{i_1}\otimes\cdots\otimes L_{i_k},$$
    and so
    $$c\parens{\Wedge^kE}=\prod_{1\le i_1<\dots< i_k\le n}c(L_{i_1}\otimes\cdots\otimes L_{i_k})=\prod_{1\le i_1<\dots< i_k\le n}(1+x_{i_1}+\dots+x_{i_k})$$
    where $x_i=c_1(L_i)$. Notice that the RHS is invariant under the action of the symmetric group of $n$ elements (i.e. permuting the $x_i$ doesn't change the end result), and so gives a polynomial in the Chern classes $c_1(E),\dots,c_n(E)$ of $E$. That is,
    $$c\parens{\Wedge^kE}=Q(c_1(E),\dots,c_n(E))$$
    for some $Q\in\Z[t_1,\dots,t_n]$. Using the splitting principle to show the above equality holds for all rank $n$ vector bundles $E$. In particular, conclude that $c_1(\det E)=c_1(E)$ for all vector bundles $E$ where $\det E=\Wedge^{\rank E}E$.
    <br>
    If you feel like, do the same thing for tensor or symmetric powers of line bundles.
</div>
<div class="remark">
    Some people don't like filtering vector bundles by rank (i.e. considering $BU(n)$ for some fixed $n$), and would rather just look at all (finite-rank) vector bundles at once. In order to do this, on first observes that $c(\underline\C^n)=1$, where $\underline\C^n$ is the trivial rank $n$ vector bundle on some base space $B$, since $\underline\C^n$ is the pullback of the vector bundle $\C^n\by\{*\}\to\{*\}$ on the one point space (whose cohomology classes obviously vanish); hence,
    $$c(E\oplus\underline\C^n)=c(E)c(\underline\C^n)=c(E),$$
    which means that characteristic class are a "stable" phenomenon. In order to leverage this, note that there is a map $BU(n)\to BU(n+1)$ which, in the moduli perspective, sends a rank $n$ vector bundle $E$ to the rank $(n+1)$ vector bundle $E\oplus\underline\C$ (i.e. it's the classifying map for the rank $(n+1)$ vector bundle $EU(n)\oplus\underline\C$ on $BU(n)$). By our observation, this map preserves Chern classes, and so Chern classes continue to be well-defined as cohomology classes of the colimit $BU:=\dirlim_{n\to\infty}BU(n)$. One can show that this space characterizes stable isomorphism classes of vector bundles ($E$ and $E'$ are <b>stably isomorphic</b> if $E\oplus\underline\C^n\simeq E'\oplus\underline\C^m$ for some $n,m\ge0$), and that its cohomology group is
    $$\ast\hom(BU)\simeq\Z[c_1,c_2,c_3,\dots]\,\,\text{ with }\,\,\deg c_k=2k.$$
    In this way, all Chern class come from a single space, and so one is able to consider all (finite rank) vector bundles (up to stable isomorphism) at once.
</div>

# Orientation and Sphere Bundles

Let's now switch gears. We've had some fun defining Chern classes, but didn't really see how they can be applied to concrete problems. To remedy this defect, we won't take a look at applications of Chern classes; instead, we'll define a new characteristic class called the Euler class, and then look at some of its applications. 

The Euler class is defined for sphere bundles, but, as we will see later, one can easily make sense of the Euler class of an (oriented) vector bundle as well. For this section, we will be working with real vector bundles instead of complex ones. Do not worry though; we will get back to $\C$ soon enough.

<div class="notation">
    Taking inspiration from field theory, given a (real or complex) vector bundle $E\to B$, we will let $\units E\subset E$ denote all nonzero elements of $E$ (so $\units E=E\sm\sigma_0(B)$ where $\sigma_0:B\to E$ is the zero section) and similarly let $\units F\subset F$ denote the nonzero elements of a fiber $F$ which is simply $\R^n$ or $\R^{2n}$, up to homeomorphism.
</div>
<div class="remark">
    The cohomological long exact sequence of the pair $(\R^n\sm\{0\},\R^n)$ includes
    $$\hom^{k-1}(\R^n;\Z)\too\hom^{k-1}(\R^n\sm\{0\};\Z)\too\hom^k(\R^n,\R^n\sm\{0\};\Z)\too\hom^k(\R^n;\Z)\too\hom^k(\R^n\sm\{0\};\Z).$$
    Since $\R^n$ is contractible and $\R^n\sm\{0\}\simeq S^{n-1}$ (homotopy equivalent), we conclude that
    $$\hom^k(\R^n,\R^n\sm\{0\};\Z)\simeq\twocases\Z{k=n}0.$$
    As a consequence, if $E\to B$ is a rank $n$ real vector bundle, and $F$ is any fiber, then also 
    $$\hom^k(F,\units F;\Z)\simeq\twocases\Z{k=n}0.$$
</div>
<div class="definition">
    Let $\pi:E\to B$ be a real vector bundle of rank $n$. An <b>orientation</b> on $E$ is a "consistent choice of generators of $\hom^n(E_b;\units E_b)$" as $b$ ranges over $B$. That is, it is a choice of generators $u_b\in\hom^n(E_b;\units E_b)$ such that for around each $b\in B$, there is a neighborhood $b\in U\subset B$ and a cohomology class $u_U\in\hom^n(\inv\pi(U),\units{\inv\pi(U)};\Z)$ such that $u_U\vert_{(E_b,\units E_b)}=u_b$ for all $b\in U$. If $E$ admits an orientation, is is called <b>orientable</b>. If it an orientation is chosen, then it is called <b>oriented</b>.
</div>
<div class="remark">
    One can equivalently define an orientable real vector bundle as one who can be given transition functions with value in $\SO(n)$. In this perspective, it is easy to see that a real line bundle is orientable iff it is trivial, and that a general real vector bundle $E$ is orientable iff its determinant bundle $\det E:=\Wedge^{\rank E}E$ is orientable (i.e. trivial).
</div>

I claimed the Euler class is naturally defined for sphere bundles, so I should at least say what a sphere bundle is.

<div class="definition">
    A <b>sphere bundle</b> $\pi:E\to B$ is a fiber bundle with fiber $F\simeq S^n$ for some $n$. If we want to specify the dimension of the fiber, we may call this an <b>$S^n$-bundle</b> instead. In particular, an $S^0$-bundle is the same thing as a degree 2 covering space.
</div>
<div class="definition">
    An $S^n$-bundle $\pi:E\to B$ is called <b>orientable</b> if one can find a compatible choice of local generators for the cohomology of a fiber. That is, it is orientable if there exists cohomology classes $\sigma_b\in\hom^n(E_b;\Z)$ (recall, $E_b:=\inv\pi(B)\simeq S^n$) generating the cohomology of the fiber and satisfying the following condition: for each point $b\in B$, there is some contractible open $U\subset B$ containing $b$ with $E\vert_U\simeq U\by S^n$ which has a generator $\sigma_U\in\hom^n(E\vert_U;\Z)$ such that $\sigma_U\vert_b=\sigma_b$ for all $b\in U$. A choice of compatible local generators is called an <b>orientation</b> and $E$ along with such a choice is said to <b>oriented</b>. 
</div>
<div class="remark">
    If $E$ has a global cohomology class which restricts to a generator of the cohomology of each fiber, then $E$ is oriented and furthermore, Leray-Hirsch tells us that
    $$\ast\hom(E;\Z)\simeq\ast\hom(B;\Z)\otimes\ast\hom(S^n;\Z).$$
</div>
<div class="remark">
    The orthogonal group $O(n+1)$ acts on $S^n$, and so some sphere bundles have $O(n+1)$ as their structure group. However, not every sphere bundle is (isomorphic to) one for which this is the case; sometimes the structure group is legitimately bigger than this. However, to define the Euler class, we will need a sphere bundle whose structure group is $SO(n+1)$.
</div>

Before defining Euler classes, let's tease out the relationship(s) between sphere bundles (the natural homes for Euler classes), real line bundles (the vector bundle analogue of sphere bundles), and complex line bundles (the things I care about).

<div class="definition">
    Let $E\to B$ be a rank $(n+1)$ vector bundle. Then, one can form its <b>unit sphere bundle</b> $S(E)$ which is, up to homotopy, just $E$ minus its zero section (i.e. $\units E$). This is an $S^n$-bundle with structure group $O(n+1)$. This is called the unit sphere bundle because, if you give $E$ a Riemannian metric, it is isomorphic to the sphere bundle obtained by restricting each fiber of $E$ to its unit sphere.
</div>
<div class="proposition">
    A vector bundle $E\to B$ is orientable if and only if $S(E)$ is orientable.
</div>
<div class="proof4">
    This is really just an earlier remark that, by looking at the long exact sequence of the pair $(F,\units F)$, we have a natural isomorphism
    $$\hom^{k-1}(\units F;\Z)\iso\hom^k(F,\units F;\Z).$$
    This let's you carry orientation back and forth between $E$ and $S(E)$.
</div>
<div class="corollary">
    A vector bundle $E\to B$ is orientable if and only if $S(\det E)$ is a disconnected double cover of $B$.
</div>
<div class="corollary">
    Every vector bundle over a simply connected base is orientable.
</div>

What about complex vector bundles? Well, given a complex vector bundle $E\to B$ of rank $n$, let $E_\R\to B$ be its underlying real vector bundle (of rank $2n$). This bundle is always orientable (and even oriented). Let $e_1,\dots,e_n$ be a complex basis of $E_b$, so $e_1,ie_i,e_2,ie_2,\dots,e_n,ie_n$ gives a real basis of $(E_\R)_ b$. This defines a canonical orientation of this fiber [^21]. One can turn this into a cohomology class by considered an (orientation-preserving) map $\Delta^n\to((E_\R)_ b,\punits{E_\R}_ b)$ which represents a homology class $\alpha$, and then considering the unique cohomology class $u_b\in\hom^n((E_\R)_ b,\punits{E_\R}_ b)$ which is a generator and satisfies $\angles{u_b,\alpha}=1$. From naturality of this construction (i.e. it not depending on the complex basis you choose in the beginning), one can show that it gives an orientation of $E_\R\to B$. Hence, for any complex vector bundle $E$, we can obtain an oriented sphere bundle $S(E_\R)$, and so we will be able to make sense of the Euler class of a complex vector bundle.

This concludes our prelims on sphere bundles, so let's actually define the Euler class now.

# Euler Class

We'll construct the Euler class in a bit of an unusual way. I think one usually first proves a "Thom isomorphism" relating the cohomology of the total space of an oriented real vector bundle $E\to B$ with that of the pair ($E,\units E$) (shifted up $\rank E$ places) via cupping with an "orientation class" $u\in\hom^n(E,\units E;\Z)$. Then, one uses the natural maps $\hom^n(E,\units E;\Z)\to\hom^n(E;\Z)\iso\hom^n(B;\Z)$ to define the Euler class as the image of $u$ in $\hom^n(B;\Z)$. However, I looked up a proof of the existence of this orientation class, and the one I saw seemed long and annoying to the read... so um, we're gonna do something else and hope no complications arise when we try to prove things about it.

We'll construct the Euler class via an exercise in my [spectral sequence post](../spectral-seq). Namely, we'll show that oriented sphere bundles come equipped with a natural long exact sequence in cohomology, and then the Euler class will arise as the image of $1\in\hom^0(B;\Z)$ under a map appearing in this exact sequence.

<div class="theorem" name="Gysin sequence">
    Let $S^n\to E\to B$ be an oriented $S^n$ bundle. Then, there exists an exact sequence
    $$\cdots\too\hom^p(B;\Z)\xtoo\alpha\hom^p(E;\Z)\xtoo\beta\hom^{p-n}(B;\Z)\xtoo\d\hom^{p+1}(B;\Z)\too\cdots$$
</div>
<div class="proof4">
    We'll construct this using the Serre spectral sequence, so we first need to know that $\pi_1(B)$ acts trivially on $\ast\hom(S^n;\Z)$. This follows from $E$ being oriented. Locally, $E$ looks like $S^n\by U$ (for $U\subset B$ open) and so loops on $B$ locally do nothing to $\ast\hom(S^n)$. Since we have a consistent choice of generator for $\hom^n(S^n;\Z)$ (the only nonzero (reduced) cohomology group), any $\gamma\in\pi_1(B)$ will take the preferred generator on $S^n\by U$ to the preferred generator on $S^n\by V$ when in the overlap $U\cap V$, and so we see that $\gamma$ acts by the identity on cohomology.
    <br>
    We can know form the Serre spectral sequence $E_2^{p,q}=\hom^p(B;\hom^q(S^n;\Z))\implies\hom^{p+q}(E)$. We have $E_2^{p,q}=0$ when $q\not\in\{0,n\}$ and so the only page with non-trivial differentials (remember the $E_k$ page has differentials with bidegree $(k,1-k)$) is the $E_{n+1}$ page. Its differentials look like
    $$\begin{CD}
        0 @>>> E_{n+1}^{p,n} @>\d_{n+1}>> E_{n+1}^{p+n+1,0} @>>> 0\\
        @. @| @|\\
        0 @>>> \hom^p(B;\Z) @>>> \hom^{p+n+1}(B;\Z) @>>> 0
    \end{CD}$$
    Thus, the objects of the $E_{n+2}=E_\infty$ page are
    $$E_\infty^{p,q}=\begin{cases}
        \hom^p(B;\Z)/\im\d_{n+1} &\text{if }q=0\\
        \ker\d_{n+1} &\text{if }q=n\\
        0&\text{otherwise}
    \end{cases}$$
    Thus, the only nonzero objects of the $p$-diagonal of the $E_\infty$-page are
    $$E_\infty^{p,0}=\hom^p(B;\Z)/\im\d_{n+1}\,\,\text{ and }\,\,E_\infty^{p-n,n}=\ker\d_{n+1}.$$
    The elements of the $p$-diagonal of the $E_\infty$-page are successive quotients in a filtration
    $$0\subset F^p\hom^p(E;\Z)\subset F^{p-1}\hom^p(E;\Z)\subset\cdots\subset F^0\hom^p(E;\Z)=\hom^p(E;\Z),$$
    so but most of quotients are $0$. In particular, $E_\infty^{k,p-k}=F^k\hom^p(E)/F^{k+1}\hom^p(E)=0$ for all $k\not\in\{p,p-n\}$, so the above filtration really looks like
    $$0\subset F^p\hom^p(E;\Z)=\cdots=F^{p-n+1}\hom^p(E;\Z)\subset F^{p-n}\hom^p(E;\Z)=\cdots=\hom^p(E;\Z).$$
    Since $F^p\hom^p(E;\Z)\simeq E_\infty^{p,0}$, we have the following exact sequence
    $$\begin{CD}
        0 @>>> F^{p-n+1}\hom^p(E;\Z) @>>> F^{p-n}\hom^p(E;\Z) @>>> E_\infty^{p-n,n} @>>> 0\\
        @. @| @| @| \\
        0 @>>> \hom^p(B;\Z)/\im\d_{n+1} @>\alpha'>> \hom^p(E;\Z) @>\beta'>> \ker\d_{n+1} @>>> 0
    \end{CD}$$
    At this point, we are basically done. Consider the compositions
    $$\alpha:\hom^p(B;\Z)\to\hom^p(B;\Z)/\im d_{n+1}\xto{\alpha'}\hom^p(E;\Z)$$
    and
    $$\beta:\hom^p(E;\Z)\xto{\beta'}\ker d_{n+1}\into\hom^{p-n}(B;\Z).$$
    These fit into a sequence
    $$\cdots\too\hom^{p-n-1}(B;\Z)\xtoo{d_{n+1}}\hom^p(B;\Z)\xtoo{\alpha}\hom^p(E;\Z)\xtoo{\beta}\hom^{p-n}(B;\Z)\xtoo{d_{n+1}}\hom^{p+1}(B;\Z)\too\cdots$$
    which we claim is exact. First, $\alpha'$ is injective, so we have $\ker\alpha=\im\d_{n+1}$ which gives exactness at $\hom^p(B;\Z)$. Second, $\ker\beta=\ker\beta'=\im\alpha'=\im\alpha$ so we get exactness as $\hom^p(E;\Z)$ as well. Finally, $\beta'$ is surjective so $\im\beta=\ker\d_{n+1}$ which gives exactness at $\hom^{p-n}(B;\Z)$. Thus the above long sequence is exact everywhere, and we win.
</div>
<div class="definition">
    Let $E\to B$ be an oriented $S^n$-bundle. Then its <b>Euler class</b> $e(E)\in\hom^{n+1}(B;\Z)$ is defined as the image of $1\in\hom^0(B;\Z)$ under the map $\d:\hom^0(B;\Z)\to\hom^{n+1}(B;\Z)$ constructed above (this is the differential on the $E_{n+1}$-page of the Serre spectral sequence).
</div>
<div class="remark">
    The reason the above definition is well-defined is that the $\hom^0(B;\Z)$ in this long exact sequence is really $\hom^0(B;\hom^n(S^n;\Z))$ which has a canonical generator (i.e. canonical choice of $1$) exactly because $S^n\to E\to B$ is oriented. When I say that $e(E)=\d(1)$ (the image of $1\in\hom^0(B;\Z)$), this is really saying that $e(E)=\d(u)$ where $u\in\hom^n(S^n;\Z)$ (recall $\hom^0(B;\hom^n(S^n;\Z))\simeq\hom^n(S^n;\Z)$ with the isomorphism once again canonical) is the preferred generator.
</div>
<div class="remark">
    Note that if $e(E)=0$, then by exactness, there's some $a\in\hom^n(E;\Z)$ such that $\beta(a)=1\in\hom^0(B;\Z)$, but as we mentioned above $\hom^0(B;\Z)\simeq\hom^n(S^n;\Z)$ with $1$ if the former corresponding to the preferred generator $u$ of the latter. Thus, if $e(E)=0$, we get a global cohomology class $a\in\hom^n(E;\Z)$ restricting to the preferred generator on each fiber. In this way, the Euler class is an "obstruction to the existence of such a global class" or a "measure of how twisted $E$ is" or "something like that." Note that, by Leray-Hirsch, this shows that $e(E)=0$ entails that $\ast\hom(E;R)$ is a free $\ast\hom(B;R)$-module with basis $u\in\hom^n(S^n;\Z)$, i.e. there are isomorphisms
    $$\hom^k(B;\Z)\iso\hom^{n+k}(E;\Z)$$
    sending $\hom^k(B;\Z)\ni\alpha\longmapsto\pull\pi(\alpha)\smile a\in\hom^{n+k}(E;\Z)$ when $e(E)=0$.
</div>
<div class="remark">
    Let $E\to B$ be an oriented $S^n$-bundle, and let $\bar E\to B$ denote $E$ with the reverse orientation. This amounts to negating the choice of preferred generator of $\hom^n(S^n;\Z)$, so we see that $e(\bar E)=-e(E)$.
</div>
<div class="exercise">
    I don't know how hard this is because I've never tried doing it myself, but show that the map $\d:\hom^k(B;\Z)\to\hom^{k+n+1}(B;\Z)$ above is given by taking the cup product with the Euler class.<br>Also show that $\alpha:\hom^p(B;\Z)\to\hom^p(E;\Z)$ is just the pullback $\pull\pi$ along the projection $\pi:E\to B$.<br>When $p=n$, the sequence includes the map $\beta:\hom^n(E;\Z)\to\hom^0(B;\Z)$. Show that composing this with the natural map $\hom^0(B;\Z)\iso\hom^n(S^n;\Z)$ gives the usual restriction map $\hom^n(E;\Z)\to\hom^n(S^n;\Z)$.
</div>

The only property of the Euler class that I think we will need to know for now is that it is functorial. The point here is that the Serre spectral sequence is itself functorial (this is clear from its construction), and so given a pullback

$$\begin{CD}
    S^n @>>> \pull fE @>>> B'\\
    @| @VVgV @VVfV \\
    S^n @>>> E @>>> B
\end{CD}$$

of sphere bundles, one obtains a commutative square.

$$\begin{CD}
    \hom^0(B';\Z) @>\d>> \hom^{n+1}(B';\Z)\\
    @A\pull fAA @AA\pull fA \\
    \hom^0(B;\Z) @>>\d> \hom^{n+1}(B;\Z)
\end{CD}$$

The left vertical map sends $1\mapsto1$, and so by commutativity, we see that

$$\pull fe(E)=\pull f\d(1)=\d\pull f(1)=\d(1)=e(\pull fE),$$

which says exactly that the Euler class is functorial. [^23]

Now that we have seen a direct construction of the Euler class, let's return to this whole "Thom isomorphism" thing I alluded to earlier. The main point of this thing was/is to construct a Thom/orientation class $u\in\hom^n(E,\units E;\Z)$ for an oriented vector bundle $E\to B$. I prefer to think in terms of sphere bundles, so we are really after a certain cohomology class $u\in\hom^n(D(E), S(E);\Z)$ where, given a rank $n$ oriented vector bundle $E\to B$, $S(E)$ as usual denotes its associated unit sphere bundle and $D(E)$ denotes its analogously defined unit disk bundle $D(E)\to B$ (with fibers homeomorphic to the $n$-disk, $D^n$). Let's take things one step further. Say, as has been the case in this section, we start with an oriented $S^n$ bundle $E\to B$ instead. How should we obtain a Thom class now? The first thing we would like to do is "fill in" the fibers of this bundle in order to obtain a $D^{n+1}$-bundle $D(E)\to B$ with $E$ as its "fiberwise  boundary." Then, the Thom class will be a certain cohomology class $u\in\hom^{n+1}(D(E),E;\Z)$ [^33].

<div class="proposition">
    Let $\pi:E\to B$ be an $S^n$-bundle. Then, there exists a $D^{n+1}$-bundle $p:D(E)\to B$ with an inclusion $E\into D(E)$ realizing $\inv\pi(b)$ as the boundary of $\inv p(b)$ for all $b\in B$.
</div>
<div class="proof4">
    Let's begin with a bit of intuition; the actual proof will be rather short. We want to "fill in" the fibers of $\pi$, and topologically, this corresponds to forming the cones $C\inv\pi(b)\cong CS^n\cong D^{n+1}$ where, in general for a top. space $X$,
    $$CX:=(X\by I)/(X\by\{0\}).$$
    Hence, one way to form $D(E)$ would be simply take the cones on each fiber (over a local trivialization) and then glue these together by lifting $\pi$'s transition functions from the fibers to their cones. However, it would be preferable to perform some global construction directly to $E$ which replaces all fibers with their cones. The key observation here is as follows: to form the cone of a fiber, you first form its cylinder and then collapse one end of the cylinder (i.e. one copy of the fiber) to a point. Since the map $\pi:E\to B$ already collapses each fiber to a (different) point, you can form the "global" cylinder $E\by I$ and then simply identity points by their $\pi$-image in $B$ in order to form the cones of all the fibers at once.
    <br>
    With that said, let $D(E):=M_\pi$ be the mapping cylinder
    $$M_\pi:=(E\by I)\cup_{(E\by\{0\})}B=\parens{(E\by I)\sqcup B}/((e,0)\sim\pi(e)),$$
    and let $p:D(E)\to B$ be the natural "projection to the base" map (i.e. $p(e,t)=\pi(e)$ for $(e,t)\in E\by I$ and $p(b)=b$ when $b\in B$). Then, by construction, for any $b\in B$, we have
    $$\inv p(b)=M_{\pi\vert_{\inv\pi(b)}}=(\inv\pi(b)\by I)\cup_{(\inv\pi(b)\by\bracks0)}\bracks b=(\inv\pi(b)\by I)/(\inv\pi(b)\by\bracks0)=C\inv\pi(b)\cong D^{n+1}.$$
    Furthermore, by restricting the locally trivial neighborhoods for $\pi$, we see that $p$ is still a fiber bundle. Finally, the map $E\into D(E)$ is simply $e\mapsto(e,1)$.
</div>

At this point, we will take some things on faith to avoid repeating ourselves [^34]. Let $\pi:E\to B$ be an oriented $S^n$-bundle as usual. By the proposition above, we have a "fiber sequence pair" $(D^{n+1}, S^n)\to(D(E), E)\to B$. Given this, just as we used the Serre spectral sequence for the fibration $S^n\to E\to B$ in order to construct the Euler class, one can use the Serre spectral for the fiber sequence pair $(D^{n+1}, S^n)\to(D(E), E)\to B$ (i.e. a spectral sequence $E_2^{p,q}=\hom^p(B;\hom^q(D^{n+1},S^n;\Z))\implies\hom^{p+q}(D(E),E;\Z)$) to construct a Thom class $u=u(E)\in\hom^{n+1}(D(E),E;\Z)$ [^35]. This Thom class is constructed so that the map [^37]

$$\mapdesc{\phi}{\hom^p(B;\Z)}{\hom^{p+n+1}(D(E),E;\Z)}{\alpha}{\pull\pi(\alpha)\smile u}$$

is an isomorphism for all $p$. Furthermore, this map gives the below isomorphism of exact sequences between the Gysin sequence and the long exact sequence for the pair $(D(E),E)$. Recall that $(D^{n+1},S^n)\to(D(E),E)\xto{(p,\pi)}B$ is our pair of fiber bundles over $B$, and that the fibration $p:D(E)\to B$ is a homotopy equivalence since the fiber is contractible.

$$\begin{CD}
    \cdots @>>> \hom^p(B;\Z) @>\pull\pi>> \hom^p(E;\Z) @>>> \hom^{p-n}(B;\Z) @>\smile e(E)>> \hom^{p+1}(B;\Z) @>>> \cdots\\
    @. @V\pull pVV @V\Id VV @VV\phi V @VV\pull pV\\
    \cdots @>>> \hom^p(D(E);\Z) @>>> \hom^p(E;\Z) @>>> \hom^{p+1}(D(E),E;\Z) @>>> \hom^{p+1}(D(E);\Z) @>>> \cdots
\end{CD}$$

In particular, the Euler class $e(E)\in\hom^{n+1}(B;\Z)$ is the preimage of the restriction $u(E)\vert_{D(E)}\in\hom^{n+1}(D(E);\Z)$ of the Thom class to the total space.

## Relation to Chern Classes

We haven't thought about classifying spaces in a while; let's change that. Let $E\to B$ be a rank $n$ complex vector bundle. This gives rise to an oriented $S^{2n-1}$-bundle $S(E_\R)\to B$, and so we can define the <b>Euler class</b> of the complex vector bundle $E\to B$ as

$$e(E):=e(S(E_\R))\in\hom^{2n}(B;\Z).$$

We saw at the end of the last section that the Euler class is functorial as a cohomology class of sphere bundles, and this extends to its functoriality as a cohomology class of complex vector bundles. Thus, just as with all characteristic classes of complex vector bundles, the Euler class (on complex vector bundles) must really correspond to some universal cohomology class

$$e\in\hom^{2n}(BU(n);\Z)\simeq\Z[c_1,c_2,\dots,c_n]_ {2n}\,\,\,\,\text{ where }c_i\in\hom^{2i}(BU(n);\Z).$$

We aim to figure out which class it is. Necessarily, $e=p(c_1,c_2,\dots,c_n)$ is some polynomial in the Chern classes, and so we just need to determine which one it is. Determining a polynomial in Chern classes is exactly the type of situation one uses the splitting principle for, and so we are instantly reduced to determining the Euler class of a sum $L_1\oplus\dots\oplus L_n$ of line bundles. This will have two parts; what's the Euler class of a line bundle, and what's the Euler class of a sum of 2 line bundles? Once we know these, we just induct and have our answer in general.

We will start with computing the Euler class of a sum of line bundles, so let $L_1\xto{\pi_1}B$ and $L_2\xto{\pi_2}B$ be complex line bundles. Note that their "internal direct sum" $L_1\oplus L_2\to B$ is the pullback of their "external direct sum" $L_1\by L_2\to B\by B$ along the diagonal map $\Delta:B\to B\by B,b\mapsto(b,b)$. That is, we have a pullback diagram.

$$\begin{CD}
    L_1\oplus L_2 @>>> L_1\by L_2\\
    @V\pi_1\oplus\pi_2VV @VV\pi_1\by\pi_2V\\
    B @>>\Delta> B\by B
\end{CD}$$ 

Now, we can compute $e(L_1\oplus L_2)$ using functoriality + knowledge of the cohomology of a product. We have $\ast\hom(B\by B;\Z)\simeq\ast\hom(B;\Z)\otimes\ast\hom(B;\Z)$ and, by considering the two projections $B\by B\rightrightarrows B$, one sees that $e(L_1\by L_2)=e(L_1)\otimes e(L_2)\in\hom^4(B\by B;\Z)$. Pulling back along the diagonal maps corresponds to taking cup products, so

$$e(L_1\oplus L_2)=\pull\Delta e(L_1\by L_2)=e(L_1)\smile e(L_2)\in\hom^4(B;\Z).$$

Thus, in general, the Euler class $e(L_1\oplus L_2\oplus\cdots\oplus L_n)$ of a sum is the product $e(L_1)e(L_2)\dots e(L_n)$ of the Euler classes.

We still need to determine the Euler class of a line bundle in terms of its first Chern class. That is, it is clear that $e(L)=kc_1(L)$ for some $k\in\Z$ independent of $L$, but we still don't know $k$ [^24]. Luckily, we can determine $k$ by looking at a simple universal case. Recall that $BU(1)\simeq\CP^\infty$, and let $\iota:\CP^1\into\CP^\infty\simeq BU(1)$ be the natural inclusion map, so $\pull\iota:\hom^2(BU(1);\Z)\iso\hom^2(\CP^1;\Z)$ is an isomorphism. Thus, we are reduced to determining the Euler class of the tautological line bundle $E\to\CP^1$ on $\CP^1$. This is the line bundle whose fiber above a point $\l\in\CP^1$ is the line $\l\subset\C^2$ represented by that point. Hence, by definition, we see that the sphere bundle $S(E_\R)$ associated to it is the Hopf fibration

$$S^1\to S^3\to S^2.$$

The Euler class of this bundle comes from the differential on the $E_2$-page of its Serre spectral sequence. That page looks like

$$\begin{array}{c | c c c c}
    \tbf q & \\
    1 & \hom^0(S^2;\hom^1(S^1))\simeq\Z a & 0 & \hom^2(S^2;\hom^1(S^1))\simeq\Z c_1a\\
    0 & \hom^0(S^2;\hom^0(S^1))\simeq\Z & 0 & \hom^2(S^2;\hom^0(S^1))\simeq\Z c_1 \\\hline
    & 0 & 1 & 2 & \tbf p
\end{array}$$

where $a\in\hom^2(S^1)$ is the preferred generator and $c_1\in\hom^2(S^2)$ is the first Chern class of the tautological line bundle $E\to\CP^1\simeq S^2$. The only nontrivial differential on this page (or any page thereafter) is $\d_2:\Z a\to\Z c_1$. Since neither $\Z a$ nor $\Z c_1$ survive to the $E_\infty$-page (the $1$- and $2$-diagonals of the $E_\infty$-page are all $0$ since $\hom^2(S^3)=\hom^1(S^3)=0$), we see that this map must be an isomorphism, so $d_2(a)=\pm c_1$. Since, by definition, $e(E)=d_2(a)$, we see that $e(E)=\pm c_1(E)$.

Thus, for a general complex line bundle $L\to B$, we have $e(L)=\pm c_1(L)$. In particular, if $L$ is given the "correct" orientation, then $e(L)=c_1(L)$. Since $L$, being a complex line bundle, comes equipped with a canonical orientation, one suspects that this one (its complex orientation) is the correct one, and so that we can safely write $e(L)=c_1(L)$ (implicitly endowing $L$ with its complex orientation). This is indeed the case, but I'm not sure if we will be able to show it [^27].

In any case, we can cheat. Let's just adopt the convention that when we write $e(L)$ for $L$ a complex line bundle, we're implicitly taking its Euler class with respect to the "correct" orientation (i.e. always $L$'s complex orientation or never $L$'s complex orientation), and, having adopted this convention, we can now safely write $e(L)=c_1(L)$. Combining this with the fact that $e(L_1\oplus L_2)=e(L_1)e(L_2)$ and with the splitting principal, one sees that for a general complex vector bundle $E\to B$, we have [^28]

$$e(E)=c_n(E).$$

## Relation to Obstruction Theory

This sign issue we ran into will be resolved in the next section. In the current one, we'll look at what might be our first actual application of characteristic classes in this post: the Euler class gives an obstruction to the existence of (non-vanishing) sections. In other words, if your Euler class is nonzero, then your sphere bundle has no sections.

<div class="theorem">
    Let $S^n\to E\xto\pi B$ be an oriented sphere bundle with a section $\sigma:B\to E$. Then, $e(E)=0\in\hom^{n+1}(B;\Z)$.
</div>
<div class="proof4">
    Recall that the Euler class originates from the Gysin sequence
    $$\cdots\too\hom^0(B;\Z)\xtoo\d\hom^{n+1}(B;\Z)\xtoo\alpha\hom^{n+1}(E;\Z)\too\cdots$$
    where, as per an exercise, $\alpha=\pull\pi:\ast\hom(B;\Z)\to\ast\hom(E;\Z)$. Since $\pi\circ\sigma=\Id_B$, we see that $\pull\sigma\circ\pull\pi=\Id_{\ast\hom(B;\Z)}$ so $\pull\pi$ is injective (in all degrees). By exactness of the above sequence, this shows that $\d:\hom^0(B;\Z)\to\hom^{n+1}(B;\Z)$ is the zero map, so $e(E)=\d(1)=0$.
</div>
<div class="corollary">
    Let $E\to B$ be an oriented real vector bundle with a non-vanishing section. Then, $e(E)=0$.
</div>
<div class="corollary">
    Let $E\to B$ be a complex vector bundle with a non-vanishing section. Then, $c_n(E)=0$.
</div>

One can naturally wonder if the converse is true. That is, if $e(E)=0$, then must there necessarily be a section of $\pi$? The answer to this turns out to be no, and the issue is essentially that $S^n$ has higher homotopy groups [^29] beyond the $\pi_n(S^n)\simeq\Z$ from which the Euler class ultimately originates. In general, when faced with lifting problems like this (can you lift a map against a fibration, possibly extending an initial lift on some subspace), one obtains a sequence $\omega_k\in\hom^{k+1}(\text{blah};\pi_k(F))$ ($F$ the fiber) of cohomology classes such that a lift exists iff all of these cohomology classes vanish. In this framework, the Euler class $e(E)\in\hom^{n+1}(B;\Z)=\hom^{n+1}(B;\pi_n(S^n))$ is what's called a <b>primary obstruction class</b> since it is the first one which can be nonzero in the situation of constructing a section of a sphere bundle [^32]. 

## Relation to Enumerative Geometry

This is the most exciting part of this whole post. The Euler class. can. be. used. to. count.

We will make sense of this in this section, and then end the post with an example. By using the Euler class to count, I mean that the Euler class, in nice situations, encodes the number of zeros of a generic section of its vector bundle. Essentially, we will refine the result that a bundle with a section with $0$ zeros has Euler class equal to $0$.

For this application, we will need not just the Euler class itself, but also the Thom class. Before, proving things, let's recall Poincare duality.

<div class="theorem" name="Poincare duality">
    Let $M$ be a compact, oriented $n$-manifold with (possibly empty) boundary. Then, there is a fundamental class $[M]\in\hom_n(M,\del M)$ such that 
    $$\mapdesc{P}{\hom^k(M,\del M;\Z)}{\hom_{n-k}(M;\Z)}{\alpha}{[M]\frown\alpha}$$
    is an isomorphism for all $k$. Above $\frown:\hom_m(M,\del M)\by\hom^k(M,\del M)\to\hom_{m-k}(M;\Z)$ denotes the cap product.
</div>

As suggested by the fact that we recalled the above theorem, for the results of this section, we will need to assume our base space in a compact manifold. Given this, we will show that the Euler class of an oriented real vector bundle is Poincare dual to the zero set of a generic section of the bundle. When the dimension of the base space equals the rank of the bundle, the a generic section will have a zero-dimensional zero set (i.e. a finite, discrete set of zeros), and so in that case, the Euler class will simply count the number of zeros.

<div class="lemma">
    Let $S^n\to E\to M$ be an oriented $S^n$-bundle over a compact $k$-manifold. Let $\sigma_0:M\to D(E)$ denote the zero section of the associate disk bundle. Then,
    $$\sigma_{0,*}[M]=\pm[D(E)]\frown u(E)\in\hom_k(D(E);\Z),$$
    i.e. the Thom class is Poincare dual to the zero section of $p:D(E)\to M$.
</div>
<div class="proof4">
    Non-connected spaces don't exist, so assume $B$ connected. Note that $D(E)$ is $(k+n+1)$-dimensional (oriented) compact manifold with boundary $E$. Hence, we have isomorphisms
    $$\Z=\hom^0(M;\Z)\xto{\pull\pi(-)\smile u}\hom^{n+1}(D(E),E;\Z)\xto{[D(E)]\frown}\hom_k(D(E);\Z)\xto{\push p}\hom_k(M;\Z)=\Z.$$
    The generator $1\in\hom^0(M;\Z)$ maps to $[D(E)]\frown u\in\hom_k(D(E);\Z)$ which must be a generator of $\hom_k(D(E);\Z)$. At the same time, $\sigma_0:M\to D(E)$ is a homotopy equivalence and so sends the generator $[M]\in\hom_k(M;\Z)$ to a generator $\sigma_{0,*}[M]\in\hom_k(D(E);\Z)$. The claim follows.
</div>

The above lemma is our first inclination that the Thom class (and hence the Euler class) has anything to do with sections of its bundle. Next, we will show how one can use Thom classes to construct the cohomology class dual to a submanifold $N\subset M$. For notational convenience, given a compact, oriented $k$-dimensional submanifold $\iota:N\into M$ (here, $\dim M=n$), let $\ast{[N]}\in\hom^{n-k}(M;\Z)$ denote the Poincare dual to $\push\iota[N]\in\hom_k(M;\Z)$.

Now, let's take a very brief detour into the theory of vector bundles on smooth manifolds. Let $N\into M$ be compact, oriented smooth manifolds of dimensions $k$ and $n$, respectively. Then, there exists vector bundles $TN\to N$ and $TM\to M$ of ranks $k$ and $n$, respectively, called the tangent bundles of $N$ and $M$. In particular, $TN$ is a subbundle of $TM\vert_N$, the tangent bundle of $M$ restricted to $N$, and so fits into an exact sequence (of vector bundles on $N$)

$$0\too TN\too TM\vert_N\too N_{N/M}\too0,$$

where the rank $(n-k)$ vector bundle $N_{N/M}$ is by definition the <b>normal bundle of $N$ in $M$</b>. Intuitively, the tangent bundle $TM$ contains all the directions one can move along in $M$ (and similarly for $TN$), so the normal bundle $N_{N/M}$ contains all the directions in $M$ which are perpendicular to $N$. The amazing fact is that there exists a "tubular neighborhood" $U\subset M$ of $N$ with a smooth embedding $U\into N_{N/M}$ sending $N\subset U\subset M$ to the zero section in $N_{N/M}$; in other words, the (unit disk bundle of) the normal bundle embeds back into the manifold. Accepting this, attached to $N\into M$ is a Thom class

$$u_N:=u(N_{N/M})\in\hom^{n-k}(D(N_{N/M},S(N_{N/M});\Z)\simeq\hom^{n-k}(U,U\sm N;\Z).$$

By excision, we have an isomorphism $\hom^{n-k}(M,M\sm N;\Z)\to\hom^{n-k}(U,U\sm N;\Z)$, and this former space naturally restricts to $\hom^{n-k}(M;\Z)$. Let $u_N^M$ denote the image of $u(N_{N/M})$ under the composite map

$$\hom^{n-k}(D(N_{N/M}),S(N_{N/M});\Z)\iso\hom^{n-k}(U,U\sm N;\Z)\iso\hom^{n-k}(M,M\sm N;\Z)\to\hom^{n-k}(M;\Z).$$

This $u_N^M$ is the Poincare dual of $N$.

<div class="lemma">
    Let $N\into M$ be the inclusion of a closed, oriented $k$-dimensional manifold into a compact, oriented $n$-dimensional manifold. Then,
    $$\ast{[N]}=\pm u_N^M\in\hom^{n-k}(M;\Z).$$
</div>
<div class="proof4">
    Let $\iota:N\into M$ be the inclusion map. It is equivalent to show that
    $$\push\iota[N]=[X]\frown u_N^M\in\hom_k(M;\Z).$$
    For this, we consider the following commutative diagram (commutativity from naturality of the cap product)
    $$\begin{CD}
        \hom_n(M;\Z)\otimes\hom^{n-k}(M,M\sm N;\Z) @>>> \hom_n(M,M\sm N;\Z)\otimes\hom^{n-k}(M,M\sm N;\Z) @>>> \hom_n(U, U\sm N;\Z)\otimes\hom^{n-k}(U, U\sm N;\Z)\\
        @VVV @V\frown VV @VV\frown V\\
        \hom_n(M;\Z)\otimes\hom^{n-k}(M;\Z) @>\frown >>\hom_k(M;\Z) @<<< \hom_k(U)
    \end{CD}$$
    where $U\subset M$ is a tubular neighborhood of $N$. Start with $[M]\otimes u_N^M$ in the bottom left. By construction of $u_N^M$, we can lift this to the top left and then pass to the top right, ending up with $[U]\otimes u_N$. By previous lemma, $[U]\frown u_N=\pm\push\iota[N]\in\hom_k(U)$ (since $\iota:N\to U$ is identified with the zero section of $N_{N/M}\to N$). Thus, by commutativity of the diagram, we must have
    $$[M]\frown u_N^M=[U]\frown u_N=\pm\push\iota[N]\in\hom_k(M)$$
    as claimed.
</div>

If one is more careful above (actually, more careful in the first lemma of this section), then they can remove the $\pm$, and just conclude that $\ast{[N]}=\pm u_N^M\in\hom^{n-k}(M;\Z).$ However, what we have above is good enough for our purposes; in the end, we'll want to count zeros of a section, and so we'll know that the correct answer will be a positive number. We'll obtain a result saying that the Euler class computes this count up to sign, so we can always get the correct result by computing the Euler class and then taking the absolute value of what we get.

<div class="theorem">
    Let $E\to M$ be a smooth, oriented rank $n$ real vector bundle over a compact, oriented manifold $M$. Let $\psi$ be a section whose graph is transverse to the zero section (i.e. a "generic section"), and let $Z=\inv\psi(0)\subset B$. Then,
    $$e(E)=\ast{[Z]}\in\hom^n(B;\Z).$$
</div>
<div class="proof4">
    Let $u\in\hom^n(E,\units E;\Z)$ denote the Thom class of $E$, and let $u\vert_E$ be its image under the map $\hom^n(E,\units E;\Z)\to\hom^n(E;\Z)$. Let $U\subset M$ be a tubular neighborhood of $Z$, and let $u_Z\in\hom^n(U,U\sm Z;\Z)$ be the Thom class of $N_{Z/M}$. Because everything in sight has secretly been given compatible orientations (and because I'm secretly neglecting to show that $E\vert_Z$ is isomorphic to the normal bundle $N_{Z/M}$), $\ast\psi\vert_Uu\in\hom^n(U,U\sm Z;\Z)$ restricts to the preferred generator of each fiber of the normal bundle, so $\ast\psi\vert_Uu=u_Z$. Given this, one applies excision to $(U,U\sm Z)\into(M,M\sm Z)$ followed by natural map $\hom^n(M,M\sm Z;\Z)\to\hom^n(M;\Z)$ in order to obtain the identity
    $$\ast\psi(u\vert_E)=u_Z^M\in\hom^n(B;\Z).$$
    Above, the LHS is the Euler class $e(E)$ while the RHS is $\ast{[Z]}$ by the most recent lemma.
</div>
<div class="corollary">
    Let $E\to M$ be a smooth, oriented rank $n$ real vector bundle over a compact, oriented $n$-dimensional manifold $M$. Then,
    $$[M]\frown e(E)\in\hom_0(M;\Z)=\Z$$
    is the number of zeros of a generic section, up to sign.
</div>
<div class="corollary">
    Let $E\to B$ be a holomorphic rank $n$ vector bundle over an $n$-dimensional complex manifold (so $2n$-dimensional as a smooth manifold). Then,
    $$[B]\frown c_n(E)\in\hom_0(B;\Z)=\Z$$
    is the number of zeros of a generic section, up to sign.
</div>

At this point one may reasonably wonder why this is such a big deal. The point (at least my point) is the following: say you want to calculate the number of some type of geometric object. It often happens that the objects you want to count are given by zero set of a well-chosen section on a suitable line bundle. Once you realize this in your specific case, the above theorem tells you that computing this count amounts to calculating a characteristic class. Even if calculating characteristic classes isn't your thing, the theorem still tells you that your geometric count is (largely) independent of the section you choose to count it! That means, even if you problem naturally presents you with one section of your line bundle, the above results says you can resolve it by counting the zeros of the section which is easiest to work with! 

Let's see some of this in action.

# 27 Lines on a Cubic

As is probably unsurprising by this point, we will end this post by determining the number of lines (copies of $\CP^1$) on a (complex) cubic surface. Let $F=F(x,y,z,w)$ be a degree 3 homogeneous polynomial, and let $X=\bracks{F=0}\subset\CP^3$ be the cubic surface it determines. What can one count the number of lines on $X$?

Well, consider $G=\mrm{Gr}(2,4)$ (or $\mrm{Gr}(1,3)$ depending on who you ask), the Grassmannian manifold consisting of $2$-dimensional subspaces of $\C^4$ (equivalently, of lines in $\CP^3$). Note that, as a complex manifold, the dimension of $G$ is $2(4-2)=4$. On $G$, one has the tautological subbundle

$$S=\bracks{(v,p):v\in p}\subset\C^4\by G\to G$$

which is a rank $2$ holomorphic vector bundle $S\to G$ whose fiber $S_p$ above a point $p\in G$ is the plane represented by that point. Consider the dual bundle $\dual S=\Hom(S,\C)\to G$ whose fiber $\dual S_p$ over a point $p\in G$ is the space of linear functions $S_p\to\C$. Since $S_p\subset\C^4$, we see that every linear functional $S_p\to\C$ is the restriction of some linear functional $\C^4\to\C$ on $\C^4$ (i.e. $\dual{(\C^4)}\to\dual S_p$ is surjective for all $p$). Letting $x,y,z,w$ suggestively denote a fixed basis for $\C^4$, we get that every linear functional on $\C^4$ (and so every linear functional on $S_p$) is given by some homogeneous linear polynomial in $x,y,z$, and $w$. That is, sections of $\dual S\to G$ correspond to homogeneous linear polynomials in the variables $x,y,z,w$. Thus, forming the symmetric bundle $\Sym^3\dual S\to G$, we get that sections of it correspond to homogeneous degree $3$ polynomials in $x,y,z,w$. In particular, there exists a section $\sigma_F:G\to\Sym^3\dual S$ corresponding to the polynomial $F$ used to define our cubic surface $X$!

Now, what does it mean for some $p\in G$ to be a zero of $\sigma_F$, i.e. when is $\sigma_F(p)=0$? Well, $\sigma_F(p)\in\Sym^3\dual S_p$ is the linear functional $F\in\Sym^3\dual{(\C^4)}$ restricted to the plane $S_p\subset\C^4$, so $\sigma_F(p)=0$ if and only if $F(c_1,c_2,c_3,c_4)=0$ for all $c_1x+c_2y+x_3z+c_4w\in S_p\subset\C^4$ (here, $c_i\in\C$). That is, $\sigma_F(p)=0$ iff $F$ vanishes along the plane $S_p\subset\C^4$. Now, we observe that a $2$-plane in $\C^4$ in precisely a line in $\CP^3$, so points of $G$ can be viewed a parameterizing all the lines on $\CP^3$, given some $p\in G$, we have $\sigma_F(p)=0$ if and only if $F$ vanishes along the line (in $\CP^3$) represented by $p$. In other words, $\sigma_F(p)=0$ iff the line $p\subset\CP^3$ lives in the set $\bracks{F=0}=:X$; the zeros of $\sigma_F$ are precisely the lines in $X$!

This brings us to the home stretch. Since $\rank S=2$, we easily see that $\rank\Sym^3\dual S=4=\dim_\C G$, so the number of lines on $X$ is (Poincare dual to) $c_4(\Sym^3\dual S)$. Let's compute this. By the splitting principle, to determine $c_4(\Sym^3\dual E)$ for a general (rank 2) vector bundle $E$, we can assume that $E=L_1\oplus L_2$ is a sum of line bundles. Let $x_1=c_1(L_1)$ and $x_2=c_1(L_2)$, so $c(E)=(1+x_1)(1+x_2)=1+(x_1+x_2)+x_1x_2$. Note that

$$\Sym^3\dual E=\Sym^3(\dual L_1\oplus\dual L_2)=(\dual L_1)^{\otimes 3}\oplus((\dual L_1)^{\otimes2}\otimes\dual L_2)\oplus(\dual L_1\otimes(\dual L_2)^{\otimes2})\oplus(\dual L_2)^{\otimes3}.$$

Thus, taking the total Chern class of both sides, we see that

$$\begin{align*}
    c(\Sym^3\dual E)
    &=(1-3x_1)(1-2x_1-x_2)(1-x_1-2x_2)(1-3x_2)\\
    &=1 - 6(x_1+x_2) + (11x_1^2+32x_1x_2+11x_2^2) - 6(x_1^3 + 8x_1^2x_2 + 8x_1x_2^2 + x_2^3) + x_1x_2(18x^2 + 45x_1x_2 + 18x_2^2)\\
    &= 1 - 6c_1(E) + (11c_1(E)^2 + 10c_2(E)) - 6(c_1(E)^3 + 5c_1(E)c_2(E)) + c_2(E)(18c_1(E)^2 + 9c_2(E))
\end{align*}$$

Thus, for any rank $2$ complex vector bundle $E\to B$, we have

$$c_4(\Sym^3\dual E)=c_2(E)(18c_1(E)^2 + 9c_2(E)).$$

Um, now we switch gears and cheat. I actually don't know a quick and easy way to calculate the above cup products [^38], so we won't compute them. Instead, we'll use the observation that $c_4(\Sym^3\dual S)$ can be computed using the zeros of <b>any</b> of its sections in order to determine the number of lines on $X$.

That is, at this point, we know that the number of lines on $X$ is given by $c_4(\Sym^3\dual S)$ for $S\to\mrm{Gr}(2,4)$ the tautological subbundle. This has absolutely no dependence on $X$, so we know already that every cubic surface (over $\C$) has the same number of lines! Thus, it suffices to just pick one and count how many lines it has. For this, we introduce the Fermat cubic surface

$$X:x^3+y^3+z^3+w^3=0.$$

Up to a permutation of coordinates, every line in $\CP^3$ is given by two linear equations of the form $x=az+bw$ and $y=cz+dw$ for some $a,b,c,d\in\C$. This will lie on $X$ if and only if

$$(az+bw)^3+(cz+dw)^3+z^3+w^3=0$$

as polynomials in $\C[z,w]$. Equating coefficients, this means that we need

$$\begin{align*}
    a^3 + c^3 &= -1\\
    b^3 + d^3 &= -1\\
    a^2b &= -c^2d\\
    ab^2 &= -cd^2
\end{align*}$$

If $a,b,c,d$ are all non-zero, then 

$$a^3=(a^2b)^2/(ab^2)=-(c^2d)^2/(cd^2)=-c^3\implies0=a^3+c^3=-1,$$

which is nonsense. Hence, possibly after renaming, we may assume $a=0$. Then, $c^3=-1$, so $d=0$ and $b^3=-1$ as well. This gives $9$ (since $3$ cube roots of $-1$) possible choices of $(a,b,c,d)$ giving rise to $9$ distinct lines on $X$. These lines are

$$x=\zeta_3^iw\,\,\,\,\text{ and }\,\,\,\,y=\zeta_3^jz$$

for some $i,j\in\bracks{0,1,2}$. The rest of the lines are given by permuting the coordinates. Base on the form these lines take, we see that we get a set of $9$ lines for every partition of the set $\bracks{x,y,z,w}$ into subsets of size $2$. Thus, there are $9\cdot3=27$ lines on $X$, and so $27$ lines on any complex cubic surface.

[^1]: No promises
[^2]: Except in footnotes where I'll reserve the power to be vague, to be handwavy, to give potentially bad intuition, and to say potentially incorrect things.
[^3]: This may make more sense by the end of the post if it doesn't right now, but because of the existence of classifying spaces, characteristic classes can equivalently be thought of as cohomology classes in $\ast\hom(BU(n);A)$ for some $n$ (the rank of the vector bundle) and abelian group $A$, assuming you only care about complex vector bundles.
[^4]: Some things I say may be false without this. For example, I think you need this for fiber bundles to be fibrations.
[^5]: "Isn't $-\gamma$ also a generator?" you ask. Yes, but it's actually a different one. The point is that $\CP^2$ has a complex structure, so a canonical orientation, so a canonical choice of generator $\gamma\in\hom^2(\CP^2;\Z)$, and this is "the same" generator we use for $\hom^2(\CP^\infty;\Z)$.
[^6]: Fix any $x\in U_i\cap U_j$. The point $(x,v)\in\inv p(U_i)\simeq U_i\by\C^{n+1}$ is identified with the point $(x,\tau_{ij}(x)v)\in\inv p(U_j)\simeq U_j\by\C^{n+1}$.
[^7]: $\pull\pi E\vert_{\P(E)_ b}\simeq\C^{n+1}\by\P(E)_ b$ is trivial since it is pullback from a vector bundle over a point. That is, letting $q=\pi\vert_{\P(E)_ b}:\P(E)_ b\to\{b\}$, we have $\pull\pi E\vert_{E_b}\simeq\pull qE_b\simeq\C^{n+1}\by\P(E)_ b$.
[^8]: It is $\ints{\P^n}(-1)$ if you are familiar with this notation.
[^9]: As the notation suggests, these coefficients are exactly the Chern classes of $E$. I think I've heard that this way of obtaining Chern classes was discovered by Grothendieck, but don't quote me on that.
[^10]: I really should have started with a rank $n$ vector bundle.
[^11]: Above, one should really write $\pull\pi c_1(EU(n))$ for $\pi:BU(n-1)\by BU(1)\to BU(n)$ instead of just $c_1(EU(n))$.
[^12]: $c_1$ corresponds to the first Chern class on the first factor, and $c_1'$ corresponds to the first Chern class on the second factor.
[^13]: I think that's how people usually prove algebraic independence of symmetric polynomials
[^14]: This is not the simplest way to do this, but more practice with Yoneda-type reasoning is never bad
[^15]: Strictly speaking, $X$ does not need to have the homotopy type of a CW-complex, but if it doesn't you need to be extra careful. In particular, $\hom^2(X;\Z)$ would not represent singular cohomology, but instead singular cohomology of a CW approximation.
[^16]: We use the same letters to denote these technically different maps in order to emphasize how closely related they are, and totally not because I was too lazy to come up with new names.
[^17]: Also, I should have also include an "identity natural transformation" $e:\bracks{0}\to\hom^2(-;\Z)$, but oh well.
[^18]: $\CP^\infty$ is like unironically the best topological space; fight me
[^19]: e.g. the cohomology class corresponding to $\mu\circ(e\by\Id)$ is $ac_1\in\Z c_1'=\hom^2(\CP^\infty;\Z)$ (cohomology of right factor of $\CP^\infty\by\CP^\infty$). One sees by tracing identifications that forming the cohomology class corresponding to $\mu\circ(e\by\Id)$ amounts to pulling back $\mu$'s cohomology class along the map $e\by\Id:\CP^\infty\to\CP^\infty\by\CP^\infty$.
[^20]: I will admit that thinking in terms of e.g. integrating differential forms is more intuitive than in terms of e.g. cupping cohomology classes. However, tough luck; I like working abstractly even when intuiting actually geometry
[^21]: There are many equivalent definitions of orientations of various objects. One way to define the orientation of a real vector space $V$ is by saying that it is a connected component of $\Wedge^{\dim V}V\sm\{0\}$. In other words, it is an equivalence class of ordered bases where two bases are considered equivalent if they differ by a matrix with positive determinant.
[^23]: In case you're wondering where we used that we were considering the pullback bundle $\pull fE\to B'$ of $E$ and not just an arbitrary vector bundle $E'\to B'$ over $B'$ with a map $E'\to E$ to $E$ (lying over the given map $B'\xto fB$), the answer is no where. In general, if $E'\to E$ is a bundle map over $B'\xto fB$, then $E'\simeq\pull fE$.
[^24]: At this point, I don't even think we know that $k\neq 0$.
[^25]: This is a very minor assumption, especially given that we were already implicitly assuming that they were paracompact and Hausdorff
[^26]: On second thought, it is possible to reach this conclusion ($p$ inducing an isomorphism on cohomology) without assuming that $E,B$ are CW complexes (up to homotopy) by using relative Hurewicz (+ universal coefficients).
[^27]: Computing differentials in spectral sequences is hard... I spent ~3 hours trying to carefully work this out because I couldn't find a source that does it (all the ones I saw either defined $c_1(L)=e(L)$ or showed $c_1(L)=\pm e(L)$ and left it at that), and in the end, I concluded that if I didn't stop thinking about it, I'd lose my mind.
[^28]: I don't think I remarked this earlier, but from the multiplicativity $c(E\oplus F)=c(E)c(F)$ of the total Chern class, one sees that $c_{\mrm{top}}(E\oplus F)=c_{\mrm{top}}(E)c_{\mrm{top}}(F)$. In particular, $c_n(L_1\oplus\cdots\oplus L_n)=c_1(L_1)\dots c_1(L_n)$ when $L_1,\dots,L_n$ are line bundles
[^29]: If $B$ does not have higher cohomology groups (i.e. if $\hom^k(B)=0$ for all $k>n+1$), then it is true that existence of a section is equivalent to vanishing of the Euler class
[^30]: I didn't quite meet this goal. Started strong but ran into issues by the end (lacking details once I start talking about Euler classes) as seems to be the norm.
[^31]: It is unclear to me if the existence of these maps is clear given the approach we have taken
[^32]: Technically speaking, the primary obstruction class has its own definition and we haven't shown that it equals the Euler class yet, but it does.
[^33]: I think one of my worse decisions this post has been to use the same symbol $E$ as the default for all my fiber bundles, whether they be (oriented) real (or complex) vector bundles, sphere bundles, principal $G$-bundles, or what have you
[^34]: In case you are wondering, yes, I could just restructure this post by showing the existence of the Thom class first and then using its existence to define the Euler class in order to avoid this omission
[^35]: Going through this yourself might be good practice. You should end up getting that $\hom^{p+n+1}(D(E),E;\Z)\simeq\hom^p(B;\Z)$ and that the Thom class $u\in\hom^{n+1}(D(E),D;\Z)$ is the unique cohomology class restricting to the preferred generator of $\hom^{n+1}(D^{n+1},S^n;\Z)\simeq\hom^n(S^n;\Z)$ on each fiber.
[^36]: Given this, the Gysin sequence we constructed earlier is really the just the long exact sequence of a pair for $(D(E),E)$.
[^37]: You may want a relative version on Leray-Hirsch to prove this
[^38]: Note that the coefficients, $18$ and $9$, add up to $27$. Also note that, even without being able to determine these cup products, we can conclude that the number of lines on a cubic surface must be some multiple of $9$ (independent of the chosen surface).
[^39]: Ostensibly, $BU(n)$ characterizes principal $U(n)$-bundles, not complex rank-$n$ vector bundles, so what gives? Well, two things: (1) every complex rank $n$ vector bundle arises from some principal $U(n)$-bundle and (2) the universal rank $n$ vector bundle is the vector bundle $(EU(n)\by_{U(n)}\C^n)\to BU(n)$ over $BU(n)$ where $U(n)$ acts on $\C^n$ by matrix-vector multiplication as one would expect
