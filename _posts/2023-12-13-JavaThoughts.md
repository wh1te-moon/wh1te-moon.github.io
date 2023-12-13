---
layout: page
title: thoughts about Java
tags: Java,algorithm
categories: study
---

## Difference with algorithm and produce

When studying algorithms, we often allocate memory upfront, such as declaring an array like 'long[10000]' or even larger. The primary focus is typically on time complexity, which indicates the computational time your code requires.

However, in real-world scenarios, during the production process, we cannot pre-allocate memory for all our data structures. Memory is allocated on-the-fly when needed. In Java, for instance, when creating an object, memory is allocated from the heap rather than the stack. The stack is faster than the heap, but what often impacts time costs the most is the allocation process, not just the time complexity.