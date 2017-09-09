---
layout: post
title: Random sampling in Big Data problems
---
One interesting big data problem I learned about in class is how do you get a random sample of a HUGE pile of data without knowing how much data you have beforehand.

Obviously, if you were writing this problem down on paper,  if your dataset was in an array-like format, you would first count the number of items in your dataset `n`, and then choose an index from `1..n`, getting the value stored at the random index you've picked. There you go! A random sample.

This is fine if you know the number of items you have beforehand, or if your dataset is finite. But what if you wanted to do this all in one pass, or if your dataset is a constant stream of data that never stops? Obviously, if `n` is abstract, it gets much  harder to choose an index from `1..n`. So our solution has to be less brute force than this.

## Coin flipping?

For the sake of example, let's say that the dataset I'm working with is a text file with a shitload of words in it. I want to choose a random word from this text file with an equal probability of choosing any word. I don't know the number of words in this file (if you know unix, let's pretend the `wc` command doesn't exist) and the number of words is so high that I couldn't keep all of them in memory if I loaded the whole file.

So, how do I choose a random words with equal chance? One idea is that for every word I read in, I flip a coin, and if the coin is heads, I replace the word I'm currently holding in favor of this new word.

Superficially, it looks like this would work. Every piece of data read in would have a 50 percent chance of being chosen as the sample. But, in terms of random sampling, being chosen is just half the battle. **Survival** is the next thing you would have to consider.

For example, let's say I flip the coin `n` times, once for each word I read in. The first word has a 50 percent chance of being chosen, and so does the last word. But the first word, if chosen, has to survive `(n-1)` extra coin flips in order to emerge as the randomly chosen word, while the last word only has to deal with one coin flip.

This is [biased](https://en.wikipedia.org/wiki/Bias_(statistics)) because this means I'm much more likely to choose the last couple of words than the first couple of words. In a random sample, I want to make sure each word has an equal chance of being chosen with no bias. So if coin flipping leads to a bias, what do  you do? 

## Reservoir Sampling

The answer is to use reservoir sampling, which is a pretty crazy method that allows you uniformly choose a new element based on the number of elements that have currently been read in. So this means that by induction, if you have `n` items, then you will be able to uniformly select an item out of your dataset, which is exactly what we want.

The algorithm for reservoir sampling requires you to keep track of the current iteration number `i` and then simply choose a number from `1..i` for each new item you read in. If the number happens to be *any particular number* from `1..n`, you choose that number. Here's what it looks like in Python:

```python
import sys
import random

iteration = 0
for word in sys.stdin:
    if random.randint(0, iteration) == 0: # why?
        choose = word.strip()
    iteration += 1
print(choose)
```

The part that's kind of confusing here is why we're specifically looking for `0`. It seems kind of arbitrary, which is true, but the best way to think about this is thinking about the coin flipping example. In the coin flipping example, we only chose a word if the coin was heads, right? Well for reservoir sampling, just pretend we're flipping an `i` sided coin every time, with a number that you choose (mine in this example is `0`) being heads. This will give you a `1/i` chance every time of choosing a particular word that particular iteration.

You *could* probably change it so that your "heads" is a constantly changing number between `0..i`, (all possibilities are `1/i` no matter what) but for sake of simplicity, it's okay to keep your "heads" consistent throughout your algorithm.

## Why does this work?

