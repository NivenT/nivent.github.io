---
layout: post
title: "Generic Wrappers in C++"
modified:
categories: blog
excerpt:
tags: [CS, C++, wrapper, macros, code]
date: 2018-09-07
---

For a blog entitled "Thoughts of a Programmer," I don't actually have many CS-related posts; a more accurate name of this blog would be something like "Grammatically Flawed Ramblings of a Not Quite Mathematician"[^1]. However, I recently wrote some code I think might be worth sharing, so this is a chance for me to return to this blog's roots [^2]. The main goal of this post is to explain the code written in [this beautiful file](https://github.com/NivenT/jubilant-funicular/tree/master/include/nta/Wrapper.h). This code automates the process of creating a wrapper class, so next time I want to have a "named int" class, I won't need to write[^3]

```c++
class NamedInt {
private:
    typedef int inner;
    int data;
public:
    NamedInt(int data = 0) : data(data) {}
    NamedInt operator+(const NamedInt& rhs) const { return data + rhs.data; }
    // All the other operators...
};
```

To avoid (some) confusion, I'll adopt the convention that the type being wrapped (e.g. `int` in the above example) will be called the inner type in contrast to the wrapper type (e.g. `NamedInt` in the above example).

# Motivation
Why create wrapper classes in the first place? The int type already exists in C++, so what's the point of creating a class whose whole point is simulating an integer? Long story short, the main reason is type safety. Programmers are fond of making mistakes, so anything we can do to make it harder for our mistakes to compile is a plus. One of the standard examples of what I'm talking about comes from writing code involving units. Imagine you're writing code to control a robot. Imagine further that this robot looks around its environment for interesting things to pick up, and then goes and picks up that thing if its close enough. You may implement this with code like
```c++
class Robot {
private:
    float goto_threshold;
    // other stuff...
public:
    bool should_goto(float interesting_object_distance) {
        return interesting_object_distance < goto_threshold;
    }
    // other stuff...
};
```
Seems simple enough. However, you probably don't want your robot wandering too far away to pick up random items because your testing area is small or because the further it goes, the more likely it is to crash into something or because whatever; hence, you set `goto_threshold = 50; // feet`. However, computer vision has come a long way [^4], so its detect objects up to 3000 feet away; to keep numbers somewhat small, this causes you to store `interesting_object_distance` in yards instead of feet. This is a problem. It means `should_goto` is comparing feet to yards, so your robot is bound to have some funky behavior [^5]. The best solution to a problem like this is to introduct a `Feet` class wrapping the float type and another `Yard` class also wrapping the float type. Then, you can declare `Feet goto_threshold = 50;` and `bool should_goto(Yard interesting_object_distance);`. Since `Feet` and `Yard` are different types, they (should) be incomparable, so the compiler will yell at this faulty comparison.

For me, the desire the use wrapper types came from an ambiguous function error. While working on a project, I wrote the following code:
```c++
class ECS {
public:
    void broadcast(const Message& msg, EntityID entity);
    void broadcast(const Message& msg, ComponentListID lists);
};
```
and the compiler was not happy. This is because, while it looks like these functions have different signatures, elsewhere in my codebase I had written
```c++
typedef uint64_t EntityID;
typedef uint64_t ComponentListID;
```
I won't get into the reasons that I needed these two similar looking functions; just know that they are semantically different, and in general, it makes sense to think of EntityIDs as being different from ComponentListIDs even if they're essentially both just (unsigned long) integers. Because of this, I decided that it would be in my best interest to make `EntityID` and `ComponentListID` wrappers around `uint64_t` instead of just typedefs. Since this is the only place in the codebase I need wrapper types, I could just have written a couple wrapper classes and called it a day, but what's the fun in that? Instead, I decided I needed to find a generic way to create a wrapper around any class so that the new wrapper class inherits all the methods (or at least all the operations) of the class it wraps. This way, not only would `EntityID` and `ComponentListID` be different types (removing the ambiguity in the definition of ECS::broadcast), but I would also still be able to do things like
```c++
EntityID a = 1, b = 3;
a += b;
if (a & b) cout<<a<<endl;
```
but, you know, more relevant to my project.

# First Attempt
Ok, so we want an automated way to create wrapper classes over arbitrary [^7] types. Well, when creating generic types in C++, the goto method is templates. As such, the first thing we might try to do is something like this:
```c++
template<typename T>
class Wrapper {
private:
    T data;
public:
    Wrapper(T d) : data(d) {}
    Wrapper operator+(const Wrapper& rhs) const { return data + rhs.data; }
    Wrapper operator-(const Wrapper& rhs) const { return data - rhs.data; }
    // other operations
};
typedef Wrapper<uint64_t> EntityID;
typedef uint64_t ComponentListID;
```

The first thing you probably noticed about this approach is that `EntityID` became a wrapper while `ComponentListID` remained a primitive type. This is because using templates only allows for one wrapper class around a given type. Thus, if you were to need, for example, a third type of ID (e.g. a `ComponentID`), this approach would be no use. However, there is an even larger issue with this approach; it is not truly generic. This gives you a way of creating wrapper classes, but it only let's you wrap types that support a given set of operations! For example, with things as they are above, you wouldn't be able to use `Wrapper<std::string>` in your code because you can't substract strings. In practise, this means that if you want to wrap some numeric type (and so want your wrapper template to support all arithmetic operations) like int or uint64_t, then you will only be able to wrap types that support all arithmetic operations. This is horribly restrictive. 

We need a better solution. One that let's us create aribtarily many (different) types wrapping the same inner, and one that causes the wrapper to inherit all the operations supported by the inner type (without causing compiler errors). 

The first issue is easy to fix. Templates only create one type wrapper class per inner type? No problem; just use macros instead. By writing
```c++
#define CREATE_WRAPPER(name, inner) \
    class name { \
    private: \
        inner data; \
    public: \
        name(inner d) : data(d) {} \
        name operator+(const name& rhs) const { return data + rhs.data; } \
        name operator-(const name& rhs) const { return data - rhs.data; } \
        /* other operations */ \
    };
CREATE_WRAPPER(EntityID, uint64_t)
CREATE_WRAPPER(ComponentListID, uint64_t)
```
we give each class a unique name, so there's no worry if two classes wrap the same type. However, there's still the issue that writing `CREATE_WRAPPER(FirstName, std::string)` would cause the compiler to yell at us. At this point, I encourage you to pause and spend a few minutes thinking about how we could fix this. [^9]

# Why This Should Be Possible
Given how well the first attempt went, it should seem like this might not be possible in C++, or at least that it would be very hard to do. Nevertheless, I would like to spend this section giving a few reasons for why you might believe that this is actually doable with reasonable effort. 

First, if it were not possible, then this blog post probably wouldn't exist. 

That actually isn't a very good reason, so here's one that's a little better. This type of thing is possible in other languages. Explicitly, using mypy with Python, you can write something like
```python
from typing import NewType

EntityID = NewType('Entity', int)
ComponentListID = NewType('ComponentListID', int)

def broadcast(entity: EntityID):
    print('Entity')
def broadcast(lists: ComponentListID):
    print('ComponentList')

broadcast(3)  # mypy complains because int is not the same as EntityID or ComponentListID
broadcast(EntityID(3)) # prints Entity
broadcast(ComponentListID(3)) # prints ComponentList
```
Now, I'm no Python expert [^6], but I have spent some time with mypy. Based on what I recall, my understanding is that this is implemented by using a "layered" approach. To python, EntityID=ComponentListID=int, so all three types support the same operations; however, mypy "artificially" considers them as separate types and keeps track of which type is used where via static analysis; this let's it catch bugs like the call to `broadcast(3)`. Unfortunately, in producing similar functionality in C++, we're constrained to work within the language and not outside of it like mypy does with Python. Still, the fact that any kind solution exists to our problem is suggestive that a solution appropriate to our needs exists as well.

The third, final, and (probably) most convincing reason to believe this is possible is that all the information we need should be available at compile-time. right? Our big issue is that we want wrappers to automatically support the same operations as the inner type. Well, when we write (something like) `CREATE_WRAPPER(EntityID, uint64_t)`, the compiler knows all the type information associated to `uint64_t`, including all its supported operations. Hence, it stands to reason that we should be able to take advantage of this to have `EntityID` support those same operations. As we will see in the next section, this can be done [^8].

# The Basic Idea
The basic idea is to have two versions of each operation. In psuedo-code, we want to write
```c++
Wrapper Wrapper::operator+(const Wrapper& rhs) const {
    if (Wrapper::inner supports addition) {
        return data + rhs.data;
    } else {
        unsupported_operation_behavior();
    }
}
```
It seems to me that there's no clear choice for what `unsupported_operation_behavior()` should do. Ideally, this code never gets run because you shouldn't try to do anything with your wrapper types that you couldn't even do on the inner type. Currently, I return a default wrapper type in these situations (in the project I'm working on), but another reasonable action would be to crash the program.

The question now becomes: how do we exploit compiletime information in order to know whether an arbitrary type supports addition? For questions like this, [the < type_traits > header](https://en.cppreference.com/w/cpp/header/type_traits) comes in handy. First, we write a custom class that checks for the existence of an addition operator.
```c++
namespace check {
    struct Nop {};
    template<typename T, typename U> Nop operator+(const T&, const U&);
    template<typename T, typename U>
    struct AddExists {
        enum { value = !std::is_same<decltype(*(T*)(0) + *(U*)(0)), Nop>::value };
    };
    // AddExists<int>::value == 1
    // AddExists<Nop>::value == 0
    // AddExists<int, std::string>::value == 0
}
```
The above code sets up a default addition operator returning a custom `Nop` type for any pair of types that doesn't support addition. Then, to find out whether two types `T` and `U` do support addition, it simple checks if adding them returns this `Nop` type or something else.

Given this, we can implement addition on our Wrapper type with code like the below (still in our macro):
```c++
template<typename T>
auto __Add(const T& lhs, const T& rhs) -> decltype(std::enable_if_t<check::AddExists<T>::value, Wrapper>{}) {
    return lhs + rhs;
}
template<typename T>
auto __Add(const T& lhs, const T& rhs) -> decltype(!std::enable_if_t<check::AddExists<T>::value, Wrapper>{}) {
    unsupported_operation_behavior();
}
Wrapper Wrapper::operator+(const Wrapper& rhs) const {
    return __Add<Wrapper::inner>(data, rhs.data);
}
``` 
I think with some thought, the above code is mostly self-explanatory. It creates two `__Add` functions, one for types that support addition and one for types that don't. When adding `Wrapper`s, the actual computation is relegated to the `__Add` functions, and C++ automatically knows which one to invoke since it knows (at compile time) whether or not `Wrapper::inner` supports addition. If you are using C++17, then the above code can be simplified a little, becoming [^10]
```c++
template<typename T>
Wrapper __Add(const T& lhs, const T& rhs) {
    if constexpr (check::AddExists<T>::value) {
        return lhs + rhs;
    } else {
        unsupported_operation_behavior();
    }
}
Wrapper Wrapper::operator+(const Wrapper& rhs) const {
    return __Add<Wrapper::inner>(data, rhs.data);
}
```
which is a little closer to the psuedo-code at the beginning of this section.

The same approach we used for addition can be used with all other operations (potentially with minor modifications). Thus, by writing lots of analagous code (and maybe some helper macros), you can use this basic idea to create our desired generic wrapper class!

# Some Hiccups
As is often the case, the full story is not as simple as one would like. When implementing this, I ran into a few issues after figuring out the basic idea outlined in the previous section. Unfortunately, I have waited long enough between writing that code and this post that I no longer recall what all those issues were. The only one that comes to mind is printing.

In C++, in order to support printing (via `cout<<`) a custom type `Wrapper`, you need to implement a function with signature
```c++
std::ostream& operator<<(std::ostream&, const Wrapper&);
```
At first, you may think you can do to same thing we did for addition and write (where I ommited the `\` after each line in order to have helpful syntax highlighting) [^11]
```c++
#define CREATE_WRAPPER(name, inner) /* This macro includes all the below code plus other stuff */
template<typename T>  
static auto __Print(std::ostream& lhs, const T& rhs) -> decltype(std::enable_if_t<check::LShiftExists<std::ostream, T>::value, std::ostream&>{}) { 
  return lhs<<#name<<"("<<rhs<<")"; 
} 
template<typename T>           
static auto __Print(std::ostream& lhs, const T& rhs) -> decltype(std::enable_if_t<!check::LShiftExists<std::ostream, T>::value, std::ostream&>{}) { 
  return lhs<<#name; 
}                      
std::ostream& operator<<(std::ostream& lhs, const name& rhs) {
  return name::__Print<inner>(lhs, rhs.data); 
} 
/* end macro stuff */
CREATE_WRAPPER(EntityID, uint64_t)
// cout<<EntityID(4); should print out "EntityID(4)"
CREATE_WRAPPER(Test, glm::vec2)
// cout<<Test(glm::vec2(0)); should print out "Test"
```
However, there are two issues with the above code. First, if you scroll all the way to the right, you will notice that the return type of `__Print` is more-or-less
```c++
decltype(std::enable_if_t<std::true_type, std::ostream&>{})
```
which is a problem. I won't get into the details, but suffice it to say, you can't (easily) use `std::enalble_if/std::enable_if_t` with reference types. This is basically because `std::enable_if` is a struct (potentially) with a field of the type specified in its (second) parameter. If this is a reference type, then we need to give it a reference when it's constructed but here we want to give it an empty construction via `{}`. At the same time, you can't simple replace `std::ostream&` with `std::ostream` because, among other reasons, the copy constructor for `std::ostream` is deleted. In the end, the solution I took was to replace the reference with a pointer, writing
```c++
#define CREATE_WRAPPER(name, inner) /* This macro includes all the below code plus other stuff */
template<typename T>  
static auto __Print(std::ostream& lhs, const T& rhs) -> decltype(std::enable_if_t<check::LShiftExists<std::ostream, T>::value, std::ostream*>{}) { 
  lhs<<#name<<"("<<rhs<<")"; 
  return &lhs;
} 
template<typename T>           
static auto __Print(std::ostream& lhs, const T& rhs) -> decltype(std::enable_if_t<!check::LShiftExists<std::ostream, T>::value, std::ostream*>{}) { 
  lhs<<#name; 
  return &lhs;
}                      
std::ostream& operator<<(std::ostream& lhs, const name& rhs) {
  return *name::__Print<inner>(lhs, rhs.data); 
} 
/* end macro stuff */
CREATE_WRAPPER(EntityID, uint64_t)
// cout<<EntityID(4); should print out "EntityID(4)"
CREATE_WRAPPER(Test, glm::vec2)
// cout<<Test(glm::vec2(0)); should print out "Test"
```

This leaves only one last issue before we're satisfied: all this code is in a header file. Recall that we wanted a generic way to create wrapper types, and settled and using a macro to do so. Well, that macro (and all its encapsulated code) are going to be stored in a single header file. Since we want printing to be supported without further user intervention, this printing code will be in the header as well. However, `std::ostream& operator<<(std::ostream&, const name&)` is a regular function and not a method of our wrapper class.  This means that the compiler will have a fun time yelling at us about this function having multiple definitions the second two files include this header. Thankfully, this has a simple fix. All you need to do is mark the function `inline`, and the compiler shuts up.

# The Finished Product
At last, we have everything we need in order create generic wrappers. If you want to see a complete implementation of this, then [check out the file I referenced at the beginning](https://github.com/NivenT/jubilant-funicular/blob/master/include/nta/Wrapper.h). If you want to see these wrapper types in action, then that project has you covered as well. In particular, [here](https://github.com/NivenT/jubilant-funicular/blob/master/tests/wrapper_tests.cpp) are tests for the wrapper macro, and [here](https://github.com/NivenT/jubilant-funicular/blob/master/src/ECS.cpp) is a wrapper type (`EntityID`) being used in the wild. For conveience, I'll end with a (modified) snippet of the tests file I just linked to
```c++
#include "Wrapper.h"
#include "utils.h"

CREATE_WRAPPER(Inches, int)
CREATE_WRAPPER(Feet, int)
CREATE_WRAPPER(Name, string)

int main(int argc, char* argv[]) {
    Inches a = 12;
    Feet b = 1;
    Name c("Steve");

    assert(utils::to_string(a) == "Inches(12)");
    assert(utils::to_string(b) == "Feet(1)");
    assert(utils::to_string(c) == "Name(Steve)");

    // Confirms that you can't check for equality between Inches and Feet even though they wrap the same type
    if ((int)check::EqualsExists<Inches, Feet>::value == 1) {
        assert(false);
    }

    assert(a == 12);
    assert(a + 5 == 17);
    assert((b << 3) == 8);
    assert(a++ == 12);
    assert(a == 13);
    assert(++b == 2);
    assert(~Inches(0) == Inches(~0));

    a *= 5;
    assert(a == 60);
    b /= 2;
    assert(b == 1);
    a -= 15;
    assert(a == 45);
    b += 8;
    assert(b == 9);
    assert(a != 10);

    assert(a > 3);
    assert(b < 10);
    assert(a <= 45);
    assert(b >= 8);

    assert(c + string(" Rogers") == Name("Steve Rogers"));
    // As a quirk of the implementation, you get an empty wrapper whenever
    // an invalid operation is performed
    assert(c - Name("Uh-oh") == Name());
    return 0;
}
```

[^1]: As much as I like this name, I have put some thought into what I could rename this blog to in order to reflect its focus on mathematics. I think I like the sound of "In a Neighborhood of the Truth."
[^2]: Incidentally, this (apparently) marks the 2-year anniversary of my first CS post.
[^3]: I should go ahead and warn you now, this post will (probably) have a lot of (C++) code (snippets).
[^4]: I you believe that you will eventually overcome the technical challenges involved it letting it chase after far off objects
[^5]: If i remember correctly, the first Mars rover crashed because of a unit issue. Some engineer or some piece of code assumed it was getting feet when it was actually getting meters or something like that.
[^6]: And certainly no mypy expert
[^7]: I'm using the word "arbitrary" in a weak and ill-defined sense here. For my purposes, I really only need to be able to do this with integral types (and really only with uint64_t). However, having something that works for a larger class of types doesn't hurt.
[^8]: Because of the specifics of how we'll do this, we actually "support" a superset of the operations of the inner type.
[^9]: If you're anything like me, your first thought is something like, "Rust has Traits and those would make this easy. Maybe I should write this project in Rust instead." Unfortunately, if you are like me, it's too late for you to write this project in Rust instead.
[^10]: I haven't actually confirmed that this compiles, so let me know if it doesn't
[^11]: Don't worry if you don't know what glm::vec2 is. All that's important is that it doesn't support printing via ostream's