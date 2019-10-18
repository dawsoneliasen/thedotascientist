---
layout: post
title:  "Win Rate Confidence Intervals"
subtitle: "Evaluating the uncertainty in win rates"
date:   2019-10-18 23:59:59
categories: [statistics]
---

Most players pay attention to win rates (the percentage of total games won), particularly for heroes they play often or heroes with which they are trying to improve. DotaBuff and The DotA client both display your win rates for all the heroes.

But how well does a win rate describe your capacity to win with a hero?

I'm sure you already have some skepticism of win rates. With a small sample size, the win rate is an unreliable estimate of your skill with a hero. But how big of a sample size (what quantity of matches) is sufficient to consider the estimate reliable? We need a *range* of reasonable values, based on the data we have. For example, if you have 32 games on Chaos Knight with a 50% win rate, we might say that we are 95% confident that your "true" win rate with Chaos Knight is anywhere between 48-52%. This is called a *95% confidence interval.*

## Formulating the scenario
Let's assume that every game of DotA that you play has a random outcome with a certain probability of winning, $p$. Certainly, the outcome of a game is not random - it's affected by things such as your team's skill, the other team's skill, the heroes in the game, the items purchased, etc. But since you can't anticipate any of these things before you click 'ACCEPT', I think that this is a reasonable assumption. The outcome of the game, then, is an example of a *Bernoulli trial*. A Bernoulli trial is simply an "experiment" with a random outcome that is either a success or a failure, and a specific probability of success. We're assuming that this probability of success is your "true" win rate with the hero, if you will. The number of wins out of a certain number of games, $n$, then, follows a *binomial distribution*. The binomial distribution can be thought of as the behavior of a series of Bernoulli trials. We can evaluate the probability of a certain number of successes, $k$, for a specific binomial random variable $X$, using the *probability mass function*:

{% raw %}
$$ p_X(k) = \begin{pmatrix} n \\ k \end{pmatrix} p^k (1 - p)^{n - k} $$
{% endraw %}

Let's not get into the probability mass function, but you can read more about the binomial distribution [here](https://en.wikipedia.org/wiki/Binomial_distribution) pmf's generally [here](https://en.wikipedia.org/wiki/Probability_mass_function).

However, in order to use the pmf, we have to know $p$, which is your probability of winning with a specific hero. Remember that the win rate displayed on DotaBuff or the game client is a (potentially unreliable) *estimate* of $p$. We can use a "hat" to denote estimates, so the win rate you see on DotaBuff is actually $\hat p$ - an estimate of $p$.

So what can we do? We can create a confidence interval.

## Calculating a confidence interval
A confidence interval for an estimate provides a range of values in which we can be "confident" the true value is contained. Generally, we calculate a confidence level by deciding on a *confidence level*, and using that to calculate the distance from the estimate which will shape the interval. A standard confidence level is 95% ($\alpha = 0.05$). 

We are modelling the number of wins on a hero as a binomial random variable with a certain number of games, $n$. The probability of an individual win is $p$ - this is called a *parameter* of the random variable. We're going to construct a confidence interval centered on $\hat p$, which is the number of wins you have divided by the number of games you have played. One formula for creating this confidence interval is

{% raw %}
$$ \hat p \pm z \sqrt{\frac{\hat p (1 - \hat p)} {n} } $$
{% endraw%}

Here, $z$ or the 'z-score' is a value that describes how unlikely an observation is from a *standard normal distribution*. For $\alpha = 0.05$, $z = 1.96$. Now we have everything we need to make a confidence interval for one of our win rates. Let's use my win rate on Morphling, which is 43.28% out of 67 games. 

{% raw %}
$$ .4328 \pm 1.96 \sqrt{\frac{.4328 (1 - 4.328)} {67} } $$
{% endraw %}

