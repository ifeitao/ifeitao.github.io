---
categories:
- coding
date: 2019-04-23
lastmod: 2019-04-23
mathjax: true
slug: frog-and-cache
tag:
- アルゴリズム
- python
tags:
- アルゴリズム
- 動的計画法
title: 蛙とキャッシュ：実用的に簡略化した動的計画法
featured: true
toc: true
---

## 1. 一匹の蛙から

![蛙](https://i.imgur.com/zuhczaLm.jpg)

ある蛙が、`n`段の階段を跳び下りて池に入ろうとしている。1回で1段あるいは2段だけ跳べるとすると、池に降りる跳び方は全部で何通りあるだろうか（たとえば`n=30`のとき）。

数学の言葉で言えば、蛙の跳び方の関数`f(n)`を求めることになる。非負整数を引数にとる関数なので、小さい場合から考えればよく、`f(1)=1, f(2)=2`はすぐに導ける。問題は、その先の虜挙がどんどん面倒になることである。

自分がその蛙だと考えてみよう。`n`段の階段を前にして、1回目に1段跳べば残りは`n-1`段で、`f(n-1)`通りの跳び方がある。1回目に2段跳ぶこともでき、その場合は残りが`n-2`段で`f(n-2)`通りである。したがってこの問題の答えは見慣れたあれ、不思議なフィボナッチ数列になる：


$$
\begin{aligned} F_{0} &=0 \\ F_{1} &=1 \\ F_{n} &=F_{n-1}+F_{n-2} \quad(\mathrm{n} \geq 2) \end{aligned}
$$


この種の関数値の問題を解く第一歩は、漸化式を見つけることである。その漸化式をpythonのコードに翻訳する：

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

実行時間は`284ms`で、かなり遅い。なぜ遅いのか。同じ計算の繰り返しがあまりに多いからである。`f(5)`の計算を例にとると、呼び出し関係は次のようになる：

```
f(5)==>f(4), f(3)
f(4)==>f(3), f(2), f(3)==>f(2), f(1)
f(3)==>f(2), f(1), f(2)==>f(1), f(0), f(2)==>f(1), f(0), f(1)
f(2)==>f(1), f(0), f(1), f(1), f(0), f(1), f(0), f(1)
f(1), f(0), f(1), f(1), f(0), f(1), f(0), f(1)
```

そこで自然な発想は、中間の計算結果をすべてキャッシュしておくことである。幸いなことに、pythonにはこの「電池」が標準で備わっている。

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

速すぎて時間が計測できなかった。pythonにおける`lru_cache`の基本原理は辞書を構築することで、辞書の`key`が呼び出しの引数、`value`がその引数に対する計算結果である。おおよそ次のコードと等価である：

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

もちろん、この問題に限れば、より細かいキャッシュの方法を使うこともできるし、再帰をやめてループに書き換えることもできる（キャッシュを2つだけ保持するのに等しく、空間の使用量を大幅に減らせる。ただし、さまざまな`n`の値を繰り返し計算するのであれば、むしろ前の方法のほうが適しているかもしれない）：

```python
def fib(n):
    a, b = 0, 1
    for i in range(n):
        a, b = b, a+b
    return a
```

この問題は [leetcode 70](https://leetcode-cn.com/problems/climbing-stairs) と等しい。leetcode上でのpython3の解答は次のとおりである：

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

実行時間52 ms、メモリ消費13.2MB。

## 2. 実用的に簡略化した動的計画法

この蛙から比較的汎用な示唆を取り出し、漸化式を構成できる同種の問題を解こう：

1. 漸化式を見つけて再帰関数を立て、問題を複数の部分問題の求解へ帰着させる。
2. 同じ部分問題を繰り返し計算しないよう、キャッシュを用い、空間と引き換えに時間を得る。

一般のアルゴリズム教科書や面接問題の解説では、このキャッシュ構造の設計にかなりの時間を割いている。実際のエンジニアリングの問題では、キャッシュ空間を多少多く使うことにそれほど敏感でないことも多く、したがって再帰関数を書き、汎用的なキャッシュの仕組みを加えるだけでほぼ解決する。キャッシュ空間が問題になって初めて、問題に適したより小さなキャッシュを検討すればよい。

この方法を検証するため、さらにいくつかの問題を見てみよう。leetcodeから直接いくつか拾って解く。

### 2.1 [最大部分配列和](https://leetcode-cn.com/problems/maximum-subarray/)

整数配列`nums`が与えられたとき、和が最大となる連続部分配列（少なくとも1つの要素を含む）を見つけ、その最大和を返す。

**例:**

> 入力: [-2,1,-3,4,-1,2,1,-5,4],
> 出力: 6
> 説明: 連続部分配列 [4,-1,2,1] の和が最大で、6 である。

配列の各位置で終わる部分配列について得られる最大和の漸化式を考える。
$$
\begin{aligned}  f(0)&=nums(0) \\ f(k)&=max(f(k-1), 0)+nums(k) \quad(k>0) \end{aligned}
$$
これに基づけば、最終的な結果が次となることは容易に分かる。
$$
ans = max_{i=0}^n(f(i))
$$
leetcode上でpython3のコードに翻訳すると次のとおりである：

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

実行時間76 ms、メモリ消費13.7 MB。

### 2.2 [最小経路和](https://leetcode-cn.com/problems/minimum-path-sum/)

非負整数を含む *m* x *n* のグリッドが与えられたとき、左上から右下への経路であって、経路上の数値の総和が最小となるものを見つけよ。

**例:**

> 入力:
> [
>   [1,3,1],
>   [1,5,1],
>   [4,2,1]
> ]
> 出力: 7
> 説明: 経路 1→3→1→1→1 の総和が最小だからである。


行列の各位置を右下角としたときの最小経路和を求めると、次の漸化式が容易に得られる：

$$
\begin{align}
f(0, 0) &= grid(0, 0) \\\\
f(x, 0) &= f(x-1, 0) + grid(x, 0) \quad(x>0) \\\\
f(0, y) &= f(0, y-1) + grid(0, y) \quad(y>0) \\\\
f(x, y) &= \min(f(x-1, y), f(x, y-1)) + grid(x, y) \quad(x>0, y>0)
\end{align}
$$


leetcode上でpython3のコードに翻訳すると次のとおりである：

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

実行時間1052ms、メモリ消費13.9M。
