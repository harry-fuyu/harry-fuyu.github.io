---
title: "Neuro & AI (I): Our Brain and Neural Networks"
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

excerpt: "Introduction to neuroscience and neural networks"
header:
  overlay_image: /images/header.jpg
---


Welcome aboard! Here's the agenda for this very first blog post focusing on introducing you to both modern neuroscience and neural networks:
- Brain as the pinnacle of human evolution
    - Brief history of neuroscience
    - Gross neuroanatomy 
    - How is human brain special?
- Introduction to neural network
    - Neural network and its history
    - Rise of deep learning

Exciting! Let's get started!

<img src="/images/MRI.png"> 

## 1. Brain as the pinnacle of human evolution

### 1.1 Brief history of neuroscience

At 3BC, brain is believed as a "cooling device" for the heart, and the first anatomical study of the brain is performed only thousand years later by Leonado Da Vinci, who is extremely interested in human anatomy, produced this annotated drawing of the brain viewed from different angles, as well as some subcortical structures like the basal ganglia on the bottom left. (don't worry! We will revisit and explain all those nouns)

![](/images/da vinci.png)

![](/images/phrenology.png){: width="200px" style="float:left; padding-right:10px" }

\\
Around 1860s, there is a new theory called phrenology that believed different parts of the skull correspond to different attributes of a person, and that one could predict characteristics and personality of others through detecting and analysing lumps and bumps on different locations of the skull. 


On the left depiction, we see that the face is sub-divided into numerous different regions, each corresponding to one aspect for an individual. No matter how ridiculous this sounds, and no matter how well we know that phrenology is pseudoscience, the starting idea and the direction in which we are going towards understanding our brain is surprisingly correct: 

> Different functions are localized in different parts of the brain.        

This idea of function localization is accurate judging from modern neuroscience, which we will talk about very soon.

!["Ramón y Cajal"](/images/cajal.png)
\\
At around the same time, the founding father of modern neuroscience, Ramón y Cajal from Spain, is making his remarkable drawings of neurons. Benefited from the invention of microscopes, Cajal is able to see tissue sections with great detail. His uses different colored inks to denote different types of neurons in the same drawing, and creativly uses darker or lighter shading to denote the depth of neuron within the piece of tissue. In this following one-of-a-kind drawing of the hippocampus of a mouse, Cajal was able to deduce the direction of signal flow just from looking at the shape of the neurons (morphology).           

![](/images/hippocampus_cajal.png)

Now I invite you to think critically on this philosophical point: is it possible to deduce function purely from morphology (shape of neurons) and connectomes (how neurons are connected)? This is largely the job of modern neuroscientists. One ambitious project at Harvard, led by professor Jeff Lichtman, is to use electronic microscopes to image and reconstruct all neurons and their connections within 1 cube millimeter of mouse brain tissue. Brain tissue is sliced into nanometer level thickness using a tiny knife made out of dimond, and sent into the EM on a tape conveyer. 60TBs of image data are produced everyday and the images are collected across half a year! This is a little digression here, but my point is, how much do you think knowing structure and connections would help us in understanding function? (surprisingly, they do tell us a lot! )


### 1.2 Gross anatomy
Next, Max Brodmann published his paper in 1909 about parcellation of different brain areas. Those areas are referred to as Brodmann areas and are still used widely today in scientific papers. For example, the famous Broca's area, which is in charge of language, largely corresponds to Brodmann area 45. 

![](/images/brodmann_area.png)

This drawing's left side corresponds to the front, and drawing's right side corresponds to the back of our head. They way that Brodmann is able to make this parcellation (dividing cortex into different areas) are largely based on cytoarchtectonical criteria:
- histology: What are the shapes of the majority of neurons in the region? Pyramidal? Short body? How are they grouped together?
- laminar patterns:  How are the cortical layers organised?
- connectivity: How deep into the cortex does the neurons project from and into? Is there any pattern in connections?

As you might have guessed, these criteria lack a clear cut off and resulted in ambiguities. Here I would not go deep into details of how the term "area" evolves, but I would like to point out that we should not take the parcellation we have today for granted. When we talk about the lobes and areas of the brain later, I would like you to constantly remind yourself of the effort that scientists have put in to make everything as rigorous as it could possibly be.

As we stare at the map that Brodmann drew for us, let us recall the lesson we learnt even from phrenology, that **distinct cortical regions are functionally specialized**. I have annotated for you this map as below, and let's dive in to different areas!

![](/images/annotated_areas.png)


Firstly, our brain can be roughly divided into four lobes: occiptal lobe (yellow), temporal lobe (light green), frontal lobe(purple), and prietal lobe(the rest:D). 

Starting from th back of our head, we first have the visual areas, which takes up a very large portion of the occipital lobe. The signal from our retina first reach the primary visual area V1 and then propagates in a parallel manner to the higher order visual areas. The spatial information goes in the direction to the top of our head (ventral) into prietal lobe, and this is called the "where" stream, and feature information goes in the direction to the lateral sides of our head (dorsal) into temporal lobe, which is called the "what" stream. We will revisit these when we talk in detail about vision!

Next major area is the somatosensory area, which is colored in dark green. This area is responsible for mainly the sense of touch. Further to the front of the head (rostral), there is motor area colored in red, just one fissue away from the somatosensory area. We will dive deeper into thoses area when we talk about topographical maps in cortical organizations!

The next interesting area is more rostral to the motor area, which is called the pre-motor area. When you run, the neurons in your motor areas are firing tirelessly, but when you are getting ready at the starting line, planning to start running as soon as the pistol fires, it is your pre-motor area firing instead of the motor areas, since its doing all the planning work. 

Finally we reached the frontal lobe which is at the most rostral position. Frontal lobe is in charge of most of the higher order cognitive functions, like moral judgements, emotion, aggressiveness... in short, it gives us our individualities. 

![](/images/subcortical.png){:align="center" width="500"}

Apart from the areas on cortex, there are many other parts of the brain that are even more important to our survival, are hidden under the cortex and burried deep in the center of our brain. These includes the subcortical structures. The basal ganglia regulates our motor functions, and is in charge of dopamine feedback with thalamus.Some diseases like Parkinsons or Huntingtons are due to basal ganglia's inability to regulate effectively. The amygdala controls our fear response. The hippocampus is extremely closely related to memory consolidation and subsequently long term memory. Last but not the least, we have the cerebellum, which is not a subcortical structure but a structure by itself. It in charge of fine motion control, and current research seems to suggest that cerebellum is somehow involved in higher cognitive functions judging from its bilateral connections to the frontal cortices(again, how can we infer function from connectivity patterns?). 

Theses are a super brief view of the anatomy of the brain and the major functions of each areas. There are so many many more details that I wish to share and I promise to unfold them in our subsequent topics!

### 1.3 Why is our brain special?

![](/images/brains.png)

Let's first have a look on the comparison of our brain to the brains of other vertebrates. It is immediately obvious that we have large brains, and our brain has much more and deeper folds. However, the conception that humans have the largest brain on the planet is false. Elephant has larger brain than us!

![](/images/EQ.png)

As you might have guessed, the comparison about size is unfair, we should normalize our brain size with our body sizes. And in fact, we as homo sapiens has the largest encephalization ratio (EQ, formula in figure). As the axis are on a log scale, the difference between human's EQ at 7.5 is a astronomical difference from the 4.0 of Monkeys. 

![](/images/bigger_brain.png)

It is remarkable that our brain size has increased exponentially at about 2 million years ago, as shown in the plot above. Why? How could this be possible?

Let's now take a perspective from evolutionary biology and think about what could be the selective pressure for larger brains? Larger brains are very un-economical for the following reasons:
- Massive recofiguration of skeleton layout is needed.
    - **Firstly, in order to have larger brain, we have to become bi-pedal first**, that is, to walk on two feet instead of walking with hands. This is an essensial prerequisite for larger brain because for non-bipedal animals like dogs or monkeys, their head is attached to the neck on the side instead of sitting right on the spine. The neck is not enough to support large brains alone!
    - Secondly, in order to be bipedal, the entire skeleton must be reconfigured. The curvature of the spine needs a massive change in order to support upper body in the best manner. The shape of feet change, all fingers on the feet become less important and they converge to grow all at the front of the feet instead of to the sides to aid easiness of walking... and etc.
- Larger brain means much more extensive energy consumption. More than half of our energy budget is spent on maintaining the need of neurons in our brain! In the world where food was scarce, why would our ancestor evolve towards this seemingly bad deal that lowers survival chance? 
- Arguable marginal benefits. Although cannot be calculated accurately, but would the benefit of being smart enough to craft a stone spear outweight the inability to obtain enough food sources? 

One huge advantage of bipedalism is that the evolution of brain and evolution of our hands can form a **positive feedback loop**. Since we do not need our hands for walking anymore, our hands are free to do whatever our creativity reaches, and in turn, stimulates more specified connections in our brain across cortices and so on. We became bipedal at about 4 million years go, shortly after which our brain size started growing exponentially! 

![](/images/compare.png){:align="center" width="600"}

The final idea that I would like to introduce before we switch to artificial neural networks is about the proportion of areas on cortex dedicated to sensory, somatosensory and motor systems. We can see that our common ancestor has alsomst all areas on the cortex dedicated to these rudimentory functions, leaving little room for higher order cognitive functions. But for us humans, these areas only takes up little room on our cortex! Our association cortices (those apart from sensory and motor purposes) have expanded disporportionately throughout the course of evolution, and offered us immense opportunities to realize much more complicated functions.


- - -

## 2. Introduction to Artificial Neural Networks

![](/images/nn.png)

### 2.1 Neural Network Basics

I first learnt the existence of neural network(NN) from Dr. Jun Liu's book _Beauty of Mathematics_ , but it took me a while to get its essential idea. To summarize NN in one sentence:

> NN is no more than a function.

To be more specific, NN is extremely flexible such that in theory, we can use it to approximate any function reasonably well, mapping from any space into any space. For example, if we ask a NN to map from image to the probability of the image containing a cat, this NN becomes an image classifier. If we ask a NN to map from user history to what video the user might watch next, this NN becomes a recommender system. If we ask a NN to map a sentence in English to a sentence in French, this NN becomes a translator. 

Therefore there's no magic (Yet!), a neural network is just a flexible function which usually denoted as $q_{\phi}(x)$, (subscript $\phi$ denotes that this NN is parameterized by a set of values called $\phi$), and we name NN as "universal approximator" due to this flexibility. 

-----------------------------------
-----------------------------------
**Mathmatically:** (please feel free to skip this technical portion)

We describe Neural Networks as universal approximators to some reasonably continuous function in the following sense 
> For every fixed precision parameter $ϵ > 0$ and every Lipschitz function $f:\[0,1\]^n →\[0,1\]$, it is possible to construct a network such that for every input $x \in [0,1]^n$ , the network outputs a number between $f(x) − ϵ$ and $f(x) + ϵ$.

The theorem is self-explanatory. For every point of $x$, we are able to construct a neural network $f$ such that $f(x)$ falls within some precision tolerance around the true value of a Lipschitz function at $x$, where Lipschitz basically means that your function's value cannot fluctuate too much within a certain interval, and hence essentially describing continuity.

-----------------------------------
-----------------------------------

Back to NN, what exactly is this function? How can a function approximate any mapping? Now let's dive into components of a NN by looking at the schematic of a typical, fully connected NN as an example.

- **nodes**: each circle is called a node, or an artifical neuron. Each neuron represents a scalar value.
- **weights**: each arrow represents a directed edge between two nodes, and there is a scalar value associated with this arrow called weights.
- **layers**: From left to right, we draw nodes that are in the same layer on the same vertical line for easier visualization. For example, the input layer, which is the first layer, consists of three yellow layers colored in yellow, and the output layer, which is the final layer, is colored in red. All layers in between are called hidden layers.
- **activation functions**: each node has an non linear activation function associated to it. Let's denote an activation function as $\sigma(\cdot)$. 

![](/images/NN forward computation.png){:width="500"}

Now let's see how values of nodes at each layer are computed. Part (a) shows the simplest NN possible: it has n nodes on the input layer, a single output layer, and n weights associated with each directed edge between input nodes and output node. The input layer has values $x_1, x_2, \ldots, x_n$, and the value of the output layer, $y_j$, is computed as taking the the sum of the product of corrsponding input values and weights, and wrap this sum with the non-linear activation function, f. In matrix notation, we have:

$$y_j = f\big (\sum_i w_{ij}x_i\big ) =f\big (W_j^TX\big )$$

Similarly for a more complex NN, such as in part (b), value of each node in the later layer is calculated by taking a dot product between value of nodes in previous layers with weights, and wrapped with its activation function. Hence the complexity grows very fast as the network has more and more layers and hence becoming deeper and deeper. The complexity of the representation (which we will explain in later posts) will soon beyond human comprehension because of this composing operation of non-linear functions.

Hence we could see that the non-linearity is crucial for NN to be an universal approximator. If the activation function is linear, then no matter how deep the NN is, we effectively only have one layer and our ability to approximate is greatly restricted, because the composition of linear functions is still linear.

Okay! We know that non-linear functions are good choices of activation functions, but what are the common activation functions in practice? Let's see some examples:

- **ReLU** (Rectified linear unit). Mathematically:

$$\text{ReLU}(x) = \max(x, 0)$$

What it does is that it mops the negative arguments to zero and keeps positive arguments unchanged.

- **Sigmoid**. The sigmoid function is defined as follows: 

$$\sigma(x) = \frac{1}{1 + \text{exp}(-x)}$$

Note that it flat for input x with large absolute values, but changes very fast around zero. In particular, the convexity changes at zero, but the function is smooth and differentiable everywhere. The value of sigmoid function is bounded between 0 and 1. 
- **tanh**. The tanh function has very similar shape to sigmoid function, except its values are bounded between -1 and 1. 

![](/images/activation_fns.png)

Those are the most common types of activation functions, and there exists many variants. To give us a glimpse into future topics, let's peek into some of the variants for ReLU function. To motivate the need of a variant, we observe that ReLU acivation has the problem that when you differentiate and the input value is constantly below zero, the gradient will be stuck at zero and permits no useful information. (we will comeback to why we need gradient in the next post) To overcome this, "leaky ReLU" is invented, such that the negative values will not be mopped to zero, but follows $f(x) = kx$, with a very small but positive $k$. 

Furthermore, we can adjust threshold of ReLU if we need to. A research group in Alibaba proposed a new activation function called "DICE". It has the same shape as a leaky ReLU, but treat both the threshold and the slope k as trainable parameters. (and we will come back to what does trainable mean and what is trainable soon!)

Now let's revisit the idea of NN as a universal function approximator. We use the word expressiveness to describe how well a neural network can approximate any function. With the composition of those non-linearities, the wider (more number of neurons within one layer) and the deeper (more number of layers in NN) the neural network has, the network will be more expressive. (Question: is higher expressiveness always desirable?)

### 2.2 History of neural network
Although neural network only started to recieve overwhelming attention in the past decade, the idea itself is almost 80 years old! Here's a brief timeline that I put up on the history of NN:
- 1943 McCulloch & Pitts came up with a math model describing neurons
- 1958 Rosenblatt invented perceptron, which is the oldest NN still in practical use
- 1959 Widrow & Hoff invented ADALINE & MADALINE, first NNs in application

-----------------------------------
- 1981-1982 No one is doing NN research, literally...

-----------------------------------

- 1994 Yann LeCun invented LeNet, the first convolutional neural network (CNN)
- 1997 Invention of RNN and LSTM 

-----------------------------------
- 1998-2010 No one is doing NN research, again... well, almost no one...

-----------------------------------

- 2012 AlexNet slammed record on ImageNet challenge!
- 2012 onwards: ResNet, VGG, Inception, GoogleNet..... (A zoo of deep learning models!)

Therefore, neural network is a very old idea instead of a new one! So what can be the application, and why has it only become popular in the recent years?

### 2.3 Rise of deep learning
Before AlexNet emerged victorious in the ImageNet challenge in 2012, scientists are all squeezing their head, trying to use feature engineering based or kernel based method for image classification. Hand picking features and improve them would certainly work and improve model performance, but the improvements came gradually at the rate about $2%$ per year. However, AlexNet improved the classification performance by about $10%$ at once, achieving what should have been done in 5 years time, and thus rocked the world of computer science. Here's a plot of what was after AlexNet, and how deep learning model finally caught up with human performance in 2015.

![](/images/imagenet_acc.png)

So, the natural question is: what did AlexNet do differently, and why now, not even 20 years earlier with LeNet?

For the first question, AlexNet used a general convolutional neural network structure, which we would comeback and visit soon in later posts. It is wider, deeper, more sophisticated, and subsequently, much more expressive than before. Therefore, it is capable of approximating and capturing the extremely hard-to-find correlations between features in images and their categories. 

For the second question, I think there are mainly two reasons:

Firstly, we thank the team that made ImageNet possible. ImageNet is a massive dataset that includes one million images of objects from vastly different categories. Back in it's time, it was legendary for the following reasons:
- All labels are done manually. The team uses Amazon MTurks to outsource the labeling process to the public. Each photo is labeled by multiple individuals and cross validated. For extremely hard photos to classify, e.g. a specific dog breed, the team actually asked relevant expert to do the labeling.
- Instead of a flat label structure, the dataset has a innovative hierachical labelling system. For example, a dog photo would not only get a label dog, but actually as animal -> dog -> chuwawa.
- This dataset is massive. Later in the post we will talk about model training in more detail, but the catch is that if we would like to train a more complicated, i.e. more expressive model, we will have more numerous parameters to train, and subsequently need much more training samples, otherwise we would encounter the problem of overfitting, where the model does great on training data but does not generalize. ImageNet with a million images, helped us mitigated this problem when training AlexNet.

Secondly and even more predominantly, is the phenominal increase in avaliable computing power. Recall the equation when we propagate values forward written in matrix form:

$$\mathbf{y} = f(\mathbf{W}^T\mathbf{X})$$

During training, a lot of matrix multiplication need to be completed (in both forward and backward pass, we will revisit this), and we know that matrix multipication, when done naively, has the complexity of $O(n^3)$ (the best runtime can be achieved is around $O(n^{2.373})$, with very smart and complecated algorithms). This basically means that the time we need to compute the product of two two dimensional square matrix with $n$ rows scales with the cube of $n$, which increments extremely fastly. Now imagine that you have one million neurons in a layer and your weight matrix is a million by million! The amount of computation is beyond imagination and traditional CPUs simply could not handle these computations. 

Luckily, GPUs, which we used for graphic rendering in games are designed to handle matrix multipications. In 2010, with some tricks, we found a way to interface with the GPU, actually training deep learning models on them and accelerating training process significantly. Here's a photo of NVIDIA's GPU. Up to my knowledge, only NVIDIA's GPUs are compatible with deep learning frameworks. (Maybe a good idea to buy NVIDIA's stocks?)
![](/images/NVIDIA.png)


Before we end this first post, I would like to elaborate more on some applications of deep learning that are already influencing our daily lives! Recall that we mentioned a neural network is a function that can map from any space to any other space, hence here I made a non-exhaustive list of some applications:

- Computer vision
    - Image classification (we will go into details): mapping image to class probabilities
    - Object tracking: mapping image to object location bounding box
    - 3D reconstruction: mapping 2D image to 3D rendering
    - Depth detection: mapping faces to probability of a real person instead of photo
    - Image caption generation: mapping image to a sentence
    - $\vdots$

- Sequence modelling
    - Natural language processing
        - Translation: mapping sentence to sentence in another language
        - Text understanding: mapping text to one sentence
    - Time series modelling
        - Finance models: mapping past data to potential future data
    - Music classification and rendering
    - $\vdots$

Combining those basic techniques, we can build much more sophisticated DL systems. For example:
- Recommendation systems
    - Use collaborative filtering with CNN
    - Treat user history as a sequence
    - $\vdots$
- Automated vehicles
- AI radiologist
    - Mainly image related DL techniques, but with much higher precision
- AI scientist
    - DL methods for foundational science research. e.g. Posterior density estimation
    - DL models that predicts molecule affinities and accelerates drug discovery
    - DL models that can write codes automatically

And many many more! 

Good job in reading through the first post in the series! I hope that you have now gained a general idea about our brain and neural nets:) Next time we will discuss what does learning mean both for neurons and for neural networks!