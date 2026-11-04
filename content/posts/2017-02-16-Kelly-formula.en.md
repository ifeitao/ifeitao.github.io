---
categories:
- life
date: 2017-02-16
lastmod: 2017-02-16
mathjax: true
slug: Kelly-formula
tags:
- Investing
- Mathematics
title: The Kelly Criterion
featured: true
---

Suppose you take 10,000 yuan to a gambling table where you may stake any amount. Win and your stake is doubled; lose and it is gone. Assume a 60% chance of winning. How much should you stake each time to earn the most?

A fool shoves the whole roll in at once — the odds favor winning, after all. But there is still a 40% chance of being wiped out in a single bet.

Suppose instead we stake a fixed fraction of the capital remaining each time. What fraction is right? Say we play 100 times, winning roughly 60 and losing 40; let the fraction be $x$. Then the profit is

$f(x)=10000*(1+x)^{60} *(1-x)^{40}$

and we need its maximum.

More generally, suppose each unit staked can earn an additional W or lose the principal L, with probability of winning p and of losing q. Then the expected return is

$$f(x)=(1+Wx)^{p} (1-Lx)^{q} $$

To find its maximum, differentiate first.

$$f^{'}(x)=Wp(1+Wx)^{p-1} (1-Lx)^{q} -L(1-p)(1+Wx)^{p} (1-Lx)^{q-1}=0$$

It is not hard to obtain

$$x=\frac {bp-q} {bL}$$

When L=1 — a loss takes everything — this is called the Kelly criterion. For the question at the start of this post, p=0.6, q=0.4, b=1, which gives x=20%. So you should stake 20% of your current capital each time. At a 90% win rate, x=0.8. At a 50% win rate, x=0 — never take an even-money bet; with less than 50%, all the less.

The Kelly criterion is only an approximation, and it rests on many assumptions: that you can play many times, that capital is infinitely divisible, that the win rate holds steady. Investment differs from it in many ways. Still, it gives us a rough estimating tool, and from the formula's point of view it is clearly necessary to keep some cash in reserve to come back from a drawdown. Probability arithmetic is essential in investment. Even though estimating the probability of profit in investing is itself something of a dark art, as Graham said, we cannot abandon quantitative calculation merely because quantitative calculation is difficult.
