---
layout: post
title: Permutations
date: 2018-1-22
---
This is something I forget about all the time - what is the difference between a combination and a permuation? We know that it's something to do with getting different sets of element orderings. Let's use "abcd" as an example.

We can easily see the differences in Python, if we import the [itertools](https://docs.python.org/3.6/library/itertools.html) library.

```
>>> import itertools
>>> string = "abcd"
```

Let's see what the permutations function does. Since the result of this function is a [generator object](https://www.programiz.com/python-programming/generator), we can use the * character to unload all the elements into the print function at once! However, if we're insistent on getting one element at a time, we can just call `next(result)`.

```
>>> result = itertools.permutations(string, len(string))
>>> print(*result)
('a', 'b', 'c', 'd') ('a', 'b', 'd', 'c') ('a', 'c', 'b', 'd') ('a', 'c', 'd', 'b') ('a', 'd', 'b', 'c') ('a', 'd', 'c', 'b') ('b', 'a', 'c', 'd') ('b', 'a', 'd', 'c') ('b', 'c', 'a', 'd') ('b', 'c', 'd', 'a') ('b', 'd', 'a', 'c') ('b', 'd', 'c', 'a') ('c', 'a', 'b', 'd') ('c', 'a', 'd', 'b') ('c', 'b', 'a', 'd') ('c', 'b', 'd', 'a') ('c', 'd', 'a', 'b') ('c', 'd', 'b', 'a') ('d', 'a', 'b', 'c') ('d', 'a', 'c', 'b') ('d', 'b', 'a', 'c') ('d', 'b', 'c', 'a') ('d', 'c', 'a', 'b') ('d', 'c', 'b', 'a')
```

Whew, that's a lot of results! 24 to be exact. Interestingly, this is equivalent to the factorial of 4 (4!). If we think about it a bit more, that actually makes a lot of sense.

We have an empty tuple to fill, and 4 possible characters to choose from:

`[ a, b, c, d ] => (_, _, _, _)`

Let's go ahead and pick one. We could pick any of 'a', 'b', 'c' or 'd', but this time around, we'll pick 'a'. This now rules out 'a' for our future picks, since we can't have it more than once!

`[ b, c, d ] => ('a', _, _, _)`

Ok, so now we have 3 choices left. Let's pick the next one, 'b'.

`[ c, d ] => ('a', 'b', _, _)`

Now we have 2 choices left. Sensing a pattern yet? The number of choices available is decreasing by 1 each time!

`[ d ] => ('a', 'b', 'c', _)`

Finally, there's only one choice of character for one spot.

`[ ] => ('a', 'b', 'c', 'd')`

Next time around, we can choose something like ('a', 'b', 'd', 'c'), and so on until everything's been done. So, for "abcd", the number of total combinations we could have is 4 * 3 * 2 * 1, which is 24.

Now, this is the number permuations for all the characters in the entire string. But what if we wanted say, to choose all the different 2 character sets instead?

```
>>> result = itertools.permutations(string, 2)
>>> print(*result)
('a', 'b') ('a', 'c') ('a', 'd') ('b', 'a') ('b', 'c') ('b', 'd') ('c', 'a') ('c', 'b') ('c', 'd') ('d', 'a') ('d', 'b') ('d', 'c')
```

That's interesting. So why do we now have 12 combinations?

The reason for this is that we're stopping the factorial early. We're only going 2 combinations deep into this 4 character array - 4 choose 2. We're not going right through every letter combination available to use like we did before.

4! / (4-2)! = 12

```
  (4 * 3 * 2 * 1) / (2 * 1)
= (24 / 2)
=  12
```

We can generalise this to be:
```
            n!
p(n, k) = ------
          (n-k)!
```

I think that makes sense! Check out how it compares to combinations does in my other post :)
