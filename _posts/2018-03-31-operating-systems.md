---
layout: post
title: Operating Systems
date: 2017-03-21
---

## Processes

A process is an instance of a computer program that is being executed. This process could be using multiple threads of execution, running the program in a concurrent manner.

## Threads

A [thread](https://en.wikipedia.org/wiki/Thread_(computing)) is the "smallest sequence of execution that can be 
managed independently by a scheduler." In most implementations, a thread is a component of a process.

Multiple threads can be components of a process, and share resources such as memory.

If the CPU only has a single processor, multithreading is implemented by giving each thread some 
amount of time to use memory - this is called time slicing.

If the CPU has multiple cores (multiprocessor) then multiple threads can execute in parallel since
they don't need to share as many resources.

## Common Concurrency Issues

Race condition: Two or more threads trying to modify data at the same time can give an inconsistent result. You don't know the order
in which the threads accessed the resource, so it's no longer deterministic.
Deadlock:
Starvation: process is repeatedly denied access to resources that it needs in order to do its work. This can be caused by errors in the mutual exclusion algorithm, resource leaks or denial of service attacks.

## [Mutexes](https://en.wikipedia.org/wiki/Mutual_exclusion)

Mutex, aka Mutual Exclusion, is a "synchronization object".
It "stands guard" to make sure that no other thread can access the same data at the same time, thereby preventing race conditions.
It's like a guard protecting a room with treasure in it.

The data is a treasure chest, the thread is a visitor, the mutex is the guard, and the lock is the lock on the door.

The mutex, or guard - controls the lock. If a person comes in to look at the treasure, the guard locks them in the room until
they want to come out.

The mutex for the data has a lifetime that is about the same as the resource it's protecting.

A mutex is a synchronization object. You acquire a lock on a mutex at the beginning of a section of code, and release 
it at the end, in order to ensure that no other thread is accessing the same data at the same time. A mutex typically has
a lifetime equal to that of the data it is protecting, and that one mutex is accessed by multiple threads.

## Locks

A lock is a synchonisation mechanism that limits thread access to a resource, when there are multiple threads in a process that can
access the same resource.

## [Semaphores](https://en.wikipedia.org/wiki/Semaphore_(programming))

A variable, or Abstract Data Type, that controls access to a resource shared by threads.
A binary semaphore, as you might have guessed - has only two values (so typically represented as a boolean), and can be used 
to tell other threads whether a resource is free or if it's in use. Binary semaphores are used to implement locks.

A counting semaphore is well, a counter for checking how many resources are available to incoming threads. If a thread wants 
access to a resource, the counting semaphore will check if it has at least one available. If it does, it decrements the counter and 
allows the thread to use the resource. If a thread is finished with the resource, the semaphore increments the count, ready to 
check it with another thread. The semaphore doesn't care which resource is being used, it only cares about whether some resources are available.

Mutexes and semaphores are very similar, and can even be implemented in the same way. But the context in which one is used
over the other is different. 

Mutex: only the thread that locked the resource can unlock it again.
Sempahore: a binary semaphore can be used as a mutex - mutexes are a subset of semaphore.

## [Monitors](https://en.wikipedia.org/wiki/Monitor_(synchronization))

Threads can have both mutual exclusion and wait for a certain condition to become true. If this happens, it can signal to other threads
that it's ready to share the resource.
