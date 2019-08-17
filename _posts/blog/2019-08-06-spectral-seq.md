---
layout: post
title: "Spectral Sequences"
modified:
categories: blog
excerpt:
tags: [math, homological algebra, primer, algebraic topology, category theory]
date: 2019-08-06
hidden: true
---

<b>If you're somehow seeing this right now, look away. It's not finished, and I'm not sure when/if it will be</b>

$
\newcommand{\msC}{\ms C}
\newcommand{\msA}{\ms A}
\DeclareMathOperator{\Ch}{Ch}
\DeclareMathOperator{\CoCh}{CoCh}
\DeclareMathOperator{\Fil}{Fil}
$
Back when I was in high-school, I became really interested in this thing called "machine learning." The main idea is that you bombard some algorithm with a ton of examples (of a task being performed or of objects being classified), and then you cross your fingers and hope it has managed to reliably learn how to do what the examples showcased. One big draw of this approach is that there are many tasks where it is not clear how to accomplish them, but where it feels like there has to be enough information present that accomplishing them is possible. For example, imagine writing a program that takes in an image and tells you if there's a bird in it; this is hard to do algorithmically, but certainly the pixel values of an image contain enough information to decide whether or not there's a bird there [^1]. The moral of this detour is that sometimes we find ourselves in situations where we have lots of information available to tackle some problem, but figuring out how to utilize all that information is quite tricky. Imagine, for example, you have some topological space $X$ with a filtration

$$X^0\subseteq X^1\subseteq X^2\subseteq\cdots\subseteq X$$

such that $X=\dirlim X^k$. The example to keep in mind is $X$ a CW-complex, and $X^k$ its $k$-skeleton. Intuitively, the cohomology groups $\hom^n(X^k)$ should approximate $\hom^n(X)$, so if you know all of them, then you should have enough information to say something about $\hom^n(X)$. Figuring out exactly what you can say in this situation (and others) is the aim of spectral sequences, which, if you haven't guessed yet, are the stars of this post.

Specifically, I'll speak abstractly about two common sources of spectral sequence. Because I really wanna talk about this material [^2], I won't do my usual thing of trying to write as if everything I've written previously on this blog forms a dense subset of what I'm assume the reader knows. Instead, I'll assume you're comfortable with the words like cohomology, category, and other things that start with a c, then go from there. With that said, I'll briefly define abelian categories, say what a spectral sequence is, given an example, and depending on how I'm feeling at the end, either say the word hypercohomology or save that for a future post. Let's get started$\dots$

# Abelian Categories Briefly

An abelian category is one that behaves like the category of abelian groups. These form the main setting for much of homological algebra, so it's probably worthwhile to see how they're defined at least once. I'll build up the definition piece by piece.

<div class="definition">
    A category $\msC$ is called <b>preadditive</b> if every hom set $\Hom_{\msC}(A,B)$ (where $A,B\in\ob\msC$) is an abelian group such that composition of morphisms is bilinear.
</div>

To get to the next step, we need the notion of a biproduct, which is just an object that is both a product (think direct product) and coproduct (think direct sum). I guess I'll define what a coproduct (of two objects) is, and leave defining product to you.

<div class="definition">
    Let $\msC$ be a category, and fix objects $X_1,X_2\in\ob\ms C$. A <b>coproduct</b> of $X_1$ and $X_2$ is an object $X$ (often denoted $X_1\amalg X_2$) together with a pair of morphisms $\iota_1:X_1\to X,\iota_2:X_2\to X$ satisfying the below universal property:
    <ul>
        <li> 
            for every object $Y\in\msC$ with maps $f_1:X_1\to Y$ and $f_2:X_2\to Y$, there exists a unique morphism $f:X\to Y$ such that the below diagram commutes
            <center>
                <img src="{{ site.url }}/images/blog/spectral-seq/coprod.png" width="350" height="100">
            </center>
        </li>
    </ul>
    In short, it's an object such that "maps out of the coproduct are maps out of each factor." In medium, it is an object that is initial in the category of objects of $\msC$ with maps from $X_1$ and $X_2$. 
</div>
<div class="remark">
    The above defines a binary coproduct. You can easily extend this definition to that of a coproduct of objects $X_i$ where $i\in I$ ranges through an arbitrary index set.
</div>
<div class="example">
    Coproducts in $\textrm{Set}$ are disjoint unions, and coproducts in $\textrm{Ab}$ are direct sums.
</div>

Now, define products in a dual way, i.e. "maps into products are maps into each factor," and then say a biproduct is an object that is both a product and coproduct (of the same set of objects). This brings us to

<div class="definition">
    A preadditive category $\msC$ is called <b>additive</b> if every finite set of objects has a biproduct, and a zero object  $0\in\msC$ (i.e. one that is both initial and final) exists.
</div>
<div class="notation">
    Given $A,B\in\msC$, an additive category, let $0_{AB}\in\Hom_{\msC}(A,B)$ denote the morphism given composed from $A\to0\to B$.
</div>

For the next step, we need to know how to define kernels and cokernels. 

<div class="definition">
    Let $\msC$ be an additive category (or even just a category with zero morphisms), and fix any morphism $f:X\to Y$ in $\msC$. Then, an object $M$ is called a <b>kernel</b> of $f$, usually denoted $\ker f$, if it is final in the category of maps to $A$ "killed by $f$". I mean to say, there exists a morphism $\mu:M\to X$ such that for any morphism $\alpha:A\to X$ such that $f\circ\alpha=0_{AY}$, there exists a unique $a:A\to M$ making the following diagram commutes
    <center>
        <img src="{{ site.url }}/images/blog/spectral-seq/ker.png" width="250" height="100">
    </center>
</div>

Cokernels are define similarly as being initial with respect to maps $\nu:Y\to N$ such that $\nu\circ f=0$. Now,

<div class="definition">
    An additive category is <b>preabelian</b> if every morphism has both a kernel and a cokernel.
</div>

Almost there. Note that if $\mu:\ker f\to X$ is the kernel of a map $f:X\to Y$, then $\mu$ is a monomorphism, i.e. if we have $a:A\to\ker f$ and $b:A\to\ker f$ such that $\mu\circ a=\mu\circ b$, then $a=b$ [^3]. We would like every monomorphism to arise in this way. Similarly, cokernels are epimorphisms, and we would like them to be the only epimorphisms [^4].

<div class="definition">
    Let $\msC$ be a preabelian category. A monomorphism is called <b>normal</b> if it is also a kernel, and an epimorphism is called <b>conormal</b> (or still just <b>normal</b>) if it is also a cokernel.
</div>
<div class="definition">
    A preabelian category is an <b>abelian category</b> if every monomorphism is normal and every epimorphism is conormal.
</div>

To sum it all up, an abelian category is one with a zero object, all binary biproducts, all kernels and cokernels, and where all monomorphisms/epimorphisms are normal. Lot's of the language used in the theory of abelian groups (quotients, subobjects, exactness, etc.) carries over to arbitrary abelian categories in a fairly straightforward manner, so you can often get away with imagining elements of abstract abelian categories as just being abelian groups or $R$-modules, or what have you. Before moving on, here's one important example of an abelian category.

Fix an additive category $\msA$. A <b>chain complex</b> [^5] $A_\bullet$ is a sequence

$$A_\bullet:\cdots\too A_1\xtoo{d_1} A_0\xtoo{d_0} A_{-1}\too\cdots$$

of morphisms in $\msA$ such that $d_n\circ d_{n+1}=0$ for all $n$. A <b>chain map</b> $f:A_\bullet\to B_\bullet$ is a commutative diagram

$$\begin{CD}
    \cdots @>>> A_1 @>d_1>> A_0 @>d_0>> A_{-1} @>>> \cdots\\
    &@Vf_{-1}VV @Vf_0VV @Vf_1VV\\
    \cdots @>>> B_1 @>d_1>> B_0 @>d_0>> B_{-1} @>>> \cdots
\end{CD}$$

whose rows are chain complexes. Let $\Ch_\bullet(\msA)$ denote the category whose objects are chain complexes in $\msA$, and whose morphisms are chain maps.

<div class="exercise">
    Show that $\Ch_\bullet(\msA)$ is an abelian category if $\msA$ is (hint: do everything componentwise).
</div>

Before going on, I should maybe also say what homology is.

<div class="definition">
    Given a category $\msC$ and a morphism $f:X\to Y$ in $\msC$, the <b>image</b> of $f$ is an object $I$, usually denoted $\im f$, with a monomorphism $\iota:I\to Y$ that is initial among morphisms that $f$ factors through. That is, there exists a morphism $e:X\to I$ such that for any morphisms $e':X\to I'$ and $m':I'\to Y$ where $f=m'\circ e'$, there is a unique morphism $v:I\to I'$ making the below diagram commute
    <center>
        <img src="{{ site.url }}/images/blog/spectral-seq/im.png" width="250" height="100">
    </center>
</div>
<div class="remark">
    When $\msC$ is an abelian category, we have $\im f\simeq\ker(\coker f)$.
</div>
<div class="definition">
    Let $A_\bullet=\bracks{d_n:A_n\to A_{n-1}}$ be a chain complex. Its <b>$n$th homology object</b> should intuitively be $\hom_n(A_\bullet)=\ker d_n/\im d_{n+1}$. I guess the way we make this formal/general/whatever is by setting
    $$\hom_n(A_\bullet):=\coker\parens{\im d_{n+1}\to\ker d_n}$$
    where the map $\im d_{n+1}\to\ker d_n$ exists (and is unique) because the composition $\im d_{n+1}\to A_n\xto{d_n}A_{n+1}$ is the zero map.
</div>

# Spectral Sequence of a Filtered Complex

Now we start developing the good stuff. I should probably start by saying that I will only be considering spectral sequences in cohomology in this post, so, for example, we'll we be working in the (abelian) category $\CoCh(\msA)$ of cochain complexes of an abelian category $\msA$. [^6]

For the remainder of this post, fix some abelian category $\msA$. Probably a good place to start here is with the definition of a filtered complex.
<div class="definition">
    A <b>decreasing filtration</b> $F$ on an object $A\in\msA$ is a famility $(F^nA)_{n\in\Z}$ of subobjects of $A$ such that
    $$A\supseteq\dots\supseteq F^nA\supseteq F^{n+1}A\supseteq\dots\supseteq0.$$
    A <b>filtered object</b> of $\msA$ is a pair $(A,F)$ consisting of an object $A\in\msA$ and a decreasing filtration $F$ on $A$. A <b>morphism</b> $(A_1,F_1)\to(A_2,F_2)$ of filtered objects is a morphism $\phi:A_1\to A_2$ such that $\phi(F_1^kA_1)\subset F^k_2A_2$ for all $k\in\Z$. We thus arrive at the category $\Fil(\msA)$ of filtered objects.
</div>
<div class="definition">
    Given a filtered object $(A,F)$, we get <b>associated graded objects</b> $G^kA=F^kA/F^{k+1}A$.
</div>
<div class="definition">
    A filtration $F$ on an object $A$ is called <b>bounded</b> (or <b>finite</b>) if there exists $n,m$ such that $F^nA=A$ and $F^mA=0$.
</div>
<div class="definition">
    A <b>filtered cochain complex</b> is an object in the category $\CoCh(\Fil(\msA))$ (equivalently, one in $\Fil(\CoCh(\msA))$).
</div>

Let $A^\bullet=\bracks{d_n:A^n\to A^{n+1}}$ be a filtered cochain complex. Its differential $d$ induces a well-defined differential $G^pA^n\to G^pA^{n+1}$, so we get an associated graded chain complex $G^pA^\bullet$. Furthermore, we get a natural filtration on cohomology given by

$$F^p\hom^n(A^\bullet)=\bracks{\alpha\in\hom^n(A^\bullet)\mid\exists x\in F^pA^n:\alpha=[x]},$$

which has assocated graded pieces $G^p\hom^n(A^\bullet)$. If we're lucky this grading will actually determine the cohomology of $A^\bullet$ via the short exact sequences

$$0\too F^{p+1}\pull\hom(A^\bullet)\too F^p\pull\hom(A^\bullet)\too G^p\pull\hom(A^\bullet)\too0.$$

It's sometimes easier to compute $\pull\hom(G^pA^\bullet)$ than $G^p\pull\hom(A^\bullet)$, so we may wonder about comparing the two in order to eventual get a handle on $\pull\hom(A^\bullet)$. It turns out that we can get from one to the other via a series of "successive approximations."

We start by denoting the associated graded complex by

$$E_0^{p,q}:=G^pA^{p+q}\text{ }\text{ with differential }\text{ }d_0^{p,q}:E^{p,q}_ 0\to E_0^{p,q+1}.$$

Denote the cohomology of this complex by

$$E_1^{p,q}:=\hom^{p+q}(G^pA^\bullet)=\frac{\ker\big({d_0^{p,q}:E_0^{p,q}\to E_0^{p,q+1}}\big)}{\im\parens{d_0^{p,q-1}:E_0^{p,q-1}\to E_0^{p,q}}}=\frac{\ker\big({d_0^{p,q}:G^pA^{p+q}\to G^pA^{p+q+1}}\big)}{\im\parens{d_0^{p,q-1}:G^pA^{p+q-1}\to G^pA^{p+q}}},$$

which we think of as a "first-order approximation" to $\pull\hom(A^\bullet)$. Let's explicitly construct a second-order approximation. Note that a cohomology class $\alpha\in E_1^{p,q}$ can be represented by a chain $x\in F^pA^{p+q}$ with differential $dx\in F^{p+1}A^{p+q+1}$. With this in mind, we define

$$\mapdesc{d_1^{p,q}}{E_1^{p,q}}{E_1^{p+1,q}}{\alpha}{[dx]}$$

One easily sees that $d_1^{p,q}\circ d_1^{p+1,q}=0$ [^7], and so we are justified in defining

$$E_2^{p,q}:=\hom^p(E_1^{\bullet, q})=\frac{\ker\big({d_1^{p,q}:E_1^{p,q}\to E_1^{p+1,q}\big)}}{\im\parens{d_1^{p-1,q}:E_1^{p-1,q}\to E_1^{p,q}}}.$$

As a sanity check to make sure things make sense, try doing the following.

<div class="exercise">
    Suppose that $F^{-1}A^\bullet=0$ and $F^1A^\bullet=A^\bullet$ (so $F^0A^\bullet$ is just some subcomplex). Show that in this case, we have $E_2^{p,q}=G^p\hom^{p+q}(A^\bullet)$.
</div>

Returning to general filtrations, we can continue to construct higher order approximations. Doing one more step before handling general approximations, note that an $\alpha\in E_2^{p,q}$ can be represented by some $\st\alpha\in E_1^{p,q}$ with differential $d_1\st\alpha=0\in E_1^{p+1,q}$. Since $d_1\st\alpha=[dx]$ where $x\in F^pA^{p+q}$ is any chain representing $\alpha$, we can take $dx$ to be the zero element of $\ker(d_0^{p+1,q})$, which is to say we can take $x$ s.t. $dx\in F^{p+2}A^{p+q+1}$ [^9]. This suggest we can get a map $d_2^{p,q}:E_2^{p,q}\to E_2^{p+2,q-1}$.

Based on what we've seen so far, it seems as though elements of an $r$th order approximation $E_r^{p,q}$ should be ultimately represented by cycles $x\in F^pA^{p+q}$ such that $dx\in F^{p+r}A^{p+q+1}$. This turns out to be exactly the case. For $r\ge0$, define

$$\begin{align*}
    Z_r^{p,q} &=\frac{F^pA^{p+q}\cap\inv d\parens{F^{p+r}A^{p+q+1}}+F^{p+1}A^{p+q}}{F^{p+1}A^{p+q}}\\
    B_r^{p,q} &=\frac{F^pA^{p+q}\cap d\parens{F^{p-r+1}A^{p+q-1}}+F^{p+1}A^{p+q}}{F^{p+1}A^{p+q}}
\end{align*}$$

and let $E_r^{p,q}=Z_r^{p,q}/B_r^{p,q}$. On these objects, we can define a differential

$$\mapdesc{d_r^{p,q}}{E_r^{p,q}}{E_r^{p+r,q-r+1}}{[z]}{[dz]}$$

where $z\in F^pA^{p+q}\cap\inv d(F^{p+r}A^{p+q+1})$. Note that $d_r$ has bidegree $(r,1-r)$. With these definitions set up, we have the following [^10].

<div class="theorem">
    <ol>
        <li> The map $d_r^{p,q}$ is well-defined with $d_r^{p,q}\circ d_r^{p-r,q+r-1}=0$. </li>
        <li> $E_{r+1}$ is given by taking the cohomology of $E_r$, i.e.
            $$E_{r+1}^{p,q}\simeq\frac{\ker\parens{d_r^{p,q}:E_r^{p,q}\to E_r^{p+r,q-r+1}}}{\im\parens{d_r^{p-r,q+r-1}:E_r^{p-r,q+r-1}\to E_r^{p,q}}}$$
        </li>
        <li> $E_1^{p,q}=\hom^{p+q}(G^pA^\bullet)$. </li>
        <li> If the filtration of $A^\bullet$ is bounded, then for every $p,q$, for $r$ sufficiently large, we have $E^r_{p,q}=G^p\hom^{p+q}(A^\bullet)$. In this case, we say $E_1$ <b>converges</b> (or <b>abuts</b>) to $\hom^{p+q}(A^\bullet)$. </li>
    </ol>
</div>
<div class="proof4">
    For convenience, let $K_r^{p,q}=F^pA^{p+q}\cap\inv d(F^{p+r}A^{p+q+1})$ and $I_r^{p,q}=F^pA^{p+q}\cap d(F^{p-r+1}A^{p+q-1})$.
    <ol>
        <li>
            It's clear by definitions that every element of $E_r^{p,q}$ can be represented by some $z\in K_r^{p,q}$ just by definition. Given such a $z$, we have $dz\in K_r^{p+r,q-r+1}$ because $dz\in F^{p+r}A^{p+q+1}$ and $d^2z=0$. Hence, it remains to show that if $z\in I_r^{p,q}$, then $dz\in I_r^{p+r,q-r+1}$. Well, if $z\in I_r^{p,q}$, then $z=dw$ with $w\in F^{p-r+1}A^{p+q-1}$, so $dz=d^2w=0\in F^{p+r}A^{p+q+1}$. Hence, $dz\in I_r^{p+r,q-r+1}$ as desired. It's clear that $d_r^2=0$ since $d^2=0$.
        </li>
        <li>
            Note that $K_{r+1}^{p,q}\subset K_r^{p,q}$, so there's a natual induced injection $Z_{r+1}^{p,q}\into Z_r^{p,q}$. Composing this with the quotient map gives a map $\phi:Z_{r+1}^{p,q}\to E_r^{p,q}$. Now, for $z\in K_{r+1}^{p,q}$, we have $\phi([z])\in\ker d_r^{p,q}$ since $d_r(\phi([z]))=[dz]\in E_r^{p+r,q-r+1}$ and $dz\in F^{p+r+1}A^{p+q+1}=F^{(p+r)+1}A^{(p+r)+(q-r+1)}$. In fact, we have that $\phi$ surjects onto $\ker d_r^{p,q}$ because its image, by definition, contains every $z$ s.t. $dz\in F^{p+r+1}A^{p+q+1}$. Now, we claim that $\ker\phi=B_r^{p,q}$ which suffices to prove 2. It's clear that $I_{r+1}^{p,q}\subset I_r^{p,q}$, so $B_r^{p,q}\subset\ker\phi$. Conversely, suppose that $z\in\ker\phi\subset Z_{r+1}^{p,q}$. Well, $\phi(z)=[z]$, so this means that $z\in B_r^{p,q}$. Hence, $z\in B_r^{p,q}\cap Z_{r+1}^{p,q}$, so $z\in B_{r+1}^{p,q}$.
        </li>
        <li>
            It's clear from definitions that $Z_1^{p,q}=\ker\parens{G^pA^{p+q}\to G^pA^{p+q+1}}$ and that $B_1^{p,q}=\im\parens{G^pA^{p+q-1}\to G^pA^{p,q}}$. 3. follows.
        </li>
        <li>
            Suppose now that there exists $n,m\in\Z$ such that $F^nA^\bullet=A^\bullet$ and $F^mA^\bullet=0$ (so $m>n$). Fix any $p,q\in\Z$. Note that $d_r^{p,q}=0$ and $d_r^{p-r,q+r-1}=0$ whenever $r>\max\{m-p,p-n\}$.
        </li>
    </ol>
</div>

Before ending this section, I should maybe mention some standard terminology. The data summarized in the above theorem (i.e. objects $E_r^{p,q}$ with differentials of bidgree $(r,1-r)$ such that $E_{r+1}$ is the cohomology of $E_r$) is collectively known as a <b>(cohomological) spectral sequence</b>. For fixed $r$, the objects $E_r^{p,q}$ form the <b>$r$th page</b> (or <b>$E_r$-page</b>) of the sequence. In general, if $E_r^{p,q}$ only depends on $p,q$ for $r$ sufficiently large, then we denote this object by $E_\infty^{p,q}$. Hence, for the spectral sequence of a bounded filtered complex $A^\bullet$, we have $E_\infty^{p,q}=G^p\hom^{p+q}(A^\bullet)$. Spectral sequences are usually drawn as a 2d grid with $p$ increasing to the right, and $q$ increasing as you move vertically upwards.

# A Couple Neat Applications

### Cellular Cohomology is Singular Cohomology

### Kunneth Formula

# Serre Spectral Sequence

Let $F\to E\to B$ be a (Serre) fibration with $\pi_1B=0$ [^8].

<div class="exercise" name="Thom-Gysin sequence">
    Let $S^n\to E\to B$ be a fibration with $B$ simply connected. Construct a long exact sequence
    $$\cdots\too\hom^{p+n}(B;\Z)\too\hom^{p+n}(E;\Z)\too\hom^p(B;\Z)\too\hom^{p+n+1}(B;\Z)\too\hom^{p+n+1}(E;\Z)\too\cdots$$
    Use this sequence to show that if $S^n\to S^{n+k}\to S^k$ is a sphere fibration, then $n=k-1$.
</div>

# Sepctral Sequence of a Double Complex

[^1]: Replace "bird" with something less ill-defined if you want
[^2]: And because singular (co)homology is one of the few things I know I never want to bother developing on this blog (along with the basics of linear algebra, most of point-set topology, and maybe some other stuff)
[^3]: Just apply the universal property to $\alpha:=\mu\circ a=\mu\circ b$.
[^4]: For intuition, in $\mathrm{Ab}$, monomorphisms are injective maps, so this is saying every subgroup should be a kernel (i.e. all quotients exist). Similarly, epimorphisms are surjective maps, so the image of every map should be the domain modulo some subgroup (i.e. first isomorphism)
[^5]: If you're reading this post, you should already know what these are. I'm just defining them here because I want this first section to stand alone as an introduction to abelian categories regardless of the fact that it fits into the broader context of this whole post.
[^6]: I'll likely say chain when I mean to say cochain many times below
[^7]: From now on, I'll start being a little more sloppy with my $d$'s, not always explitily giving them their upper indexing.
[^8]: This condition can be weakened, but it makes things easier for me to assume it.
[^9]: There's some dubious reasoning here, but I'm only trying to build intuition so that's fine
[^10]: Don't read the proof of this; do it for yourself. The only reason I have it typed up here is that I've never worked through it on my own before this.