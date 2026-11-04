---
categories:
- coding
date: 2016-12-24
lastmod: 2016-12-24 22:19:17 +0800
slug: debug-is-technology
tags:
- Programming
- Debugging
- Reading notes
title: 'Debugging Rules!: Debugging Is a Technical Skill'
featured: true
---

Usually, when an engineer calls something an art, or even mysticism, it means the thing is hard and there aren't many rules to follow. Debugging is one of those. Practically every programmer has been flogged half to death by a bug; sometimes you turn it over and over and the problem seems gone, but you don't know why, so you file it under inexplicable mysticism. The most infuriating kind is the bug that shows up now and then and is hard to reproduce — the technical name is Heisenberg bug.

But software is still within the realm of science and technology, and debugging ought to be a technical skill too. *Debugging Rules!* is a rare book that talks about debugging as technique. Its nine general principles apply not only to developing and maintaining software and hardware, but even to daily life. Finding this book took some effort; luckily Turing Community still sells the [legitimate e-book](http://www.ituring.com.cn/book/84).

Honestly, many of the author's examples lean toward hardware, so there's a gap when reading them, but the nine principles are genuinely practical. In my earlier development and debugging work I probably summed up a few of them without realizing it, yet after reading the book it still felt like being handed a martial arts manual. Now let me walk through the nine principles again to deepen my understanding.

## 1 Understand the system

This is the most important principle. To analyze a bug you obviously have to understand how the system works, which means learning some fundamentals and carefully reading the documentation for the specific libraries, tools and technologies involved. I only got into the habit of seriously reading official documentation in the last few years. Search engines made us Google-oriented programmers: facing a problem we want it solved in one shot, and the result is usually a pile of detours, all because we begrudge the time to read the signposts. The book particularly insists on reading the manual "word for word" — a blunt blow to the impatient. Starting to debug without understanding the system is the same lineage as writing code without understanding the principles; the common name for it is "programming by coincidence".

## 2 Make it fail 

This principle is about why and how to reproduce a bug. A bug definitely happens under some particular condition; peel it apart layer by layer until you find that condition and you're halfway there. From my hardware maintenance experience: it helps enormously if the person who found the bug records the whole process in detail. Many bugs need fairly narrow conditions to appear, hence one of a programmer's stock phrases, "works on my machine". For this kind of bug, first try to find a way to simulate it, for instance speeding up the interaction and running stress tests; second, have a detailed and sensible logging mechanism inside the software, so the reproducing conditions can be found from the inside.

## 3 Don't think, look 

This one stresses the importance of observation: reality beats idle speculation. Language shapes thinking, so the phrase on hitting a bug should be "let me look" rather than "I guess it's because". We should try every means to see the details of the bug clearly, so a mature program should carry debugging infrastructure; in my experience, logging at minimum is indispensable. Junior programmers tend to debug entirely with breakpoints, except a breakpoint itself changes the flow of execution (especially with multiple threads). Guessing is still useful, of course: it narrows the range of observation, or at least sets a priority for what to look at first, which is where experience pays off. But no matter what, experience cannot replace observation.

## 4 Divide and conquer 

Binary search turns lookup from linear time into logarithmic time. It isn't only an algorithm inside programs, it's a methodology for debugging. Once a system has this awareness, the key question is how to divide the system — back to principle 1. At the very least, when you debug with breakpoints, bisection can locate the bug, and the same principle applies when inserting log statements. The book also mentions bugs influencing each other; I'd say there's even a bug seesaw. The way out is to let none of them go. When debugging reveals that the code quality is really bad, refactoring is sometimes necessary — you can't build a tower on loose sand — and after an effective refactor the bug often turns up and gets removed on its own.

## 5 Change one thing at a time 

This is like the control principle in experimental science: examine one variable at a time, compare the normal case against the abnormal case, and never ignore any difference in test conditions. The previous principle says let no bug go, but they still have to be handled one by one, and when refactoring don't hack away at code you don't understand. Much code is dangerous because one pull of a hair moves the whole body; I think that's the biggest risk in fixing bugs — you often remove one bug and add several. Back to principle 1: understand the system. Although understanding other people's code is easier said than done, which is a reminder to build up good karma when writing code: don't imagine code is written for the compiler, it's written for whoever maintains it later.

## 6 Keep an audit trail 

This principle is about why and how to keep records. I think of it as a doctor taking a history: you need to ask the right questions and get concrete, useful answers. My own experience is that once I start debugging a bug I sink in completely and can't get out; writing things down pulls me out of the mental swamp and lets me keep correcting my plan and method for debugging. With some specialized system software you need to train the users in how to record bug occurrences in effective language; without records, the person debugging has to ask the right questions to jog the user's memory. Beyond that, a bug you can't crack at midnight deserves a night's sleep, letting divergent thinking work on its own; usually it's solved by morning.

## 7 Check the plug 

This principle is roughly about so-called "stupid mistakes" — like my mother telling me the computer speakers have gone silent, and my first question having to be whether the power is on. Or writing main as mian. Once I set a breakpoint and it just wouldn't hit; later I found that two blocks of code looked much alike and I had set the breakpoint in the wrong place. Depending on the scenario and your experience, ask yourself whether you've made the mistake that is common in this scenario; that often solves a pile of problems on the spot, just as the troubleshooting FAQ in many appliance manuals also tells you to check the plug. You could say a stupid mistake is stupid in difficulty, not in frequency.

## 8 Get a fresh view 

This principle is about asking for help and talking things over. The important part is using another person's viewpoint to break your own mental set, so it's best to describe only the symptoms in detail and not your guesses, lest you contaminate their judgment. For a programmer, Google-oriented programming is astonishingly powerful at this point: nine out of ten problems don't need you to actually ask anyone, just the right search terms. For Chinese programmers, searching in English is a required skill, and of course really understanding what you find matters too — don't swallow every pill you see. If Google genuinely can't find it, that proves you've climbed a level; then go ask on communities like Stack Overflow.

## 9 If you didn't fix it, it ain't fixed 

This principle says don't count on luck, and don't play ostrich just because the bug only flashed by once. What has to come will come; the bill isn't cancelled, only deferred. Real situations can be complicated, of course — software engineering is a compromise among time, cost and quality — but even when you let some bugs go, work out the consequences that may follow and put adequate safeguards in place, which is why many software certification schemes include software safety integrity levels. This also touches on reproducing the bug and generalizing the fix: confirm that you have really found the cause, provide an effective fix, and sweep for all similar problems. Fix one memory leak and you have to fix every piece of code that causes that kind of leak.

## Postscript: how to write code that is easy to debug

Seen from the other side, the principles of debugging help with building software itself. Debugging only patches holes, after all; better to write code with fewer bugs and leave yourself more handles for when you do debug. A brief summary of my own experience, which probably needs continual refinement:

1. The program should provide a logging mechanism, emitting debug information in the debug build, and even in release recording the details of what went wrong (an exception thrown in C#, say);
2. Write code fit for humans to read, otherwise whoever maintains it later can't understand it, let alone debug it. *Code Complete* says the most about how; besides the various idiomatic ways of writing, I think putting yourself in the reader's shoes matters a lot;
3. When using libraries or tools, try to understand the principles and read the official documentation carefully. Some libraries explain in detail how to avoid memory leaks and how to handle multithreading; read it clearly before you use it and you plant fewer seeds of disaster — at least you won't be a headless fly guessing at causes when the debugging comes;
4. Write code that is easy to test, so that problems can be isolated during debugging, or bisected. TDD practice covers this fairly well; I need to work on it myself.
