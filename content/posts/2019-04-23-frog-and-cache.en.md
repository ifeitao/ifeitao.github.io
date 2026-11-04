---
categories:
- coding
date: 2019-04-23
lastmod: 2019-04-23
mathjax: true
slug: frog-and-cache
tags:
- Algorithms
- Dynamic Programming
title: 'Frog and Cache: A Simplified, Practical Dynamic Programming'
featured: true
toc: true
---

## 1. Starting with a frog

![frog](https://i.imgur.com/zuhczaLm.jpg)

A frog wants to hop down `n` steps into a pond. Each hop covers 1 or 2 steps. How many distinct ways can it get down there (say, when `n=30`)?

In mathematical terms we want a function `f(n)` for the frog's jumps. For a function on non-negative integers we can start from small cases, and it is not hard to get `f(1)=1, f(2)=2`. The problem is that brute-force enumeration gets painful fast.

Imagine you are that frog facing `n` steps. On the first hop you can take 1 step, leaving `n-1` steps with `f(n-1)` ways down; or you can take 2 steps, leaving `n-2` steps with `f(n-2)` ways down. So the answer is nothing new — it is the Fibonacci sequence:

$$
\begin{aligned} F_{0} &=0 \\ F_{1} &=1 \\ F_{n} &=F_{n-1}+F_{n-2} \quad(\mathrm{n} \geq 2) \end{aligned}
$$


The first step in solving this kind of function-value problem is to find a recurrence. Translate the recurrence into Python:

```python
def fib(n):
    if n==0:
        return 1
    if n==1:
        return 1
    return fib(n-1)+fib(n-2)
```

```
%%time
fib(30)

Wall time: 269 ms
832040
```

The runtime is `284ms` — slow enough. Why? Because there is far too much repeated computation. Take `f(5)` as an example; the calls look like this:

```
f(5)==>f(4), f(3)
f(4)==>f(3), f(2), f(3)==>f(2), f(1)
f(3)==>f(2), f(1), f(2)==>f(1), f(0), f(2)==>f(1), f(0), f(1)
f(2)==>f(1), f(0), f(1), f(1), f(0), f(1), f(0), f(1)
f(1), f(0), f(1), f(1), f(0), f(1), f(0), f(1)
```

The natural idea, then, is to cache every intermediate result. Fortunately Python ships that "battery" already.

```python
from functools import lru_cache
@lru_cache()
def fib(n):
    if n==0:
        return 1
    if n==1:
        return 1
    return fib(n-1)+fib(n-2)
```

```
%%time
fib(30)
Wall time: 0 ns
832040
```

So fast that no time could be measured. The basic mechanism of `lru_cache` in Python is a dict whose `key` is the call argument and whose `value` is the result for that argument. It is roughly equivalent to this code:

```python
def fib(n):
    if n in fib.cache:
        return fib.cache[n]
    if n==0:
        ans = 1
    elif n==1:
        ans = 1
    elif:
        ans = fib(n-1)+fib(n-2)
    fib.cache[n] = ans
    return ans
fib.cache = {}
```

Of course, for this specific problem we can use a more careful caching scheme, or even drop recursion in favor of a loop (equivalent to keeping only two cached values, which cuts space usage a lot — but if we need to compute many different `n` values over and over, the previous method may be the better fit):

```python
def fib(n):
    a, b = 0, 1
    for i in range(n):
        a, b = b, a+b
    return a
```

This problem is identical to [leetcode 70](https://leetcode-cn.com/problems/climbing-stairs). The python3 solution on leetcode is:

```python
from functools import lru_cache
class Solution:
    @lru_cache()
    def climbStairs(self, n: int) -> int:
        if n==0:
            return 1
        if n==1:
            return 1
        return self.climbStairs(n-1)+self.climbStairs(n-2)
```

Runtime 52 ms, memory 13.2MB.

## 2. A simplified, practical dynamic programming

The frog gives us a fairly general lesson for problems where a recurrence can be constructed:

1. Find a recurrence relation, write the recursive function, and the problem becomes solving a set of subproblems;
2. To avoid recomputing the same subproblem, use a cache — trade space for time.

General algorithm textbooks and interview write-ups spend a lot of time designing that cache structure. In real engineering we are usually not that sensitive to using a bit more cache space, so writing the recursive function plus a generic cache basically solves the problem. Only when cache space itself becomes a concern do we need to think about a smaller cache tailored to the problem.

To test this approach, let us look at a few more problems, pulled straight from leetcode.

### 2.1 [Maximum Subarray](https://leetcode-cn.com/problems/maximum-subarray/)

Given an integer array `nums`, find the contiguous subarray with the largest sum (the subarray contains at least one element) and return that sum.

**Example:**

> Input: [-2,1,-3,4,-1,2,1,-5,4],
> Output: 6
> Explanation: The contiguous subarray [4,-1,2,1] has the largest sum, 6.

Consider the recurrence for the maximum sum obtainable by a subarray ending at each position in the array.
$$
\begin{aligned}  f(0)&=nums(0) \\ f(k)&=max(f(k-1), 0)+nums(k) \quad(k>0) \end{aligned}
$$
From that, the final answer is easy:
$$
ans = max_{i=0}^n(f(i))
$$
Translated into python3 on leetcode:

```python
from functools import lru_cache
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        self.nums = nums
        return max(self.f(i) for i in range(len(nums)))
    
    @lru_cache()
    def f(self, k):
        if k == 0:
            return self.nums[0]
        else:
            return max(self.f(k-1), 0) + self.nums[k]
```

Runtime 76 ms, memory 13.7 MB.

### 2.2 [Minimum Path Sum](https://leetcode-cn.com/problems/minimum-path-sum/)

Given an *m* x *n* grid of non-negative integers, find a path from the top-left corner to the bottom-right corner such that the sum of the numbers along the path is minimized.

**Example:**

> Input:
> [
>   [1,3,1],
>   [1,5,1],
>   [4,2,1]
> ]
> Output: 7
> Explanation: The path 1→3→1→1→1 has the smallest sum.


Treating each cell of the matrix as the bottom-right corner and computing the minimum path sum to it gives the recurrence below:

$$
\begin{align}
f(0, 0) &= grid(0, 0) \\\\
f(x, 0) &= f(x-1, 0) + grid(x, 0) \quad(x>0) \\\\
f(0, y) &= f(0, y-1) + grid(0, y) \quad(y>0) \\\\
f(x, y) &= \min(f(x-1, y), f(x, y-1)) + grid(x, y) \quad(x>0, y>0)
\end{align}
$$


Translated into python3 on leetcode:

```python
from functools import lru_cache
class Solution:
    def minPathSum(self, grid: List[List[int]]) -> int:
        self.grid = grid
        return self.f(len(grid)-1, len(grid[0])-1)
    @lru_cache()
    def f(self, x, y):
        if x == 0 and y == 0:
            return self.grid[0][0]
        elif y == 0:
            return self.f(x-1, 0) + self.grid[x][0]
        elif x == 0:
            return self.f(0, y-1) + self.grid[0][y]
        else:
            return min(self.f(x-1,y), self.f(x,y-1)) + self.grid[x][y]
```

Runtime 1052ms, memory 13.9M.
