---
layout: post
title: "Surreal Numbers"
modified: 2017-01-05 13:03:00
categories: blog
excerpt:
tags: [math]
image: 
  feature: 
date: 2017-01-04 03:30:00
---

When people talk about "numbers", they usually mean real numbers or natural numbers. I like to think that when God talks about "numbers", he means surreal numbers. Surreal numbers are a beautiful class of numbers with a simple construction with the surprising property that they include "All numbers great and small". 

# Construction

> Definition<br>
A **surreal number form** is an ordered pair $$(L, R)$$ of two sets of surreal number forms: the left set $$L$$ and the right side $$R$$.

That's it. Maybe not all of it, but that's pretty much it. It doesn't look like much, and it may not be obvious that this is a valid definition, but it's almost all there is to it. Let's look at an example. To start with, there are no surreal number forms, the only possibility for $$L$$ and $$R$$ is the empty set. Hence, $$(\emptyset, \emptyset)$$ is our first surreal number form (Spoiler [^1]).

One thing to notice is that I am calling these things surreal number forms, and not just surreal numbers. There's a reason for this. Not every surreal number form is a surreal number.

> Definition<br>
Given two surreal number forms $$x=(X_L, X_R)$$ and $$y=(Y_L, Y_R)$$, we say that $$x\le y$$ if there is no $$y_R\in Y_R$$ s.t. $$y_R\le x$$ and there is no $$x_L\in X_L$$ s.t. $$y\le x_L$$. 

As we'll see with the next couple of definitions, the intuition behind a surreal number is that it's value lies between the values in its two sets. If $$x$$'s left set is $$\{0, 1\}$$ and its right set is $$\{2, 3\}$$, then whatever number $$x$$ is should be larger than $$0$$ and $$1$$, but smaller than $$2$$ and $$3$$. With that in mind, this definition says that $$x\le y$$ when $$x$$ is smaller than the things larger than $$y$$, and $$y$$ is larger than the things smaller than $$x$$.

Before moving on to the next definition, I want to fix some notation. Throughout this post, I will try to use lowercase variables $$(x, y, z, \dots)$$ for surreal number forms, and uppercase variables for sets of surreal number forms. The subscripts $$L$$ and $$R$$ will be used to differentiate left and right sets. The above definition gives examples of what I mean. Finally, instead of writing pairs completely explicitly (Ex. $$(\{0, 1\}, \{2, 3\})$$), I'll write them as $$\{L\mid R\}$$ where $$\mid$$ separates the two sets, and the only curly braces appear on the outside (Ex. $$\{0, 1\mid2, 3\}$$).

>Definition<br>
A surreal number form $$x=\{X_L|X_R\}$$ is **well-formed** if no member of $$X_R$$ is lequal to a member of $$X_L$$. Symbolically[^2], $$\forall x_L\in X_L\forall x_R\in X_R$$ $$ x_R\not\le x_L$$

Another quick aside. I'm likely going to be less formal later in this post than in the previous two definitions, so just remember that if you see something that looks like $$x_L$$, then its a member of some set $$X_L$$ that is the left set of some surreal number (form) $$x$$. I won't always make this explicit.

Now that we've defined well-formed, we can finally define surreal numbers. First, note that since we have a definition for lequality, we automatically get natural defintions for grequality, equality, strict less than [^3], and strict greater than as well. As an example $$x=y\iff x\le y\text{ and }y\le x$$.

>Definition<br>
The **surreal numbers** are the equivalence classes of the class[^4] of well-formed surreal number forms under the equivalence relation $$x\sim y\iff x\le y\text{ and }y\le x$$.

Now that we've finally gotten to this definition, I advise that you ignore it for the most part. It's really not necessary it have it in mind for working with surreal numbers; it just serves to make things mathematically precise and well-defined. One thing that happens with well-formed surreal number forms is that numbers have multiple representations (Ex. $$\{0,3,6\mid\}=\{2,6,1\mid\}$$), but these representations are different under the normal interpretation of equality (equality as pairs of sets). While we are working with pairs of sets, we're thinking of them as numbers and not as pairs, so we want to use a different type of equality and this is down by considering equivalence classes. This let's us have different representations for a value, but only one object (its equivalence class). This is like how $$\frac48$$ and $$\frac12$$ are formally different, but still equal and refer to the same value.

For thinking about surreal numbers, you really only need to keep in mind the original definition of a surreal number form, and the fact that surreal numbers are well-formed (i.e. that the left set is strictly "smaller" than the right set).

# Making Sense of This
If you feel like the definition of surreal numbers makes complete sense, then skip this or just read the summary at the end of it.

So, a surreal number is two sets of surreal numbers, a left set and a right set. Every member of its left set is less than every member of its right set. One surreal number is less than another one if its less than the second's right set and its left set is less than the second one. 

Honestly, it's not even obvious this makes sense. In the standard approach to constructing numbers, you have real numbers made from rational numbers, and ration numbers made from integers. Every type is constructed using previous types. Here, there is only one type, so isn't it circular? [^5]

The thing to keep in mind is that concepts surrounding surreal numbers are defined in terms of other surreal numbers, but they only in terms of simpler surreal numbers! As you "unfold" these definitions, you will eventually reach the simplest surreal number of all $$\{\mid\}$$, and at this point you are done. Since there is nothing left to unfold (and members of the empty set satisfy all properties[^6]), these definitions are perfectly fine. This actually has a nice side affect. If you want to prove a statement about the natural numbers, you can do so inductively. You show that it holds for 0, and that if it holds for some number $$k$$, then it also holds for $$k+1$$, and this shows that it's true for all natural numbers [^7]. Surreal numbers have their own form of induction. If you want to prove a statement holds for all surreal numbers, it's enough to show that if it holds for all members a number's left and right sets, then it holds for that number; you don't even need a base case! This is because the base case would be $$\{\mid\}$$ but everything holds for the empty set so its trivially satisfied.

To summarize, surreal number definitions make sense because everything is defined in terms of simpler numbers. A consequence of this is that statements can be proved inductively by showing that if a claim holds for all $$x_L$$ and all $$x_R$$, then it also holds for $$x$$. In my opinion, this second part is amazing. Surreal numbers contain far more values than the real numbers, but at the same time allow for induction that is arguable simpler than induction on natural numbers.

# Happy Birthday
Finally, all the set up is out of the way; we can start playing with these things. As I mentioned before, the first and simplest surreal number is $$\{\mid\}$$ which we'll call $$*$$ for now. From this, we can create 4 possible new forms

$$\begin{array}[c c]
 \{\{\mid\} && \{*\mid\} \\
\{\mid*\} && \{*\mid*\}
\end{array}$$

The top-left one is just $$0$$ again so nothing new. The bottom right one is not well-formed so that's not a surreal numbers. The other two however actually look like two new surreal numbers. We'll call them $$\{*\mid\}=\uparrow$$ and $$\{\mid*\}=\downarrow$$. Before moving on, let's verify that these actually are new numbers, and not just $$*$$ in disguise.

>Theorem<br>
$$\downarrow<*<\uparrow$$

We'll prove this in 4 separate parts [^8]

<div class="proof">
Part 1: \(\downarrow\le*\)<br>

We want to show that \(\{\mid*\}\le\{\mid\}\), so we need to show that \(\downarrow\) is less than everything in \(*\)'s right set and everything in \(\downarrow\)'s left set is less than \(*\). Both of the sets in equation (\(*_R\) and \(\downarrow_L\)) are empty, so both statements hold and we're done.
</div>
<hr style="height:0pt; visibility:hidden;">
<div class="proof">
Part 2: \(*\not\le\downarrow\)<br>

We want to show that \(\{\mid\}\not\le\{\mid*\}\). This is the case since \(*\le *\) and \(*\in\downarrow_R\) 
</div>
I won't bother doing the other two parts, but they work out as well and you can do them youself.$$\square$$

The above proof should seem misleading. Not because the theorem is false, but because I'm using things we haven't prooved yet. Namely, reflexivity and transitivity of $$\le$$. These properties hold for $$\le_{\mathbb R}$$, but we're working with a different concept of lequality here. To calm our worries, in the next section, we will show that transitivity and reflexivity hold here as well. We'll also recover some other familiar properties of "numbers", and rename the 3 numbers we've created thus far.

Before that though, let's introduce some useful terminology for talking about surreal numbers. From the three we've seen so far, it's clear how the rest of the numbers will be constructed. Each step along the way, the $$k$$ numbers already construct form $$4^k$$ [^9] candidate new surreal numbers, some (only few) of which will actually be new numbers. With this in mind, there's a kind of order to the numbers separate from lequality: some are made before others. To capture this notion, we define the following

>Definition
The ancestors of $$x$$ are all the numbers $$x_L$$ and all the numbers $$x_R$$

>Definition
We say $$\{\mid\}$$ was **born on day 0**. In general, $$x$$ was born 1 day after the oldest of its ancestors (members of either $$X_L$$ or $$X_R$$). We call the day a number $$x$$ was born its **birthday** or **birthday number**.

>Definition
We say $$x$$ is **simpler** than $$y$$ if $$x$$ was born before $$y$$

These definitions will give a nice way of identifying surreal numbers. In the next section, we will prove the following theorem

>The Simplicity Theorem<br>
Given any surreal number $$y=\{Y_L\mid Y_R\}$$, if $$x$$ is the simplest number such that $$Y_L<x<Y_R$$, then $$x=y$$.

The notation $$Y_L<x$$ means that $$\forall y_L$$ $$y_L < x$$. In generally, when a relation is applied to a set (of surreals), it is applied elementwise.

# Some Properties
The surreal numbers form what's called an [ordered Field](https://www.wikiwand.com/en/Ordered_field). This means four things. You can add them, you can multiply, you can order them, and all these things play nicely with each other and generally behave as you would expect. We won't show all of this here because it would be a lot and I don't want to, but we'll a thing or two about the ordering, define addition and multiplication, and then probably show some other stuff [^10] [^11].

>Theorem (Transitivity of $$\le$$)<br>
If $$x\le y$$ and $$y\le z$$, then $$x\le z$$ [^12]

<div class="proof">
As I suggested before, the standard way for proving things about surreal numbers is induction. With that said, assume the theorem holds for any triple (\(x', y', z')\) where \(x'\) is an ancestory of \(x\) and similarly for \(y'\) and \(z'\). Furthermore, assume \(x\le y\) and \(y\le z\). We need to show that \(x\) is lequal to every \(z_R\) and every \(x_L\) is lequal to \(z\). For the first condition, \(x\le y\) and \(y\le z_R\) (by assumption), and so \(x\le z_R\) by induction (since \(z_R\) is an ancestor of z). For the second condition, \(x_L\le y\le z\) by assumption and so \(x_L\le z\) (by induction). Hence, \(x\le z\) and we are done. \(\square\)
</div>

We had this messy recursive definition of $$\le$$, and we just showed it was transitive using induction pretty simply without even needing a base case. Take some time to convince yourself that the above proof is actually correct and not just cheating. I'll wait. Now that we have transitivity, the natural thing to prove next is reflexivity, and then we'll have shown that $$\le$$ is a partial order[^13]. Instead of doing that here, I'll leave that to you and prove something else.

>Theorem<br>
$$X_L<x<X_R$$. Possibly more clearly, $$\forall x_L\in X_L\forall x_R\in X_R$$ we have $$x_L<x<x_R$$

<div class="proof">
We start by showing that \(x>X_L\). Fix any \(x_L\), so we need to show that \(x>x_L\). This follows from the definition since \(x_L\le x_L\) (\(x>x_L\iff x\not\le x_L\) and lequality requires no \(x_L\) s.t. \(x_L\le x_L\)).<br>
We now show that \(x< X_R\). Fix any \(x_R\), so we need to show that \(x_R>x\) or equivalently that \(x_R\not\le x\). This once again follows from the definition since \(x_R\le x_R\). \(\square\)
</div>

The next theorem blew my mind the first time I saw it.

>The Simplicity Theorem (Again)<br>
Given any surreal number $$y=\{Y_L\mid Y_R\}$$, if $$x$$ is the simplest number such that $$Y_L<x<Y_R$$, then $$x=y$$.

<div class="proof">
Let \(y\) be any surreal number, and let \(x\) be the simplest number s.t. \(Y_L< x < Y_R\). We first show that \(x\le y\), which is the case iff \(x < Y_R\) and \(y > X_L\). The first inequality holds by assumption. For the second inequality, we use contradiction. Assume \(y\le x_L\) for some \(x_L\). Then, \(Y_L < y \le x_L < x < Y_R\) which contradicts our assumption on \(x\) being the simplest such number. Thus, \(y > X_L\) and so \(x\le y\). Similarly, it can be shown that \(y\le x\) and so \(x=y\). \(\square\)
</div>

This theorem (and the next one) is extremely useful for identifying surreal numbers. It can also be used to find an explicit formula for the number of surreals born on each day [^14].

>Theorem<br>
$$\{X_L\mid X_R\}=\{\max X_L\mid \min X_R\}$$ when the maximum and minimum both exist.

Proof left for reader.

Let's move on to some arthmetic. What might we mean by $$x+y$$? One important property of addition of real numbers (important enough for it to be required of all ordered fields) is that $$a\le b\iff a+c\le b+c$$. With this in mind, we would want the following to hold in the case of surreals: $$x+y_L\le x+y\le x+y_R$$. Motivated by this, we make the following definition

>Definition<br>
$$x+y=\{X_L+y,x+Y_L\mid X_R+y,x+Y_R\}$$

This satisfies $$x+y_L\le x+y\le x+y_R$$ by construction and also satisfies other properties of addition that you would expect. For brevity, we will only prove communitivity here because it has a short proof.

>Theorem<br>
$$x+y=y+x$$

<div class="proof">
Using induction
$$\begin{align*}
x+y=
\{X_L+y,x+Y_L\mid X_R+y,x+Y_R\}=
\{y+X_L,Y_L+x\mid y+X_R,Y_R+x\}=
y+x
\end{align*}$$ \(\square\)
</div>

Nice and simple. Another thing of note is the following

>Theorem<br>
$$x+\{\mid\}=x$$. That is, $$\{\mid\}$$ is the additive identity.

<div class="proof">
Note that \(x+\emptyset=\emptyset\) since there is nothing to add to \(x\). Assume the claim holds for all of \(x\)'s ancestors, and let \(*=\{\mid\}\). Then,
$$\begin{align*}
x+* &= \{X_L+*,x+\emptyset\mid X_R+*,x+\emptyset\} \\
&= \{X_L+*\mid X_R+*\} \\
&= \{X_L\mid X_R\} \\
&= x
\end{align*}$$ \(\square\)
</div>

Awesome. We just found an additive identity, and we use this as justification to name $$0=\{\mid\}$$. Seeing that we have a $$0$$, the next natural question is to ask whether there are additive inverses, and if so, how to find them.

>Definition<br>
$$-x=\{-X_R\mid-X_L\}$$

It is up to the reader to verify that this actually is the additive inverse of $$x$$. 

Next up is multiplication. Looking at field properties we might want satisfied, we see that $$0\le a,0\le b\implies0\le ab$$. It isn't immediately obvious how we might use this discover the correct definition of multiplication, but replacing the $$0$$'s with variables gets us there

$$\begin{align*}
a'\le a,b'\le b &\implies
0\le(a-a'),0\le(b-b') \implies
0\le(a-a')(b-b') \\&\implies
0\le ab - a'b - ba' + a'b' \implies
a'b + ba' - a'b'\le ab
\end{align*}$$

This (and similar considerations) motivates the next definition

>Definition<br>
$$xy=x*y=\\\{X_L*y+x*Y_L-X_L*Y_L,X_R*y+x*Y_R-X_R*Y_R\mid\\ X_L*y+x*Y_R-X_L*Y_R,X_R*y+x*Y_L-X_R*Y_L\}$$

Not gonna lie. This one is pretty ugly, and they only get uglier from here [^15]. On the bright side, they still behave nicely. For instance

>Theorem<br>
$$0x=0=x0$$ and $$x*\{0|\}=x=\{0|\}*x$$

<div class="proof">
Each sum involved in calculating \(0x\) or \(x0\) includes a term containing the left (or right) set of \(0\). This is the empty set, so when you multiply it by something, you still get the empty set. When that resulting empty set is added to other sets, you still have the empty set so both the left and right sets of \(0x\) or \(x0\) are empty and hence \(0x=0=x0\).<br>
The other half of the theorem is easily seen. \(\square\)
</div>

Now that we have an additive inverse as well, we call $$1=\{0\mid\}$$. Furthermore, we note that, by definition, $$-1=\{\mid-0\}=\{\mid0\}$$, and so we finally have approriate names for all 3 surreal numbers we have constructed.

# All Numbers Great and Small
We have $$0, 1$$, and $$-1$$, but what about the rest of the numbers. First, note that $$\{0\mid\}+\{0\mid\}=\{1\mid\}$$ and that in general, letting $$y=\{x\mid\}$$, $$y+1=\{x\mid\}+\{0\mid\}=\{x+1,y\mid\}$$ [^16]. If you start with $$y=0$$, and keep adding 1 in this way you find that the usual natural numbers are embedded in the surreal via $$n\mapsto\{n-1\mid\}$$. You get the rest of the integers by considering their negatives: $$-n\mapsto\{\mid-(n-1)\}$$.

What about the rationals? First note that, letting $$x=\{0\mid1\}$$, $$\{0\mid1\}+\{0\mid1\}=\{x\mid1+x\}=1$$ by the simplicity theorem, and so we say $$\{0\mid1\}=\frac12$$. Similarly, we define $$\{0\mid\frac12\}=\frac14$$ and $$\{\frac12\mid1\}=\frac34$$.

We can combine these two observations into the following theorem

>Theorem<br>
Let $$-x_m<\dots<-x_1<x_0=0=x_0<x_1<\dots<x_m$$ be all the numbers born on some (finite) day $$n$$ or earlier. Then, the numbers born on day $$n+1$$ are the following where $$0\le i\le m-1$$
$$\begin{matrix}
\{x_m\mid\hfill\} &=& x_m+1\\
\{x_i\mid\hfill x_{i+1}\} &=& \frac12(x_i+x_{i+1})\\
\{\mid\hfill-x_m\} &=& -(x_m+1)\\
\{-x_{i+1}\mid\hfill-x_i\} &=& -\frac12(x_i+x_{i+1})
\end{matrix}$$

The proof of this theorem is omitted. Hint for proving it yourself, use the simplicity theorem and use $$x=\frac12y\implies x+x=y$$.

The above theorem classifies all numbers born on finite days. One thing to notice is that the integers get special treatment, and the dyadic rationals [^17] get special treatment, but the reals and the rationals in general do not. In fact, on any finite day, the only numbers are integers and dyadic rationals. There's no $$\pi$$, no $$e$$, nothing. Things don't really get interesting until day $$\omega$$.

[$$\omega$$](https://www.wikiwand.com/en/Ordinal_number#/Transfinite_induction) can be thought of as the number after all the natural numbers. In the surreals, we actually define $$\omega=\{0,1,2,3,\dots\mid\}$$ and this is a completely legitimate surreal number; it behaves all the same rules as the other surreals and can. It is born on day $$\omega$$, but is not the only number born on day $$\omega$$. You also get, for example,

$$\begin{align*}
\frac13&=\left\{\frac14,\frac5{16},\frac{21}{64},\dots\mid\frac12,\frac38,\frac{11}{32},\dots\right\}\\
\varepsilon&=\left\{0\mid1,\frac12,\frac14,\frac18,\dots\right\}
\end{align*}$$

$$\varepsilon$$ is an interesting number. It is larger than $$0$$, but smaller than any positive dyadic rational (and by extension, any positive real number). For this reason, it is called an infinitesimal. 

Another interesting fact is that on day $$\omega$$, you get every real number. They can be constructed using a process similar to [Dedekind cuts](https://www.wikiwand.com/en/Dedekind_cut). This is nothing new, but what makes things interesting is that the fact that prior to day $$\omega$$ the only non-integers constructed are the dyadic rationals suggests a method of finding appropriate cuts for each real number. Consider any real number $$x$$ and write it out in binary [^18] (Ex. $$\pi=11.00100100001111110\dots_2$$). To form the members of $$X_L$$, take substrings of $$x$$'s binary expansion that end in 1. To form the members of $$X_R$$, take substrings of $$x$$'s binary expansion that end in 0, execpt replace the final 0 with a 1. Doing this for real number yields its equivalent surreal number and shows that all real numbers are born by the end of day $$\omega$$. Ex.

$$\begin{align*}
\pi=\left\{3,3\frac18,3\frac9{64},\dots\mid3\frac12,3\frac14,3\frac3{16},\dots\right\}
\end{align*}$$

So on day $$\omega$$ you have all the reals, an infinite number, and an infinitesimal. Of course, it doesn't stop there. On day $$\omega+1$$, you get numbers like

$$\begin{matrix}
\{0,1,2,3,\dots\mid\omega\} &=& \omega-1\\
\{0\mid\varepsilon\} &=& \frac\varepsilon2\\
\end{matrix}$$

By the time you reach day $$\omega$$, you start seeing things like

$$\begin{matrix}
\{\omega,\omega+1,\omega+2,\omega+3,\dots\mid\} &=& 2\omega\\
\{0,1,2,3,\dots\mid\omega,\omega-1,\omega-2,\omega-3,\dots\} &=& \frac\omega2\\
\varepsilon\omega &=& 1
\end{matrix}$$

From here, there is no limit. The surreals also contain strange numbers like

$$\begin{align*}
1 + \sqrt{4\pi+\omega} & &
\frac\varepsilon\omega & &
\frac{\omega-8}{7} & &
e^{\omega/3} & &
\log(\omega-(1+\varepsilon)^\omega) & &
\omega^{\omega^{\omega^{\omega^{\omega^{\omega^{\omega^{\omega^\omega}}}}}}}
\end{align*}$$

The amazing thing about this is not that these are actual constructible numbers, but they these are well-behaved numbers. Most notions of doing arithmetic with infinity that you come across either don't work very well or are very limited. Here, you have infinities and infinitesimals interacting just like any pair of numbers. Everything is legitimate and well-definied, and the whole thing forms an ordered field! You can pick any two of the numbers above, and one is larger than the other, and that order is well-behaved. It plays nice with multiplication and addition and many other operations. Not only that, but you can do more than just arithmetic with surreal numbers. In his book [On Numbers and Games](https://www.amazon.com/Numbers-Games-John-H-Conway/dp/1568811276), Conway takes the theory of surreals much farther than I touched on in this post. He studies [^19] analysis, algebra, and number theory of surreals.

# There's More
Unfortunately, this post got really long, really fast, and so I was not able to talk about everything I wanted to. In particular, I didn't even touch on what's maybe the most surprising property of surreal numbers: how they were discovered. [Conway](https://www.wikiwand.com/en/John_Horton_Conway) originally discovered surreal numbers while studying the board game [Go](https://www.wikiwand.com/en/Go_(game)). He found a way to represent Go positions as sums of smaller games, and evenetually realized that the games he was studying behaved like numbers. What I called a surreal number form in the beginning is more appropriately dubbed a Game. Games in general share many of the properties of surreal numbers (which are just a subclass of games), and there are many interesting games that are not well-formed. This post is too long as is to go into the details, but if you want learn more about the connection between surreal numbers and games, I recommend [Winning Ways for Your Mathematical Plays](https://www.amazon.com/Winning-Ways-Your-Mathematical-Plays/dp/1568811306).

In you just want more practise with surreals, Knuth has a [nice book](https://www.amazon.com/Surreal-Numbers-Donald-Knuth/dp/0201038129) about them, told from the perspective of two people stranded on an island who find a rock with a couple definitions, and find they have way too much free time.

[^1]: We'll see later in this post that this number is 0. Technically, we can call this whatever we want. We'll see that we want to call it 0
[^2]: The upside-down A means "for all". There's also a backwards E that means "there exists"
[^3]: I'm tempted to call this strict lequality, but the name sounds misleading. In case it's not clear, I'm referring to < here
[^4]: not set
[^5]: Spoiler: no
[^6]: That is, any statement of the form "for all x in A, blah" is true when A is empty
[^7]: Truth for 0 implies truth for 1, truth for 1 implies truth for 2, etc. It's like how if you line up a bunch of dominoes and knock over the first one, you know they'll all fall because the first one falls and every one that falls knocks over the next one
[^8]: I'm not sure how I feel about making the areas where the proof is stand out.
[^9]: Try to see why (Hint: This upper bound is much larger than the true number, and much larger than other upper bounds you could come up with)
[^10]: I will most likely end up using x_L to refer to different things at different times in the same proof (either as a specific member of X_L or any general member of X_L). Try to keep up.
[^11]: Throughout this whole post, I'm talking about things in the order in which they pop into my head, so theorems and definitions do not necessarily appear in the most logical order. Keep that in mind.
[^12]: If it's not clear from reading the follow proof, I was not entirely sure how to formulate in the induction in a way that didn't feel hand-wavy. What you see below is the result of me going back and forth between different formulations and between whether or not I should just ignore the specifics and hope no one notices. Honestly, no one reads this blog so I could have done that.
[^13]: Also show that if x is not lequal to y, then y is lequal to x to show that it is in fact a total order
[^14]: Hint: It's much less than the 4^k upper bound
[^15]: Seriously, look up the definitions for 1/x and sqrt(x).
[^16]: When y is an integer, x+1 >= y. For what other cases does this inequality hold?
[^17]: rationals with denominator a power of 2
[^18]: we use binary because writing a number in binary is equivalent to writing it as a sum of numbers of the form 1/2^n and so we are only using already constructed numbers
[^19]: does? performs? What's a good verb here?