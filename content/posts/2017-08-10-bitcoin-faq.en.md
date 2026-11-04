---
categories:
- life
date: 2017-08-10
lastmod: 2017-08-10
mathjax: true
slug: bitcoin-faq
tags:
- Bitcoin
- FAQ
title: Bitcoin FAQ
featured: true
---

This Bitcoin FAQ tries to give a simple introduction to Bitcoin in FAQ form. It draws mainly on the [Bitcoin whitepaper](https://bitcoin.org/bitcoin.pdf) and Princeton's textbook [*Blockchain: Technology-Driven Finance*](https://u.jd.com/C2NMOf), and inevitably contains a good deal of personal interpretation. Discussion welcome.

[First draft 2017-08-10 / minor update 2020-05-01]

## 1. What is Bitcoin?

Bitcoin is a digital currency. It does not depend on any central institution to issue it; it depends on the internet, and is issued on the basis of cryptography and distributed computing theory. Anyone can take part, its total supply is capped, and you can think of it as a kind of gold in the digital world.

## 2. What is Bitcoin good for?

The most important thing Bitcoin can buy today is other countries' currencies. As a digital currency, its original design intent was to partially replace fiat money, so in theory it can do anything money can do. In practice, buying things directly with Bitcoin is still at a very early experimental stage, supported by only a few merchants, the most famous being [Microsoft](https://support.microsoft.com/zh-cn/help/13942/microsoft-account-how-to-use-bitcoin-to-add-money-to-your-account). Personally I think three things block broad adoption. First, Bitcoin payment fees are currently too high, and the dispute over how to fix that even split Bitcoin into two forks: BCH, which backs big blocks, and BCC, which backs the Lightning Network. Second, Bitcoin's price is still far too volatile; more people treat it as an investment or a speculation. Third, because currencies compete, most governments are not keen on it.

Bitcoin is now described as digital gold, with the emphasis on its store-of-value role, but its payment value is the base layer of its value. If Bitcoin ultimately cannot be used for general transactions, its value is questionable.

## 3. A currency should be backed by state credit, and Bitcoin has none. Where does its credit come from?

A currency does not have to be backed by state credit — gold, for instance, still works as an internationally accepted money. A currency's credit comes from how many people believe it is money. State-issued paper money tells one story; Bitcoin, issued on cryptographic consensus, tells another. Humans can organize cooperation on a larger scale precisely because we have the capacity to believe in stories. (Recommended reading: [*Sapiens*](https://u.jd.com/oYTXl4).)

Bitcoin's source of credit really is hard to grasp. In a distributed way, it reaches consensus on the question of who owns how much, in a manner that no one participating in the system can deny. What you still need to understand is that any modern currency is a story, and the defining property of money is that the more people acknowledge its monetary value, the more monetary value it has — so yes, there is an element of faith in this.

## 4. So is Bitcoin a pyramid scheme, or a Ponzi scheme?

Bitcoin has one thing in common with pyramid and Ponzi schemes: both need a bit of faith. The difference is mainly that faith in Bitcoin actually makes this currency genuinely valuable — its value is existing as a currency, and nothing else. What pyramid and Ponzi schemes produce is more people getting taken in.

The Bitcoin community first gathered a bunch of geeks and cypherpunks who wanted to build a new monetary system; the starting point was absolutely not to swindle money. Of course, with the enormous speculative opportunity that hype around Bitcoin and blockchain has created, **the so-called coin circle is possibly where swindlers are densest**. My advice to everyone: don't invest in what you don't understand.

## 5. How exactly is Bitcoin issued?

Apart from the 50 Bitcoin in the genesis block, all Bitcoin is a reward for the right to keep the ledger, and comes into existence gradually as the Bitcoin network runs. Bitcoin needs to periodically confirm and record all unconfirmed transactions, and whoever wins that bookkeeping right receives a Bitcoin reward. These rewards are Bitcoin's original source. Each batch of recorded transactions is packed into a so-called block, and every block carries a pointer to the previous block — hence "blockchain."

## 6. How is "who owns how much Bitcoin" recorded? Is there an account like a bank account?

There is no concept of a bank account. The Bitcoin blockchain records only the creation of Bitcoin and every transfer since creation. When Bitcoin has been transferred to an address and not yet sent out, that address owns that Bitcoin.

## 7. What is an address?

An address can be understood as a kind of identity credential. It is public, like the number plate on your front door that everyone can see. But only you hold the key that opens the door. This uses signature algorithms from cryptography; broadly, you prove through the private key that this address (the public key) is under your control.

## 8. Does Bitcoin really consist of individual coins?

As said above, the Bitcoin blockchain is one big ledger, so there are no individual coins the way there are individual renminbi notes. There is only the fact, visible to everyone, that a given address holds a quantity of Bitcoin that has not been spent yet, and Bitcoin at that address can only be spent by someone holding the private key, after signing. Bitcoin is therefore in effect the private key, because whoever knows the private key can spend the Bitcoin.

## 9. How do you store Bitcoin?

First, as noted, storing Bitcoin primarily means storing the private key — that is the main function of a so-called Bitcoin wallet. Leak the private key and the Bitcoin is gone. Beyond that, how much a given address holds is determined by the public blockchain; anyone can connect to the Bitcoin network and verify it.

## 10. So who actually does the bookkeeping? Why should I trust the bookkeeper?

This is Bitcoin's most ingenious design. Who does the bookkeeping is not a settled matter: every node has to spend a long time computing (which burns electricity) to compete for that right. Having won it, if you record nonsense, the other nodes will not accept it and the block you produced is void. It still points to the previous block and forms a chain, but others can create a block with broader acceptance, producing a longer chain that voids your short one — you burned electricity and get no block reward. This ingenious design achieves trustworthiness by relying on the fact that human nature chases profit.

## 11. What are mining and mining machines?

As in the previous point, the work of competing for bookkeeping rights — that is, competing for the Bitcoin reward generated by bookkeeping — is called mining. Mining requires a hash computation that makes the resulting hash contain a certain number of zeros; that number grows as the total hashing power of the Bitcoin network grows, so that the block-packing speed, and hence the rate at which Bitcoin is created, stays roughly constant. The race for computing speed is therefore close to an arms race: from CPUs to GPUs, and now to machines built specifically for computing hashes.

The mining reward halves at intervals, so the rewards miners receive shrink steadily. But the Bitcoin network has another mechanism: every person making a transfer pays a small fee, as a reward to the miner who successfully packs the block.

## 12. How do I get Bitcoin?

Competing for bookkeeping rights — mining — is now highly professional and difficult, so you would have to buy specialized mining hardware and join a so-called mining pool to share hashing power and Bitcoin rewards.

The simplest way is still to find someone who holds Bitcoin and buy it with renminbi. As for how to trade: with regulation tightening in most countries, exchanges mostly no longer support direct fiat-to-Bitcoin trading the way stock exchanges work, only so-called over-the-counter platforms, where the platform provides escrow like Taobao — or no escrow at all, just listings — and the trade is C2C. My advice is to buy on a large, well-known platform that offers escrow; I won't recommend specific ones here.

## 13. Every block creates Bitcoin, so will there just be more and more of it?

No. Each block's reward halves at intervals, so it is a geometric series with ratio 1/2, totaling 21 million. Bitcoin is therefore designed to be deflationary.

## 14. A deflationary currency buys more and more goods over time, so in theory everyone will hoard Bitcoin instead of spending it. Does it still have monetary value?

That is a good question. My understanding is that at a certain point — once Bitcoin has the standing it deserves and its price stabilizes — holders will naturally spend it, just as people who own gold do today. And Bitcoin can form a monetary system together with inflationary currencies, just as gold and fiat money do today.

## 15. I hear Bitcoin is anonymous, so it is all used to buy drugs?

Bitcoin is a public ledger, but its addresses are strings of characters that cannot be tied directly to a person, so there is some anonymity. At the same time the ledger is public and its history is immutable and inspectable at any time; in that respect it is less anonymous than cash, because once a Bitcoin address is linked to a person, all of its history can be traced. In fact the Silk Road, which sold drugs for Bitcoin, was taken down by the FBI. Bitcoin is just a tool; it is not inherently friendly to crime.

## 16. I hear Bitcoin is used for money laundering?

As with the previous question, I do not think Bitcoin is inherently friendly to money laundering. The Chinese government, for instance, has begun supervising the risk of money laundering through Bitcoin on exchanges. I think Bitcoin should be used more for compliant, lawful applications.

## 17. Since Bitcoin is only a technology, issued by no organization, anyone can casually produce similar digital currencies. Does Bitcoin still have any special value?

You can indeed produce any number of similar digital currencies, and their technology can even be better. But two things matter. Bitcoin has a first-mover advantage, and the value of a digital currency grows with the number of participants; with Bitcoin already holding the high ground, other digital currencies find it hard to build an advantageous position from scratch. Second, Bitcoin itself can evolve through technical innovation.

## 18. What is the Bitcoin split about?

Bitcoin's rules and software are open source, so when someone disagrees with the current approach, they can start from a certain block and pack transactions (mine) under new rules, rejecting blocks mined under the old rules — and conversely the old rules no longer accept blocks mined under the new ones. From that block on, two chains each go their own way. Bitcoin that was unspent before the split block can be transferred onto both branches, so one old Bitcoin effectively becomes one Bitcoin on each of the two new chains.

## 19. Doesn't that split mean Bitcoin doubled?

Not exactly. After a split, the two versions diverge in value as participants vote with their feet, and from the standpoint of established fact, only the more valuable one counts as the authentic Bitcoin. Bitcoin's transfer fees are currently high, and the two proposals for solving that produced two camps: those backing an increase in block size forked off a digital currency called BCH, while the other, more complex protocol temporarily kept the name BTC.

## 20. What is the relationship between Bitcoin and blockchain?
Blockchain technology arose from the development of Bitcoin and has since spun off more technologies, but blockchain's application scenarios still need to be pinned down in earnest. The current boom is largely bubble, and personally I think digital currencies represented by Bitcoin are the application scenario blockchain has actually delivered. Many use cases have no need for blockchain at all, while digital currency very likely is necessary; I cannot go into that here — see Hayek's *Denationalisation of Money*.

## 21. How should I invest in Bitcoin?
For most people the only workable way is to buy Bitcoin with a small amount of money that does not affect your life at all, and hold it for 5 to 10 years. Bitcoin's price is still wildly volatile, so any attempt to chase rallies and dump dips will land you in a gambler's position. **With any investment, always remember: don't invest in what you don't understand.**
