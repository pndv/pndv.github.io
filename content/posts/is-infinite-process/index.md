---
title: "Is Infinite Process: An Interesting 'Easy' Problem"
date: 2023-05-23T13:22:17-07:00
draft: false
---

This is an interesting problem I came across on [CodeSignal](https://app.codesignal.com/); it is marked as easy but 
it took me some time to figure out (with help from the Internet). Here is the problem:
---
Given integers a and b, determine whether the following pseudocode results in an infinite loop

while a is not equal to b do
increase a by 1
decrease b by 1
Assume that the program is executed on a virtual machine which can store arbitrary long numbers and execute forever.

Example

For a = 2 and b = 6, the output should be
solution(a, b) = false;


For a = 2 and b = 3, the output should be
solution(a, b) = true.
---

The first approach was:

1. To trivially return `true` if `a` > `b`
2. Run a loop 10 times, noting the difference each time, return false (i.e. it will go in infinite loop) if:
   1. difference becomes zero any time
   2. absolute difference between two numbers has been consistently decreasing over the loop

Needless to say, this approach failed. 

This is marked as an "Easy" problem, so I was slightly embarrassed at not getting it right. Nevertheless, I 
persisted in trying with various conditions, seeing why the code is succeeding. After 2 days, I decided to look on 
the web to see where I was going wrong. I came across this one-liner in `python`:

```python
def isInfiniteProcess(a, b):
    return True if (a-b) % 2 == 1 or a>b else False
```
Which left me with more questions... what exactly is this logic?

#### The Aha! moment
The difference of two numbers should be odd, then it will go in infinite loop. But why? Here is the reasoning, if 
you look at the number line:

![Number Line](number-line.gif)

The blue lines show convergence, the difference between the two numbers is even. Whereas, the numbers marked with 
red have odd difference, at each loop, you see even though they are getting closer, at one point, given in orange, 
they _cross over each other without meeting_.

