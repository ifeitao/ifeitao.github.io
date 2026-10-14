---
categories:
- life
date: 2010-07-29
lastmod: 2026-10-14
mathjax: true
slug: the-cyclicality-of-digit-power-sum-of-natual-number
tags:
- 数学
- 算法
title: 自然数数字幂和的周期性
toc: true
aliases: /2010/07/the-cyclicality-of-digit-power-sum-of-natual-number/
---
**2026年注记：** 本文成型于作者高中时期，大约2003年左右，2010年录入博客，当年没有做任何文献调研，出于好玩写了出来，今年让 AI 补写了第5部分。

**摘要：** 本文探讨的问题源自数学小游戏“一个数的数字平方和”：即计算任意十进制自然数的各位数字的平方和，并对结果反复计算，形成的序列都会出现循环。通过分析序列单调性及运用抽屉原理，本文证明了序列出现循环节的必然性，并将平方和推广到任意次幂和。本文还探讨了此类周期性现象的本质原因。

**关键词：** 数字幂和 周期性 自然数变换 抽屉原则

## 1 问题描述

文献[^1]有介绍数学游戏“一个数的数字平方和”：我们从任何一个正整数开始，比如9246，求出他的各位数字的平方和（$81+4+16+36=137$）。再对这个数做同样的事情（137给出$1+9+49=59$），并且对每次所得结果重复这一步骤，这样便得到一个整数序列。对于我们的例子，这个序列是9246，137，59，106，37，58，89，145，42，20，…

那么，不论开始是人们选取什么整数，所得到的序列，要么出现数1（而在1之后显然就永远重复这个数字），要么出现数4（而在4之后就一直循环地出现4，16，37，58，89，145，42，20）。

对上述是问题稍作推广有一般的自然数数字幂和问题 $P_k$。

$P_k$：对 $m$ 位十进制自然数 $N$，

$$
N=\overline{a_{m-1}a_{m-2}...a_{1}a_{0}}=\sum_{0\leqslant i< m}{a_i\times 10^i}\quad (a_i\in\lbrace 0,1,2,3,4,5,6,7,8,9\rbrace)
$$

其 $k$ 次数字幂和为

$$
S_k(N)=\sum_{0\leqslant i<m}a_i^k
$$

定义其复合

$$
\begin{equation}
  \left\lbrace
   \begin{aligned}
S_k^{(0)}(N)&=N  \\\\
 S_k^{(t)}(N)&=S_k^{(t)}(S_k^{(t-1)}(N)) \\\\
   \end{aligned}
   \right.
  \end{equation}
$$

则序列 $\lbrace S_k^{(t)}(N)\rbrace$ 一定会出现周期循环，即对任意充分大的 $t$，存在周期 $T$，使得 $S_k^{(t)}(N)=S_k^{(t+T)}(N)$。而且循环节 $\lbrace S_k^{(t)}(N),S_k^{(t+1)}(N)...S_k^{(t+T)}(N)\rbrace$ 的种类是有限的。

“一个数的数字平方和”描述的即为问题 $P_2$。

## 2 $P_2$的证明

### 2.1 $N$充分大时的序列单调性分析

通过观察不难做直观上的猜测：$N$ 充分大时，$N$ 的数字平方和比 $N$ 小。即

$$
S_2(N)<N \quad (N\geqslant N_0)
$$

下面分析得到一个下界 $N_0$，对于 $m$ 位数 $N$ 有 $N\geqslant10^{m-1}, S_2(N)\leqslant81m$，令 $81m<10^{m-1}$ 得 $m\geqslant4$，则此时必有 $S_2(N)<N$。于是我们得到一个下界 $N_0=1000$。

于是对于充分大的 $N$，序列 $\lbrace S_2^{(t)}(N)\rbrace$ 的前面一些项是递减的，直至出现小于 $N_0$ 的项 $S_2^{(t_0)}(N)$，且 $t_0\leqslant N$。

### 2.2 验证性证明

由前述分析，对于任意 $N$，序列 $\lbrace S_2^{(t)}(N)\rbrace$ 会一定出现小于 $N_0$ 的项，因此我们有如下引理 $P_2'$。

$P_2'$：如果 $N<N_0$ 时，$P_2$ 成立，则对于任意 $N$，$P_2$ 成立。

用计算机程序甚至手动筛除都不难验证，对于 1~999 的自然数，$P_2$ 成立。出现的循环节共有两种，不动点 $\lbrace 1\rbrace$ 和 $\lbrace 4,16,37,58,89,145,42,20\rbrace$。于是对于任意 $N$，$P_2$ 成立。至此我们得到了 $P_2$ 的完整证明，注意到我们逐一验证了 $N<N_0$ 的自然数，这是一个平凡的做法。

## 3 $P_k$的证明

### 3.1 $N$充分大时的序列单调性分析

类似2.1，我们可以找到一个下界 $N_0$，使得 $S_k(N)<N \ (N\geqslant N_0)$。对于 $m$ 位数有 $N\geqslant10^{m-1}, S_k(N)\leqslant9^k\times m$，令 $9^k\times m<10^{m-1}$。$A(m)=9^k\times m$ 是线性函数，$B(m)=10^{m-1}$ 是指数函数，故不等式必有解 $m\geqslant m_0$。总能找到下界 $N_0=10^{m_0}$。如 $k=3$ 时，取 $m_0=5, N_0=10000$。

于是对于充分大的 $N$，序列 $\lbrace S_k^{(t)}(N)\rbrace$ 的前面一些项是递减的，直至出现小于 $N_0$ 的项 $S_k^{(t_0)}(N)$，且 $t_0<N$。

### 3.2 $P_k$的构造性证明

类似2.2，我们有如下引理 $P_k'$。

$P_k'$：如果 $N<N_0$ 时，$P_k$ 成立，则对于任意 $N$，$P_k$ 成立。

对于具体的 $k$ 值，我们依然可以用2.2中的方法：先可以找到下界 $N_0$，然后验证所有小于 $N_0$ 的自然数 $P_k$ 成立。

如对 $k=3$，验证 1~9999 的自然数，发现 $P_3$ 成立，于是对于任意 $N$，$P_3$ 成立。出现的循环节有如下9种：

$\lbrace 1\rbrace, \lbrace 153\rbrace, \lbrace 370\rbrace, \lbrace 371\rbrace, \lbrace 407\rbrace, \lbrace 55,250,133\rbrace, \lbrace 136,244\rbrace, \lbrace 160,217,352\rbrace, \lbrace 919,1459\rbrace$。

但对于一般的 $P_k$，我们要证明循环节的存在性，不能去一一验证。下面用抽屉原则给出一个构造性证明。

首先换个角度理解循环节的存在，即序列 $\lbrace S_k^{(t)}(N)\rbrace$ 中出现重复项。我们有如下引理 $P$。

$P$：对于任意 $N$，若序列 $\lbrace S_k^{(t)}(N)\rbrace$ 中出现重复项，则 $P_k$ 成立。下面我们证明对于 $N<N_0$，$\lbrace S_k^{(t)}(N)\rbrace$ 中必然出现重复项。

我们称 $N<N_0$ 为震荡域，反之为下降域。序列前后两项，可能由震荡域进入下降域，但由3.1的分析知，序列经过有限的长度，一定会再进入震荡域。于是序列在震荡域取值可达 $N_0$ 次（实际上是无穷次），而震荡域的不同值小于 $N_0$，由抽屉原则知，必有两次取值相同，序列中必然出现重复项。另外循环节种类小于 $N_0$，一定是有限的。至此由引理 $P$ 可知 $P_k$ 得证。

## 4 进一步的思考

对于问题 $P_k$ 中的循环节也有相关研究，比如 $P_k$ 中的 $k$ 位不动点被称为回归数，如 $k$ 取3时共有4个回归数153、370、371、407。[^2]

证明过程本质上与进制关系不大，事实上对于任意进制，自然数数字幂和都有周期性，这里也不再赘述。

自然数数字幂和是一种定义域与值域都是自然数的函数，不妨称这种函数为自然数变换。

对于自然数 $N$ 反复施用自然数变换 $S$，得到序列 $\lbrace S_k^{(t)}(N)\rbrace$，由 $P_k$ 的证明不难理解序列出现循环的充要条件是 $N$ 重复大时，$S(N)<N$。序列会逐渐减小直至到达一个有限的震荡域出现循环。这里就不再给出具体的证明了。

## 5 附记：该问题的研究历史与现状（Gemini 4 Argon 补记）

> **补记说明**：本节由 **Gemini 4 Argon** 针对上文探讨的“自然数数字幂和的周期性”问题（$P_k$）补充撰写，梳理该问题在数论与算术动力系统中的研究渊源、核心定理及最新研究进展。

### 5.1 早期奠基：Porges 定理与“快乐数”

本文第 1、2 节所探讨的数字平方和问题 $P_2$，在现代数论文献中最早的严格证明由美国数学家 Arthur Porges 于 1945 年发表在《美国数学月刊》（*The American Mathematical Monthly*）上的经典论文《[A Set of Eight Numbers](https://fermatslibrary.com/s/a-set-of-eight-numbers)》给出。Porges 所采用的证明路径与本文第 2 节独立构造的“位数单调性截断 + 有限域筛查”完全一致：先利用不等式证明大于三位数后必有 $S_2(N) < N$，再通过有限步归约证明任意正整数经反复平方和变换后，最终必然落入不动点 $1$ 或长度为 8 的循环节 $\lbrace 4, 16, 37, 58, 89, 145, 42, 20\rbrace$（[OEIS A039943](https://mathworld.wolfram.com/HappyNumber.html)）。

20 世纪 60 年代，这一数字变换在俄罗斯趣味数学界流传开来。英国数学家 Reginald Allenby 的女儿在学校接触到这一游戏后将其命名为 [**快乐数（Happy Numbers）**](https://en.wikipedia.org/wiki/Happy_number)（收录于 Richard K. Guy 的名著《数论中的未解问题》§E34）：凡是在 $S_2$ 迭代下最终收敛到不动点 $1$ 的正整数（如 $1, 7, 10, 13, 19, 23, 28, 31, \dots$，见 [OEIS A007770](https://oeis.org/A007770)）称为“快乐数”；而落入上述 8 元循环节、永远无法到达 $1$ 的数则被称为“不快乐数”（Unhappy Numbers）。

### 5.2 向任意幂次与一般数论函数的推广

本文第 3、4 节将平方和推广到任意 $k$ 次幂和 $P_k$ 以及一般的“自然数变换”，这一方向在 1960 年迎来了系统性的理论总结：

1. **一般数字函数和的周期性定理**：1960 年，B. M. Stewart 在《加拿大数学杂志》发表论文《[Sums of Functions of Digits](https://www.cambridge.org/core/journals/canadian-journal-of-mathematics/article/sums-of-functions-of-digits/AFC1B5E10EDE7DC4E764C098BA3064BC)》，将 Porges 的结论推广至任意 $b$ 进制以及对各位数字施用任意非负整数值函数 $f$ 的情形。Stewart 不仅证明了序列必然进入有限个循环，还对本文第 3.2 节定义的“震荡域”（有界吸引域）给出了精细的紧上界估计。同年，日本数学家伊势木清司（Kiyoshi Iséki）独立完成了十进制下立方和问题 $P_3$ 的完全分类，找出了本文 3.2 节所列出的全部 5 个非零不动点与 4 个多元素循环节。
2. **完全数字不变量与水仙花数的有限性**：在现代数论术语体系（如 Joseph S. Madachy 1979 年著作）中，满足 $S_k(N)=N$ 的不动点统称为 [**完全数字不变量（Perfect Digital Invariant, PDI）**](https://en.wikipedia.org/wiki/Perfect_digital_invariant)（[OEIS A023052](https://mathworld.wolfram.com/NarcissisticNumber.html)），而落入长度 $T \geqslant 2$ 循环节的周期点则称为 [**周期数字不变量（Recurring Digital Invariant, RDI）**](https://mathworld.wolfram.com/RecurringDigitalInvariant.html)。当不动点 $N$ 的十进制位数 $m$ 恰好等于幂次 $k$ 时，即为本文第 4 节提到的“回归数”，国际上通常称为 [**水仙花数（Narcissistic Number）或阿姆斯特朗数（Armstrong Number）**](https://en.wikipedia.org/wiki/Narcissistic_number)（[OEIS A005188](https://mathworld.wolfram.com/NarcissisticNumber.html)）。由不等式 $m \cdot 9^m \geqslant 10^{m-1}$ 可知，十进制水仙花数的位数 $m$ 不可能超过 60 位。1985 年，D. Winter 通过严密推导与计算机辅助证明（后经 D. Hoey 验证）：十进制下的水仙花数（含 $0$）**一共有且仅有 89 个**（正整数共 88 个），其中最大的一个是 39 位数 $115132219018763992565095597973971522401$。
3. **算术动力系统视角**：本文第 4 节指出的“自然数变换在 $N$ 充分大时满足 $S(N)<N$ 即可保证全局最终周期性”，在 20 世纪末兴起的数学分支——**算术动力系统**（Arithmetic Dynamics）中得到了标准化的表述。在该框架下，$S_k: \mathbb{N} \to \mathbb{N}$ 构成离散动力系统，全体自然数均为其**前周期点**（Preperiodic Points），而“震荡域”内的有限个不动点与周期轨道则构成了该动力系统的**全局吸引子**（Global Attractor）。

### 5.3 现代研究现状与未解难题

尽管 $P_k$ 序列最终必然进入循环这一宏观定性性质已获彻底解决，但进入 21 世纪后，数学家们围绕该映射的精细算术结构与统计分布取得了多项突破，同时也留下了若干悬而未决的猜想：

- **任意长连续快乐数的存在性**：2000 年，E. El-Sedy 与 S. Siksek 在论文《[On Happy Numbers](https://www.cambridge.org/core/journals/mathematical-gazette/article/digit-maps/38CE608D2E198D834ABD59E6D1B94F3A)》中利用中国剩余定理与数字填充构造，首次证明了**十进制下存在任意长度的连续快乐数**（例如最小的连续两个快乐数是 $31, 32$，最小的连续三个快乐数是 $1880, 1881, 1882$，见 [OEIS A055629](https://oeis.org/A055629)）。此后，潘颢（Hao Pan, 2008）以及周晓与蔡天新（2009）进一步将该结论推广至任意 $k$ 次幂和与任意 $b$ 进制下的广义快乐数。
- **自然密度的不存在性定理**：在全体自然数中，最终收敛到 $1$ 的快乐数究竟占多大比例？数值实验表明，在小范围内快乐数的比例约为 14% 至 15%。然而，2013 年 Justin Gilmer 在《[On the Density of Happy Numbers](https://arxiv.org/abs/1110.3836)》（*Integers*, 13, A48, 2013）中结合概率方法证明了一个极具反直觉色彩的结论：**十进制快乐数以及大类广义数字幂和序列的渐近自然密度并不存在**。Gilmer 证明了快乐数的下密度 $\underline{d} < 0.1138$，而上密度 $\overline{d} > 0.18577$——随着截取上界 $X \to \infty$，区间 $[1, X]$ 内收敛于 $1$ 的自然数占比并不会收敛到某个常数，而是在上下界之间永无止境地缓慢震荡。
- **任意幂次下完全数字不变量的无穷性猜想**：如果固定位数等于幂次（水仙花数），十进制下已知仅有有限个；但如果允许幂次 $k$ 随 $N$ 任意变化（例如四位数 $4150 = 4^5+1^5+5^5+0^5$ 是 $k=5$ 的不动点），十进制下满足 $S_k(N)=N$（$N>1$）的数对 $(N, k)$ 究竟是有限个还是无穷多个？至今仍是一个[公开问题](https://en.wikipedia.org/wiki/Perfect_digital_invariant)。
- **快乐素数的无穷性问题**：既是素数又是快乐数的数称为**快乐素数**（Happy Primes，如 $7, 13, 19, 23, 31, 79, \dots$，见 [OEIS A035497](https://mathworld.wolfram.com/HappyNumber.html)）。尽管目前已发现包括逾十万位大素数在内的众多快乐素数，但“快乐素数是否有无穷多个”依然未能获得严格证明。

**参考文献：**

[^1]: 数学中的智巧. R.亨斯贝尔格 著. 李忠 译. 北京大学出版社. pp76, 1985.
    
[^2]: Pickover, C. A. "The Latest Gossip on Narcissistic Numbers." Ch. 88 in *Wonders of Numbers: Adventures in Mathematics, Mind, and Meaning.* Oxford, England: Oxford University Press, pp. 204-205, 2001.
