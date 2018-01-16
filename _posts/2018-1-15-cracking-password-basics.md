---
layout: post
title: Cracking Password Basics
date: 2018-1-15
---

Whelp, it's about 1.30am on a Sunday, and I can't sleep - I'm too wide awake, too busy thinking about everything I did today! So hopefully, by writing it out of my system it'll be a bit easier to go to sleep.

Today, I learned about one way of cracking a password given a hash. The way I will describe today uses the DES-based crypt function, which is available on most Linux systems. This is just one of many different ways to encrypt passwords, and luckily the ones most people use are much harder to crack than this one! I thought it was cool anyway, here's the breakdown.

Security 101: it's very bad practice to store passwords in plain text! If some ill-meaning person were to snoop around your PC when you weren't watching, they could quite easily see your passwords and do some real damage in your name! Naturally, we don't want this to happen.

To prevent this, the combination of numbers and letters that make up the password undergo a series of mathematical operations such that it's obfuscated. This is supposed to make it really hard to guess what the original password was. The set of mathematical operations which do this are called a one-way hash. It'll always give the same resulting hash each time for a given input.

Sometimes, some extra data is used in the hash to help avoid certain kinds of [attacks](https://en.wikipedia.org/wiki/Rainbow_table). This is called a "[salt](https://en.wikipedia.org/wiki/Salt_(cryptography))".

If you have a Linux operating system, passwords for users can be stored in ```/etc/shadow```. If you look in here, you might see some long weird words like "50JIIyhDORqMU" - that's the hash we're talking about! If we think this hash was the result of a password that was passed to the basic DES function, we could start deducing some information about it. For example, the [man page for the crypt function](http://man7.org/linux/man-pages/man3/crypt.3.html) which generates this hash tells use that the first two characters, "50" in this case, are the salt that's used to hash it.

If we have a hunch that the password that was encrypted was 5 characters long or less, then we can probably use our super fast computers to try all the different combinations of letters and numbers. This would take a human a really long time to do, but computers can do this in minutes, usually less!

Ok cool, so we know that we can probably brute force the password, we know the salt, and we know what the resulting hash is. So what do we do now? We can create a whole bunch of different combinations of characters to create the new key, feed this generated key into the crypt function along with the salt, and see what it returns us. If it gives us back the same hash function as the one we had initially, then our generated key must be the same as the original! Successfully cracked.

Seems kind of easy, doesn't it. Fortunately, most Linux systems these days use way better cryptographic hashing functions than the basic DES one, like [SHA-2](https://en.wikipedia.org/wiki/SHA-2).
