---
layout: post
title: Problem Solving
date: 2018-1-4
---

# Problem Solving

After spending lots of money on my education, it's been a joy to discover that I can continue to learn for free on my own terms. I'm very fond of online learning. One of my favourite courses was Udacity's "Introduction to Programming." Chapter 10, "How to solve problems" was one of the highlights of this course. When you learn to code, you're often not taught how to approach a problem systematically. I feel that the earlier you begin to solve problems in this way, the less time and frustration you'll feel!

## The Approach

In summary, this is the approach:

- What are the inputs?  
- How are the inputs represented?  
- What are the outputs?
- How are the outputs represented?


## The Problem

To learn a problem solving process, it helps to demonstrate this process with an actual problem.

In this case, let us think about the following problem. Given your birthday and the current date, calculate your age in days, compensating for leap days. Assume that the birthday and the current date are correct dates (and no time travel is possible).

For example, if you were born 1 January 2012 and the date is currently 2 Jan 2012, you are 1 day old!

We can define this function in the following stub in Python:

```
days_of_months = [31, 28, 31, 30, 31, 30, 31, 30, 31]

def is_leap_year(year):
    pass
```

## What is the first thing we should do to solve a problem like this one?

First, it's really important that you understand the problem before writing a line of code. At first glance it's easy to think "I have an idea of what it's asking me, I'll dive in and figure it out on the way." While this is super tempting to do, it's probably not going to be the fastest way to solve the problem.

But what does understanding a problem actually mean? How do we know that we understand it completely and fully?

A computational problem, which can be considered to be a function, is defined by the set of its possible inputs, and how these inputs relate to the set of possible desired outputs.

## What are the inputs?

In this case, the 2 inputs to the problem are defined in the question: a birthday and the current date. 
```
Inputs:
birthday date
current date
```

However, even if we know what inputs are wanted, there may be different ways of representing that data - some of which will be applied more easily to the problem than others.

Having constraints or assumptions on the input parameters is also very important, as it reduces the input range. For example in this problem, our assumption is that the birthday and current date are correct dates, and that the second date will always be on or after the first. 

Despite having these assumptions, it's good defensive programming to check that these cases hold, and to fail gracefully if we recieve an unexpected input.

We will make the assumption that the dates are correct in accordance with the Gregorian calender, to simplify the problem.

## How are the inputs represented?

We could use a Date object, but for the purposes of this exercise we will simply list out the day, month and year for each date as parameters.

```
def days_between_dates(year1, month1, day1, year2, month2, day2):
```

## What are the outputs, and how are they represented?

We can figure out the output from this phrase, "calculate your age in days, compensating for leap days." In this case, we should return the number. Generally, it's good to return a value you can do something with, rather than just printing the result in the function as you might want it later!