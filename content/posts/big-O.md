+++
title = 'What is Good Code'
date = 2025-10-08T23:14:09-04:00
draft = false
toc = false
categories = ['Coding']
tags = ['big O']
series = ['DSA']
+++

> Before saying someone's code is sh*t code, you should know what is good code.

Apart from those that are not readable, in general, the good code should run fast and take up less memory space. Everyone can say their code is good, but how do you prove it? Simply monitoring runtime and memory space may not be accurate due to various factors-the data matters, and hardware also matters. A more scientific way to do so is to look at the **"trend"**-if the number of items grows, how would the time and space grow?

**Big O** is used to describe the *time complexity* or *space complexity* of algorithms. 

### Time Complexity

Most of the time when talking about big O, people refer to time complexity. For example, a for loop enumerates `n` items, then its time complexity is `O(n)`.

Why does this matter? Because in real-world applications, this `n` could be extremely large. A small difference in algorithm design can increase the time by a huge amount. Just think of GTA online loading time ([story](https://nee.lv/2021/02/28/How-I-cut-GTA-Online-loading-times-by-70/)).

So here's how we do big O analysis:
1. Think about the "Worst Case"
   - Given an array, we want to find an item. The position of that item matters to the computation time, but we only consider the worst-case scenario, where the item is positioned last.
2. Remove Constants
   - A function might have more than one loop and some other commands: `O(2n + 3)`
   - If the `n` is a million or more, drop the constants because they don't matter: `O(n)`
3. Different terms for inputs
   - If there are two input arrays, each of them has a loop.
     - Because we don't know their size, we can't combine them together, so: `O(a + b)`
   - If there's a nested function, it could be `O(n * n) = O(n^2)`
4. Drop Non Dominants
   - If the big O for a function is `O(n + n^2)`, we drop `n` because `n^2` is more important: `O(n^2)`

But how does this help me learn data structures and algorithms?

We all know that a program combines data structures and algorithms. A data structure stores the data, and an algorithm processes it.

Using big O notation, we can determine which data structure and algorithm to choose. For example, accessing an item in an array is O(1), while searching for an item takes O(n).

### Space Complexity

The reason people don't talk about "space complexity" that much is that hardware is cheap nowadays. But still, terrible algorithm can cause issues like stack overflow.

Space complexity is mainly focus on "additional space". If the input is a super huge array but the function only print the items out, it would be `O(1)` because it doesn't add any space. If we copy that into a new array, then the space complexity would be `O(n)`.

### Conclusion

So, what is good code?
- It should be "readable" and clean, so other people can maintain it.
- It should have fast "speed", so it can scale.
- It should not use a lot of "memory", so it doesn't take too much resources.

---

Big-O Cheat Sheet: [link](https://www.bigocheatsheet.com/)

||||
|---|---|---|
| O(1) | Constant | no loops |
| O(log N) | Logarithmic | searching algorithms |
| O(n) | Linear | normal for loop |
| O(n*log(n)) | Log Linear | sorting algorithms |
| O(n^2) | Quadratic | e.g. two nested loops |
| O(2^n) | Exponential | recursive algorithms |
| O(n!) | Factorial | don't do it |