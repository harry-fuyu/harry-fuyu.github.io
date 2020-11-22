---
title: "Neuro & AI (III): Classification: Understanding Representation"
comments: true

toc: true
toc_label: "Table of Contents"
toc_icon: "cog"

categories:
  - Neuro&AI
tags:
  - Neuroscience
  - Machine Learning
  - Learning Theory

published: true

excerpt: "Biological bases for feature representation and intro to classification algorithms "
header:
  overlay_image: /images/header2.png
---

<!-- ### III. Classification: understanding representation
- Representation in human
    - Correct classification requires forms of representation
    - Firing patterns of neurons as representations of concept
    - Topographical maps in cortical organization
- Classification with algorithms
    - Decision boundary: goal of classification
    - Metric for performance: Confusion matrix
    - Perceptron algorithm
    - Feature engineering
    - Demo: TensorFlow playground
    - Extension: Shattering -->

Welcome and congratulations on making it through to the third major topic of the series about classfications. Classification is one of the earliest, most classical, and extremely widely carried out machine learning task that has profound influences, and it is also a task that we perform second to second in our daily lives, either consciously or even subconsciously. When we are driving, it is essential for us to be able to tell apart cars from pedestrians, red traffic light to green ones. Taking it further, our decision making process could be classified as a classification task too: whether it is safe to press the gas pedal translates to the problem of classifying current scenarios faced into safe ones and risky ones. Therefore, it is essential for us to not only talk about how we make classifications, but more about **what enables classification**. Towards this end, we are going to explore the concept of **representation**, both in the realm of neuroscience and machine learning.

## 1. Representation in human

![](/images/catanddog.png)

### 1.1 Necessity of representation as a template

Imagine the scenario of your boss wanting you to find Bob on the busy morning street of New York. To find this Bob, you must ask yourself first: how does Bob look like? You guys might have met at the firm's cocktail party once or twice, but you had a deep impression about his appearance. You recall that Bob is around 50 years old, a little bit bold and always wears a black leather jacket. I'm running out of my literary juices here, but the point is that, this description is a representation of Bob, and more specifically, how your brain represents Bob. After having these descriptions, essentially you are performing multiple template matching problem on the street of New York: every time you see a man, you would compare it against Bob's representation that serves as a template, and look for a close match, essentially classifying each pedestrians as "Bob" and "not Bob".

Through this little story we can see that **if we were to be able to correctly classify something, we need to understand what that thing is first, and our understanding comes in the form of representation.** Here is another example, when we are trying to identify the cat among the "sea" of owls.

![](/images/catowl.png)

To successfully find the cat, we have to look for the features that are exclusive to cats, and exclude those objects matching the exclusive features of owls.

- Unique cat features: wiskets, four legs, two triangular ears
- Unique owl features: wings, sharp beak, talons

With those features, we have successfully formed the templates for cats and owls in our brain. So, have you found our cat?

### 1.2 Neural representation: firing pattern

Now a more interesting is: **how does our brain store this representation?** There are a lot of possibilities, and the reality will definitely be far more complicated than the story that we are going to see, but I would like to propose the simplest possible case where our brain will be able to successfully store the representation of cats and owls, and avoid mixing them up.

Let's think of neurons abstractly as nodes drawn in circles, and axons connecting between neurons will be lines between nodes called edges. In this way, we think of a neural circuit abstractly as graphs. Let each neuron represent a **binary feature**, denoting the presence or the absence of that corresponding feature. For example, the neuron representing sharp beaks would have value $1$ (neuron is firing) if an owl is seen, and have value $0$ (neuron is silent) if a cat is seen. Here is a graph for this much simplified neural circuit.

![](/images/catowlfeatures.png)

When a cat is seen, the cat features will light up:

![](/images/cattemplate.png)

When an owl is seen, the cat features will light up:

![](/images/owltemplate.png)

Hence, we only need to have another set of neurons that associates this **entire firing pattern** with corresponding categories, then we can automatically perform classifications whenever we see something! Although this is a much simplified scenario, it nonetheless illustrates how powerful and useful it is to store representations as neural firing patterns.


### 1.3 Topographical maps

A large part of the surface of our brain, i.e. the cerebral cortex, is organized in a manner such that neurons in adjacent parts on the cortex are responsive to adjacent spaces of the stimuli. In other words, there is a (mostly) continous mapping from the world to the representation of neurons on our cortex topographically, and this mostly happens for our sensory systems. We hence call it a **topographical map**. 

#### 1.3.1 The visual map

![](/images/topography_visual.png)

<!-- 
![](/images/newton_topography.png)

#### 1.3.2 The Homunculus: the somatosensory map

![](/images/somatosensory.png)

![](/images/homunculus.png) -->