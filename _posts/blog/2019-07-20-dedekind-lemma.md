---
layout: post
title: "A Nice Lemma about Dedekind Domains"
modified:
categories: blog
excerpt:
tags: [math, Dedekind domain, adeles, localization, completion, projective module]
date: 2019-08-12
---

Often times in these posts, the main focus is some big/nice theorem/result; however, this time there's [a nice lemma about Dedekind domains](https://www.youtube.com/watch?v=F8mYLi3PGOc) that I think merits its own post. This is partially because I'm still shocked that it's true, and partially because I don't know where else it is written down. After proving it, I will (maybe briefly [^9]) mention one of its uses [^1]. However, I think this use is less exciting than the lemma itself. The gist of the lemma is that lattices over Dedekind domains can be modified at a single prime.

# The Lemma

I guess I might as well start with stating this thing. Before I can do that though, it's probably worthwhile to define what I mean by a lattice.
<div class="definition">
    Let $A$ be an integral domain with fraction field $F$. Let $V$ be an $F$-vector space. Then, an <b>$A$-lattice</b> (or <b>lattice over $A$</b>) $L\subset V$ is a torsion-free, finitely generated $A$-module. Its <b>rank</b>
 is $\dim_F(F\otimes_AL)$.
</div>
<div class="lemma" name="This Post's Main Lemma">
    Let $R$ be a Dedekind domain with fraction field $F$, $\mfp$ a maximal ideal of $R$, and $R_\mfp$ the localization of $R$ at $\mfp$. For an $R$-lattice $L$ and $R_\mfp$-lattice $L_0$, both in $F^n$, there exists a unique $R$-lattice $L'$ in $F^n$ such that $L'_\mfp=L_0$ and $L_\mfq=L'_\mfq$ for all maximal ideals $\mfq\neq\mfp$.
</div>

Notice above that we have hard equalities. These aren't abstract isomorphisms; all of these lattices are literal subsets of our fixed vector space $F^n$, and these are literal equalties of sets. 

What freaks me out about this lemma is that it (almost) tells us that we can consider some global $R$-lattice as a collection of local $R_\mfp$-lattices, make arbitrary changes to the local lattices, and then stitch all these changes together to get some global transformation of the lattice we started with. I feel like you generally don't have this much global control at the local level.

Anyways, let's prove this thing. The first thing we'll want to do is reduce the statement of the lemma to something more manageable. Right now, we have infinitely many local conditions we need our fabled lattice $L'$ to satisfy (one for each prime of $R$), and infinity is a pretty big number. It would be nice if we only had finitely many constraints instead. This brings us to our first step. [^2]

<div class="claim">
    Same setup as the main lemma. There exists some $r\in R$ such that, for proving the main lemma, it suffices to satisfy some local conditions just for the (finitely many) primes $\mfq\mid(r)$ as well as one at $r$ itself.
</div>
<div class="proof4">
    Let's start by letting $M$ be the $R$-span of an $R_\mfp$-basis for $L_0$. Then, $M$ is a (global) lattice and will be our surrogate for $L_0$. Fix a uniformizer $\pi$ for $\mfp$ (i.e. a generator of $\mfp R_\mfp$). Note that $R_\mfp[1/\pi]=F$, and
    $$M_\mfp[1/\pi]=M_F=F^n=L_F=L_\mfp[1/\pi]$$
    where the notation $M_F$ refers to the $F$-span of $M$. Hence, $L[1/\pi]$ and $M[1/\pi]$ are $R[1/\pi]$-lattices which become the same after localizing at $\mfp'=\mfp R[1/\pi]$. We claim that there exists some $s\in R[1/\pi]\sm\mfp'$ such that $L[1/\pi]_s=M[1/\pi]_s$. To find such an $s$, (implicitly fix bases for $M[1/\pi]$ and $R[1/\pi$], then) let $B\in\GL_n(F)$ be a change of basis matrix between $L[1/\pi]_{\mfp'}$ and $M[1/\pi]_{\mfp'}$. Since $F=R[1/\pi]_{\mfp'}$ and $B$ has only finitely many entries, we can write $B=s'B'$ with $B'\in\GL_n(R[1/\pi])$ and $s'\in R[1/\pi]\sm\mfp'$. Hence, we see that we can take $s=s'\det(B')$ since then inverting $s$ inverts both $s'$ and $\det(B')$.
    <br>
    Now, it's harmless to replace $s\in R[1/\pi]$ with its numerator in some fractional expression, so we can form $r=s\pi\in R\sm\{0\}$. We have $M_r=L_r$ as $R_r$-lattices inside $F^n$. Now, let $M'=L\cap M$, an $R$-lattice in $F^n$, and observe that $M'_r=L_r=M_r$. We claim that, for proving the main lemma, it suffices to find an $R$-lattice $L'$ containing $M'$ such that (i) $L'_r=M_r'$ and (ii) for each of the finitely many primes $\mfq\mid(r)$, we have $L'_\mfq=L_\mfq$ if $\mfq\neq\mfp$ and $L'_\mfp=L_0$ (i.e. $M_\mfp$) otherwise. This is because for $\mfq\nmid(r)$, we also would have $L'_\mfq=L_\mfq$ since $L'_r=M_r'=L'_r$ (i.e. $L'_\mfq=(L'_r)_{\mfq'}$ where $\mfq'=\mfq L_r$).
</div>

Hence, we've reduced proving the main lemma to constructing this $R$-lattice $L'$ mentioned at the end of the above argument. Writing $V=F^n$ for ease of notation, we can view $L'$ as a finitely generated $R$-submodule of the (huge) $R$-module $V/M'$. While $V/M'$ may seem largely unwildly, we actually have some hope of being able to understand/work with it since it is torsion (e.g. think of $\qz$). To see that it's torsion, note that $M_F'=V$, so every element of $V$ looks like $\frac mr$ with $m\in M'$ and $r\in R$, and so is killed (in $V/M'$) when multiplied by its denominator. Now, to make working with $V/M'$ easy, we'll prove a general fact that torsion $R$-modules decompose into sums of (some of) their localizations.

<div class="claim">
    Let $N$ be a torsion $R$-module, and fix any $a\in R$. Then, the natural map
    $$N\too N\sqbracks{\frac1a}\oplus\parens{\bigoplus_{\mfq\mid(a)}N_\mfq}$$
    is an isomorphism.
</div>
<div class="proof4">
    It suffices to check this after localizing at each prime $\mfP$ of $R$. If $\mfP\mid(a)$, then, because $N$ is torsion, localizing kills all $N_\mfq$ on the RHS except for $N_\mfP$. Furthermore, since $N_\mfP$ is a dvr (in particular, a PID) and $a\in N_\mfP$ is a non-unit, we see that
    $$N\sqbracks{\frac1a}_\mfP=N_\mfP\sqbracks{\frac1a}=0$$
    as well, so this map is an isomorphism at all primes dividing $(a)$. Similarly, if $\mfP\nmid(a)$, then, since $N$ is torsion, all $N_\mfq$ are killed after localizing at $\mfP$ while, since $a\not\in\mfP$,
    $$N\sqbracks{\frac1a}_\mfP=N_\mfP,$$
    so this map is also an isomorphism at all primes not dividing $(a)$. Thus, it is an isomorphism locally which implies that it is one globally.
</div>

In our particular case, the above says that

$$\frac V{M'}\iso\parens{\frac V{M'}}\sqbracks{\frac1r}\oplus\parens{\bigoplus_{\mfq\mid(r)}\parens{\frac V{M'}}_ \mfq}$$

Now, we're practically done. Using the description on the RHS, take $L'$ to be the $R$-submodule of $V/M'$ given by inserting the chosen $R_\mfq$-submodule of each $(V/M')_ \mfq$ for $\mfq\mid(r)$ (and $0$ for $(V/M')[1/r]$). One needs to check that this module is finitely generated over $R$. However, this is clear since a finitely generated torsion $R_\mfq$-module is just a finitely generated module over $R_\mfq/(\mfq R_\mfq)^N=R/\mfq^N$ for some large $N$ (and hence also finitely generated over $R$). There are only finitely many primes dividing $(r)$, so we win.

There we have it. Lattices over Dedekind domains can be modified one prime at a time.

# Its Use

For this part of the post, you'll probably want to have some familiarity with completions of rings (e.g. be comfortable with inverse limits) and adeles (e.g. know what a restricted direct product is).

We'll switch up notation in this section. Previously, given a Dedeking domain $R$ with prime ideal $\mfp$, we used $R_\mfp$ to denote its localization at $\mfp$. From now on, we'll instead let $R_\mfp$ denote $R$'s completion at $\mfp$. That is,

$$R_\mfp:=\invlim_nR/\mfp^n$$

is the valuation ring (i.e. elements with norm $\le1$) of the (analytic) completion $F_\mfp$ of $F$ with respect to the absolute value $\abs x_\mfp=\eps^{-v_\mfp(x)}$ where $0<\eps<1$ and $v_\mfp(x)$ is the largest power of $\mfp$ dividing $(x)$.

The point of this section will be to use the main lemma to prove that (isomorphism classes of) finitely generated projective $R$-modules of rank $n$ are classified via a certain double coset space. [^3] Before stating this, it will be useful to define/prove a few things.

<div class="proposition">
    Let $\wh R=\invlim R/\mfa$ be the "profinite" completion of $R$; this inverse limit is taken along all nonzero ideals of $R$, with each $R/\mfa$ discrete. Then,
    $$\wh R\simeq\prod_\mfp R_\mfp$$
    as topological rings.
</div>
<div class="proof4">
    We'll first construct the left-to-right map. A map to a direct product is a map to each factor, so fix some prime $\mfp$; we'll construct a map $\wh R\to R_\mfp$. Now, a map into an inverse limit is a (consistent choice of a) map into each factor, so we really just need to map $\wh R\to R/\mfp^n$. However, we have a natural choice of such a map since $\mfp^n$ is an ideal of $R$ and $\wh R=\invlim R/\mfa$ is formed along all ideals (for the same reason, these maps are consistent and so do in fact give a map $\wh R\to R_\mfp$). We claim that the map $\wh R\to\prod_\mfp R_\mfp$ that we've constructed is continuous. This is the case iff all projections $\wh R\to R/\mfp^n$ are continuous, and this is the case since given $a\in R/\mfp^n$, its preimage is the open set
    $$\wh R\cap\sqbracks{\prod_{\mfa\neq\mfp^n}R/\mfa\by\{a\}}.$$
    Now, since $\wh R$ is compact and $\prod_\mfp R_\mfp$ is Hausdorff, to show that this map is an isomorphism of topological rings, it suffices to show that it is a bijection. For injectivity, fix some $a=\parens{a_\mfa}_\mfa\in\ker\parens{\wh R\to\prod_\mfp R_\mfp}$. The statement that this is in the kernel is exactly the statement that $a_{\mfp^n}=0$ for all primes $\mfp$ and natural $n\ge0$. Because $R$ is a Dedekind domain, we can write
    $$\mfa=\prod_{\mfp\mid\mfa}\mfp^{v_\mfp(\mfa)}$$
    as a finite product of prime powers, so
    $$R/\mfa\simeq\prod_{\mfp\mid\mfa}R/\mfp^{v_\mfp(\mfa)}.$$
    Hence, $a_\mfa=0$ for all $\mfa$ as its projection to each prime power factor is trivial. Thus, $a=0$. By the same kind of Chinese Remainder Theorem argument, we see that this map is surjective, and hence an isomorphism of topological rings.
</div>
<div class="corollary">
    $$\wh\Z\simeq\prod_p\Z_p$$
</div>

Our next definition will be that of the <b>adele ring</b> $\A_R=F\otimes_R\wh R$, where $F=\Frac(R)$. Note that when $R=\Z$ (or, more generally $R=\ints K$ for $K$ a number field), this is just the ring of finite adeles instead of the usual adele ring over $\Q$ (or $K$) which also contains information about $R$'s infinite places. Now, if you've seen adeles before, you're probably used to seeing them defined via some kind of restricted direct product instead of this weird tensor. The two definitions are equivalent.

<div class="proposition">
    $$\A_R\simeq\prodp_{\mfp}\parens{F_\mfp,R_\mfp}$$
    where we remember that $F_\mfp$ denotes the completion of $F$ at $\mfp$ and $R_\mfp$ denotes the completion of $R$ at $\mfp$ (the valuation ring of $F_\mfp$). Similarly,
    $$\GL_n(\A_R)\simeq\prodp_{\mfp}\parens{\GL_n(F_\mfp),\GL_n(R_\mfp)}.$$
</div>
<div class="proof4">
    We'll only prove the first part here. Note that we have a map
    $$\mapdesc\phi{\A_R}{\prodp_\mfp\parens{F_\mfp,R_\mfp}}{x\otimes\parens{r_\mfp}_\mfp}{\parens{xr_\mfp}_\mfp}$$
    using the description $\A_R\simeq F\otimes_R\wh R\simeq F\otimes_R\prod_\mfp R_\mfp$. This map is well-defined because $xr_\mfp\not\in R_\mfp\implies v_\mfp(x)\neq0$ and this latter part can only be true for finitely many primes. To see that this is an isomorphism, first note that ($a,b,c,d\in R$)
    $$\frac ab\otimes(r_\mfp)_\mfp+\frac cd\otimes(s_\mfp)_\mfp=\frac{ad}{bd}\otimes(r_\mfp)_\mfp+\frac{bc}{bd}\otimes(s_\mfp)_\mfp=\frac1{bd}\otimes(adr_\mfp)_\mfp+\frac1{bd}\otimes(bcs_\mfp)_\mfp=\frac1{bd}\otimes\parens{adr_\mfp+bcs_\mfp}_\mfp,$$
    so all tensors here are simple. Now, injectivity is clear because every ring in sight is an integral domain. Surjectivity is also easy to see essentially because collecting the denominators of the (finitely many) non-integral components of the restricted direct product gives you an element of $F$.
    <br>
    Showing that $\GL_n(\A_R)$ is also a restricted direct product is left as an exercise.
</div>

Cool. Now that we know something about adeles, we can prove the thing we alluded to at the beginning of this section. Recall that an $R$-module $P$ is called <b>projective</b> if any of the following hold

<ul>
    <li> Every short exact sequence $0\too K\too E\too P\too 0$ splits </li>
    <li> There exists an $R$-module $Q$ such that $P\oplus Q$ is $R$-free </li>
    <li> The (covariant) function $\Hom_R(P,-)$ is exact </li>
</ul>

When $R$ is a Dedekind domain (and $P$ is finitely generated), this is just a fancy way to say that $P$ is torsion-free [^4]. Given a projective $R$-module $P$, its <b>rank</b> is $\dim_F(P\otimes_RF)$ where $F=\Frac(R)$ [^5]. 

One last thing: for proving the below theorem, it will be helpful to know that (finitely presented) projective modules are "locally free" in the below sense. [^7]

<div class="proposition">
    Let $M$ be a finitely presented $R$-module. Then, TFAE
    <ul>
        <li> $M$ is projective. </li>
        <li> There exists $r_1,\dots,r_k\in R$ s.t. $(r_1,\dots,r_k)=R$ and $M[\frac1{r_i}]$ is a free $R[\frac1{r_i}]$-module for all $i$. </li>
    </ul>
</div>
<div class="proof4">
    Somewhere in <a href="http://math.stanford.edu/~church/teaching/210A-F17/math210A-F17-hw3-sols.pdf">here</a>.
</div>

Finally, the one use of our main lemma I know is proving the following:

<div class="theorem">
    Let $R$ be a Dedekind domain with fraction field $F$. Then, the set of isomorphism classes of finitely generated projective $R$-modules of rank $n$ can be identified with the double coset space $\GL_n(\wh R)\sm\GL_n(\A_R)\,/\,\GL_n(F)$.
</div>
<div class="proof4">
    First convince yourself that $\GL_n(\wh R)\simeq\prod_\mfp\GL_n(R_\mfp)$. Now we'll describe the map
    $$\bracks{\text{isomorphism classes of finitely generated projective $R$-modules of rank $n$}}\too\GL_n(F)\sm\GL_n(\A_R)\,/\,\GL_n(\wh R).$$
    Let $P$ be such an $R$-module, fix an $F$-linear isomorphism $f:F\otimes_RM\iso F^n$, and choose any prime $\mfp\subset R$. Now, fix $r_1,\dots,r_m$ (I'm pretty sure, secretly, $m=n$ but that's not needed for this proof) as in the previous proposition, and let $\bracks{\ith e_j}_{j=1}^n$ be an $R[\frac1{r_i}]$-basis for $M[\frac1{r_i}]$. Choosing a basis like this gives rise to a map $\ith g:F\otimes_{R[\frac1{r_i}]}M[\frac1{r_i}]\iso F^n$. Noting that
    $$F\otimes_{R[\frac1{r_i}]}M\sqbracks{\frac1{r_i}}\simeq F\otimes_{R[\frac1{r_i}]}R\sqbracks{\frac1{r_i}}\otimes_RM\simeq F\otimes_RM,$$
    and comparing $\ith g$ with $f$ gives us some $\ith T\in\GL_n(F)$.
    $$\begin{CD}
    F\otimes_RM @>f>> F^n\\
    @VVV @VV\ith TV\\
    F\otimes_{R\sqbracks{\frac1{r_i}}}M\sqbracks{\frac1{r_i}} @>\ith g>> F^n
    \end{CD}$$
    Now we make use of the prime $\mfp$ we fixed earlier. Since $(r_1,\dots,r_m)=R$, there must exist some $k=k_\mfp\in\{1,\dots,m\}$ such that $r_k\not\in\mfp$, so $\bracks{\Ith ek_j}_{j=1}^n$ descends to an $R_\mfp$-basis of $M_\mfp$, and $\Ith Tk$ descends to a map $\Ith Tk_\mfp\in\GL_n(F_\mfp)$. Now, we investigate when we further have that $\Ith Tk_\mfp\in\GL_n(R_\mfp)$. By construction, $\det(\Ith Tk_\mfp)=\det(\Ith Tk)$, so since there are only finitely many $\ith T$, we claim that we will have $\Ith Tk_\mfp\in\GL_n(R_\mfp)$ for all but finitely many $\mfp$. In more detail, we can first fix some $a\in R$ s.t. the matrix for $a\ith T$ has $R$-entries for all $i$. Hence, if both $a$ and $\det(a\Ith Tk)$ are invertible in $R_\mfp$, then $\Ith Tk_\mfp$ will be an element of $\GL_n(R_\mfp)$. Thus, any prime $\mfq$ with $\Ith T{k_\mfq}_\mfq\not\in\GL_n(R_\mfq)$ must divide
    $$a\prod_{i=1}^m\det\parens{a\ith T}\in R.$$
    There are only finitely many such primes, so (we claim that) our desired map is
    $$\mapdesc\psi{\bracks{f:F\otimes_RM\iso F^n}}{\GL_n(\wh R)\sm\GL_n(\A_R)\,/\,\GL_n(F)}f{\parens{\Ith T{k_\mfp}_\mfp}_\mfp}$$
    where we really should have chosen notation that made it clear that $\Ith T{k_\mfp}_\mfp$ depends on $f$. To show that this map is well-defined, we will show that changing the isomorphism $f$ affects our result by an element of $\GL_n(F)$ on the left, while changing the local bases affects the result by an element of $\GL_n(\wh R)$ acting on the right.<br>
    Let $\phi:M\to N$ be an isomorphism of projective $R$-modules. Then, we get a commutative diagram
    $$\begin{CD}
        F\otimes_RM @>f>> F^n\\
        @V{1\otimes\phi}VV         @VVTV\\
        F\otimes_RN @>g>> F^n
    \end{CD}$$
    where $T\in\GL_n(F)$. Now, using the composition $g\circ(1\otimes\phi)$ in place of $F$ has the effect of turning $\ith T$ into $\ith T\inv T$ as one sees by staring at the below commutative diagram
    $$\begin{CD}
    F\otimes_RM @>g>> F^n\\
    @A{1\otimes\phi}AA @AATA\\
    F\otimes_RM @>f_\mfp>> F^n\\
    @VVV @VV\ith TV\\
    F\otimes_{R\sqbracks{\frac1{r_i}}}M\sqbracks{\frac1{r_i}} @>\ith g>> F^n
    \end{CD}$$
    Hence, changing our isomorphism really does correspond to an action of $\GL_n(F)$ on the right.<br>
    Now, fix a prime $\mfp\subset R$ and an $R_\mfp$-basis $\bracks{f_j}_{j=1}^n$ for $M_\mfp$. What would happen to $\Ith Tk_\mfp$ if we used this basis instead of $\bracks{\Ith ek_j}_{j=1}^n$? Well, this alternate choice of basis gives rise to a map $g_\mfp:F_\mfp\otimes_{R_\mfp}M_\mfp\iso F_\mfp^n$, and then again, you stare at a diagram and see that this would have the effect of replacing $\Ith Tk_\mfp$ with $T_\mfp\Ith Tk_\mfp$ where $T_\mfp$ is what makes the below commute
    $$\begin{CD}
    F_\mfp\otimes_{R_\mfp}M_\mfp @>f>> F^n_\mfp\\
    @VVV @VV{\Ith Tk_\mfp}V\\
    F_\mfp\otimes_{R_\mfp}M_\mfp @>\Ith gk_\mfp>> F^n_\mfp\\
    @VVV @VV{T_\mfp}V\\
    F_\mfp\otimes_{R_\mfp}M_\mfp @>g_\mfp>> F^n_\mfp
    \end{CD}$$
    Clearly, $T_\mfp\in\GL_n(\mfp)$ since it corresponds to changing $R_\mfp$-bases from our original choice to our new choice, so changing all local bases at once corresponds to an action of $\GL_n(\wh R)$ on the left as desired.<br>
    So far, all we've done is defined this map; we still need to show that it's a bijection. We start with surjectivity. Fix some representative $(T_\mfp)_\mfp$ of an element of $\GL_n(\wh R)\sm\GL_n(\A_R)\,/\,\GL_n(F)$ (i.e. $T_\mfp\in\GL_n(F_\mfp)$). Since $T_\mfp\in\GL_n(R_\mfp)$ almost always, we can act by $\GL_n(\wh R)$ on the left to assume that $T_\mfp=I$, the identity for all but finitely many $\mfp$. The point of doing this is that taking $L=R^n$ and letting $f:F\otimes_RL\iso F^n$ be the natural isomorphism, we get that $\psi(f)$ is represented by the identity in every slot. Hence, $\psi(f)_\mfp=T_\mfp$ for all but finitely many $\mfp$, and we use our main lemma to change $L$, one prime at a time, in the finiely many differing slots to arrive at a new lattice $L'$ for which $\psi(L')=(T_\mfp)_\mfp$, proving surjectivity. <br>
    I'll leave injectivity for the reader because I mainly just cared about applying the main lemma, and I've done that now.
</div>

I don't actually know why this theorem is useful, but it probably is for something. I guess, geometrically, rank $n$ projective $R$-modules correspond to rank $n$ vector bundles over $\spec R$, so this gives some characterization of vector bundles in terms of this double coset space. [^8] When $n=1$, we see that the Picard group $\Pic(R)$ is $\units{\wh R}\sm\units{\A_R}\,/\,\units F$. Maybe one could use this to prove finiteness of class groups when $R=\ints K$ is the ring of integers of some number field or something; I really don't know.

# An Exercise

The simplest Dedekind domains are PIDs. Try proving the results of this post just for PIDs to see if you can make the proofs much simpler.

[^1]: If you know other uses of this lemma, please let me know.
[^2]: This is like a lemma for a lemma. What do you call that?
[^3]: Assuming I'm not remembering things incorrectly, when $n=1$, this gives the Picard group of $R$.
[^4]: Exercise: prove this (hint: use the fact that $R$ is locally a PID and (finitely generated) torsion-free modules over PIDs are free)
[^5]: Secretly, the rank of a projective $R$-module $P$ is supposed to be a function $r:\spec(R)\to\N_{\ge0}$ given by $r(\mfp)=\dim_{R/\mfp}(P\otimes_RR/\mfp)$, but this function is constant (and equal to what I wrote outside this footnote) when $R$ is not stupid (e.g. when $R$ is an integral domain)
[^6]: Exercise: prove that these are equivalent
[^7]: We say an $R$-module $M$ is finitely presented if there exists a short exact sequence $0\to A\to F\to M\to 0$ with $F$ a finitely generated free $R$-module and $A$ finitely generated. When $R$ is Noetherian, this is equivalent to being finitely generated.
[^8]: Something something the geometry of Dedekind domains is controlled by adeles something something?
[^9]: Spoiler: I accidentally ended up spending most of my time on this one use instead of keeping focus on the lemma throughout