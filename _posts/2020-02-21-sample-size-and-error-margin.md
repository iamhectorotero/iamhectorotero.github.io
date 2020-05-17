---
layout: post
title: How many shots do I need to measure my free throw accuracy?
---
*Let's say you hear that to become a world-star basketball player, you need to score at least 90%
of your free throws. So you train for a day, a week, a month, a year... and you consider yourself
ready. Now it is time to test. But... how many free throws do you need to shoot to accurately
measure your free throw accuracy?*

It is hard to say. Do you need to score 9 out of 10 to consider you have a 90% accuracy? 90 out of 100?
900 out of 1000? You'll never be 100% certain what your accuracy is because shooting a few more free throws
may lead to a slightly better or worse accuracy. Since, practically speaking, you don't have all your life
to shoot free throws, let's see how many do you actually need to be happy with the accuracy you measure.

You need to answer two questions:

### 1. What is the lowest accuracy I'd be okay with having if I actually want a 90% accuracy?

This is a weird question that we need to answer due to sampling.
When we sample, we 1) take a subset of the population we are testing. 2) measure
the statistic we're interested in (average, maximum, minimum, etc). 3) generalize and say that the
statistic obtained in the sample is approximately that of the entire population. For example, if you're trying
to see what the average weight (*statistic*) of your favourite bag of chips is (long live Salt and Vinegar!),
you won't be able to buy every existing bag (i.e. the entire *population*) and measure it. You'll buy a subset of all
existing bags (i.e you'll take a *sample*) and measure their weight (i.e. obtain a *sample statistic*). Then you'll say that
the true average weight of the entire population, which you haven't really measured, is approximately the average weight of your sample.
So, going back to our free throw example, you can't shoot forever (population), you'll have to stop after
a certain number of free throws (sample) and measure your accuracy (sample statistic). 

Whenever we measure a statistic from a sample, we'll do so with a margin of error. That is, it is possible that if we
measured more bags (or shot more free throws), the average weight would be different. In the case of a binary variable,
like making a free throw (1) or not (0), the margin of error is calculated as:

```
Let p̂ be the accuracy we've had in the N free throws we have shot. Our margin of error will be calculated as:

margin of error = z-score * sqrt(p̂ * (1 - p̂) / N) = z-score * SE
```

where p̂ is our sample success (in this case, accuracy) and N is the sample size (in this case, the number of free throws we have shot)
So, for example, if we make 60 out of 100 free throws, our sampled accuracy would be p̂=0.6 and our sample size 100. 
Defining a margin of error will allow to say that, with *some certainty*, our true accuracy lies in the interval
[60% - margin of error, 60% + margin of error]. If we would be ok to say we have a 90% accuracy
if our true accuracy may be 85% (or 95%), we say we're ok having a 5% or less margin of error. If we want to
be more strict and will only be ok with 89%, our margin of error will be 1%. The more strict we are,
the more shots we'll need to shoot (the higher the N). 

### 2. Ok, I have defined my margin of error. How do I get my sample size? 

Knowing that, for example, a 5% error or less is ok with us. We need to solve the equation above
for our chosen margin of error 5% (that is, 0.05):
```
0.05 <= z-score * sqrt(p̂ * (1 - p̂) / N)

N >= (p̂ * (1 - p̂)) / (0.05/ z-score)^2
```

We still have two unknowns in the right side: p̂ and z-score. That's a problem since we need to know p̂ before we measure it and
that is physically impossible. That is, we can't know what our sample statistic will be before taking the sample
(following our bag of crisps example, we can't know how much the bags will weigh before buying and weighing them).
But not everything is lost, we can choose to be on the safe side and select the p̂ that will maximise our error. Given the
first equation above, the value of p̂ that maximises the right-hand side is 0.5, so to calculate N we will use p̂=0.5.
Now that we have p̂, what is our z-score? Well, you need to decide how sure you want to be that your true accuracy
lies within your margin of error. Do we want to be 50% sure? 80%? 90%? 95%? 99%? The more sure we want to be, the
larger your sample size (N) will need to be.

If you are taking basketball very seriously you may decide that you want you be 99% certain. If, on the other hand,
shooting free throws is a very boring thing to do for you, you may be okay with being 75% sure or less. Once we decide what our
confidence interval will be, we can obtain its corresponding [z-score](https://en.wikipedia.org/wiki/Standard_score).
Typical values for our confidence interval are 90%, 95% and 99%. A 95% confidence interval, for example, has a z-score of 1.96.
Once we have our z-score, we can calculate how many shots we need to shoot. 

## AN EXAMPLE

Let's say I wanted to calculate it for myself, a well-known free throw star. I want my true accuracy to be within
1% of my sample accuracy. That is, my margin of error needs to be 0.01 or less. And I want to be 99% sure that it is
like this. The z-score for a 99% confidence interval is... (*googles 'z-score 95 confidence interval'*)... 2.576. So, I need
to throw at least:

```
N >= (0.5 * (1 - 0.5)) / (0.01/ 2.576)^2 = 16,589.
```

16,589 free throws. Ok. See you guys in a couple of years.
