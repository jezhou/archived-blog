---
layout: post
title: A high level explanation of Semaphores
---
*I'm writing this explanation of semaphores because a lot of the articles / explanations I see are too technical.*

I'm currently taking a operating systems class and one of the coolest concepts I've learned about so far is the **semaphore**. Semaphores are essentially variables that help enforce the concept **synchronization** in software. 

Synchronization helps to make sure that two or more concurrent processes don't *modify the same data at the same time*. A good example of why synchronization is so important is the classic bank deposit and withdrawal situation. Feel free to [skip ahead](#semaphores) if you already know about this problem.

## The bank problem

Suppose you have an impatient person who wants to make multiple transactions through an ATM. The person makes the transactions faster than the ATM can process them. This person wants to deposit $20, and then withdraw $60. Let's say he has $100 in the bank.

![illustration of depositing]()

Now, our intuition goes like this. If the transactions go through correctly, this person should have $60 in hand, and $60 in the bank. But let's say the ATM **does not let its processes synchronize**. This means the deposit transaction and the withdrawal transaction do not wait for each other to finish before working with the data. This means that each transaction uses the same base amount of money in your bank account.

![synchronization problem]()

Essentially, whatever transaction finishes last will be the amount of money that is incorrectly in your bank account. If the deposit transaction finishes first, you will have $120 in your account. But since the withdrawal transaction is finishing last and is using the *old amount in your bank account*, which is $100, you end up with a measly $40 in your bank account. You just lost money sucker!

Ideally, you would want your deposit to go through first and have your withdrawal request wait for the deposit to go through. This is where semaphores can come in.

<a name="semaphores"></a>
## So, back to sempahores

So then, what exactly is a semaphore and how it help you make the transactions in the bank example wait for each other? 

Semaphores are best thought of as *bouncers to a club or a bar*. These bouncers make sure only a certain amount of people are in the bar at any given time, while making everyone else wait outside.

![bouncer making people wait outside](/content/images/2016/03/bouncer.jpg)

In this particular example, our club and/or bar is  the **critical section**. A critical section is essentially the very sensitive part that can only handle a few things at a time (in the bar example, these things are people, while in the bank example, these things are transactions).

The number of things that you can allow into a critical section depends on a certain postive value you assign to a semaphore. The higher the number you assign to a semaphore, the more things you can let into the critical section.

So, going back to the bouncer example, assigning the number 6 to a semaphore is like if I told the bouncer

> Hey, right now, only let **6** people in right now, everyone else has to wait for at least one person to come out before going in.

Sucks for the people waiting, but hey! Things will get rowdy if we don't keep things under control.

## An interesting case 

So right now, we've dealt with what semaphores are and how to deal with positive values assigned to semaphores. But what if the value is negative, or 0?

I'm going to say that there is pretty much never a really good reason why you should be assigning a semaphore to a negative number. I think it makes no sense, and there has to be one hell of an edge case to why you would want to do such thing. But in case there is one, feel free to email me or leave a comment somewhere below.

However, assigning a semaphore to 0 is where things really get interesting. **If you assign a semaphore to 0, you are essentially telling the process to wait for some initial setup to be completed before entering the critical section.**

This is equivalent to telling the bouncer

> Keep everyone out of this club until we finish setting it up.

Just a note, "setting up" can mean anything, but it's just what made sense for this particular example. If you just want everything else to wait before you do something, then that's when you assign 0 to a semaphore.

## Conclusion

What I've explained so far is a very high level overview of what semaphores are, why they're important, and essentially how to use them. But there are probably a lot of lingering questions you have, like:

* Why does assigning a positive or zero value change the behavior of a semaphore?
* Can more than one semaphore exist?
* How do I implement semaphores in a project I'm doing?

In order:

1. This goes more into the technical details of semaphores that are harder to describe unless you actually take some kind of Operating Systems class. A TL;DR version of it is that everytime you are about to enter a critical section, you signal the semaphore which decrements a value inside the semaphore. Everytime you leave a critical section, you signal it again, which increments the value. Depending on what the value is and how many processes you have waiting to get into the critical section, you tell the semaphore to essentially "freeze" or "unfreeze" the process. There's a really good video a TA at UCSD made on the technical details of semaphores, and if you are trying to implement one for a class or project, I highly recommend you take a look at it. I'll link it below.

2. Yes, in fact, it's probably really good practice to keep a bunch of them assigned to do different tasks. Like, for the bar example, we would have a "wait-for-setup" bouncer and a "capacity" bouncer. Not so smart when we translate this to real life because we have to pay for more bouncers, but smart when it comes to operating systems.

3. If you are using a high level language, there are built in synchronization features in almost every single one of them! Semaphores are just a building block of the larger concept of synchronization, and you usually don't need to implement semaphores unless you're writing some kind of system from the ground up.

Anyway, I hope this helped a lot! I would recommend viewing this video if you want more information about the technical details of semaphores (like when to increment /  decrement, psuedocode, etc).

<iframe width="420" height="315" src="https://www.youtube.com/embed/t0CnClz8Jo4" frameborder="0" allowfullscreen></iframe>
