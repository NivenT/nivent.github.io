---
layout: post
title: "When do you understand mathematics?"
modified: 
categories: blog
excerpt:
tags: [math, maybe some other stuff]
image: 
  feature: 
date: 2017-03-25 22:05:00
---

# Calculating isn't enough

I remember one day in middle school when I was complaining about my math homework [^1]. Fed up with my complaints, and wanting to put me in my place, my sister decided to show me her homwork. It made no sense. It was asking strange questions about even stranger concepts.

> Question<br>
What's the derivative of $$\hspace{2pt}3x^4-7x^2+x-8$$?

My sister quickly explained to me that to take one of these derivatives, you multiply the number in front by the exponent, then subtract one from it. Simple enough. I now knew about derivatives and how to compute them, except I didn't. For years, all a derivaitve was to me was a process of transforming polynomials. It had no connection to slopes, areas, linear transformations, etc.;[^2] it was just symbolic manipulation. I saw examples where people were asked to take the derivative of strange things like $$\sin(x)$$, but although I knew of $$\sin$$, I had no idea what mysterious black magic was required to differentiate something like it.

# Locality isn't enough

Fast forward a number of years, and I am a junior in high school. I am no longer that ignorant middle schooler; my mathematical knowledge is leaps and bounds ahead of what it was before. At this time I was taking an "Advance Logic" course at a local university, and I was loving it. A more descriptive title for the course would have been Metalogic. In it, we considered a few different logic systems, and proved soundness and completeness of them. We did other stuff, but that was the big idea.

>Aside[^3]<br>
When studying something reasoning system, you can study it in terms of semantics or syntax. Semantics is about assigning meaning to the system. You define models for it which can be thought of as examples of things that follow its rules. Syntax is all about manipulating symbols. You say your system has some ground truths (axioms) and deduction rules for getting new truths, and then see what true things result from this (this is how you might want a computer to view your system). A system is sound if syntactic manipulation always results in semantically true conclusions. A system is complete if every true statement can be proven syntactically.

We started with propositional logic, moved onto modal logic, and then did a little excursion into three-valued logics. The whole journey was amazing, made sense, and really gave me a newfound appreciation and interest for and in logic. Then, in the last part of the class, we moved on to first order logic. I had been looking forward to this all semester.

First order logic was a different beast altogether. Everything before made sense; it had clicked; FOL did not. The further along we went, the less I understood. Don't get me wrong. I followed what was going on. Every single step made sense and was internally verified, but I could not grasp the big picture. In the words of the topologist inside of me, I had local understanding, but still lacked understanding. I could see what was going on in class, and I could reproduce and modify proofs for homework and tests, but almost nothing that happened[^4] felt like it made sense.  

# Passing isn't enough
This brings us to now. I just finished up a quarter at school, and among the classes in my schedule was one called Algebraic Topology. In this class, something happened that I had convinced myself would never happen [^5]. I failed - I failed a math class. I didn't fail in the obvious interpretation of that word; my grade in the class is fine [^6]. I failed in a more personal sense. Like derivatives and FOL metatheory before it, I do not understand algebraic topology, but this case is worse than those.

When I did not understand derivatives, I had no reason to. My only formative experience with them was a quick demonstration of how they're calculated on a specific type of function. I had no need or incentive to know them any better at the time. When I did not understand FOL, it was only one part of a much larger course. Everything else felt more intuitive, and even FOL itself locally made sense. When it comes to algebraic topology, I just don't feel like I understand it. There were moments of me appreciating things[^7], but I'd be hard pressed to say there was even local understanding of the material.

I still did well on the problem sets. I would work together with a friend, and every week we managed to push out 10 (mostly) correct proofs. What little reasoning power I had that was trying to approach understanding was cultivated in these sessions, but there was no shift. Often[^8] when taking a math class, the first couple of problem sets are the most difficult. In the beginning, you only have your default mathematical prowess available to you to use. You have yet to build up a feeling for the field; you do not yet know how to approach a proof. Somewhere during the course, however, there is a shift. You start thinking like a topologist, geometer, algebraist or whatever; when seeing a proposed claim, you also see techniques to prove it or at the very least, you see an idea of its placement in your internal map of the field. You see other results its related to, other theorems it could have similar proofs to, ideas it depends on, etc. 

This was a change I had become accustomed to. When I took a Graph Theory class, every problem seemed novel and individual for the first half of the class. It felt like I had to reinvent the wheel everytime I had to prove some claim, and it was not easy. By the second half of the class, though, I had begun thinking like a graph theorist. I had a more standard set of tricks I could employ, I had better examples to refer to, and I felt like I was working on a theory and not a collection of claims. The same thing was true on a smaller scale in my math class my first quarter here, which was a sort of linear algebra for combinatorics course. There were two techniques we learned in the class that had become my gotos by the end, but were very mystical for quite some time: dimension arguments and the related polynomial method[^9]. Again, in Game Theory I had an extremely hard time doing the first problem set, but when I finished the course, I returned to it, and everything seemed so obvious and simple. The arguments were nothing special, and applying them was mentally quick. In all these cases, I had built up an intution and appreciation for the subject.

I cannot say the same for algebraic topology. This really hit me when, the day before the final, a friend asked me what class I was studying for, and I drew a blank on trying to explain the course to him; I not only drew a blank in how to verbally descibe the class, but I also drew an internal blank in my own understanding of the course. It is normal for me to not know how to tell someone about math[^10], but I at least always have some idea of what the math is to me. Here, there was nothing. I had no internalized overarching picture of algebraic topology, and this was a first.

My suspisions were confirmed when I took the final. It was brutal; I am legitimately scared to see my grade on it because (almost) nothing I did felt convincing. The whole class seems to have similarly struggled with the final, so there is an argument to be made that it was just a particularly hard test, but I don't think that's the case. The test was not trying to trick you. Every question felt unfair while I was taking it, but in hindsight, they were questions that I believe you could have answered if you understood the material. To someone who really absorbed and built up a good intuition for the material, the test would have been appropriate. Sadly, that was not me.

# Final Thoughts
> Question<br>
What is enough?

That's the million dollar question, and one I do not have the answer to, except to say you may never know. I thought I understood derivatives, until some weeks ago I learned that a derivative is not just a number. It's a linear transformation; specifically, it is the linear transformation that best locally approximates the function [^11]. I am now in a position similar to my first derivative experience. I know enough to say that, but I have not looked into things enough to understand what derivatives really are. After my logic course, I thought I understood my logic was about, then I learned that there were way more logics out there than the few we studied, that logic had interplays with some surprisign fields [^12], and that this stuff gets really deep. In the end, I'm not sure there's anything I do understand.

When I first decided to write a post talking about my experiences in AT, I wanted to do so in the context of revisitng mathematics in order to learn it. That clearly didn't happen, but in order to shine some light in the no so hopeful picture of understanding mathematics that I painted, I will say that there is benefit to serious revisiting of mathematics. I have learned linear algebra in 3 different settings now [^13], and each time I revealed something I had previously missed. Not necessarily some piece of knowledge I did not have before, but some insight I had yet to see. With that in mind, understanding math just takes time, and I might try to revisit AT at some point...[^14]

[^1]: It was either too hard or too easy. I can't remember which.
[^2]: What's the proper grammatical syntax for this
[^3]: warning, the following is simplified and so erroneous
[^4]: whether I did it or the professor did it, whether it was correct or not
[^5]: specifically, would never happen to me
[^6]: technically to soon to say this because I don't have my grade yet, but with high probability, it's fine
[^7]: a good proof, a nice example, the one time it felt like communtative diagrams actually had some use
[^8]: for me at least
[^9]: to this day whenever I see a bound, my first instinct is to form polynomials
[^10]: describing math in an understandable, engaging, nonsuperficial way is no easy task
[^11]: That is, the derivative operator does not take in a function and a point, and spit out a number (or vector). It takes a function and a point, and spits out a function. If you want to learn more about this, look into differential geometry. That's what I was looking at when I first came accross it.
[^12]: e.g. Game Theory, Measure Theory, Graph Theory, etc.
[^13]: never feeling like my understanding was lacking after any of them
[^14]: Alternate titles for this post that I considered include "Learning math", "(Failing at) Learning math", and "Math is Hard"