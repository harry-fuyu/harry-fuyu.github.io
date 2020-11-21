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

excerpt: "Bayesian thinking and statistical learning theory"
header:
  overlay_image: /images/header.jpg
---

Welcome back! In this post, we will briefly introduce two more interpretations of learning, both from statistical perspectives. The first is learning as updating conditional probabilities, where we discuss the profound yet simple Bayes theorem, and perception as an inference problem. Secondly we are going to introduce some introductory learning theory concepts, including the idea of PAC learnability. How can the topic on learnign be complete if we do not mention learning theory itself! 


<!-- - Thinking as Bayesian
- Statistical learning
    - Hypothesis class, Empirical risk minimizer
    - PAC learnable
    - No free lunch
- Compare and contrast -->

## 1. Thinking as a Bayesian

### 1.1 The Bayes Theorem

Thinking of learning as a optimization problem is not the only perspective possible. More intuitively, learning is all about acquiring more accurate information from past experiences. For example, people often use the phrase "I have recently learned that... " to show that an update in the knowledge that they know. In the same sense, the Bayesian framework offers us an equivalent way to think about learning.

But first of all, what does Bayesian mean? In statistics, there are two main schools of thinking: frequentists and Bayesian. I would suggest not to think of them as a dichotomy, but rather two sides of the same coin. To frequentists, probability is a long term frequency (and hence the word "frequentists"). For example, the probability of the coin landing heads is $0.5$ means that if we flip the exact same coin, say $10000$ times, we would have around $10000 \times 0.5 = 5000$ heads. This approach to probability would encounter difficulty in some non-repeatable experiments. For example, what is the probability that Beth will give birth to a girl for her next child? Obviously you can't ask any one to repeat this "experiment" unless multiple universe exists. 

Now Bayesian came in to our rescue. The central idea of Bayesian perspective is to put a distribution on everything. For example, for a coin tossing experiment, we started with no knowledge about this coin. Hence we can put a prior, which is a uniform distribution, on the probability of the coin landing heads, meaning that our prior belief is that this coin will land heads with probability ranging from 0 to 1 equally likely. However, if we now flip the coin ten times and observed ten heads and no tails, we would be pretty confident that this coin is extremely unfair. 

The Bayes theorem summarizes this idea of updating our knowledge upon observing experiment outcomes succinctly. Suppose that we are conducting experiments to estimate parameter $\theta$ and have some observations $X$. The conditional distribution of $\theta\| X $ describes what our new knowledge about $\theta$ is, given what has happened during the experiment. The Bayes theorem states that:

$$P(\theta|X) = \frac{P(X|\theta)P(\theta)}{P(X)}$$

The proof is astoundingly simple: By definition of conditional probability, $P(\theta \cap X) = P(\theta\|X)P(X)$, but also $P(\theta \cap X) = P(X\|\theta)P(\theta)$. Rearranging the terms would yield the Bayes theorem. But yet, this theorem is so profound, single handedly defining the whole field of Bayesian statistics. Before displaying the interpretation for each terms, I would like to point out that here information, whether it's innate or learnt, are discribed formally in terms of distributions. You can imagine that a flat distribution is saying that we are not sure of the value of the parameter, and a narrow, low variance distribution would mean that we are fairly sure about the value of our parameter. 

- $P(\theta)$: **prior**. The prior represents what information we have about $\theta$ _before_ the experiment. 
- $P(X\|\theta)$: **likelihood**. The likelihood represents how probable it is for us to observe what we have observed if the parameter has the value $\theta$. i.e. this is the probability of data given parameter $\theta$.
- $P(\theta\|X)$: **posterior**. The posterior describes what we know about our parameter _after_ the experiment, and this is also the goal of Bayesian statistics! We must remind ourselves that with our Bayesian "goggles", we are not interested in a _specific value_ of $\theta$ anymore, but only its posterior distribution.
- $P(X)$: **evidence**. The evidence is a constant that is fixed once our data is fixed. Hence, we usually do not compute evidence explicitly, but rather calculates it at last by normalizing and making the posterior density to integrate to one. Note that computing this constant is usually computationally hard, as we need to integrate out $\theta$.

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

<!-- _As this is the first discussion section in the whole series, I thought it would be beneficial to say that I do not have a clear answer for all the questions that I pose. I will throw out questions along the way, and I do hope that you as my readers would like to get involved by actively pondering on those questions, and it would be wonderful if you could post what you think in the comment section at the end of the post._ -->

When we receive sensory information and perceive about the world, all our brain doing is to make sense of all information and form an explanation. This process is exactly the same as performing inference. For example, visual depth perception is inferred from photons bouncing off the same object and recieved in the retina of both eyes, and in the more extreme examples of bats or barn owls, where location information is all calculated in their delicated auditory systems according to time delays at both ears. Let's dive into this example right now!

#### 1.3.1 Case study: Auditory perception in Barn Owls

Humans are always described as visual animals, and out of our five senses, vision is unarguably the most "essential" for normal everyday life. But getting visual is not the only way to conduct life. In this diverse animal kingdom, many chose other means of navigation other than seeing. One important way is via sound, and another main way is through electrocurrents. 

Let's focus on the cases where sound is used to locate and navigate, and specifically in barn owls. One common misconception about localization with audio signal is that our brain calculates the distance or angle to the target by directly calculating the time difference between the arrival of sound in both ears. Here's why this can't be true. Let us crudely estimate the diameter of head of bar owl to be around 15cm, and the speed of sound propagation in the air is around 330m/s. This means that the time difference between the arrivals in the two ears of the barn owl, which is called **interaural time**,  is at maximum $0.15/330 = 0.45$ ms! Relating back to the signal conduction in neurons, it takes 10ms for an action potential to propagate itself. Therefore, it is impossible to implement the neural circuit in a way that calculates the interaural time directly.

Instead, evolution has brought us an ingenious solution. Here is a real image of the portion of brain stem that implements the neural hardware that found a way to be able to calculate interaural time. 

![](/images/barn_owl_section.png)
*Carr and Konishi, 1990*

Here we can see the clear, elongated and rectanguar shading of *nucleus laminaris* (NL) leaning about 45 degrees to the left, and to the right is the circular *nucleus magnocellularis* (NM). Zooming out, with the following schematic we can see the relavant parts about the morphology and connections of the neurons:

![](/images/barn_owl_neural.png)
*Carr and Konishi, 1990*

We curiously observe that the neural morphologies are disalike on the two sides. On the right, the axons split off at a central location relative to the right NL, and goes into different segments of NL like a canopy span. However, on the left, the axon split off very close to the middle line, meaning that the axons reaching to the far edge of left NL has to be much longer than the part of axon going into the part of NL that is closer to the middle. This asymetry is observed in the counter part of this neuronal pattern, meaning that what is ommitted from this figure for the purpose of clarity, are another clusters of neurons that have its axon split of like a canopy on the left NL and split unequally on the right, just the opposite of what the figure is showing. The next figure illustrates both sets of neurons, on the right side of NL as follows:

![](/images/NL.png)
*Carr and Konishi, 1990*

The ingenious part is that this neural circuits is able to detect the 0.45ms interaural (between the two ears) delay. The axons carry forward neural signals just as electric cables carry forward electric current, and hence it takes time for the signals to travel down the axon, with the time taken proportional to axonal length. Now let us imagine that the auditory signal hits the left ear slightly earlier than the right. The signal at left ear is picked up only by the neuron on the top in the above figure, and the signal at right ear is only picked up by the neuron at the bottom. The idea is that, **different extent of interaural delay will result in the top and bottom signals converging at different blue neurons in the above figure**. Therefore, if we have another set of neurons mapping those blue neurons to different angles, our brain in able to pinpoint the angle at which the signal is coming from. 

In some sense, our brain is trying to solve an inference problem in this context. Given an observed sound signal, our brain wishes to estimate its incoming angle. However, though this method is very smart to circumvent the issue of being unable to directly compute interaural time, it also has its limitations. For example, one thing I could think of is that this implementation is discretizing continuous angles. If we have a mapping between different "blue neurons" and different angles, and we have a limited number of those "blue neurons", then we are only able to pinpoint the direction with limited certainty. Say if we have a total of 360 of those "blue neurons", and the neuron corresponding to 60 degrees (with respect to where we are facing) lights up, we only know that the source ranges from 59.5 to 60.5 degrees. Hence, a little digression here is that, it seems that all that we experienced, though feels continuous, is actually all discrete. We see continuous motion, but what is really happening is that our retina retains its response to photons a little such that snapshots are glued together into continuous motion. That's also how film works. But back to thinking as a Bayesian, the response of our 360 neurons can be interpreted as a discretized estimation of the posterior distribution of the angle.


## 2. Very gentle introduction to statistical learning

I accredit this section to the textbook _Understanding Machine Learning: From Theory to Algorithms_ written by Shai Ben-David and Shai Shalev-Shwartz. I think this is really a fantastically written and organized book and I draw havily on the reference and ideas from the first few chapters of this book when I write this section. Very interestingly, the first chapter about the book is an extremely well written discussion about what is learning. While I am trying to lay out in detail how neuroscientists and statisticians interpret learning, they gave a extremely well summarized overview of the topic, and expecially why we care about machine learning. Hence, I sincerely recommend everyone to read it.

### 2.1 The framework

Here we aim to introduce machine learning problems in generality with formality. We shall refer to our machine as a "learner". This learner might be as complex as a autonomous robot or as simple as a linear regression model, but we shall refer to it as our learner irrespectively. Now we are able to introduce all elements one by one.

- The inputs to the learner:
  - **Domain set**, $\mathcal{X}$. This is the set of where our data is coming from. For example, if we have a classification problem to classify whether an avocado is ripe, then we have all avocados as our domain set. It is usually represented by the space of avaliable features, for example, softness and degree of greenness of the avocado.
  - **Target set**, $\mathcal{Y}$. This is the set of all possible labels. In the avocado example, our target set would consist of ripe, represented by number $1$, and not ripe, represented by number $0$.
  - **Data set**, $\mathcal{D} = \lbrace (x_i, y_i) \rbrace_{i=1}^N$ with $n$ data points. Note that each data point is in the set $\mathcal{X}\times \mathcal{Y}$, consisting of the features and its corresponding true label.

- The output of the learner:      
A function mapping the domain set into the target set, i.e. it outputs a **hypothesis** $h$ with $h:\mathcal{X}→ \mathcal{Y}$. For example, a classifier that classifies all soft avocados as ripe avocados is a valid hypothesis, since it maps softness feature, part of the domain set, to ripeness, the target set. For each learner, it pre-chooses a set of hypothesis, called a **hypothesis class**, denoted by $\mathcal{H}$, that contains all possible hypothesis that the learner is able to choose from.

- Data generation model:        
A model of how data is generated. Formally, we view this as a probability measure of $\mathcal{D}$ over $\mathcal{X}$, let's denote this distribution as $\mu_{\mathcal{D}}$.

- Labelling function (the oracle):      
In some cases, we assume that there is a function that maps data to its ground truth labels, hence a "omniscious oracle". Mathematically, we are saying that there exists a function $f:\mathcal{X}→ \mathcal{Y}$ such that $f(x_i)=y_i$ for all $i$. 

- Measurement for error:
We define error of a hypothesis to be the probability that the hypothesis does not agree with the true labeling function at some point. Moreformally, if we have a subset $\mathcal{A}\subset \mathcal{X}$, with given dataset $\mathcal{D}$ and labelling function $f$, then the error for the hypothesis $h$ is defined as:

$$\mathcal{L}_ {\mu_{\mathcal{D}},f}(h) := \mathbb{P}_{x\sim \mu_ {\mathcal{D}}}(h(x)\neq f(x))$$

One important point to note is that our learner has no knowledge of the data generating $\mu_{\mathcal{D}}$ and $f$. In fact, as we can see, our learner's sole purpose is to learn about $f$.


### 2.2 PAC learning

Interestingly and somewhat surprisingly, PAC learning stands for **Probably Approximately Correct learning**. The idea is that, PAC learning formalizes the ability of a learner to output a "reasonable" hypothesis comparing to the true labeling function under some conditions. More formally, "approximately correct" correspond to the $\epsilon$ parameter, which bounds the tolerance of mistake made by hypothesis $h$ on data points, and "probably" corresponds to the $\delta$ parameter, which controls the probability of the hypothesis making an unacceptable mistake. 

The intuition for PAC learning is that, a hypothesis class is learnable, i.e. a good enough hypothesis $h$ can be chosen to approximate labelling function $f$, if we can find a learning algorithm and select out this $h$ by running the algorithm on finite number of training data. It would be definitely not learnable if even infinite data is no use! More formally, restricting ourselves to supervised binary classification here: (please feel free to skip)

> **(PAC learnability)** If there exist a learning algorithm such that for every $\epsilon, \delta \in (0,1)$, for any $\mu_{\mathcal{D}}$ and $f$, if $\exists h^* \in \mathcal{H}$ such that $\mathcal{L}_ {\mathcal{D},f}(h^* ) = 0$, and if exists a function $m_ {\mathcal{H}}:(0,1)^2→\mathbb{N}$, and by training this learning algorithm on no less than $m_ {\mathcal{H}}(\epsilon, \delta)$ i.i.d. data samples generated by $\mathcal{D}$ and labeled by $f$, it would return a hypothesis $h$ with $\mathcal{L}_ {\mathcal{D},f}(h) < \epsilon$, then we call this hypothesis class $\mathcal{H}$ PAC learnable.

The mysterious function $m_ {\mathcal{H}}$ essentially describes minimal number of training data we need to select out a good enough hypothesis, and hence the name **sample complexity**. A bit more math would show that if the size of our hypothesis class is finite, then the sample complexity depends on the log of the size, and in fact, every finite size $\mathcal{H}$ is PAC learnable!

> **Finite size hypothesis class is PAC learnable**, with sample complexity upper bounded by:

$$m(\epsilon, \delta) \leq \frac{1}{\epsilon}\log (|\mathcal{H}|/\delta) $$


### 2.3 Back to learning as optimization: Empirical risk minimization

Recall that in the last post, we introduced neural network under the topic treating learning as an optimization problem. I wrote about how the most common gradient based optimization methods work and how we calculates those gradients by back propagation algorithm, but we never really ask ourselves: **Is optimizing over training loss the right thing to do?** This is one of the central questions of machine learning. With the tool of statistical learning theory, hopefully we can answer the question of when and how is minimizing training loss a sensible, and more importantly, an useful approach for our learners. 

You might say, well, isn't the question self explanatory? We even call it "training error" and errors are meant to minimized. However, this is not always the case. You might have heard the term **overfitting**, which describes the situation where a trained model achieves very low training error on the training dataset, but does very poorly on the testing dataset. Hence, the story is not a simple one. But let use define training error more formally first. 

Since our learner has no information about the data generating distribution $\mu$ and the labelling function $f$, we subsequently have no access to the true error, which is a function of $\mathcal{D}$ and $f$. Hence, with only the access to the true labels restricted to the training set, we can define the training error, or **empirical risk**, as the proportion of misclassified data points:

$$\mathcal{L}_{\mathcal{D}}(h)=\frac{1}{N}| \lbrace i\in \mathcal{I}: h(x_i)\neq y_i \rbrace |$$

where $\mathcal{I} = \lbrace 1,2,\ldots,N \rbrace$ is the set of indices. The whole learning paradigm that aims to minimize this emprical risk, and hence optimization of it, is termed **empirical risk minimization (ERM)**. Hence, ERM aims to find the hypothesis $h'$ that minimizes training error:

$$\mathcal{L}_{\mathcal{D}}(h') = \min_{h\in \mathcal{H}}\mathcal{L}_{\mathcal{D}}(h)$$

Overfitting is precisely the limitation of ERM. In fact, the restriction to a subset of all avaliable hypothesis, i.e. the definition for a hypothesis class $\mathcal{H}$, is to restrict ourselves the choices of hypothesis such that over-complicated models are not chosen, and hopefully overfitting can be avoided. Hence, we are interested in finding out when performing ERM will not lead to servere overfitting. The short story is that **if the hypothesis class is PAC learnable, then ERM rule works**! How wonderful is that! In fact, the ERM algorithm, i.e. an algorithm that minimizes training error, will be the learning algorithm satisfying the conditions in the definition of PAC learning. 

This provides some justifications for why we would like to reduce training errors. However, we still made a lot of assumptions in our PAC learnability definition and is far from the real life story when we train a neural network.


- - -

Congratulation on reading through this difficult post! I hope my effort of explaining what is learning was illustrative and interesting. Starting next post, we are going into the theme of vision, where both human and machine vision will be introduced and discussed in detail!


