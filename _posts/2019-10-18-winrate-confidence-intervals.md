---
layout: post
title:  "Win Rate Confidence Intervals"
subtitle: "Evaluating the uncertainty in win rates"
date:   2015-10-18 23:59:59
categories: [statistics]
---

Most players pay attention to win rates (the percentage of total games won), particularly for heroes they play often or heroes with which they are trying to improve. DotaBuff and The DotA client both display your win rates for all the heroes.

But how well does a win rate describe your capacity to win with a hero?

I'm sure you already have some skepticism of win rates. With a small sample size, the win rate is an unreliable estimate of your skill with a hero. But how big of a sample size (what quantity of matches) is sufficient to consider the estimate reliable? We need a *range* of reasonable values, based on the data we have. For example, if you have 32 games on Chaos Knight with a 50% win rate, we might say that we are 95% confident that your "true" win rate with Chaos Knight is anywhere between 48-52%. This is called a *95% confidence interval.*

## Formulating the scenario
Let's assume that every game of DotA that you play has a random outcome with a certain probability of winning, \(p\). Certainly, the outcome of a game is not random - it's affected by things such as your team's skill, the other team's skill, the heroes in the game, the items purchased, etc. But since you can't anticipate any of these things before you click 'ACCEPT', I think that this is a reasonable assumption. The outcome of the game, then, is an example of a *Bernoulli trial*. A Bernoulli trial is simply an "experiment" with a random outcome that is either a success or a failure, and a specific probability of success. We're assuming that this probability of success is your "true" win rate with the hero, if you will. The number of wins out of a certain number of games, $n$, then, follows a *binomial distribution*. The binomial distribution can be thought of as the behavior of a series of Bernoulli trials. We can evaluate the probability of a certain number of successes, $k$, for a specific binomial random variable $X$, using the *probability mass function*:

{% raw %}
$$ p_X(k) = \begin{pmatrix} n \\ k \end{pmatrix} p^k (1 - p)^{n - k} $$
{% endraw %}

Let's not get into the probability mass function, but you can read more about the binomial distribution [here](https://en.wikipedia.org/wiki/Binomial_distribution) pmf's generally [here](https://en.wikipedia.org/wiki/Probability_mass_function).

However, in order to use the pmf, we have to know $p$, which is your probability of winning with a specific hero. Remember that the win rate displayed on DotaBuff or the game client is a (potentially unreliable) *estimate* of $p$. We can use a "hat" to denote estimates, so the win rate you see on DotaBuff is actually $\hatp$ - an estimate of $p$.

So what can we do? We can create a confidence interval.

## Calculating a confidence interval


