---
layout: post
title: "Algebra Part II"
modified:
categories: blog
excerpt:
series: "Algebra Primer"
tags: [math, algebra, rings, fields]
date: 2017-11-21 3:00:00
---

This is the second post in a series that serves as an introduction to abstract algebra. In the [last one](../group-intro), we defined groups and certain sets endowed with a well-behaved operation. Here, we'll look at rings which are what you get when your set has two operations defined on it, and we'll see that much of the theory for groups has a natural analogue in ring theory.

>Bit of a Disclaimer<br>
I can't possibly mention everything on a particular subject in one post, and I am not a particular fan of writing insanely long posts, so some things have to be cut. In particular, I aim to introduce most of the important topics in each subject without necessarily doing a deep dive, and while I will try to mention specific examples of things, I won't spend too much time looking at them closely. It will be up to you to take the time to make sure the example makes sense. Because of this, I'll try to include exercises that should be good checks of understanding. Finally, as always, things are presented according to my tastes and according to whatever order they happen to pop into my head; hence, they are not necessarily done the usual way.

## Rings and Better Rings
If you've heard of groups, I doubt I need to motivate rings much. Things like the integers, real numbers, matrices, etc. all form groups but when considering them as such, you have to make a choice about whether you want to consider they're additive structure, or their multiplicative structure; why not look at both? 

>Definition<br>
A **ring** $(R, +, \cdot)$ is a set $R$ together with two operations $+:R\times R\rightarrow R$ and $\cdot:R\times R\rightarrow R$ satisfying the following for all $a,b,c\in R$<br>
$$\begin{align*}
&\bullet (R, +)\text{ is an abelian group with additive identity }0\\
&\bullet a\cdot(b\cdot c) = (a\cdot b)\cdot c\\
&\bullet a\cdot(b+c) = a\cdot b+a\cdot c\text{ and }(a+b)\cdot c=a\cdot c+b\cdot c
\end{align*}$$<br>
If additionally, $a\cdot b=b\cdot a$ always, then we call this a **commutative ring**

There are a few things worth noticing about the definition of a ring. First of all, it's kinda short; at least, it was shorter than I expected the first time I saw it. There are like four different properties you need to satisfy to be an abelian group; to be a ring, you just need associative multiplication and (both left and right) distributivity. You don't need inverses, and you don't even need to have a multiplicative identity. This means you can get some weird stuff happening in general rings.

* In $2\Z$, you have $ab\neq a$ no matter which $a,b\in2\Z$ you choose
* In $\zmod8$, you get $4*2=0$ even though $4,2\neq0$
* Also in $\zmod8$, you get $7^2=1^2=3^3=5^2=1$ so you have 4 different square roots of $1$

Because of this, we will see a number of different types of rings with increasingly more conditions on them, guaranteeing nice behavior. Also, in case you were wondering by require an abelian group under addition and not just a group, it's because general groups and noncommutative rings are ugly enough separately, having one object that doesn't commute under addition or multiplication just sounds awful [^1]. Now, leet's see some additional conditions we may want to place on rings

>Definition<br>
A ring $R$ is said to **have unity** (alternatively, $R$ is **unital**) if there exists some $1\in R$ such that $a\cdot1=1\cdot a=a$ for all $a\in R$.

This gets rid of the first problematic ring I mentioned above, but not the other two. The third one may stick around for awhile, but the second we really don't like.

>Definition<br>
An element $a\in R$ is called a **zero divisor** if there exists some nonzero $b\in R$ such that $ab=0$

>Definition<br>
An **integral domain** $D$ is a commutative ring with unity and no zero divisors

>Question<br>
Is the zero ring an integral domain?

Now that's something we can work with. It practive, almost all rings you work with will have unity, the majority will be commutative [^2], and plenty of them will be integral domains. The fact that integral domains don't have zero divisors means that we can "cancel" multiplication. Normally when we have some equation like $ab=ac$, we cancel out the $a$'s and conclude that $b=c$. However, as the $4\cdot2=0$ example from $\zmod8$ shows, this isn't always legitimate. In high-school algebra, we justify this cancellation by 
saying we multiply both sides by $a^{-1}$, but $a^{-1}$ won't exist most of the time in general! Luckily, even if it doesn't we can still justify cancellation most of the time.

>Theorem<br>
Let $D$ be a ring. Then left (respectively, right) cancellation holds iff $D$ has no zero divisors

<div class="proof2">
Pf: $(\rightarrow)$ Assume left cancellation holds. Pick $a,b\in D$ such that $ab=0=a0$. By left cancellation, this means $b=0$ so there are no zero divisors.<br>
($\leftarrow$) Assume $D$ has no zero divisors. Pick $a,b,c\in D$ with $a$ nonzero such that $ab=ac$. Then, we can subtract to get $0=ac-ab=a(c-b)$. Since there are no zero divisors, either $a=0$ or $c-b=0$, but $a\neq0$ by assumption so $c-b=0$ and $c=b$. $\square$
</div>

Above you'll notice that we used $a0=0=0a$ for all $a$ in a ring. This is nonobvious, but also not all that profound. You can prove basic properties of rings like this [^3] without much effort, so I'll omit them. Furthermore, as with groups, we can define **ring homomorphisms (or ring maps)** as maps $f:R\rightarrow S$ such that $f(a+b)=f(a)+f(b)$ and $f(ab)=f(a)f(b)$; additionally, if $R,S$ both have unity we require $f(1_R)=1_S$. We can also define the **kernal** of a ring map $f:R\rightarrow S$ to be the subset of $R$ mapping into $0$. There's also a notion of subring that's exactly what you think it is.

For the rest of this post, I think we'll be looking (almost) exclusively at commutive rings with unity, so unless otherwise specified, assume that's the case. Now, before moving onto more definitions and whatnot, I want to make note of one of the most important classes of rings: polynomial rings.

> Definition<br>
Given a ring[^4] $R$, the **polynomial ring** $R[x]$ is the ring of (formal) polynomials in $x$ with coefficients in $R$.

The above definition isn't all that formal, but the idea is that you have things like $3x^2+2x-7\in\Z[x]$, $\pi x^4-e\in\R[x]$, $3x-1/2\in\Q[x]$, etc. One thing to be careful about is that two polynomials are equal iff they are identically the same; any polynomial $p(x)\in R[x]$ gives write to a function $$R\rightarrow R$$ via evaluation, but the mapping $p\mapsto[r\mapsto p(r)]$ [^6] is not necessarily injective! That is, you can have distinct polynomials that determine the same function such as $p(x)=x^2$ and $q(x)=x$ in $\zmod2[x]$; $p(x)\neq q(x)$ as polynomials even though $\forall n\in\zmod2:p(n)=q(n)$.

>Aside<br>
If you wan't to careful define the polynomial ring, you can define it as the subset of the ring $R^{\N}$ of functions from $\N$ to $R$ consisting of elements that evaluate to 0 on all but finitely many $n\in\N$. You also have to specify what multiplication looks like because it's not the usual componentwise product.

# Domains
Unfortunately, unlike the previous post on groups, there isn't some major result like Langrange's Theorem of the First Isomorphism Theorem that we're working towards here; this post is more a goaless overview of some basics in ring theory.

>Proposition<br>
If $D$ is an integral domain, then so is $D[x]$

Before proving this, we'll define the degree of a polynomial which is a notion we'll see more than once.

>Definition<br>
Given some polynomial $p(x)=\sum_{k=0}^na_kx^k\in R[x]$, its **degree** $\deg p(x)$ is the largest $k$ such that $a_k\neq0$. Note that $\deg0$ is undefined whereas $\deg r=0$ for any nonzero $r\in R$.

>Remark<br>
Given nonzero $p,q\in D[x]$ where $D$ is an integral domain, we have $\deg(pq)=\deg p+\deg q$ which is simple but important.

The above remark is actually strong enough to imply to proposition, so we omit a formal proof of that. In the remark, we require $D$ to be an integral domain so that the leading coefficient [^5] of $pq$ is guaranteed to be nonzero since it's the product of two nonzero things (i.e. the leading coefficients of $p$ and $q$). I don't have a good transition here, but another important thing related to integral domains is...

>Definition<br>
Given a (possibly non-commutative) ring $R$ with unity, there is a unique ring map $\Z\rightarrow R$ (why?). If $D$ is a domain, then we define the **characteristic** $\Char D$ of $D$ to be the least positive $n\in\Z$ mapping to 0 under this unique ring map. If no positive integer maps to 0, then we say $\Char D=0$.

There are a few ways to think of characteristic. In a while when we define ideals, it'll become clear that the characteristic of $D$ is the generator of $\ker(\Z\rightarrow D)$; we can also say that $\Char D$ is the (least) number of times you can add 1 to itself in a ring before getting $0$ [^7]; alternatively, remembering that rings are abelian groups, $\Char D$ is the additive order of $1$. Good examples to keep in mind here are $\Char\Z=0$ and $\Char\zmod p=p$. Vaguely put, characteristic is a good indicator for the behavior of a ring; weird things can happen in rings of low characteristics.

>Theorem<br>
Given an integral domain $D$ of nonzero characteristic, $\Char D$ is prime

<div class="proof2">
Pf: Let $D$ be an integral domain and assume $\Char D=n\neq0$. Now, write $n=ab$ ($a,b$ both positive) and let $f:\Z\rightarrow D$ be the ring map. We have $0=f(n)=f(ab)=f(a)f(b)$ but $D$ has no zero divisors so $f(a)=0$ or $f(b)=0$. Assume WLOG that $f(a)=0$. Since $a\le n$ and $n$ is the minimal integer with $f(n)=0$, we conclude that $a=n$ which means $b=1$. Thus, the only divisors of $n$ are $1,n$ so $n$ is prime. $\square$
</div>

>Corollary<br>
$\zmod n$ is an integral domain implies that $n$ is prime

The converse of that corollary is true as well, and proving both directions is left as an exercise. Let's shift gears a little, and instead of talking about properties of rings, we'll look at some specific types of elements.

>Definitions<br>
Let $R$ be a ring. An element $r\in R$ is called a **unit** if it divides 1. That is, there exists some $s\in R$ such that $rs=1$. We say a non-zero non-unit $r\in R$ is **irreducible** if whenever we write $r=ab$, it must be the case that either $a$ or $b$ is a unit. Finally, a non-zero non-unit $r\in R$ is **prime** if $r\mid ab$ implies that $r\mid a$ or $r\mid b$.

In the integers $\Z$, the only units are $\pm1$, and prime and irreducible mean the same thing. In general, prime implies irreducible.

>Theorem<br>
Let $D$ be an integral domain. Then, every prime element is irreducible

<div class="proof2">
Pf: Pick some prime $p\in D$ and write $p=ab$. Then, $p\mid ab$ so $p\mid a$ or $p\mid b$. Assume WLOG that $p\mid a$ and write $a=pc$. Substituting into the first equation, we have $p=pcb$ which means $1=cb$ and so $b$ was a unit. $\square$
</div>

The converse of this theorem does not hold in general though. For a counter example, we can consider the ring $\Z[\sqrt{-5}]=\\{a+b\sqrt{-5}:a,b\in\Z\\}$. Here, $2$ is irreducible as can easily be proven using the norm map [^8]. However, $2$ divides $6=(1+\sqrt{-5})(1-\sqrt{-5})$ but divides neither of $1\pm\sqrt{-5}$ since, for example, any multiple of $2$ will have both components even. Since the two definitions coincided for integers, we'd like to study other rings where they are the same as well. To that end, we define the following

>Definition<br>
A **unique factorization domain** (or UFD) $U$ is an integral domain where every non-zero $x\in U$ can be written as a product $x=up_1p_2\dots p_n$ of a unit $u$ with irreducibles $p_i$. Furthermore, this representation is unique in the sense that given $x=wq_1q_2\dots q_m$ as well, we must have $m=n$ and (after rearrangement) $q_i=v_ip_i$ for units $v_i$.

That definition is a bit of a mess, but the basic idea is that we have some analogue of the fundamental theorem of arithmetic. A good example of a UFD to keep in mind is $\Z[x]$, and in fact more generally

>Theorem<br>
If $U$ is a UFD, then so is $U[x]$

<div class="proof2">
Pf: Omitted. At this point, I don't think we've quite developed enough theory to prove this nicely, so look up a proof after finishing this post.
</div>

Because I don't want to wait too long before saying this, and because it's related previously omitted proof, let's look at just about the nicest rings known to algebra.

>Definition<br>
A **field** $k$ is a ring such that $(k-\\{0\\},\cdot)$ is an abelian group. i.e. all non-zero elements of $k$ are units.

Examples of fields include $\Q, \R, \C,$ and $\qadjs2=\\{a+b\sqrt2:a,b\in\Q\\}$. Because multiplicative inverses exist, cancellation automatically holds in fields and so all fields are domains. The 4 examples I just gave all have characteristic 0, but fields with prime characteristic exist as well.

>Proposition<br>
$\zmod p$ is a field. More generally, any finite domain is a field.

<div class="proof2">
Pf: Let $D$ be a finite domain, and fix some non-zero $d\in D$. Consider the map $m_d:D\rightarrow D$ given by $m_d(a)=da$. We claim this map is injective. Pick some $a\in\ker m_d$. Then, $m_d(a)=da=0\implies a=0$ since $d\neq0$ by assumption. Thus, $m_d$ has trivial kernal and hence is injective. Now, any injective map between finite sets is automatically surjective, so $\image m_d=D$. In particular, there exists some $c\in D$ such that $m_d(c)=dc=1$ so $d$ has an inverse. $\square$ 
</div>

When thinking of $\zmod p$ as a field, we usually denote it $\F_p$ and call it the (finite) field with $p$ elements. This is not the only connection between domains and fields. It's clear that every subring of a field is a domain, but it turns out the converse also holds.

>Definition<br>
Given a domain $D$, its **field of fractions** $\Frac(D)$ is the fields whose elements are formal symbols $\frac ab$ ($a,b\in D$) modded by the relation $\sim$ with addition and multiplication given by<br><center>
$$\begin{align*}
	\frac ab+\frac cd=\frac{ad+bc}{bd} && \frac ab\frac cd=\frac{ac}{bd} && \frac ab\sim\frac cd\iff ad=bc
\end{align*}$$</center>
Note that we can embed $D$ in its field of fractions via the map $d\mapsto\frac d1$

It's up to you to verify that this construction gives an actual field. After that, forgetting fields for a moment, we look again at the definition of a UFD and realize that units can be annoying, so we'll turn our attention to something a little more unit-agnostic.

# Ideals
The big payoffs of the group theory post both were related to the idea of quotient groups. In this section, we'll see how to define the analgous idea of quotient rings.

>Definition<br>
Given a ring $R$, an **ideal** $I\subseteq R$ is an additive subgroup such that $ar\in I$ for all $a\in I$ and $r\in R$.

>Remark<br>
Depending on the author, ideals may or may not be rings. They are if you don't require rings to have unity, but aren't otherwise.

We could have followed the footsteps of the group theory post and defined ideals as kernels of ring maps, but ideals have more a life of their own that normal subgroups, so this definition is the one always used.

>Proposition<br>
Given a ring map $f:R\rightarrow S$, its kernal $\ker f\subseteq R$ is an ideal.

<div class="proof2">
Pf: Exercise to reader
</div>

Now, recall that in abelian groups, all subgroups are normal. Luckily for us, all rings are additive abelian groups, so ideals are automatically normal subgroups. This means we can form the quotient group $R/I$ as before; however, the additional condition that $I$ "absorbs" $R$ ensures that we can endow this quotient with a ring structure.

>Definition<br>
Given a ring $R$ and ideal $I\subseteq R$, the **quotient ring** $R/I$ is the quotient group endowed with the following multiplication of cosets<br><center>$$(a+I)(b+I)=ab+I$$</center>

>Exercise<br>
Verify that this definition gives a well-defined ring.

>Exercise<br>
Prove the first isomorphism theorem for rings: Given a surjective ring map $f:R\rightarrow S$, we have $R/\ker f\simeq S$

As there are different types of rings, we have different types of ideals depending on how nice the associated quotient ring is. It's worth convincing yourself that any ideal containing a unit must be all of $R$, and the only ideals of a field are the trivial ones [^9]. 

>Definition<br>
Let $R$ be a ring and $I\subseteq R$ an ideal of $R$. We say that $I$ is **prime** if $R/I$ is an integral domain, and $I$ is **maximal** if $R/I$ is a field.

>Theorem<br>
Let $R$ be a ring with ideal $I$. Then, $I$ is prime iff $ab\in I\implies a\in I$ or $b\in I$, and $I$ is maximal iff $I\neq R$ and given any ideal $J$ with $I\subseteq J\subseteq R$, either $J=I$ or $J=R$.

<div class="proof2">
Pf: The statement about prime ideals is left as an exercise, but we'll prove the one about maximal ideals here. $(\rightarrow)$ Assume $I$ is maximal, and pick some ideal $J$ with $I\subseteq J\subseteq R$. Let $f:R\rightarrow R/I$ be the quotient map. It's easily verified that $f(J)$ is an ideal so $f(J)=\{0\}$ or $f(J)=R/I$. In the first case, we have $J\subseteq\ker f=I\implies J=I$. In the second, any preimage of $1\in R/I$ is necessarily a unit, so $J=R$ as it contains a unit. ($\leftarrow$) Conversely, assume that $I\subseteq J\subseteq R\implies J=I$ or $J=R$. Let $f:R\rightarrow R/I$ be the quotient map again, and consider an ideal $\tilde J\subseteq R/I$. It's again easily verified that $f^{-1}(\tilde J)$ is an ideal. Since $0\in\tilde J$, we must have $I\subseteq f^{-1}(\tilde J)\subseteq R$ so $\tilde J=\{0\}$ or $R/I$. This implies that $R/I$ is a field. Indeed, given any nonzero $x\in R/I$, the ideal it generates $(x)=R/I$ so there must be some $y\in R/I$ such that $xy=1$. $\square$
</div>

The above proof makes use of the **ideal generated by x** which is given by $(x)=Rx=\\{rx:r\in R\\}$. We can generalize this notion to any collection of elements

>Definition<br>
Given a (not necessarily finite) subset $S\subseteq R$, the **ideal generated by S** is the ideal<br><center>$$\left\{\sum_{s\in S}a_s\cdot s:a_s\in R,\text{all but finitely many }a_s\text{ are zero}\right\}$$</center>
When $S=\\{x_1,\dots,x_n\\}$ is finite, this is commonly denoted<br><center>$$(x_1,\dots,x_n)=\sum_{i=1}^nRx_i=\{r_1x_1+\dots+r_nx_n:r_i\in R\}$$

With this, we can define that last special type of ideal in this post.

>Definition<br>
We call an ideal $I\subseteq R$ **principal** (or say it's **principally generated**) if it is generated by a single element.

Principal ideals are some of the nicest ideals, and behave very similar to numbers (i.e. elements of $R$). However, they have the added benefit that if you multiply one by a unit, nothing changes. Hence, we arrive at our next kind of ring

>Definition<br>
If $R$ is a domain where every ideal is principal, then we call $R$ a **principal ideal domain**, or **PID**.

>Theorem<br>
Every PID is a UFD

<div class="proof2">
Pf: One of my goals this post is to avoid writing any proofs involving UFDs, so omitted.
</div>

Examples of PIDs include $\Z$, and as we'll see in a moment $k[x]$ for $k$ a field. One thing that is true in general is that $(p)$ is a prime ideal if $p$ is a prime element. Given the following theorem, this means that for PIDS, every prime ideal is maximal.

>Theorem<br>
In a PID, an ideal is maximal iff its generated by an irreducible

<div class="proof2">
Pf: $(\leftarrow)$ Let $I=(r)$ where $r\in R$ is irreducible and $R$ is a PID. Consider some ideal $J=(a)$ with $I\subseteq J\subseteq R$. Since $r\in(a)$, there must exist some $b\in R$ with $r=ab$. However, because $r$ is irreducible, either $a$ is a unit or $b$ is. If $a$ is a unit, then $J=R$. If $b$ is a unit, then $J=I$ since unit multiplies generate the same ideal. Thus, $I$ is maximal. ($\rightarrow$) Run the same argument in reverse: $I=(r)$ is maximal and $r=ab$ implies $(r)\subseteq(a)\subseteq R$ so fill in the blank. $\square$
</div>

One application of the above theorem is that it let's us generate fields of varying sizes.

>Exercise<br>
Show that if $f(x)\in\F_p[x]$ is an irreducible polynomial, then $\F_p[x]/(f(x))$ is a finite field of size $p^{\deg f}$

Showing something is a PID directly can be difficult, so it's sometimes helpful to instead show the stronger condition that your ring has a Euclidean algorithm on it.

>Definition<br>
A **Euclidean domain** $E$ is an integral domain with a function $f:R-\\{0\\}\rightarrow\Z_{\ge0}$ such that for any $a,b\in R$ with $b\neq0$, there exists $q,r\in R$ where $a=bq+r$ and $r=0$ or $f(r)<f(b)$.

In essence, you can perform division in $E$, and there's a sense in which the remainder is smaller than what you started with. Examples include $\Z$ where $f(n)=\|n\|$ and any field $k$ with $f(x)=1$. A more interesting example is the Gaussian integers $\Z[i]$ with $f(a+bi)=a^2+b^2$. If you've been paying attention, you'll notice that there was no $R\text{ PID}\implies R[x]\text{ PID}$ theorem; this is because this statement is false (for a counter example, consider $R=\Z$. The ideal $(2,x)\subset\Z[x]$ is not principal). However, with strong assumptions, you can get something almost like this.

>Theorem<br>
If $k$ is a field, then $k[x]$ is a Euclidean domain

<div class="proof2">
Pf sketch: For your function $f:k[x]-\{0\}\rightarrow\Z_{\ge0}$, you just use $f(p)=\deg p$. With this choice, polynomial long division gets you what you need. Since we're working over a field, you can always scale the leading coefficient of the divisor to cancel out all higher order terms of the dividend so that the remainder has strictly smaller degree. $\square$
</div>

>Theorem<br>
Every ED is a PID

<div class="proof2">
Pf: Let $E$ be a Euclidean domain with ideal $I$. Pick non-zero $x\in I$ so that $f(x)$ is minimal among elements of $I$. Now, consider any $a\in I$ and divide to get $a=xq+r$ where $r=0$ or $f(r)< f(x)$. We claim that $a\in(x)$. Note that $r=a-xq\in I$ so $f(r)\ge f(x)$ (if $r\neq0$) by minimality of $x$. This means that $r=0$ so $a=xq\in(x)$ as desired and so $I=(x)$ is principal. $\square$
</div>

Hence, the polynomial ring over any field is a PID.

# A Glimpse of Field Theory
Hopefully there's nothing major I forgot to say [^10]. With this last bit, I want to mention one neat result about fields. For this, I'm going to need to assume you know a little linear algebra: specifically, the definition of a vector space over a field, and the fact that every vector space has a basis. We'll use this to show that the sizes of fields are pretty constrained.

>Definition<br>
Let $F,E$ be fields and assume that $F\subseteq E$. We call $E$ an **extension field** of $F$ and denote this $F/E$

One of the most important things about extension fields is that if $F/E$ is a field extension, then $F$ is an $E$-vector space! Although it's not difficult to see, you should verify this claim. It basically boils down to the fact that multiplication is linear.

>Definition<br>
The **degree** of a field extension $E/F$ is $[E:F]=\dim_FE$ the dimension of $F$ as an $E$-vector space

With that, our last result

>Theorem<br>
Let $E$ be a finite field. Then, $|E|=p^n$ for some prime $p$ and integer $n$

<div class="proof2">
Pf: Let $p=\Char E$ which must be prime since it's nonzero. Let $F$ be $E$'s so-called $\textit{prime subfield}$ which is the image of the map $\Z\rightarrow E$. Finally, let $n=[E:F]$ and let $e_1,\dots,e_n\in E$ be an $F$-basis for $E$. Then, every element of $E$ can be written uniquely in the form $$a_1e_1+\dots+a_ne_n$$ where $a_i\in F$. Since $|F|=\Char E=p$, and there are $n$ coefficient's to choose, there are $p^n$ expressions of this form and correspondingly $|E|=p^n$. $\square$
</div>

[^1]: Also, such objects don't show up in practice then often (read: ever)
[^2]: Matrices are the standard example of non-commutative rings
[^3]: (multiplicative) inverses are unique when they exists, if its a ring with unity that (-1)a = -a (i.e. -1 times a is the additive inverse of a), etc.
[^4]: While typing this, I realized I don't know if people ever work in polynomials over non-commutative or non-unital rings
[^5]: coefficient of $x^d$ where $d=\deg p$
[^6]: This is shorthand for a map that given a polynomial p, returns a function that takes some element r and returns p(r), the result of evaluation p at r
[^7]: This is how I've always seen characteristic define, but it leads to confusing notation like n1:=1+1+...+1 (n times), so you write things like n1=(ab)1=(a1)(b1) and it gets annoying to keep track of which 1's matter and which you can drop because identity. I much prefer making explicit mention to a ring map
[^8]: previously defined [here](../solving-pell)
[^9]: the zero ideal and the field itself
[^10]: Worst-case scenario, I just edit this post later on to add in anything missing