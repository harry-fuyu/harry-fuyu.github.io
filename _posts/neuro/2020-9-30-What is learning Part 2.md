---
title: "Neuro & AI (II): What is learning? (Part 2)"
comments: true

toc: true
toc_label: "Table of Contents"
toc_icon: "cog"

categories:
  - Neuro&AI
tags:
  - Neuroscience
  - Deep Learning
  - Neural Network
published: true

excerpt: "Interpretation of learning in the statistical sense"
header:
  overlay_image: /images/header.jpg
---

Welcome back! In this post, we will briefly introduce two more interpretations of learning. I would expect this post, especially the second half to be very technical, so I will specify clearly which parts could be skipped without affecting the flow of understanding the whole blog series. However, I do think it would be extremely rewarding if we could perservere a little bit and dig throught the material that I intend to share!

<!-- - Thinking as Bayesian
- Statistical learning
    - Hypothesis class, Empirical risk minimizer
    - PAC learnable
    - No free lunch
- Compare and contrast -->

## 1. Thinking as a Bayesian

### 1.1 The Bayes Theorem

Thinking of learning as a optimization problem is not the only perspective possible. More intuitively, learning is all about acquiring more accurate information. For example, people often use the phrase "I have recently learned that... " to show that an update in the knowledge that they know. In the same sense, the Bayesian framework offers us an equivalent way to think about learning.

But first of all, what does Bayesian mean? In statistics, there are two main schools of thinking: frequentists and Bayesian. I would suggest not to think of them as a dichotomy, but rather two sides of the same coin. To frequentists, probability is a long term frequency (and hence the word "frequentists"). For example, the probability of the coin landing heads is $0.5$ means that if we flip the exact same coin, say $10000$ times, we would have around $10000 \times 0.5 = 5000$ heads. This approach to probability would encounter difficulty in some non-repeatable experiments. For example, what is the probability that Beth will give birth to a girl for her next child? Obviously you can't ask any one to repeat this "experiment" unless multiple universe exists. 

Now Bayesian came in to our rescue. The central idea of Bayesian perspective is to put a distribution on everything. For example, for a coin tossing experiment, we started with no knowledge about this coin. Hence we can put a prior which is a uniform distribution, meaning that our prior belief is that this coin will have any probability of landing heads with probability ranging from 0 to 1 equally likely. However, if we now flip the coin ten times and observed ten heads and no tails, we would be pretty sure that there is extremely high probablity that the coin is extremely unfair. 

The Bayes theorem summarizes this idea of updating our knowledge upon observing experiment outcomes succinctly. Suppose that we are conducting experiments to estimate parameter $\theta$ and have some observations $X$. The conditional distribution of $\theta\| X $ describes what our new knowledge aobut $\theta$ is, given what has happened during the experiment. The Bayes theorem states that:

$$P(\theta|X) = \frac{P(X|\theta)P(\theta)}{P(X)}$$

The proof is astoundingly simple: By definition of conditional probability, $P(\theta \cap X) = P(\theta\|X)P(X)$, but also $P(\theta \cap X) = P(X\|\theta)P(\theta)$. Rearranging the terms would yield the Bayes theorem. But yet, this theorem is so profound, single handedly defining the whole field of Bayesian statistcs. Before displaying the interpretation for each terms, I would like to point out that here information, whether it's innate or learnt, are discribed formally in terms of distributions. You can imagine that a flat distribution is saying that we are not sure of the value of the parameter, and a narrow, low variance distribution would mean that we are fairly sure about the value of our parameter. 

- $P(\theta)$: **prior**. The prior represents what information we have about $\theta$ _before_ the experiment. 
- $P(X\|\theta)$: **likelihood**. The likelihood represents how probable it is for us to observe what we have observed if the parameter has the value $\theta$. Note that here we are switching our perspective and treating the parameter $\theta$ as _fixed_, and looking at it as a function of data.
- $P(\theta\|X)$: **posterior**. The posterior describes what we know about our parameter _after_ the experiment, and this is also the goal of Bayesian statistics! We must remind ourselves that with our Bayesian "goggles", we are not interested in a _specific value_ of $\theta$ anymore, but only its posterior distribution.
- $P(X)$: **evidence**. The evidence is a constant that is fixed once our data is fixed. Hence, we usually do not compute evidence explicitly, but rather calculates it at last by normalizing and making the posterior density to integrate to one.

Each time we collect some results, we apply Bayes rule to incorporate what we have learned about the parameter in terms of new posterior probabilities. Then this exact posterior becomes the new prior if we have additional data for future updates. Hence, Bayesian statistics has two fundamental underlying assumptions:

- Whether we update data sequentially or all at once should not affect the posterior obtained.
- Posterior should be permutation invariant to the order of data if it is updated sequentially, under some independence assumptions about experimental trials. This is to say that the order of observing data should not matter, because essentially if we observed the same results, these results should contain the same amount of information about our parameter.

### 1.2 Learning as updating conditional probabilities

As we accumulate information and do posterior updates, we would expect our distribution to become more and more narrow and focused after observing the actual outcomes of experiments about the parameter. Indeed, here we see a nice example. 

![](/images/posterior_compromise.png)

We would like to know if a coin is fair. Before the experiment, I have no information about the coin, and I assume a Beta(2,2) prior, which is the green curve. I throw the coin $10$ times, out of which $4$ times the coin landed heads. The likelihood of this happening as a function of $\theta$ is likelihood plotted in blue. With this information, we perform posterior updates according to the Bayes rule and obtain the posterior probability in red. As expected, we would naively guess from the experiment that the coin would roughly have the probability of $0.4$ of landing heads, and indeed, the peak of the posterior is much closer to $0.4$ than the prior, which centers at $0.5$.

We see that our prior is a significantly wider distribution than the posterior, since we had less information before the experiment and have to just take a whild guess. Practically we could take any guess, as long as the domain (more technically called the support of the distribution) is within reasonable range. For example, if we are doing a coin throw, it would be bad if the prior has non-zero probability taking on values that are negative.

Another takeaway from the above demonstration is that we could almost think of posterior as a "compromise" between prior and likelihood. As we see, the peak of posterior, which is red, is sitting between the peaks of the prior and the likelihood. Initially with few rounds of coin tosses, we do not have clear idea about whether the coin is fair, and the posterior is close visually to the prior, but as the experiments goes on, we will have better and clearer idea about the probability of coin landing heads, and hence the posterior would be much closer to likelihood instead.

### 1.3 Perception as inference

_As this is the first discussion section in the whole series, I thought it would be beneficial to say that I do not have a clear answer for all the questions that I pose. I will throw out questions along the way, and I do hope that you as my readers would like to get involved by actively pondering on those questions, and it would be wonderful if you could post what you think in the comment section at the end of the post._

When we receive sensory information and perceive about the world, all our brain doing is to make sense of all information and form an explanation. This process is exactly the same as performing inference. For example, visual depth perception is inferred from photons bouncing off the same object and recieved in the retina of both eyes, and in the more extreme example of bats, the location information is all calculated in their delicated auditory systems according to time delays at both ears. (we will discuss its wonderful neural implementation in detail at some point definitely) 






