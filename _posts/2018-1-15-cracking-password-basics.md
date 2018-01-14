---
layout: post
title: Cracking Password Basics
date: 2018-1-15
---

Whelp, it's about 1.30 on a Sunday night, and I can't sleep - too wide awake, too busy thinking about everything I did today! So hopefully, by letting it out it'll be a bit easy to get some rest.

Today, I learned about one way you can crack a password given a hash. The one I will describe today is by using the DES-based crypt function, which is available on most Linux systems. This is just one of many, and passwords now generally have better encryption methods (thank goodness), but I thought it was cool! Here's the breakdown.

It's very bad practice to store passwords in plain text. If some baddy were to snoop around your PC when you weren't watching, they could quite easily see your passwords and do some real damage in your name! Naturally, we don't want this to happen.

To avoid this, passwords are encrypted. The combination of numbers and letters that make up the password undergo a series of mathematical operations such that it's obfuscated, but easy to reverse, if you know what operations were done to it in the first place. It's supposed to make it really hard to guess what the original password was. The set of maths operations on the original text so that it's easy to reverse in this case is called a "one-way hash".

Sometimes, some extra data is used in the hash to help avoid certain kinds of attacks by people. This is called a "[salt](https://en.wikipedia.org/wiki/Salt_(cryptography))".

If you have a linux operating system, passwords for users can be stored in ```/etc/shadow```. If you look in here, you'll see some long weird numbers like "50JIIyhDORqMU" - that's the hash we're talking about! If we know this hash was the result of a password passed to the basic DES function, we could start deducing some information about it. For example, we know that the first two characters, "50", are the salt that's used to encrypt it.

If we have a hunch that the password that was encrypted was 5 characters long or less, then we can probably use our super fast computers to try all the different combinations of letters and numbers. This would normally take a human a really long time to do this, but computers can do this in minutes, usually less!

Ok cool, so we know that we can probably brute force the password, we know the salt, and we know what the resulting hash is. So what do we do now? We use the same hash function used to generate the password, and then feed all the combinations of characters in the password! 

You start off going through "A", "B" ... 

Continue continuing through "ABcd", "ABCe" ... 

Finally, you finish at "zzzzz". 

Along the way, if we'd stumbled across a combination that happens to result in the same hash function, then that's the right combination to match the password! Successfully cracked.

In this case, the right library to use is crypt, which is available on pretty much most linux operating systems. Luckily, an extended version of crypt is now used, which makes cracking passwords much harder.