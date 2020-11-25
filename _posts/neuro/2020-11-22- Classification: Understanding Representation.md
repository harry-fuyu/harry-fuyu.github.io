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

published: true

excerpt: "Biological bases for feature representation and introduction to classification algorithms "
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

Welcome and congratulations on making it through to the third major topic of the series about classfications. Classification is one of the earliest, most classical, and extremely widely carried out machine learning task that has profound influences, and it is also a task that we perform second to second in our daily lives, either consciously or even subconsciously. When we are driving, it is essential for us to be able to tell apart cars from pedestrians, red traffic light to green ones. Taking it further, our decision making process could be classified as a classification task too: it is viable to treat the problem of "it is safe to press the gas pedal" as the problem of "classify current scenarios faced into safe ones and risky ones". Therefore, it is essential for us to not only talk about how we make classifications, but also about **what enables classification**. Towards this end, we are going to explore the concept of **representation**, both in the realm of neuroscience and machine learning. 

Specially, I would like to dedicate my thanks to Dr. Randy Buckner, who showed me so many great ideas in our neuroanatomy class and inspired me in so many ways, much pertaining to the first section of the post.

## 1. Representation in human

![](/images/catanddog.png)

### 1.1 Necessity of representation as a template

Imagine the scenario of your boss wanting you to find Bob on the busy morning street of New York. To find this Bob, you must ask yourself first: What does Bob look like? You guys might have met at the firm's cocktail party once or twice, but you had a deep impression about his appearance. You recall that Bob is around 50 years old, a little bit bold and always wears a black leather jacket. I'm running out of my literary juices here, but the point is that, this description is a representation of Bob, and more specifically, how your brain represents Bob. After having these descriptions, essentially you are performing multiple template matching problem on the street of New York: every time you see a man, you would compare it against Bob's representation that serves as a template, and look for a close match, essentially classifying each pedestrians as "Bob" and "not Bob".

Through this little story we can see that **if we were to be able to correctly classify something, we need to understand what that thing is first, and our understanding comes in the form of representation.** Here is another example, when we are trying to identify the cat among the "sea" of owls.

![](/images/catowl.png)

To successfully find the cat, we have to look for the features that are exclusive to cats, and exclude those objects matching the exclusive features of owls.

- Unique cat features: wiskets, four legs, two triangular ears
- Unique owl features: wings, sharp beak, talons

With those features, we have successfully formed the templates for cats and owls in our brain. So, have you found our cat?

### 1.2 Neural representation: firing pattern

Now a more interesting question is: **how does our brain store this representation?** There are a lot of possibilities, and the reality will definitely be far more complicated than the story that I am going to share, but I would like to propose the simplest possible case where our brain will be able to successfully store the representation of cats and owls, and avoid mixing them up.

Let's think of neurons abstractly as nodes drawn in circles, and axons connecting between neurons as edges (lines) between nodes. In this way, we think of a neural circuit abstractly as a graph. Let each neuron represent a **binary feature**, denoting the presence or the absence of that corresponding feature. For example, the neuron representing sharp beaks would have value $1$ (neuron is firing) if an owl is seen, and have value $0$ (neuron is silent) if a cat is seen. Here is a graph for this much simplified neural circuit.

![](/images/catowlfeatures.png)

When a cat is seen, the cat features will light up, and when an owl is seen, the owl features will light up:

![](/images/combined.png)

Hence, we only need to have another set of neurons that associates this **entire firing pattern** with corresponding categories, then we can automatically perform classifications whenever we see something! Although this is a much simplified scenario, it nonetheless illustrates how powerful and useful it is to store representations as neural firing patterns.


### 1.3 Topographical maps

A large part of the surface of our brain, i.e. the cerebral cortex, is organized in a manner such that neurons in adjacent parts on the cortex are responsive to adjacent spaces of the stimuli. In other words, there is a (mostly) continous mapping from the world to the representation of neurons on our cortex topographically, and this mostly happens for our sensory systems. We hence call them **topographical maps**. 

#### 1.3.1 The visual map

We know that when a photon hits the retina, the retinal ganglion cells conduct the signal up into the brain through the visual canal to thalamus, and then to the **primary visual cortex (V1)** in the occipital lobe sitting at the back of our head. We will discuss the anatomy in detail in the next post, but the idea here is to realize that cells in the primary visual cortex, as well as cells in other areas in the first few visual areas on the cortex up the hierachy, are only responsive to stimulus in a small area in our **visual field**, which is the total range of the world that we are able to see. This small area is a property of that specific cell, called its **receptive field**, and the sensory neuron, in our case a cell in the primary visual cortex, would be ignorant for whatever that is happening outside its receptive field.

Hence, as the visual cortex is topographically organized, we must have that **the cells adjacent to each other in the visual cortex having adjacent receptive fields** too. Here is an illustration called **visualtopic map** of how our visual field maps out onto our brain by the wonderful neuroscientist Dr. Marcelo Rosa:

![](/images/topography_visual.png)
_M.G.P.Rosa,Braz J Med Biol Res, Vol 35(12), 2002_

In A, we see that V1 and V2 are located at the back of the head (caudal is the anatomical directional term), and specifically, we see that V1 and V2 are illustrated to have clear cut boundaries defined by solid black lines. This clear boundary is shown by thick black dotted lines in B. The left of B is an illustration for an unfolded visual cortex, and the right of B is its corresponding visual field positions, and line types matches to show corresponding locations. We see that there is a star at the right of the unfolded cortex, corresponding to the center of our visual field. Expanding out from the horizontal white dotted line upwards and downwards on the unfolded cortex corresponds to rotating towards the vertical mid line in the visual field. When it reaches the boundary of V1, the direction flips and we would find ourselves in V2, and going upwards or downwards in V2 on teh unfolded cortex would instead corresponds to going back to the mid horizontal line. In fact, this flip is how neuroscientists identify the boundary of V1 and V2. The only discontinuity comes from the periphery of the unfolded cortex, where the entire parameter, as well as the middle horizontal line, would need to be integrated to form the middle horizontal line in the visual field. Upper in the visual hierachy, more and more complex integrations like this are involved, and it is amazing that what we perceive is a single piece of vision, with no overlaps and gaps!

![](/images/newton_topography.png)

To add more spices to this story of topological mapping, we see that the map is distorted in the above figure, and realize that **different areas in the visual field is represented disproportionately on the cortex**, and the center of the visual field which corresponds to the fovea on our retina has much larger surface area and hence neurons on the cortex dedicated to it. If we were to find the corresponding neurons that fire when we see the face of Issac Newton, we will see a inverted, distorted face centered at the most caudal part of the occipital lobe.

#### 1.3.2 The Homunculus: the somatosensory map

Apart from visual representations, our somatosensory system also has topographical representations. Above is an illustration of the correspondence between positions on the somatosensory cortex and its responsible body parts. Note that the hands, face, tongue has disproportionately large representations on the cortex. 

![](/images/somatosensory.png)

Another interesting point is about the symmetry as well as the asymmetry. We see that since we have two hands, two feet and so on, the representations are mostly symmetrical. The asymmetries, however, are more intriguing. 
![](/images/homunculus.png){: width="300px" style="float:left; padding-right:10px"}
For example, the parts corresponding to vocalization function is almost all on the left hemisphere (corresponding to the right side of this figure), which is reasonable, since the language related regions (Broca's, Wernicke's) are exclusively on the left too. If we were to draw a little man figure that has body parts proportional to its area of representation, we would have gotten this interesting homunculus figure on the left.

## 2. Classification with algorithms

![](/images/classification.png)

### 2.1 Feature and decision boundary

Let us imagine a naive method of performing classification according to some criterion in our former case of classifying cats and owls. First, we decide on some cat features and owl features, combine them into a feature vector for each of the cat and owl photos that we have (our dataset). For example, let us assume that we have the following four features: body length, size of eyes, pointy-ness of mouth and presence of feathers. 

(Note that some features are discretized, meaning that it can only take few plausible values. For example, presence of feathers is such a discrete feature, and it is binary, because an object either has feather, corresponding to a $1$, or does not have feather, corresponding to a $0$. On the other hand, some features take on continuous values. For example, body length is such a continuous feature. However, it is always possible to treat continuous features as discrete ones by grouping into bins. For example, we can make body length less specific by using the bins of short, medium and tall.)

Now, for each object that we see, the algorithm transforms it into a set of measurements corresponding to each feature. By putting each feature as a dimension (an axis) and forming a **feature space**, each object can then represented by a **feature vector**. For example, the feature space of body length, size of eyes is two dimensional, and the plot of eight hypothetical feature vectors are shown as follows:

![](/images/bad_feature_space.png)

For this binary classification problem, what we would like to have is to draw a **decision boundary** that could separate the two categories, and declare all points on one side of it as cats and all points on the other side to be owls. In the above illustration, with the green decision boundary, we are saying that every point above the line should be cats(blue) and everything below should be owls(red). These points are purely hypothetical, but the interpretation here, if those measurements are true, is that cats tend to have larger eyes and longer bodies than owls.

We notice that there are two **misclassified** points marked out by purple boxes. In fact, in this scenario, (let's restrict ourselves to the linear case first) it is impossible to draw a straight line that separates the red and blue points! The crucial point here is that the separability of feature vectors depends heavily on which features we use. Consider the alternative feature space with pointy-ness of mouth and presence of feathers drawn as follows:

![](/images/good_feature_space.png)

Note how well the same colored points are clustered together! This is because the two features here better distinguishes the two categories, and hence a straight line can easily be drawn such that the two categories can be separated perfectly. We call the case where this is possible as **linearly separable**. In the previous feature space, the two categories are not linearly separable.

Therefore, we can now have a better understanding of what neural networks are doing. Each neuron represents a feature, and through training, although the features that the neurons represent are not easily interpretable, the neurons nonetheless finds and represent useful features that can tell apart categories and enhance the network's discriminative power, such that the resulting feature vectors of different categories are more far away from each other! Essentially, **neural network is trying to approximates the function that transforms the space into one in which the feature vectors are more (linearly) separable**.

### 2.2 What is a good classifier?

We always have to ask ourselves: what is good? In this case, what is a good classifier? How do we evaluate the performance of a classifier?

When I first started my research, I was terribly ignorant about what I am trying to convey to you now, that **accuracy is NOT a good metric**. A good classifier should be able to truely tell apart cats from owls, not merely by guessing. However, if we just focus on whether the classifier can get all cats right, what the classifier should do to maximize this accuracy is to simply classify everything it sees as cats, because that would confirm $100\%$ accuracy on cats. However, this classifier gets all owls wrong, and hence in fact, shockingly yet reasonably, has zero discriminative power.

Towards finding a good metric, consider the following four possible senarios, treating cat as our positive target: a cat correctly labeled as a cat (True Positive); a cat incorrectly labeled as an owl (False Negative); an owl correctly labeled as an owl (True Negative); and an owl incorrectly labeled as a cat (False Positive). A good classifier would love to maximize TP and TN, while minimizing FP and FN. We can also see that our naive classifier saying all the time gets $100\%$ TP, but at the same time $100\%$ FP. 

Hence, as you might have sensed, no lunch comes for free, and we must trade an increase in TP with some increase in FP! The question is, how much FP do we have to compromise for a increase in TP, and how do we minimize it? The following illustration would be very helpful to see this compomise:

![](/images/ROC.png)

In the case where positive and negative examples are not separable, we have to draw a cutoff threshold (a one dimensional decision boundary to simplify things) and say that everything beyond the threshold should be classified as positive and everything below it negative. However, in order to increase TP, we have to decrease the threshold such that more positive examples can be at the right of the threshold, but by doing so, we inevitably allowed more negative examples to the right of threshold too, and there is no work around! 

Depend on the situation, we might have different attitudes towards having FP. For example, if radar shows anomaly, the military base better prepare itself, because it's better to be safe than sorry! In this case, FP is greatly tolerated, but FN of not detectly enemy threat could be detrimental and extremely costly. However, in other real life examples, hasty indictions might lead to FP, jailing innocent citizens, and should be avoided at all costs.


### 2.3 The Perceptron algorithm

![](/images/perceptron.png){: width="350px" style="float:left; padding-right:10px"}
Here we introduce the classical perceptron algorithm as promised in the first post. Please feel free to skip this part, since there's math piling up here. The take away message is that, although the name perceptron certainly sounds like advanced tech from the Star War, it is only a single layer neural network with one output neuron and a step activation function (as manifested in the sign operation later), with its structure as shown on the left. It is the first applicable algorithm involving neural network, and was invented back in 1958 by Frank Rosenblatt.

Denote our $i$th data point out of a total $N$ data points to have the feature vector $s^i = (s_1, s_2, \ldots, s_K)^T$ with its corresponding label $y_i$. Note that the labels take on binary values from $-1$ and $1$. Denote the weight from $s_j$ to the output node $T$ as $w_j$, and the entire weight vector is $w = (w_1, w_2, \ldots, w_K)^T$, such that the output will be 

$$T^i = \sum_{i=1}^K w_js^i_j = w^Ts^i$$

To make a prediction, we pass the feature vector through this network and use the sign of $T$ as the predicted label, that is,

$$\hat{y}_i = sign(T^i) = sign(w^Ts^i)$$

The critical observation here is that **if the prediction is correct, then the product of $y \cdot \hat y$ must be positive**. (If true label is $-1$, and predicting $-1$ and if true label is $1$ and predicting $1$) Hence, if the classification is wrong, $y \cdot \hat y < 0$, and we add/subtract scaled version of the current data point to the weight, i.e.

$$w^{(t+1)} = w^{(t)} + \eta y^is^i$$

This will result in the new prediction:

$$\hat{T}_i^{(t + 1)} = (w^{(t+1)})^T s_i = (w^{(t)} + \eta y^is^i)^T s^i = \hat{T}_i^{(t)} + \eta y^i(s^i)^Ts^i$$

This is because if we miss classified things as negative, then true label $y_i=1$, with $(s^i)^Ts^i$ positive since its sum of squares from a dot product, $\hat{T}_i^{(t + 1)}$ is more positive than $\hat{T}_i^{(t)}$, moving toward the right direction. (recall that $\hat{y}^i = sign(\hat{T}_i)$)

The constant $\eta$ is called **learning rate**, a concept which we mentioned before in the introduction of gradient descent. Here it also controls how fast we learn from misclassfied samples. Note that in this example, the decision boundary is linear and it goes through the origin (why?), hence an update would corresponds to the rotation of decision boundaries. A good leanring rate must be chosen, such that it does not rotate too much and result in faster and better convergence. Summarizing our algorithm:

Here is a solid example with specific numbers, and I have worked out for you each update. We have three negative examples in blue $(-1,1), (-2,-3), (0,-2)$ and three positive examples in red $(1,2), (2,3), (3,-1)$. We fix learning rate at $\eta = 0.7$ and we get the correct boundary in only two updates:

First we pick $s^1 = (-1,1)$, note this choice is random.
![](/images/perceptron1.png)

Note that the decision boundary marked in light green is rotated towards the right and towards $(-1,1)$. Next we update on $s^2 = (3,-1)$.
![](/images/perceptron2.png)

And just by that all points are now classified correctly!
![](/images/perceptron3.png)

To show that the algorithm converges is much more work, but the good news is that it can be proven that if the dataset is linearly separable, that by running the above update rules, it is garanteed that the perceptron algorithm will eventually converge to the right solution.


### 2.4 Feature engineering

As we have seen, the perceptron update rule is simple and effective. However, its convergence garantee only depends on the premise that the data is linearly separable. From section 2.1 we have discussed that the choice of features is extremely important to obtain a linearly separable feature space. 

Before the time of neural network, the main focus of research is to hand design features such that classification rules such as perceptrons can be more easily applied. With neural network, this task becomes automated through backpropagation and updating using gradients. However, the importance of feature selection can still be illustrated with this wonderful visualization tool: [googles tensorflow playground](https://medium.com/@fu_yu_6553/https://playground.tensorflow.org/#activation=tanh&batchSize=10&dataset=circle&regDataset=reg-plane&learningRate=0.03&regularizationRate=0&noise=0&networkShape=4,2&seed=0.73380&showTestData=false&discretize=false&percTrainData=50&x=true&y=true&xTimesY=false&xSquared=false&ySquared=false&cosX=false&sinX=false&cosY=false&sinY=false&collectStats=false&problem=classification&initZero=false&hideText=false)! Positive and negative examples are colored differently, and the thickness of connections is proportional to the magnitude of the corresponding weight:

![](/images/playground1.png)

In the above simplistic case where data is clearly linearly separable, only a single layer network with two features $x_1$ and $x_2$ would produce the right result. However, in the following complicated case, we are not quite able to achieve good classification performance:

![](/images/playground2.png)

However, if we simplify the structure of the network and reduce some features used, very good decision boundary can be learned:

![](/images/playground3.png)

Hence, the moral of the story is that the entire process is still a process of trial and error. It is extermely hard to pinpoint what is the suitable number of hidden layers and what kind of features are the best to use. We will discuss more about the heuristic aspect of deep learning soon when we discuss more about model training!

- - -

Thanks again for reading! With the new understanding of representation, we are ready to dive into human and machine vision, and finally talk about exciting concepts like the convolutional neural networks, and how machines see things differently than us! After introducing the common deep learning models, we can revisit the problem classification, and have a post with actually implementations!
