---
layout: post
title: "Demystifying Emulators"
categories: blog
modified:
excerpt:
tags: [CS, emulator, Haskell, Chip-8, C++, Python, Rust]
image: 
  feature: 
date: 2017-07-12 00:00:00
---

I don't remember when I first discovered emulators, but I remember thinking they were absolutely amazing. All of a sudden, I could play games from old systems I knew I would never own, replay games I had owned but lost, etc. I didn't think much of them past what games I could play until I started getting more into serious about coding and realized that there must be some magic going on underneath the hood that's making these things work. I tried imagining how they might work, but to no avail; they remained a black box. Because of that, I made it a goal of mine to write my own emulator one day, and as it turns out, [dreams do come true](https://github.com/NivenT/RGB).

Here, I want to talk a little bit about how emulators work [^1], and about how they're not magic after all. The basic idea behind emulators is surprisingly straightforward. They're very aptly named in that they do exactly what they say; they emulate. An emulator works by reproducing in software the same functionality provided by the hardware. Then, when you feed that software the same input as you would the hardware, it does the same things, and you have a working game system right on your computer.

So the basic idea is to convert hardware into software, but what does that actually mean? I don't really know a good single answer to that quation. Instead, it depends on the level of granularity you use. You could imagine you wanted to emulate a simple four-function calculator.

<center><img src="https://www.staples-3p.com/s7/is/image/Staples/m001843923_sc7?$splssku$" width="250" height="250"/><br>image source: <a href="https://www.staples.com/Impecca-Standard-Function-Calculator-Black-Ivy/product_1480120">Stables</a></center>

One way to do this would be to take a higher level approach where you let users type the corresponding keys on their keyboard, and implement the logic with a single `switch` statement. The workhorse of your code might look something like this[^2]

```python
def eval(lhs, rhs, op):
  return {
    '+': lhs+rhs,
    '-': lhs-rhs,
    '/': lhs/rhs,
    '*': lhs*rhs,
  }[op]
```

At this point, this doesn't feel much like an emulator, but it's doing the same thing the calculator does so I'd call it one. If you wanted a lower level, more granular approach, you might end up writing something like this to simulate to underlying logic circuits used by the calculator

```python
def addBits(lhs, rhs):
  total = lhs ^ rhs
  carry = lhs & rhs
  return (total, carry)
```

In this example, thinking as low as this is overkill, but that's not always the case. You will end up writing code that looks more like this than the `dictionary` lookup above, but you have to be careful not to think too granularly. I remember when I first heard this idea of emulators being software ports of hardware, I immediately starting imagining how to go about making classes for things as low level as the system bus and logic gates, and how to piece these together to get a working emulator. Sure, you could do something like that and make things work, but you don't have to stay that faithful to the hardware. Now that we have the general idea covered, let's dive into a working example

# curly-succotash
One of the simplest systems you can emulate that is still non-trivial is the [Chip-8](https://www.wikiwand.com/en/CHIP-8). Hence, for the purpose of this blog, I wrote a [sample Chip-8 emulator](https://github.com/NivenT/curly-succotash) to use as a reference. Before getting into the details, I should preface things by saying that this emulator is flawed in many ways. Aside from not being very user friendly, and possibly slow, it's main issue is that it was written in [Haskell](https://www.haskell.org/). I chose Haskell because I wanted to learn the language, and this seemed like a decently sized project for that, but given that Haskell is functional and so tries to avoid things like state and sequential logic, it's not the ideal language for an emulator[^3]. Also, Haskell isn't super popular, and doesn't have to most readable syntax to someone who doesn't know it. That being said, let's get started.

# Starting Off
With emulators, I like to think of the project as writing a CPU. Every other part of the machine is just a peripheral to help make sure the CPU is working properly. This mindset, while not always accurate, helps me focus my efforts and gives me a starting point from where to branch off other parts of the project. So we need to build a Chip-8 CPU. To start with that, we better make sure we have everything that the CPU needs to interact with so we can implement all its instructions. A quick Google search reveals that [Wikipedia has all the information we'll need on one page](https://www.wikiwand.com/en/CHIP-8), so we can go there to see the various registers and whatnot that make up our system. I chose to emulate each component like so

```haskell
data Chip8 = Chip8 {
  mem            :: [Word8],                  -- 4096 1-byte address
  regs           :: [Word8],                  -- 16 registers
  stack          :: [Int],                    -- 16(?) levels of addresses
  ptr            :: Int,                      -- I register (usually stores memory address)
  pc             :: Int,
  sp             :: Int,
  delay_timer    :: Int,
  sound_timer    :: Int,
  keys           :: [Bool],                   -- 16 keys
  screen         :: Map.Map (Int, Int) Bool   -- 64x32 pixels
} deriving (Show)
```

- The memory is just an array of values, and addresses are represented implicitly by index.
- A register is just some value; it's completely determined by the number it stores.
- The simplest representation of a key is just a Bool saying whether it's pressed or not. It's also possible to explicitly store the mapping between computer keys and Chip-8 keys here, but I generally prefer to keep that separate.
- The screen is a map from pairs of ints (pixel coordinates) to bools (pixel values: on/off). I originally had this as a 2d list, but that made some of the code more complicated than need be, so I changed it to this. Normally, a 2d array would be fine, but Haskell[^4].

Once you have this framework for the pieces of the emulator in place, you can start making it do stuff [^5]. In practice, this means implementing cpu instructions. Things like adding registers together or loading a value from memory into a register and stuff like that. The majority of instructions are fairly simple. Unfortunately, there are usually a lot of them which makes it easy to make mistakes, and boring to implement. Because of that, I like to only write a few at a time. I'll implement a couple, run the code and have it throw an error whenever it comes accross an instruction it doesn't know; then I'll implement that instruction, rinse, wash, and repeat. This cycle makes sure you're always working towards a working product, and let's you catch other bugs early on.

One common bug is to mess up the initial state of the system. This will manifest itself in your emulator trying to execute the opcode for an instruction that doesn't exist. I ran into that issue [here](https://github.com/NivenT/curly-succotash/blob/d6ad6144acd739b8e7ab113cc38cbd24a4978161/emu.hs#L85) when I first tried implementing game loading. I had memory laid out like

$$\newcommand{\x}{\text{x}}
\begin{array}{| c | c | c |}
0\x0 & 0\x1 & 0\x2 & \dots & 0\x4F & 0\x50 & 0\x51 & 0\x52 & \dots & S & S+1 & S+2 & \dots\\\hline
f_0 & f_1 & f_2 & \dots & f_{79} & g_0 & g_1 & g_2 & \dots & 0 & 1 & 2 & \dots\\
\hline
\end{array}$$

where $$f_0,f_1,f_2,\dots,f_{79}$$ is the font data [^6], $$g_0,g_1,g_2,\dots,g_N$$ is the game data, and $$S=0\x50+N+1$$ is the beginning of memory after all game data.

This is wrong for two reasons. First of all, the Chip-8 begins executing instructions from memory address $$0\x200$$ so that's where game data should begin. Secondly, the unused locations ($$S$$ and beyond) should be populated with all $$0$$'s. I caught this bug because earlier versions of the emulator would try to execute a non-existent instruction. If I had implemented all instructions before testing and only seen the issue then, I would have assumed the issue was with an incorrectly implemented instruction and not been able to fix things as quickly. 

The [correct memory layout](https://github.com/NivenT/curly-succotash/blob/master/emu.hs#L110) is

$$\newcommand{\x}{\text{x}}
\begin{array}{| c | c | c |}
0\x0 & 0\x1 & \dots & 0\x4F & 0\x50 & 0\x51 & \dots & 0\x200 & 0\x201 & \dots & T & T+1 & \dots\\\hline
f_0 & f_1 & \dots & f_{79} & 0 & 0 & \dots & g_0 & g_1 & \dots & 0 & 0 & \dots\\
\hline
\end{array}$$

where $$T=0\x200+N+1$$ takes the role of $$S$$.

For actually implementing instructions, you need some kind of mapping from opcodes to the execution of the instruction itself. One way of doing this that works fairly well is to just use a `switch` statement like in the calculator emulator we started with. The nice thing about this is that, if done right [^7], it's simple, efficient [^8], and [works](https://github.com/NivenT/curly-succotash/blob/master/op.hs#L81). However, it can also be a pain to maintain a giant switch statement, so you might want something more sophisticated. One things you can do is use a [struct](https://github.com/NivenT/RGB/blob/master/src/emulator/instructions.rs#L542) to hold basic information about instructions that can replace you having to re-lookup all the details hidden in your switch statement [when things go wrong](https://github.com/NivenT/RGB/blob/master/src/emulator/emulator.rs#L326).

# Aside on Switch Statements
This section is pretty unrelated to the rest of the post, but is something interesting I wanted to talk about. I mentioned in a footnote that `switch` statements can be faster than a series of `if` and `else if`'s. This may seem counterintuitive because the two appear to be doing functionaly equivalent things, and the obvious way to implement a switch statement is with if and else if. Take a look at this code

```c++
void use_switch(int val) {
  switch(val) {
  case 0: func0(); break;
  case 1: func1(); break;
  case 2: func2(); break;
  case 3: func3(); break;
  default: func4(); break;
  }
}

void use_if(int val) {
  if (val == 0) {
    func0();
  } else if (val == 1) {
    func1();
  } else if (val == 2) {
    func2();
  } else if (val == 3) {
    func3();
  } else {
    func4();
  }
}
```

A priori these two functions should be carried out the same way, but the difference is that using a switch statement means you are comparing `int`s to decide what to do whereas an if statement could rely on any condition. This may not seem like much, but in practice it means that `use_switch` can be implemented with an array of function pointers instead of a series of ifs. Perhaps more clearly, it could expand to something like this[^9]

```c++
typedef void (*FunctionPtr)();

void switch_expanded(unsigned int val) {
  FunctionPtr arr[5] = {func0, func1, func2, func3, func4};
  arr[val < 4 ? val : 4]();
}
```

Notice that these only makes use of a single condition but is functionally equivalent to the switch statement. As the number of cases in the switch grows, you can still only need to check a single condition whereas you'd (potentially) need to check all of them with if statements. Hence, you could think of the improvement of `switch` over `if` as being $$O(1)$$ versus $$O(n)$$, but things aren't this simple in practice. 

# Seeing Stuff + More than a CPU
Back to emulators... Ultimately, you want your emulator to do more than execute instructions. Specifically, from most to least important, you want it to display things, get user input, and produce sound. Displaying things can be tricky. Representing the state of the screen internally in the emulator and showing it to a user are two very different things. The best way to handle this I've found is to use OpenGl for rendering. You can draw a single rectangle that covers your entire screen and then give it a texture made from data from your emulator. I do not do that in curly-succotash because I could not figure out how to do textures with Gloss, and it seemed like overkill for what was supposed to be a simple project, but [here's a place I do do that](https://github.com/NivenT/RGB/blob/master/src/rendering.rs#L57). Getting to the point that your emulator displays anything intelligible is a major step; displaying things correctly can be one of the harder parts to get right. As an example, [look at the relative complexity of the draw_sprite function to every other instruction in Chip-8](https://github.com/NivenT/curly-succotash/blob/master/op.hs#L81). User input is usually much more tame, and I have not yet figured out a good way to do sound.

With Chip-8, that's basically all there is to it. Once you've implemented CPU instructions, the user can press buttons, and it beeps, you're done. You can have a functioning emulator in only a few hundred lines of code, and no magic. If you tackle a larger system, then there's more to do. You might have an actual GPU separate from the CPU, have more complicated timers or interrupts, different kinds of memory storage schemes, etc. However, in the end, it's all the same thing: you're just trying to get familiar enough with a system to be able to translate what it does to code. 

# Last words
Something you don't want to do with an emulator is render the screen by manually drawing the individual pixels. This is needlessly slow and (potentially) pixelated when you could get better, faster results by just using a single rectangle + a texture. An example of what not to do would be

```haskell
square :: Int -> Int -> Picture
square r c = Polygon $ map f [(r,c), (r,c+1), (r+1,c+1), (r+1,c)]
  where f (r, c) = (800.0/64.0 * (fromIntegral c) - 400.0, 600.0/32.0 * (fromIntegral r) - 300.0)

render_emu :: Chip8 -> Picture
render_emu emu = pictures . Map.foldrWithKey draw_pixel [] $ screen emu
  where draw_pixel (r, c) v lst = if v then (Color white $ square (31-r) c):lst else lst
```

One thing that is helpful is comments. Naturally with an emulator, there will be things you have to do because of something specific requirement or implementation detail of the system you're recreating. It's really easy to forget these details later one, so it helps to remind yourself of them as you move forward.

Finally, remember not to take things too literally because that can complicate how you do stuff. When you see an instruction or component you need to implement, focus more on replicating its behavior than its hardware implementation or the wording used to describe it. An example of this is instruction $$0\text{x}\text F00\text A$$ which in the Chip-8 which waits until a key is pressed, then stores that key in register $$\text V0$$. It's easy to think of doing this with a while loop or something like that, but that blocks all other parts of your code from running (something more complicated than Chip-8 could have [parts that run independently from the CPU](https://github.com/NivenT/RGB/blob/master/src/emulator/emulator.rs#L230)) and is needlessly complicated. Instead, you can implement this waiting behaviour with something a little more clever[^10]

```haskell
-- 0xFX0A Wait for a key press, then store key in VX (note: blocking operation)
  | (.&.) op 0xf0ff == 0xf00a  = case get_key ks of
                                   Just i  -> Left(rng, emu{regs=rpl_nth rs x $ fromIntegral i})
                                   Nothing -> Left(rng, emu{pc=p-2})
```

[^1]: I should probably mention that I'm no expert on emulators or really anything I'm gonna talk about in this post, so do with my advice what you will. Also, some of the advice I give is stuff I learned (i.e. stole) from other people. I'm too lazy to credit them everywhere I do it. Just know that if something I say seems like a well-thought out good idea, it probably wasn't mine.
[^2]: Ignore the fact that this calculator has a decimal point button, or a percent button, or whatever that thing in the top left is
[^3]: And given that it's not super popular, it's not an ideal language for a blog post. 
[^4]: Probably a way to make it work w/o ugly code, but I'm still new
[^5]: It's common, for me at least, to be missing pieces the first time you do this. However, that's fine. You'll realize that you're missing stuff when a CPU instruction requires it or later when trying to flesh out other parts of the emulator in the case of more complicated systems.
[^6]: The Chip-8 has 16 predefined sprites that are the hex digits
[^7]: curly-succotash does not do this right. A better way to do it would be to switch on the first (hexadecimal) digit of the opcode, and then nest more switch statements if needed (at most 4 deep, but really only like 2 deep in practice)
[^8]: It's not uncommon for switch statements to be faster than sequences of if's and else if's
[^9]: I made val unsigned to not have to deal with negative issues. It doesn't really affect anything
[^10]: Just decrement the program counter so this same instruction gets executed next timestep