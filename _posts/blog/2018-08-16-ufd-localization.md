---
layout: post
title: "UFDs and Localization"
modified:
categories: blog
excerpt:
tags: [math, localization, algebra, UFD, conjecture]
date: 2018-08-16 14:37:00
---

This post will be a little random. I plan on talking about a couple sufficient criteria for a ring $R$ to be a UFD, and then use (one of) them to show that the group ring $R[\Z^n]$ is a UFD when $R$ is [^1]. These criteria will involve the concept of localizing a ring, which is something I have wanted to talk about on this blog for a while now, so let's start with that.

# Localization
Localiztion [^3] is just about the nicest algebraic operation [^2] one can apply; although this is not apparent from its definition. In essense, localization gives us a way to invert a subset of elements of a ring $R$. In this way, it is a generalization of the field of fractions of a ring. Before constructing the localization of a ring, we need to know which subsets of elements we can invert. Throughout this post, all rings are commutative with unity.
<div class="definition">
    Let $R$ be a ring. A subset $S\subset R$ is called <b>multiplicative</b> if $1\in S$ and $a,b\in S\implies ab\in S$.
</div>
<div class="definition">
    Given a multiplicative set $S\subset R$, we can form the <b>localization</b> $\sinv R$ which is the ring
    $$\sinv R=\brackets{\left.\frac ab\right| a\in R,b\in S}$$
    where addition and multiplication are defined as expected, and we say
    $$\frac ab=\frac cd\iff\exists u\in S:0=u(ad-bc)$$
</div>
<div class="exercise">
    Prove that addition and multiplication on $\sinv R$ are well-defined and actually do give it a ring structure.
</div>

Note that when $R$ is a domain (and $0\not\in S$), the condition on equality of fractions becomes the usual $a/b=c/d\iff ad=bc$. Note furthermore that $\sinv R\subset\Frac(R)$ and $\Frac(\sinv R)=\Frac(R)$. Finally, $\sinv R=0\iff0\in S$. In order to prevent me from saying something technically false, for the rest of the post, assume that $0\not\in S$ for any multiplicative set we consider.

<div class="remark">
    There is a natural map $R\to\sinv R$ given by $r\mapsto r/1$, and this map is injective when $S$ contains no zero divisors (e.g. if $R$ is a domain) as $r/1=0/1\iff\exists u\in S:0=ur$.
</div>
<div class="example">
    There are two standard classes of multiplicative sets. These are
    <ul>
        <li> $S=\{1,x,x^2,\dots\}$ for some $x\in R$. In this case, we write $\sinv R=R\sqbracks{\frac1x}\simeq R[y]/(1-xy)$</li>
        <li> $S=R\sm\mfp$ where $\mfp\subset R$ is a prime ideal. In this case we write $\sinv R=R_\mfp$</li>
    </ul>
</div>

Note that when $R$ is a domain and $\mfp=(0)$, we get $R_{(0)}=\Frac(R)$. In general, the second example above is particularly prevalent because it let's you study rings "one prime at a time". In particular,...

<div class="lemma">
    Given an ideal $I\subset R$, the set $\sinv I=I\cdot\sinv R=\brackets{\left.\frac as\right|a\in I,b\in S}$ is an ideal of $\sinv R$.
</div>
<div class="proof4">
    Exercise.
</div>
<div class="definition">
    A ring $R$ is called <b>local</b> if it only has 1 maximal ideal.
</div>
<div class="theorem">
    $R_\mfp$ is a local ring.
</div>
<div class="proof4">
    We claim that $\mfp R_\mfp$ is the only maximal ideal of $R_\mfp$. This will follow from showing that every $\mfp R_\mfp$ is literally the set of all non-units in $R_\mfp$. Pick som non-unit $a/s\in R_\mfp$. Then, $a\not\in S$ since otherwise $s/a\in R_\mfp$ would be an inverse. Hence, $a\in R\sm S=\mfp$ so $a/s\in\mfp R_\mfp$. Conversely, if $a/s\in\mfp R_\mfp$, then we can assume that $a\in\mfp$. Suppose that $b/t$ was an inverse to $a/s$; then,
    $$\frac{ab}{st}=\frac11\iff\exists u\not\in\mfp:0=u(ab-st)\iff ab-st\in\mfp\iff st\in\mfp$$
    which is impossible since $st\in S$, so $a/s$ must not be a unit. Thus, $\mfp R_\mfp$ is the set of all non units, and hence the unique maximal ideal.
</div>

In addition to this, localization also respects many properties of the original ring. For example, we have the following theorems. I will leave the first as an exercise and prove the second.

<div class="theorem">
    If $R$ is a domain, then so is $\sinv R$.
</div>
<div class="theorem">
    Let $\mfq\subset\sinv R$ be a prime ideal and let $f:R\to\sinv R$ denote the map $f(r)=r/1$. Then, $\mfp:=\inv f(\mfq)$ is a prime ideal of $R$. When $R$ is a domain, we have $\mfp=\mfq\cap R$.
</div>
<div class="proof4">
    In general, given two rings $R,R'$ with a map $g:R\to R'$ and a prime ideal $\mfq\subset R'$, $\inv g(\mfq)$ is a prime ideal of $R$ since 
    $$ab\in\inv g(\mfq)\iff g(a)g(b)\in\mfq\iff g(a)\in\mfq\iff a\in\inv g(\mfq)$$
    where I should really say $g(a)$ or $g(b)$ is in $\mfq$ above, but meh.
</div>
<div class="exercise">
    This won't come up here, but prive that $\sinv R$ is a PID when $R$ is a PID.
</div>

I think this should be everything we need for this post. With that done, when is a ring a UFD?

# UFD Criteria
I always hate trying to prove rings are UFDs because my go-to tactics are to prove something stronger (e.g. its a PID), but this clearly isn't always possible. The definition of a UFD is kind of messy, so it's nice to have alternative, sufficient conditions for the property. One[^4] such condition is

<div class="lemma">
    Let $R$ be an integral domain. If every element of $R$ is a product of primes, then $R$ is a UFD.
</div>
<div class="proof4">
    First, let $\pi$ be an irreducible element, and write $\pi=\tau_1\dots\tau_n$ as a product of primes. Then, since $\pi$ is irreducible, we really have (possibly after rearranging the $\tau_i$) that $\pi=u\tau_1$ for some unit $u$, so $\pi$ is a prime. Thus, every element of $R$ factors into a product of irreducibles. Suppose that
    $$u\pi_1\dots\pi_n=U\Pi_1\dots\Pi_N$$
    where $u,U$ are units and $\pi_i,\Pi_i$ are irreducibles ($\iff$ primes). We need to show that (possibly after rearrangement) $\pi_i,\Pi_i$ are associates and $n=N$. Well, $\pi_1$ is prime so $\pi_1\mid\Pi_j$ for some $j$. Rearrange to assume that $j=1$, and divide by $\pi_1$ to get that $u\pi_2\dots\pi_n=U'\Pi_2\dots\Pi_N$ for some unite $U'$. The claim then follows by induction, so $R$ is a UFD.
</div>
<div class="theorem" name="Kaplansky's Criterion">
    Let $R$ be an integral domain. Then, $R$ is a UFD iff every (nonzero) prime ideal of $R$ contains a (nonzero) principal prime ideal (i.e. contains a prime element).
</div>
<div class="proof4">
    $(\implies)$ This direction is easy. If $R$ is a UFD and $\mfp$ is a prime ideal, then consider any $x\in\mfp$. We can write $x=\pi_1\dots\pi_n$ as a product of prime elements, and primality of $\mfp$ implies that $(\pi_i)\subset\mfp$ for some $i$, giving us the result.
    <br>
    $(\impliedby)$ For this direction, let $S$ be the set of all (finite) products or prime elements of $R$ (including the empty product so $1\in S$). Then, $0\not\in S$ and $S$ is clearly multiplicative, so we can form the (nonzero) ring $A=\sinv R$. We claim that $A$ is a field. Pick any nonzero nonunit $r\in R$. Suppose that $1/r\not\in A$, so $(r)\subsetneq A$ meaning that it is contained in some maximal ideal $\mfm\subset A$. Then, $\mfp=\mfm\cap R$ is prime, and hence contains a principal prime ideal $(\pi)$. But this means that $\sinv(\pi)\subset\sinv\mfm\subsetneq A$ which is impossible as $\pi\in S$ so it's definitely a unit in $A$. Thus, $1/r\in A$, so we can write
    $$\frac1r=\frac b{\pi_1\dots\pi_n}\in A$$
    where $b\in R$ and the $\pi_i\in R$ are all prime. We now prove by induction on $n$ that $r$ is the product of prime elements. If $n=1$, then $rb=\pi_1$ so since primes are irreducible and $r$ is not a unit, $r$ must itself be prime. For $n>1$, we have $rb=\pi_1\dots\pi_n$ so each $\pi_i$ divides $r$ or $b$. If some $\pi_j$ divides $b$, then $b=c\pi_j$, so $rc$ is a product of $n-1$ primes, meaning $r$ is a product of primes by induction. Otherwise, each $\pi_i$ divides $r$ so $\parens{\frac r{\pi_1\dots\pi_n}}b=1$, making $b$ a unit and $r$ a product of primes. Hence, we have that every element of $R$ is a product of primes, and so $R$ is a UFD. 
</div>
<div class="cor">
    Every PID is a UFD.
</div>
<div class="cor">
    Let $R$ be a Dedekind domain. Then, $R$ is a UFD iff $R$ is a PID.
</div>

It is maybe worth mentioning that the above [^8] can be proven without localizing. You replace the supposition that $(r)\subsetneq\sinv R$ with the supposition that $(r)\cap S=\emptyset$ to eventually show that $rb=\pi_1\dots\pi_n$ for some $b$. When doing this, you have to use Zorn's lemma to show that there's some prime ideal of $R$ containing $(r)$ that is disjoint from $S$ whereas we get the analagous fact more easily by considering an appropriate maximal ideal of $\sinv R$[^7].

So UFDs are integral domains where every element is a product of primes or are integral domains where each prime ideal contains a principle prime ideal. To me, these conditions [^5] sound more reasonable to prove than the original unique factorization into irreducibles formulation. As an application of the second of them, we also prove the following.

<div class="theorem">
    Let $R$ be a UFD. Then, $\sinv R$ is a UFD.
</div>
<div class="proof4">
    Let $\mfq\subset\sinv R$ be a prime ideal, so $\mfp=\mfq\cap R$ is prime in $R$. This means that it contains a principal prime $(\pi)\subset\mfp$, so $\pi\in\mfq$. Thus, it suffices to show that $\pi$ is a prime of $\sinv R$. Pick $a/s,b/t\in\sinv R$ and suppose that $\pi\mid\frac{ab}{st}$. Then, $\pi\mid ab$ (multiply by $st$) so $\pi\mid a$ or $\pi\mid b$ ($\pi$ is prime in $R$), but this means that $\pi\mid a/s$ or $\pi\mid b/t$ (since $s,t$ are units). Thus, $\pi$ is prime in $\sinv R$ and $\sinv R$ is a UFD.
</div>

If that's not a clean proof, then I don't know what is [^6]. In addition, we can clear some intellectual debt by proving a statement I avoided earlier on this blog.

<div class="theorem">
    Let $R$ be a UFD. Then $R[x]$ is a UFD.
</div>
<div class="proof4">
    Let $\mfq\subset R[x]$ be a non-principal prime ideal. Let $\mfp=\mfq\cap R$, so $\mfp$ contains some prime ideal $(\pi)\subset R$ which means that $\pi\in\mfq$. Since $\pi$ is still prime as an element of $R[x]$ as $R[x]/(\pi)\simeq(R/(\pi))[x]$, a domain, Kaplansky's criterion implies that $R[x]$ is a UFD.
</div>
<div class="remark">
    In the standard proof of this fact, one first proves that $\F[x]$ is a UFD (even a PID) for $\F$ a field and then uses this to establish the theorem for general UFD via an argument that involves passing to the fraction field. A consequence of this is that anyone (who accepts this as the proof that $R$ UFD $\implies R[x]$ UFD) who says that $\F[x]$ is a UFD because $\F$ is a UFD is actually making a circular argument. One thing I like about the above proof instead, is that it allows you to non-circularly say that $\F[x]$ is a UFD because $\F$ is a UFD.
</div>

Based on the last two proofs, we see that the following holds in general. [^9]

<div class="theorem">
    Let $R$ be a UFD and let $A$ be an integral domain containing $R$. If all primes $\pi\in R$ of $R$ remain prime when considered as elements of $A$, then $A$ is a UFD.
</div>

# An Interesting Conjecture
First, a crash course on group rings.
<div class="definition">
    Let $R$ be a ring and $G$ be a group. The <b>group ring</b> $R[G]$ is the ring of formal sums
    $$R[G]=\brackets{\left.\sum_{g\in G}r_g\cdot e_g\right|r_g\in R}$$
    where $e_g\cdot e_h=e_{gh}$ for $g,h\in G$, and more generally:
    $$\parens{\sum_{g\in G}r_g\cdot e_g}\parens{\sum_{h\in G}s_h\cdot e_h}=\sum_{g\in G}\sum_{h\in H}r_gs_h\cdot e_{gh}$$
    The additive identity is the sum 0, and the multiplicative identity is the identity element of the group.
</div>
<div class="remark">
    Group rings satisfy the following:
    <ul>
        <li> $R[G]$ is commutative iff $G$ is abelian. </li>
        <li> $R[G]$ has zero divisors if $G$ has a torsion element. Indeed, if $x^n=1$ in $G$, then $(1-e_x)\in R[G]$ is a zero divisor (where by $1$ we technically mean $1e_1$).</li>
        <li> For $G=\Z$, we have $R[G]\simeq R[t,\inv t]\simeq R[t,s]/(1-st)$ </li>
    </ul>
</div>
Now, I came across Kaplansky's Criterion while trying to resolve the following:

<div class="question">
    Let $k$ be a field. Is the group ring $k[\Z^n]$ a UFD (or even a domain)?
</div>
This turns out to be true with a simple proof once you know that localization preserves UFD-ness.
<div class="theorem">
    Let $R$ be a UFD. Then, $R[\Z^n]$ is a UFD.
</div>
<div class="proof4">
    It is not hard to see that
    $$R[\Z^n]\simeq R[x_1,\inv x_1,\dots,x_n,\inv x_n]$$
    We now proceed by induction. The claim is true when $n=0$ since $R[\Z^0]\simeq R$, so suppose that $n>0$ and that $A:=R[x_1,\inv x_1,\dots,x_{n-1},\inv x_{n-1}]$ is a UFD. Then, $A[x_n]$ is a UFD as is its localization $A[x_n]\sqbracks{\frac1{x_n}}$ but clearly, $R[\Z^n]\simeq A[x_n]\sqbracks{\frac1{x_n}}$ so $R[\Z^n]$ is a UFD as claimed.
</div>

At this point, the only remaining question is why would I care about that. Well, one of my friends mentioned the following problem, and I was surprised that this is not already known to be true, so we set about convincing ourselves it held in the simplest possible case: finitely generated abelian groups.

<div class="conj" name="Kaplansky's Conjecture">
    Let $K$ be a field, and let $G$ be a torsion-free group. Then, the group ring $K[G]$ does not contain nontrivial zero divisors.
</div>

[^1]: Depending on how I'm feeling when I get to that part, I might also say why I care about this fact and/or "plug a hole" in this blog by proving that R[x] is a UFD when R is a UFD since I didn't [last time](../ring-intro) I had a chance to.
[^2]: "functor"
[^3]: I won't get into why it's called this, but it's related to studying functions defined near a point of a space by looking at the functions that do not vanish at that point.
[^4]: Two?
[^5]: Or at least the second one
[^6]: That's a lie; I do know. The following proof is even cleaner.
[^7]: The kicker is that proving that any ideal is contained in a maximal one involves using Zorn's lemma, so we still appeal to Zorn's lemma; we just do so more implicitly.
[^8]: theorem, not lemma or corollary
[^9]: I'm not gonna lie: Kaplansky's Criterion has way more applications than I realized when I started writing this post. Why isn't it more popular?