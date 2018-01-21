---
layout: post
title: Bit Manipulation
date: 2018-1-21
---
## Binary (Positive Numbers)

How is 583 represented in base 10?

base10 -> 583

     5 |    8  |    3
  10^2 | 10^1  | 10^0 
  100  |   10  |    1 
=======================
  5*102 + 8*101 + 3*100
= 500   + 80   +    3

How is 5 represented in base 2?

     1 |    0  |   1 
   2^2 |  2^1  | 2^0 
     4 |    2  |   1 
=======================
 1*22  +  0*21  + 1*28
=  4   +    0  +   1
=  5

## Binary Addition

Binary addition is not so different to adding in decimal.
This is the standard way to add numbers in decimal:

   1 1
   583
+  637
======
  1220

And this is how we do it in binary - we simply carry the one if there’s more than two 1’s there.

  1 1
  101
+ 011
=====
 1000
 
## Binary (Negative Numbers)

Negative numbers are stored in Two’s Complement form. The first bit (most significant bit) represents the sign of the number. 
If the leftmost bit is a 0, it’s positive. If it’s a 1, it’s negative.

For example, this is how 18 is represented in an 8 bit integer:

18 = 00010010

Say that we want to express -18 in binary. Since we know the leftmost bit needs to have a 1 in order to have a negative sign, we can think about this as wondering what number we need to add to our positive number, in order to get the most significant bit to flip:

     0010010
  +  ???????
 ===========
    10000000
    
The easiest way to do this, is to add the inverse of the number.

     0010010
  +  1101101
  ==========
     1111111
     
This gives us all ones. Now, we need to add one to this number to make them all flip!

     0010010
  +  1101110
  ==========
    10000000
    
So, 1101110 is the right answer. Let’s try this with one more example:

123 = 01111011

    1111011                              1111011
  + 0000100                            + 0000101
  ==========   so, adding 1 gives us   ==========
    1111111                             10000000

10000101 is -123.

In summary, this is how to get the negative number of a given number:

1. Convert positive number to binary
2. Invert the bits
3. Add 1

## Shifting Bits

There are two types of shifting bits - arithmetic and logical.

For example:
00010111 = 23

Left shifting this number yields:

00010111 = 23
00101110 = 46 -> Left shift 23 by 1
00001011 = 11 -> Right shift 23 by 1

### Logical Shifting

Logical shifting doesn’t preserve the signed bit - it just falls off the end. So if you have a negative number and expect to double it using a logical left shift operation, it will give you a nonsensical result.

### Arithmetic Shifting

Arithmetic shifting to the left has the bit fall off the end, but it’s replaced again straight after so the math still holds.

## Masks

Using a “mask” can help with some operations.

0 & 0 = 0
1 & 0 = 0
1 & 1 = 1

0 | 0 = 0
1 | 0 = 1
1 | 1 = 1

0 ^ 0 = 0
1 ^ 0 = 1
1 ^ 1 = 0

### Get the i’th bit

How do we know whether a bit in the i'th position is a 0 or a 1? For example, what is the bit in position 6 from the left in the number 00101100?
One way we can do this is to create a mask with only that bit, and do a logical and operation on it.

  00101100
& 00100000
==========
  00100000
  
Shift the number of this mask by i spots to find out which number it is. If 0, then whole number is 0, otherwise it’s a 1.
x&(1<<c)) != 0

### Set the i’th bit

x|(1<<c)

  00101100
| 00100000
==========
  00101100

### Clear the i’th bit

To clear the i’th bit, you need to use a mask that contains all 1’s except for the bit you are targeting, which should be a 0.

x|(1<<c)

  00101100
& 11011111
==========
  00001100
  
How do we do this? We invert our existing mask from before.
~(1<<c)
x&(~(1<<c))
