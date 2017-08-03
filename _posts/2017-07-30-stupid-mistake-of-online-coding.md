---
layout: post
title: 在线编程（刷题）的低级错误
categories: coding
mathjax: true
---

最近几天在一些OJ网站上刷了不少算法题，都是直接在网页上写代码，脑中调试，然后提交，发现提交通不过大概有以下几种情况：

1. 算法设计出现根本性错误，一般是对题意有误解，或重要的分支情况未考虑到；
2. 算法设计基本正确，但是有一些边界情况未考虑到；
3. 时间复杂度太高；
4. 低级错误。

以上的1、2、3属于算法的基本功，无论你是在线刷题，还是用IDE刷题，都避免不了，但是对于低级错误，IDE的编辑器静态分析就能发现一批，编译时又能发现一批，似乎也不是什么问题。

问题在于，技能的反面就是解决问题，解决一些低级错误是会浪费时间的，而且，有一些低级错误会躲过编译器，造成更大的危害，因此很有必要尽量减少这些低级错误。在线刷题时，我自己常见的低级错误（主要是java语言的）：

1. 没有写分号，或者写了中文分号；
2. 括号未匹配；
3. 未记住一些API的名称，比如HashMap中的containsKey而不是contains；
4. 拼写错误，导致API调用错误，甚至标识符前后不一致；
5. 更改了某个标识符，但是没有更改完全；
6. 忘记写返回语句，或者某些支路忘记写返回语句，甚至返回了错误的变量或变量类型；
7. 重复声明变量，比如循环内外各申明一次；
8. 想要在循环外使用循环变量，但没有在外面声明；

暂时这些，以后不断补充。

如何改善？我发现我这么多年来都犯了一个错误，因为自己粗心，又觉得不可能不犯错误，就放弃了改善的机会，有些放任自流，从认识上就需要提高。以下是一些观点和方法，希望慢慢能标本兼治：

1. 人都会犯错误，甚至犯低级错误，即所谓的粗心，粗心不能根除，但是可以改善；
2. 意识到自己的低级错误并改善，而不要视而不见，放任自流；
3. 适当放慢速度，萝卜快了不洗泥；
4. 第一遍写的时候随时自我复查，要习惯脑子里有一个角色在复查，争取一次写对；
5. 写完复查一遍。
6. 及时总结自己犯了哪些低级错误。

这里谈的都是低级错误，还每涉及到如果提高程序的正确性，这一点以后再总结。