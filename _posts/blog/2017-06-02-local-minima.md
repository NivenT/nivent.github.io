---
layout: post
title: "Local Minima"
modified: 
categories: blog
excerpt:
tags: [CS, matrix]
image: 
  feature: 
date: 2017-06-02 22:48:00
---

My friend told me about an interesting algorithms problem he had come across and had not yet solved a while ago. We then worked on it together for some time, and eventually arrived at what believe to be a solution. This post is my attempt to recall the problem and our solution[^1][^2].

# Warmup Problem
The problem has to do with finding a certain element of a matrix. Before getting to it, I want to start with a simpler case of the problem just to get used to things. We first need to know what we are searching for.

>Definition<br>
A <b>local minimum</b> of an array of numbers is an element that is (strictly) smaller than its all of its neighbors[^3].

So, unsurprisingly, we are gonna be searching for local minima. One important thing, though, is that we assume no array has a repeated element.

>Problem<br>
Given any array of $$n$$ unique numbers, how do you find a local minimum in time $$O(\log n)$$?

The solution, as hinted by the $$O(\log n)$$ time complexity, is to essentially do a binary search. Start by looking at the middle element. If it's a local minimum, you're done. If it's bigger than the element to the right, then recursively search the right half of the array.

Below in an example of this algorithm[^4] run on a list of unique numbers. The convention I use is that a number is large if its part of the numbers currently being considered by the algorithm, and it is huge if its the sole number the algorithm is looking at in the moment.

$$\begin{matrix}
\Large{1} & \Large 4 & \Large 3 & \Large{12} & \Large{11} & \Large 0 & \Large{10} & \Large 9 & \Large 8 & {\Huge 7} & \Large 6 & \Large 2 & \Large{14} & \Large{13} & \Large{17} & \Large{15} & \Large{16} & \Large 5 \\

 &&&&&&&&&\bigg\downarrow \\

{1} & \ 4 & \ 3 & {12} & {11} & \  0 & {10} & \ 9 & \ 8 & { 7} & \Large 6 & \Large  2 & \Large{14} & \Large{13} & {\Huge 17} & \Large{15} & \Large{16} & \Large 5 \\

 &&&&&&&&&\bigg\downarrow \\

{1} & \ 4 & \ 3 & {12} & {11} & \  0 & {10} & \ 9 & \ 8 & { 7} & \Large 6 & \Large  2 & {\Huge 14} & \Large{13} & { 17} & {15} & {16} &  5 \\

 &&&&&&&&&\bigg\downarrow \\

{1} & \ 4 & \ 3 & {12} & {11} & \  0 & {10} & \ 9 & \ 8 & { 7} & \Large 6 & {\Huge 2} & { 14} & {13} & { 17} & {15} & {16} &  5
\end{matrix}$$

I coded this up in C++ as below

```c++
inline bool isSmallerLeft(const vector<int>& arr, int index) {
  return index <= 0 || arr[index] < arr[index-1];
}

inline bool isSmallerRight(const vector<int>& arr, int index) {
  return index + 1 >= arr.size() || arr[index] < arr[index+1];
}

inline bool isLocalMin(const vector<int>& arr, int index) {
  return isSmallerLeft(arr, index) && isSmallerRight(arr, index);
}

int findLocalMin(const vector<int>& arr) {
  int lo = 0, hi = arr.size() - 1;
  while (hi >= lo) {
  	int mid = (lo + hi) >> 1;
  	if (isLocalMin(arr, mid)) {
  	  return mid;
  	} else if (isSmallerLeft(arr, mid)) {
  	  lo = mid+1;
  	} else {
  	  hi = mid-1;
  	}
  }
  return -1;
}
```

>Theorem<br>
The above algorithm is correct and $$O(\log n)$$

<div class="proof2">
Pf: Assume without loss of generality that you just checked an element \(x\) and found out it was bigger then the element to the right of it (This is the only interesting case). Then, you know there must a local minimum to the right of \(x\) in the array. Why? Either the array keeps decreasing, in which case the last element is necessarily a minimum, or the array increases at some point in this direction. In that case, you will find a minimum where that increase happens. Thus, the algorithm is definetly correct. Analyzing its time complexity is left as an exercise to the reader who is currently unconvinced of it. \(\square\)
</div>

# Real Problem
Now that we got that out of the way, let's look at something a little bit harder. Now, instead of considering 1D arrays, we'll look for a local minimum of a matrix. We still require every number in the matrix to be unique, and it is (probably) important to keep in mind that when we search for local minima, any entry in a matrix has at most 4 neighbors.

>Problem<br>
Given an $$n\times n$$ matrix of unique numbers, how can you find a local minimum in time at worse $$O(n)$$?

The first thing to notice is that moving from arrays to matrices cause our time complexity to go from $$O(\log n)$$ to $$O(n)$$. I don't know about you, but seemed strange to me. I don't know of a clear realtion between $$\log n$$ and $$n$$ in the context of matrices. Furthermore, you would expect the matrix problem to be slower, but it actually has better complexity in relation to what it could be[^5]. What I mean is that in the worst case we check every element, so we can look at ratios to get a sense of how much better than worst-possible we are doing. In the array case, we get $$\frac{\log n}n$$, but in the matrix case we get $$\frac n{n^2}=\frac1n$$ which is even smaller. 

At this point, I encourage you to stop reading and spend the next couple of hours thinking about this problem, trying to come up with a solution. I'll wait$$\dots$$

You're back; let's say more stuff [^6]. As it turns out, this lack of obvious relation between time complexites is related to there being fundamentally different ideas going into how each problem is solved. The issue with trying to generalize the case of arrays is that with matrices there's no nice ordering on the indices. You could "flatten" an $$n\times n$$ matrix into a large array and run the previous algorithm on it, and this would get a solution in time $$O(\log(n^2))=O(2\log n)=O(\log n)$$ which is even better than we want, but you are not actually guaranteed to get a local minimum by doing this! [^7] If this isn't obvious, stop for a second and convince yourself that it is. Below, you probably want to read the footnotes.

Instead, here's the solution my friend and I came up with. Start with the middle row, and find its absolute (read: not local) minimum [^8]. If its a local minimum, we win. If not, then either the value above or below it is smaller. Recursively find a local minimum in the half-matrix containing the smaller value [^9]. That's it. Note that because of the nature of the algorithm, the only things we consider as possible local minima are the absolute minimal elements of rows.

Before looking at an example, let's calculate its time complexity $$T_n$$ on an $$n\times n$$ matrix. It is

$$\begin{align*}
T_n = n + \frac n2 + \frac n2 + \frac n4 + \frac n4 + \frac n8 + \frac n8 + \dots = 3n = O(n)
\end{align*}$$

where we consecutively look at matrices of size $$n\times n,(n/2)\times n,(n/2)\times(n/2),(n/4)\times(n/2),\dots$$

The above calucation was informal, but that's ok since its correct. Below is an example run of the algorithm with the same conventions as before with an addition of a star by the row or column whose minimum was found.

$$\begin{matrix}
\begin{matrix}
\\
& \Large{22} & \Large{7} & \Large{21} & \Large{4} & \Large{12} \\
& \Large{6} & \Large{2} & \Large{8} & \Large{13} & \Large{10} \\
* & \Large{17} & \Huge{5} & \Large{15} & \Large{14} & \Large{9} \\
& \Large{16} & \Large{11} & \Large{18} & \Large{3} & \Large{20} \\
& \Large{19} & \Large{23} & \Large{1} & \Large{25} & \Large{24} 
\end{matrix}
\longrightarrow
\begin{matrix}
 & & * & &\\
\Large{22} & \Large{7} & \Large{21} & \Large{4} & \Large{12} \\
\Large{6} & \Large{2} & \Huge{8} & \Large{13} & \Large{10} \\
{17} & {5} & {15} & {14} & {9} \\
{16} & {11} & {18} & {3} & {20} \\
{19} & {23} & {1} & {25} & {24} 
\end{matrix}
\longrightarrow
\begin{matrix}
\\
\Large{22} & \Large{7} & {21} & {4} & {12} & \\
\Large{6} & \Huge{2} & {8} & {13} & {10} & *\\
{17} & {5} & {15} & {14} & {9} & \\
{16} & {11} & {18} & {3} & {20} & \\
{19} & {23} & {1} & {25} & {24} & 
\end{matrix}
\end{matrix}$$

>Exercise<br>
Write code that performs this algorithm, and count the number of steps (comparisons) it takes to find a local minimum on a large sample of random $$n\times n$$ matrices. See if this number is actually roughly $$3n$$ as expected. 

Finally, a far too wordy proof...

>Theorem<br>
This algorithm is correct with time complexity $$O(n)$$.

<div class="proof2">
Pf idea: The claim of the time complexity was shown earlier, so we only argue for the algorithm's correctness here. If the first value checked (the minimum of the middle row) is not a local minimum, how do we know we will still find one? The first thing to notice is that every matrix (and hence every matrix of original \(n\times n\) matrix) has a local minimum. Hence, we could recursively search any submatrix and find a local minimum, except for the fact that a local minimum of a submatrix might not be a localminim of the original matrix (Ex. take the extreme case of a one-element submatrix). It is not too hard to see that if a local minimum of a submatrix fails to be a local minimum of the original matrix, then it must lie on the edge of the submatrix. Thus, without loss of generality, assume the middle element of the first row is not a local minimum and the element directly above it is smaller than it. In this case, we would recursively search the top half of the matrix and everything is fine unless the local minimum we find is on the row directly above the middle row (then things might or might not be fine), so assume this is the case. Note that some element of this row is smaller than the minimum element of the middle row (that's why this submatrix was chosen), and so the middle element of this row is smaller than the minimum elment (and by extension any element) of the middle row. Here, using the fact that our algorithm only searches minimal elements of rows, the minimum element of the row above the middle row must be the number we returned given the assumptions we've made. This number is smaller than the numbers directly above it and to its left and right (if it were not, then we wouldn't have chosen it as the local minimum). By the previous reasoning, its also smaller than the number directly below it, so it is in fact a local minimum. Since this was the only case things could go wrong, our algorithm must work in all cases. \(\square\)
</div>

Take some time to make sure this proof makes sense to you and is legit. If after a while, you're still not convinced and you know a case where things go wrong, then leave a comment telling me where I went wrong.

# Bonus
This post lacked much motivation and insight into where these solutions came from, and I usually like to try to have those things. I won't include them here, but I will say I feel I somewhat robbed you of the chance to solve these problems yourself, so here's an (unrelated) bonus problem I found just before writing this post. It's not quite as difficult as this problem, but (hopefully) not immediately obvious

>Problem<br>
Given a sorted $$n$$-element array where every element appears 2 times except for a single number appearing once, how do you find this number in time $$O(\log n)$$?

As an example, given the array $$\{1,1,2,2,3,3,5,5,7,8,8,9,9\}$$, you would return $$7$$ as your answer. 

[^1]: Warning: I'm not 100% sure our solution is correct. It's fairly handwavy
[^2]: Warning: This post might end up being kinda dense because I'm not sure what to say other than "here's a problem; here's a solution"
[^3]: When we move on to matrices, most elements will have 4 neighbors. Diagonal elements are not neighbors.
[^4]: Modulo me being inconsistent about which element is the middle one
[^5]: I'm not an Algorithms person, and this is not a standard complexity comparing method. This is just a way I think/thought of things
[^6]: If you didn't come up with a solution, you're not alone. This problem originated in an Algorithms class here on a problem set, but was hard enough that the professor changed his mind after assigning it and decided to not make it mandatory. Instead, it became a bonus problem.
[^7]: There might be a way to fix this issue to end up with a working algorithm. I have not explored this option.
[^8]: If there are fewer columns than rows, start with the middle column
[^9]: Every step you end up rotating the matrix 90 degrees. For example, in the first step, you search a row of size n, but in the second you search a column of size n/2. Note that you don't actually rotate the matrix because that would waste time. You just switch between rows and columns.