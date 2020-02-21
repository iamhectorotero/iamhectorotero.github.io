---
layout: post
title: How many shots do I need to measure my free throw accuracy?
---
*Let's say you hear that you become a world-star basketball player, you need to score at least 90%
of your free throws. So you train for a day, a week, a month, a year... and you consider yourself
ready. Now it is time to test. But... how many free throws do you need to shoot to accurately
measure your free throw accuracy?*

It is hard to say. Do you need to score 9 out of 10 to consider you have a 90% accuracy? 90 out of 100?
900 out of 1000? It is clear to see that you'll never be 100% certain what your accuracy is. Since,
practically speaking, you don't have all your life to shoot free throws, let's see how many do you actually
need to be happy with the accuracy you measure.

To do so, you need to answer two questions:


### What is the lowest accuracy I'd be okay with having if I actually want a 90% accuracy?

This is a priori a weird question that we need to answer. It is due to sampling.
When sampling, we take a subset of the whole population we are testing for and measure
the statistic we're interested in. For example, if you're trying to see what the average weight (*statistic*)
of your favourite bag of chips (long live Salt and Vinegar!) is, you can't buy every
existing bag (*population*) and measure it. You'll buy a subset of all existing bags (a *sample*) and measure
their weight (*sample statistic*). Then you'll say that the true average weight, which you haven't really measured,
is approximately the average weight of your sample. So, going back to our free throw example, you can't shoot forever 
(population), you'll have to stop after a certain number of free throws (sample). 

Whenever we measure a statistic from a sample, we'll do so with a margin of error. That is, it is possible that if we
measured more bags (or shot more free throws), the average weight would be different. In the case of a binary variable,
like making a free throw (1) or not (0), the margin of error is calculated as:

```
Let p̂ be the accuracy we've had in the N free throws we have shot. Our margin of error will be calculated as:

margin of error = z-score * sqrt(p̂ * (1 - p̂) / N) = z-score * SE
```

So, for example, if we make 60 out of 100 free throws, our sampled accuracy would be p̂=0.6. 
Defining a margin of error will allow to say that, with *some certainty*, our true accuracy lies in the interval
[60% - margin of error, 60% + margin of error]. If we would be ok to say we have a 90% accuracy
if our true accuracy may be 85% (or 95%), we say we're ok having a 5% or less margin of error. If we want to
be more strict and will only be ok with 89%, our margin of error will be 1%. The more strict we are,
the more shots we'll need to shoot. 

### 2. Ok, I have defined my margin of error. How do I get my sample size? 

Knowing that, for example, a 5% error or less is ok with us. We need to solve the equation above
for our chosen margin of error 5% (that is, 0.05):
```
0.05 <= z-score * sqrt(p̂ * (1 - p̂) / N)

N >= (p̂ * (1 - p̂)) / (0.05/ z-score)^2
```

We still have two unknowns in the right side: p̂ and z-score. HOW CAN WE KNOW OUR p̂ BEFORE WE ACTUALLY MEASURE IT?!?
Well, we can't. So we can choose to be on the safe side and select the p̂ that will maximise our error. That p̂ is 0.5 (you 
can check yourself by solving the equation). Now, what is our z-score?  Well, you need to decide how sure you want to 
be that your true accuracy lies within your margin of error. Do we want to be 50% sure? 80%? 90%? 95%? 99%? The more
sure we want to be, the larger our sample size (N) will need to be.

If you are taking basketball very seriously you may decide that you want you be 99% certain. If, on the other hand,
shooting free throws is a very boring thing to do for you, you may be okay with being 75% sure or less. Once we decide what our
confidence interval will be, we can obtain its corresponding [z-score](https://en.wikipedia.org/wiki/Standard_score).
Typical values for our confidence interval are 90%, 95% and 99%. A 95% confidence interval, for example, has a z-score of 1.96.
Once we have our z-score, we know how many shots we need to shoot. 

## AN EXAMPLE

So, let's say I wanted to calculate it for myself, a well-known free throw star. I want my true accuracy to be within
1% of my measured accuracy. That is, my margin of error needs to be 0.01 or less. And I want to be 99% sure that it is
like this. The z-score for a 99% confidence interval is... (*googles z-score 95 confidence interval*)... 2.576. So, I need
to throw at least:

```
N >= (0.5 * (1 - 0.5)) / (0.01/ 1.576)^2 = 6209.
```

6,209 free throws. Ok. See you guys next year.


