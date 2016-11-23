---
layout: post
title: "Goldilocks and the Three Bears"
modified: 
categories: blog
excerpt:
tags: [math, linear algebra, combinatorics]
image: 
  feature: 
date: 2016-11-22 09:50:00
---

Three mathematicians -- Alice, Bob, and Charlie -- found themselves helping a mayor run her town. The mayor had a problem with the residents forming too many clubs. According to town law, each club was given some amount of money by the town to help facilitate their club stuff. Taking advantage of this, the $$n$$ residents of the town had requested to form all $$2^n$$ possible clubs[^1], but the mayor knew the town didn't have an exponential amount of money to be giving away. Thus, she hired a few mathematicians to come up with rules for which clubs were allowed. The mathematicians could choose any rules they liked as long as they satisfied the following

* The rules were simple enough for any person to tell when a new club was allowed or disallowed.
* The rules limited the possible number of clubs to something more reasonable than $$2^n$$
* The rules did not limit the clubs to a number so small that the residents would quickly run out of space avaiable for legitmate clubs[^2] and would complain.
* It shouldn't be obvious that the rules are just there to limit the number of clubs. Ex. The rule can't be only 100 clubs allowed.

# Eventown
After a bit of contemplation by the mathematicians, Alice went first, proposing what she called "Eventown". There were two simple rules

* Each club must have an even number of members
* Any two clubs must have an even number of members in common

"They couldn't possible come up with many ways to have even intersections!" Alice exclaimed, triumphantly. The mayor wasn't quite convinced, and began trying to come up with counterexamples to Alice's claim. Unfortunately, keeping track of so many clubs in your head is not an easy task, and so she failed to see any way these rules could go wrong. Then, Bob said, "What if they pair off?" It donned on everyone that the residents could simply form pairs and each club would be made by grouping pairs together. They would make $$n/2$$ pairs, and so you would get $$2^{\frac n2}$$ clubs doing this, which is still way too many.

# Oddtown
Having shot down Alice's idea, Bob proposed a slight revision he called "Oddtown". His rules were almost the same as Alice's

* Each club must have an odd number of members
* Any two clubs must have an even number of members in common

Unimpressed, the mayor asked "That's basically the same as before. How will it be much better?" Bob assured him that this set of rules would restrict the number of clubs further than Alice's had, although he admitted he didn't know how much they would be restricted by. Everyone gave it some thought, and after a while of failing to find counterexamples, the mathematicians went to work proving an upper bound for the number of clubs[^3].

"We only care about parity here, so we should be doing arithmetic$$\pmod 2$$"

"Good point, but before that, how do we represent the clubs?"

"As sets obviously; that's what they are. We number the residents $$1,2,3,\dots,n$$ and then each club is just a subset of $$[n]=\{1,2,3,\dots,n\}$$"

"That doesn't really give us much to work with though. Sets are too general, too unstructured. Instead of working with sets, we could work with vectors. Each club is an $$n$$-dimensional vector, 1 dimension for each resident. The $$i^\text{th}$$ coordinate of a club is 1 if that resident is in the club and 0 otherwise."

"If we're thinking of the clubs as vectors, then we need a vector space to work in. We're doing everying $$\pmod 2$$, so the natural choice is $$\mathbb F_2^n$$[^4]."

"Right. Now we just need a way of saying our rules in the language of vectors$$\dots$$We can use dot products! Say we have $$m$$ clubs $$v_1,v_2,\dots,v_m\in\mathbb F_2^n$$. The dot product of two club vectors tells us the parity of the number of members they have in common, so the rules say $$v_i\cdot v_i=1$$ and $$v_i\cdot v_j=0$$ for any $$i\neq j$$!"

"Wait a second; hold up. Can we use dot products? We're working over $$\mathbb F_2$$ and not $$\mathbb R$$, so we're not in an inner product space."

"That's true, but that doesn't stop us from defining a dot product, even if it's technically not an inner product, so we are still good."

"We're better than good; we have the answer. Those rules look a lot like they're saying the club vectors form an orthogonal set, and so they must be linearly independent. Thus, there are at most $$n$$ clubs since we are in $$n$$-dimensional space."

"That's true, but just to be safe, let's run through the proof. Pick $$c_1,c_2,\dots,c_m\in\mathbb F_2$$ such that $$c_1v_1+c_2v_2+\dots +c_mv_m=0$$. Then, for any $$i$$, we can take the dot product of $$v_i$$ with both sides of the equation to get $$c_1(v_1\cdot v_i)+\dots+c_m(v_m\cdot v_i)=0\cdot v_i\implies c_i(v_i\cdot v_i)=0\implies c_i=0.$$"

"Since this works for all $$i$$, all of the coefficients must be 0, and so the club vectors are indeed linearly independent. Like you said, this means we have at most $$n$$ clubs."

Finally, the mayor chimed in, "$$n$$ clubs for $$n$$ residents? That's kinda like a club per person. Seems kind of small doesn't it?" Bob's rules had indeed restricted the number of clubs drastically, but unfortunately it resulted in a number that was too small.

# Town
The mathematicians were feeling disheartened. Alice's idea had been quickly defeated; Bob's idea was fun to work out, but it worked too well; and there didn't seem to be a nice, obvious way to tweak things to have them come out more nicely. 10 minuites of silence passed before Charlie, the most creative of the bunch, proposed what he called "Town". Town only had 1 rule.

* The size of the symmetric difference between any two clubs must be one of two numbers. These two numbers can be whatever the residents want, and we'll call them $$a$$ and $$b$$.

"Symmetric difference? What's that?" asked the mayor. "It's the residents in one club, but not the other. Like the opposite of their common residents," explained Alice. Everyone was skeptical about Charlie's confidence in this rule, but he assured them that this would lead to a good upper bound.

"Shall we begin exploring this rule?" Charlie finally asked

"Guess so. Vectors worked well last time, so let's use them again. Like before, we'll represent each club by a club vector of 1's and 0's."

"We care about more than just parity, so we'll work in $$\mathbb R^n$$ this time. Let's let $$v_1,v_2,\dots,v_m\in\mathbb R^n$$ be our club vectors."

"We still need to translate our rule into linear algebra. How do we calculate the size of the symmetric difference using vectors?"

"It's the number of residents in one club, but not the other, right? So it's the number of positions where one club vector has a 1, and the other has a 0. Sounds a lot like distance to me."

"True, but you have to be careful. Distance has that pesky square root at the end, so we really need squared distance. Then, the rule is that for any $$i\neq j$$, the squared distance between $$v_i$$ and $$v_j$$, $$\|v_i-v_j\|^2$$, is either $$a$$ or $$b$$."

"Nice, but that effectively gives us 2 conditions for each pair of vectors. It would nice if we had a way to combine them into one."

"That's simple; just use multiplication. We combine our two conditions into one that says $$(\|v_i-v_j\|^2-a)(\|v_i-v_j\|^2-b)=0$$."

"Now we're getting somewhere. Wait, or are we? Honestly, I'm not seeing how any of this is helping us get an upper bound."

"It helps because we just have to... Actually, I'm not sure where to go from here either. Last time we got an upper bound by showing the club vectors were linearly independent. This condition doesn't look like it says much about the linear dependence of the vectors."

"Maybe we are focusing on the wrong vectors. When you think about it, this equation is a polynomial in the coordinates of $$v_i$$ and $$v_j$$, and polynomials are vectors too."

"But $$v_i$$ and $$v_j$$ are constant, so it's not much of a polynomial; it's a constant polynomial. In fact, it's just the zero polynomial."

"What if he replace one of them? Yeah, I think that'll work. For each $$j$$, we define the function $$f_j(x)=(\|x-v_j\|^2-a)(\|x-v_j\|^2-b)$$. Now, for each $$v_j$$, we have a corresponding polynomial."

"We have more than that! $$f_j(v_i)=0$$ when $$j\neq i$$ and $$f_j(v_j)=ab\neq0$$, so we once again have something similar to an orthogonal set. We can show they're independent using the same argument as before, but instead of taking the dot product of both sides with $$v_j$$, we'll apply both sides to $$v_j$$ in order to see that all coefficients must be 0."

"So the $$f_j$$'s are linearly independent, and so there must be at most $$n$$ of them! This bound is no better than before."

"Slow down. Last time, the bound was $$n$$ because the vectors lived in $$n$$-dimensional space. We need to know the dimension of the space the $$f_j$$'s live in. They are all polynomials, but the space of polynomials is infinite dimensional, not a very helpful bound."

"We can do better. Think about it, taking the squared distance is a quadratic thing, and so multiplying two of them gives you something quartic. The $$f_j$$'s live in the space of polynomials with total degree at most 4 and $$n$$ variables, one for each coordinate of $$x$$."

"Right. We can form a basis for that space by taking all the monomials[^5] in $$n$$ variables with total degree at most $$4$$. We're counting monomials that look like $$x_1^{a_1}x_2^{a_2}\dots x_n^{a_n}$$ where $$a_1+a_2+\dots +a_n\le4$$ and each $$a_i$$ is at least 0."

"This is classic stars and bars. We only need to calculate the number of ways to choose $$a_1,a_2,\dots, a_n$$. To do that, we can introduce a slack variable $$a$$ so that $$a_1+a_2+\dots +a_n+a=4$$ and count the number of choices of $$a_1,\dots, a_n, a$$. Each such choice can be visualized using 4 stars and $$n$$ bars. The $$n$$ bars separate the 4 stars into $$n+1$$ groups, and the number of stars in each group corresponds to the value of some $$a_i$$ (or the value of the slack variable $$a$$). Thus, we have $$4+n$$ symbols, and need to pick out $$4$$ of them to be stars, so the number of such arrangements is $$\binom{n+4}4$$, which must also be the dimension of the space."

"That was a lot, but I think I follow. So, there are at most $$\binom{n+4}4$$ of the $$f_j$$'s, and thus at most that many clubs can be formed."

"Yes, but there's a better upper bound. Think about it. We haven't even used the fact that each club vector only contains 1's and 0's. We've been think about the $$f_j$$'s as functions from $$\mathbb R^n$$ to $$\mathbb R$$ this whole time, but we can easily restrict them to be functions from $$\{0,1\}^n$$ to $$\mathbb R$$."

"Good catch. If we do that, then our polynomials aren't degree at most 4. Well, they are, but we can say something more. They are multilinear. $$0^k=0$$ and $$1^k=1$$ for all $$k$$, so every exponent becomes 1. All variables in each factor are by themselves, so when we multiply them, there are at most 2 variables together in one term, so the total degree is at most 2. Thus, we only need to consider multilinear polynomials of degree at most 2 to get a basis for the space the $$f_j$$'s live in."

"Right. In general, there are $$\binom nd$$ multilinear polynomials of degree exactly $$d$$ in $$n$$ variables, since you just choose $$d$$ variables to form one. Thus, our space has a basis of size $$\binom n0+\binom n1+\binom n2=1+\frac{n(n+1)}2$$, and this is an upper bound for the number of clubs that can be formed."

With this, the mathematicians were satisfied. The mayor remarked that such a bound was just right, as it let the residents form roughly $$n^2$$ clubs, which would be plenty, but not insanely many. Right when the mayor was about the bring the meeting to a close, a thought crossed her mind. "When you guys were figuring this out, you originally thought the upper bound was $$\binom{n+4}4$$, but then you reduced that to $$\binom n0+\binom n1+\binom n2$$. How do you know there's not an even better upper bound that is only linear in $$n$$?" The mathematicians pondered this for a second before Alice stepped forward. "Like with my set of rules, the answer lies in pairs. There could be a club for each pair of residents, and 1 club that was completely empty. This gives $$\binom n0+\binom n2$$ clubs satisfying the rule, which means the maximum number of clubs must grow quadratically with the number of residents." The mayor thought this over, and was convinced that indeed, the mathematicians had given her a worthwhile rule.

[^1]: A club is a subset of residents. If two clubs have exactly the same members, they are the same club.
[^2]: Ones made not just for the free money.
[^3]: It's unimportant who said which part. If you want, imagine Alice spoke first, then Bob, then Charlie, then Alice again, and so on.
[^4]: F_2 is the finite field with 2 elements. F_2={0,1} where 0+0=0, 0+1=1, 1+1=0 and 0\*0=0, 0\*1=0, 1\*1=1. Essentially even numbers are 0 and odd numbers are 1. Addition and Multiplication tell you the result of adding/multiplying even/odd numbers. F_2^n is the space of vectors with n elements from F_2.
[^5]: up to constant factor