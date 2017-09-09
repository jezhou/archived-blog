---
layout: post
title: Ulam Spiral Art
---
I was mindlessly browsing YouTube the other day (as most college kids do) and I found an extraordinary video on Prime Spirals, discovered by the Polish-American mathematician Stanislaw Ulam while doodling at a "boring meeting" in 1963.

And it turns out prime spirals are pretty frickin' cool. Allow me to demonstrate.

### What is a prime spiral?

The basic idea is to write out numbers `1..n`, spiraling outwards from the center. 
![prime spiral]

After writing out all of the desired numbers, one would highlight every prime number, and it turns out that this generates a unique pattern that after careful inspection, seems to be non-random. 

![pattern]

Most people at first glance might associate this pattern with randomness, but let's compare an Ulam spiral pattern with a randomly generated pattern.

![]

One can very clearly see that the Ulam spiral, despite its somewhat chaotic look, still has a pattern, and that pattern seems to be that prime numbers form along diagonal lines, although not perfectly. These imperfect diagonal lines turn out to the outputs of [prime-generating polynomials](http://mathworld.wolfram.com/Prime-GeneratingPolynomial.html).

Here, I am highlighting `n^2 + n + 41`, a famous prime-generating polynomial discovered by Euler, infamous mathematician hated by high school calculus students everywhere.

![highlighting]

It turns out, you can modify the Ulam spiral and turn it into a Sack spiral. Basically, it's a Ulam spiral that is superimposed on a Archimedes spiral, so that the initial sequence of numbers is spaced fairly along the curve. Then, as always, you would highlight the prime numbers.

![Sacks spiral]

Same concept as the diagonals: the curves that are generating by Sack's spiral fall into some sort of pattern! But let's not stop there: here are some other Prime spirals I've generated using different configurations and different shapes.

![]

Depending on how you want to visually represent each prime number
