---
layout: post
title: "Writing a Library"
modified: 
categories: blog
excerpt:
tags: [Rust, REnforce, CS]
image: 
  feature: 
date: 2016-11-19 02:30:00
---

When I began coding, I focussed mainly on games. I programmed tic-tac-toe, snake[^1], a side scrolling ASCII game I called jumper[^2], a couple mario clones, a maze solving game, and a few others[^3]. Somewhere along the way, I started losing interests in games, and gaining interests elsewhere; the types of programs I made changed. I wrote programs to do a little exploring of some mathy things, and tried to do some AI-y things as well. However, despite this, one thing stayed the same: I only wrote applications. But everything changed, when [the fire nation attacked](https://github.com/NivenT/REnforce)[^4].

# A Little Background
Less than two months ago, I started working on REnforce, a reinforcement learning[^5] library written in [Rust](https://rust-lang.org). Over the summer, I had gotten interested in reinforcement learning, read bits and pieces of a [book](http://www.springer.com/us/book/9783642276446) about it, and done a little messing around with [OpenAI's](https://openai.com/blog/) [gym](https://gym.openai.com/). This project was motivated by my desire to give myself an excuse to learn more about RL, and my desire to have a way to test my understanding. Also, as far as I could tell, There aren't a lot of RL libraries out there, so there was always the chance people would notice this one, and I could have a lot of people contributing to or using it[^6].

# The Library
Like I said, REnforce is a RL library. My original goal was to have a library such that anyone could design their own environment, and then use my library to pick from a host standard, ready-implemented RL algorithms to train their agent on. Other goals included allowing customizability/modularity for people who wanted a lot of control over the fine details, being fast enough that people would actually be willing to use it in projects (no matter how small), and of course, having a simple, powerful, consistent, understandable API.

When I first thought of writing a library, I planned to write it in C++. C++ is my oldest language, it's one of my favorites, it had been a while since I wrote a lot of C++, and I had recently decided to make an effort to improve my C++ coding abilities: start making use of modern features, write more safe and idiomatic code, gain an actual understanding of C++'s move semantics[^7], etc. After further thought, I decided to use Rust instead for one main reason: [Traits](https://doc.rust-lang.org/book/traits.html).

Traits in Rust are amazing. They are like abstract base classes or Java interfaces, but way better. Once defined, they can be implemented on any type and they allow for some nice generic programming. When I say nice, I mean that you can have restrictions on what types some genertic code ues (you require that it implements some traits), but since the compile does type inferencing, the user of the code does not necessarily need to know about all these restrictions. This fit well into my goal of having both a simple, and modular API. Under the hood, the different types I define are generic over multiple parameters, but when creating and using them, the user does not have to specify any of these parameters, the compile figures it out for her. This allows me to write code like this that has multiple generic types, each required to implement some trait(s).

~~~ rust
impl<N: Num, S: Space, A: FiniteSpace, Q, T> ParameterizedFunc<N> for EGreedyQAgent<S, A, Q, T>
	where 	T: Chooser<A::Element>,
		Q: QFunction<S, A> + ParameterizedFunc<N> {
		// blah
}
~~~

The above is generic over 5 types; it requires that N implements the train Num[^8], S implements Space[^9], A implements FiniteSpace[^10], T implements Chooser[^11], Q implements QFunction and ParameterizedFunc[^12]. This looks pretty ugly. However, when making use of this, the compiler figures out what type each of these is, and makes sure the types implement everything they need to for us, so we end up writing

~~~ rust
let mut agent = EGreedyQAgent::new(q_func, action_space, 0.2, Uniform);
let mut trainer = CrossEntropy::default().eval_period(TimePeriod::TIMESTEPS(5));

trainer.train(&mut agent, &mut env);
~~~

which hides the fact that there is something ugly behind the scenes[^13]. One thing you may notice in first code example is the strange `A::Element` syntax. Traits in rust allow you to specify what are called associated types. Basically, you define a trait (like `Space`) and say that this trait has some companion type (like `Element`), and you can even put restrictions on the companion type. This restrictions can be found in the trait itself, or in subsequent uses of the trait.

~~~ rust
pub trait Space {
	type Element : Debug + PartialEq + Clone;
	// blah
}

impl<T, S: Space, A: FiniteSpace, M: Model<S, A>> OnlineTrainer<S, A, T> for DynaQ<S, A, M>
	where T: QFunction<S, A> + Agent<S, A>,
		  S::Element: Hash + Eq,
		  A::Element: Hash + Eq {
	// blah
}
~~~

In order to be a `Space`, your `Element` must be clonable, debugable, and must be have a sense of equality between members. In order to use the Dyna-Q algorithm, your space's elements must also be hashable. Again, a lot of restrictions are put in place inside the library in order to make sure the different algorithms and concepts are properly used, but the user of the library can be completely unaware of all of this as long as she doesn't try to do something not allowed. This is the beauty of Traits.

# The Name
The name REnforce[^14] was originally conceived as a homage to Rust's trait system. The 'Enforce' part was due to type restrictions being enforced by the library through its heavy use of traits. The 'R' was just there because for some inexplicible reason[^15] I often feel the need to begin my projects written in rust with an 'R' to signify that they are written in Rust. A moments reflection caused me to realize that 'REnforce' could be pronounced 'reinforce', which seemed appropriate given the nature of the library, and so the name stuck. I really like how the 'H' in [HLearn](https://github.com/mikeizbicki/HLearn) stands for 3 different things having to do with the library, and briefly entertained the idea of thinking up something similar for REnforce[^16] and putting it in the readme, but decided that having some words about it in a blog post would be plenty. 

# Kinda What This Post Was Supposed to be About
Writing a library has been an interesting experience[^17]. I don't know if I have done a good job at it so far, since REnfoce has no users[^18], but I definitely feel like I am getting better at it. One of the hardest parts has been testing the code. A library could potentially be put through many different use cases, and I imagine people want a library that works in every case, or at least just the ones they plan on using it for. When developing applications, testing code is easy, because you just run it and see what happens. Working on this library, I haven't found good, obvious tests for the code I write. Originally, for each new RL algorithm I implemented, I would write a short example making use of the algorithm to see if it could sucessfully train an agent in some environment. This is better than nothing, but it doesn't do much to make sure the algorithm is aptly named[^19] and it is hard/annoying to come up with a different example for each algorithm. Recently, I started testing every algo on the same simple environment, which alleviates the second problem, but possible worsens the first as simple environments are easier to learn. However, the examples seem to work for the most part, and I have been getting a nice sense of accomplishment everytime I run an example and the agent has actually learned, so this approach isn't all bad.

One thing that makes me nervous is that I am no expert in RL or library writing for that matter. While writing this, I am having to make a lot of  decisions about implementations and type restrictions. I am not always confident that my choices accurately reflect the requirements of an algorithm, or the best approach to do what I want. When writing applications, if I have this doubt, it's less nerve racking since the application is mainly meant to only be used by me. Working on a library, it feels more like everything I do has to be as close to perfect as possible. This concern has only been growing, as I have been trying to put it on hold while I add more features to the library in the hopes of getting it to the point where it feels like more than just a toy project, and could actually be used for something non-trivial. 

Another issue I have noticed is that I am not sure what a simple, clean, nice, powerful, customizable, understandle, constructive, modern API looks like. The only way I have of getting an idea of how developing with this library feels like[^20] to someone else is by writing examples, but this hasn't stopped me from wondering if things or too verbose, or if I've achieved a decent level of simplicity. I found several types, I would try to implement something, commit my changes, and then need to go back and tweak/add things after trying to use my latest addition in an example. Whenever I notice that I've missed things like this, I can't help but wonder if there is other stuff I missed that I just didn't notice. I think the lesson here is that the best way to know how good of job you are doing at designing an API is for it to be tested.

Overall, the expierence has been a good one. I mainly talked about the less fun points here, but it has been nice writing this code, and especially getting more familiar with Rust's trait system. Hopefully, I continue to work on this for a while, and it grows into something bigger than I think it will.

[^1]: Like 4 times. It was always interesting seeing the different ways I implemented it as I learned more about coding. I have lost most of my implementations, but I still have the most recent one, from when I was a sophomore in high school, a simpler time.
[^2]: You were a square that was constantly moving to the right. You had to press space to jump in order to avoid obstacles and collect powerups that would change your speed, give you extra lives, etc. I had so much fun making it because it was my first "original" game. I'm sad I no longer have the source code for it.
[^3]: Not in that order. Very much not in that order.
[^4]: One of my favorite shows when I was younger. Good times.
[^5]: Not entirely important what this is, but the basic idea is you have your program interact with some environment, and you tell it how good it is doing without telling it what to do. It then uses the rewards/punishments you give it to figure out what to do. Think 5 year old learning not a touch a hot stove (environment) by touching one (interacting) and seeing that it hurts (punishment).
[^6]: So far, so good. I estimate I have about 0 users, and 0 non-me contributors.
[^7]: I still have no idea when I need to use `std::move()` and when the compiler figures things out, or how many &'s I need to use for the different constructors and assignment operators I implement myself. 
[^8]: N must be a type of number. It is the type returned by the function represented by EGreedyQAgent
[^9]: S must be a mathematical space (like the plane) where the agent's obervations are drawn from
[^10]: A must be a space like S, but must also be finite.
[^11]: T is a function that randomly selects an element from a list
[^12]: Q is a parameterized, Q function
[^13]: The last line is the one that invokes the previous code snippet. CrossEntropy only trains agents that are also parameterized functions, and so the call to train forces the compile to make sure everything is as it should be.
[^14]: Pronounced R-enforce, reinforce, or REN-force
[^15]: Honestly not sure why I started doing it, but I think some other people do it too 
[^16]: The R is for Rust, the R is for Reinforcement learning, the R is for Really gotta think of a third word I can use.
[^17]: Somewhere along the way, I think I forgot this was intended to be about my experiences writing the library code I had written so far, and started feeling the need to defend my choice of Rust. Speaking of which, Cargo is awesome for getting dependencies and testing code.
[^18]: I can't blame people for not using it. It kinda sucks.
[^19]: It doesn't tell me if the algorithm I implemented is what I say it is. Even though the thing I'm calling QLearner can train an agent to escape a maze, it might not actually be performing Q-learning due to me implementing it incorrectly
[^20]: *would feel like