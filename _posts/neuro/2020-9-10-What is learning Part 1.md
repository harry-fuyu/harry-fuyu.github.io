---
title: "Neuro & AI (II): What is learning? (Part 1)"
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

excerpt: "Interpretation of learning in neurons and neural networks"
header:
  overlay_image: /images/header.jpg
---

Welcome to the second post in the series of Neuro & AI! This post covers one of my favorite topics, and to some extent even philosophical, about what the process of learning is. When we were kids and we were trying to learn how to ride a bike, what is the process going on in our brain? Is this process different when we associate a newly seen word "bike" to the object in front of us with two wheels? 

We mentioned several times even in the first post, and you might have known that neural network needs to be trained. If we were to teach the network, how is the network learning? What information, in what form, is retained during its learning? 

We are also interested in two philosophical points: (Will be in part 2)
-  We will dive deeper in to statistics and talk about learning from a Bayesian perspective. We would first understand what is Bayesian thinking, and I will try to convince you that in the Bayesian world, learning is purely about updating conditional probabilities we call posterior. From here, we are heading into another major philosophical theme, which is that perceptions done by the brain can be treated as a statistical inference problem. (we will definitely discuss this in more detail in later posts)
- How is learning in human brain different from learning in neural networks? On which abstraction levels are they similar, and on which level are they not? From this discussion, we are heading into one of the philosophical themes of the blog post series, which is about whether making neural networks more similar to human brains would always be beneficial for model performance.

If you can't wait to find out to some of the questions above, great! Let's dive right into it!

## 1. Learning in the brain

![](/images/aplysia.png)

### 1.1 Neuron 101: Cell structure and chemical synapse

Neuron is a very special type of cell that is in charge of signal transmission. The estimate is that our brain contains about 80 billion neurons (that's right, $8\times 10^{10}$), which is an astronomical number! Neurons varies in their shape, which we call morphology, but they all have structures in common. Let's look at those structures in the direction of signal flow.

![](/images/neuron_structure.png)

Chemical signals from the preceeding neuron are captured by **dendrites**, which are usually short, tree like structures around the body, which is the **soma** of the neuron. The chemical signals are processed and transformed into electrical signals, integratd over all dendrites to see if the total activity level received has exceed the **threshold** for the neuron to initiate the process of passing down this signal to the proceeding neurons. If the threshold is exceeded, the electric signal will be passed down along the long **axon** towards its ends, which are called **synaptic terminals**. Around axons, there are node like coverings like structure called **myelin sheath**, they facilitate and accelerate propagation of signals along the axon by boosting electrical resistance of the cell membrane.

How the signal is generated within the neuron is not the focus of this post, though it is achieved by manipulating Sodium and Potassium ion fluxes and resulting changes in electrical potentials across the membrane. However, despite the details, I hope that you could understand the following concepts:

- Signal transmissions within a neuron on an axon is electrical, where as signal transmissions across neurons are chemical.
- Neuron has a threshold. If activity exceed threshold, the neuron passes down the signal, if not, signal ends within neuron.(Humm which function does this threshold thing remind you of? Can you see the motivation for that function?)

At synaptic terminal, the neuron makes a connection onto the next neuron's dendrite, and this connection is called a **synapse**. At a chemical synapse, electrical signals are converted into chemical ones. I specically called it a chemical synapse instead of synapse, because there exists (rarely) electrical synapses. Those neurons with a electrical synapses directly pass down the electrical signal, without the need of changing the signal type back and forth. The pros is that the signals can be transmitted a lot faster this way, but the critical cons is that electrical synapses does not offer room for **synaptic modulation**, which is the external control of how strong the synaptic connection is, which is absolutely essential for learning, as we will see soon.

![](/images/chemical_synapse.png)

I will outline how the synapse works in a chemical synapse. I decide to write everything out in fine details because it would really help you understand the biological basis of learning, so I kindly ask you not to skip the next few paragraphs.

After the electrical signals reaches the synaptic terminal, the signal (very positive electrical potential, which we call **depolarization**) will trigger the opening of a gate for Calcium ions. Since each Calcium ion has two positive charges, it forms a positive feedback for influx of more Calcium ions. The rise in Calcium ion concentration triggers the release of **vesicles**. The vesicles starts to fuse with the **presynaptic membrane**, which is the cell membrane on the previous neuron facing the signal recieving neuron, and release its contents, which are called **neurotransmitters**. Neurotransmitters are molecules that can be received by **receptors** on the **postsynaptic membrane** on the signal recieving neuron, and some examples would be dopamine, acetylcholine and glutamate. 

The stronger the electrical signal arriving at the synaptic terminal (encoded in frequency of depolarization), the more vesicles will be released, the more neurotransmitter will be received by the next neuron, which will induce a stronger chemical signal in the post synaptic neuron, which has a higher chance of reaching the threshold and start passing down the signal one after another.


### 1.2 Neurons: Short term learning by changing synaptic efficacy

Finally we are equipped with the jargons and concepts to talk about learning. Learning can be very broadly categorized into short term learning and long term learning depending on how long they last. Short term learning does not involve structural change, but rather a change in synaptic efficacy. The effect usually last by on the order of seconds or minutes.

So how can the transient change in synaptic strength be achieved?

#### 1.2.1 Method 1: Releasing vesicles

As previously mentioned, the vesicles in presynaptic terminal that contains neurotransmitters. If there are more vesicles released from the presynaptic terminal, more neurotransimitter molecules would be released into the space between the pre- and post- synaptic terminals called the **cleft**, causing the concentration of those molecules in the cleft to increase. As the concentration rises, there is a higher chance for the receptors on postsynaptic membrane to catch a floating neurotransmitter molecule and cause a small depolarization in the postsynaptic terminal. Hence, releasing more vesicles can definitely elicit a stronger response from the postsynaptic neuron, thereby enhancing synaptic strength, but only temporarily, since the access neurotransmitters can be recycled by presynaptic terminal or diffuse into other places are are lost.

#### 1.2.2 Method 2: Facilitation

After the previous depolarization in the postsynaptic terminal, the electrical potential there would go back to its original state due to ions diffusing down their concentration gradient in and out of the postsynaptic cell. This means that the potential would decrease down slowly until it reaches the equilibrium at around -70mV, which is called the **resting potential**. This subsidizing process is slow: imagine a cup of hot tea set on a table in room temperature. The tea would cool down very fast at first, but the process of cooling slows down as the temperature of the tea gets closer to room temperature. Same thing happens here in the neuron, as the electrical potential restores towards the resting potential, the process of getting there gets slower. 

Hence, facilitation happens when another small depolarization happens before the previous depolarization has fully subsided, resulting in the second depolarzation to reach a more positive potential than the neurotransimitters could ever contribute, by piggy-bagging on the first depolarization. Here is a graphical illustration.

#### 1.2.3. (passive) Method 3: Vescicle depletion

As vescicle fuses with the presynatic membrane, more and more vescicles are being produced at another site by cutting off the infolding of the presynaptic membrane. In the situation where stimulus arrives quickly in succession, the speed of vescicle regeneration lag behind the rate of vescicle release, resulting in less vescicle fusions and less neurotransmitter release than it should have been. This passive mechanism would hence decrease the synaptic strength temporarily. If we allow a short period of time for the vescicles to regenerate, this effect would be no longer in place.

### 1.3. Long term learning by structrual change

#### 1.3.1 Hebb's postulate
Hebb's learning rule describes how structural change should be directed by learning activities. It can be stated succinctly in the following two sentences:

> Fire together, wire together.

> Out of sync, unlink.

This sentence states that the neurons firing simultaneously should have a permanent increase in synaptic strength, because the synchronization has a functional relavence, and the second statement states the opposite direction. Hebb's rule has direct biological evidence from neuron recordings, that the aquisition of new skills are achieved by the synchronized firing of a pattern of neurons.

- - - 
##### Mathematical formulation

Mathematically, if two neurons have activations $x_i$, $x_j$, then the weight $w_{ij}$ connecting those two neurons should have the value:

$$w_{ij} = x_ix_j$$

This says the the weight between two neurons are directly proportional to the activation of both neurons, elegantly capturing the idea of Hebb's postulate. This learning rule for the value of weights is called the **Hebbian learning rule** in computational neuroscience.

- - - 

#### 1.3.2. Long term potentiation (LTP)
LTP and it's opposite, long term depression (LTD), lies at the heart of long term learning, and these mechanisms are what allows the implementation of Hebb's rule. LTP is a viable candidate for the cellular mechanism for learning and memory!

![](/images/LTP.png)

LTP has a mechanism that involves the G-protein cascade that acts as a coincidence detector that is activated if both presynaptic activity and postsynaptic depolarzation happens simultaneously. If this coincidence detector is activated, then LTP changes the structure of this synapse by buiding and inserting more neurotransmitter receptors into the postsynaptic membrane, expanding current postsynaptic terminal, or even split current terminal into two for stronger response, as shown in figure above.

![](/images/LTP_example1.png)
![](/images/LTP_example2.png)

Now I'll try to convince you that LTP modulation on neuron is a frequent event and the structural change can be quite drastic. In the figure above, scientists imaged part of the mouse brain area that are responsible for whisket activities. The transient dentritic spines are marked in blue in the bottom row of images. We see that a brand new, large dentritic spine emerged on day 5, and completely dissappeared on day 6. There is also another spine marked in red that only appeared for three days.

### 1.4 Case Study: Learning in Aplysia

One of the most curious example is provided in Aplysia, a type of sea snail. Please allow me to digress a little bit on why neuroscientists love to study creatures from the sea. Recall that we talked about the presence of myelin sheath around the axon in our neurons in section 1, and it turned out that myelination is a advanced invention that allows faster transmission of electrical signals down the axons. 

We can basically treat the axon as an electric cable and describe it's electrical resistance using the formulas in physics:

$$R = \frac{\rho L}{A}$$

where $R$ is electrical resistance, $\rho$ is resistivity of material, $L$ is the length of the cable, and $A$ is the cross sectional area. In rather premitive animals that does not have myelin sheath, $\rho$ might be large, since the memberanes of the axon is leaky, and ions will leak out due to diffusion, hindering further signal transmission. In order to minimize electrical resistance, those animals who really need fast, instant signal transmission with strong physical and muscular response would seek to increase cross sectional area of the axon. This results in gigantic axons, particularly in huge marine animals like squids, to which a extremely strong escape response will be essential to its survival when danger is detected, and those giant axons would grow to about 1mm in diameter, fully visible under human eye. This is also how scientists first know about the content of an axon: they practically squeezed out the content of a giant axon and measured concentration of different ions. We humans, and other small animals, apparently cannot afford such a giant axon. Hence we resort to myelination, which is essentially a multiple wrapping of cellular membranes around the axon by another cell called Schwann cell, therefore greatly increasing electrical resistance across the memberane of the axon with reduced ion leakage, and much faster, stable signal transmission down to synaptic terminal, without having a large cross sectional area.

![](/images/aplysia1.png)
![](/images/aplysia2.png)

Back to Aplysia, this wonderful creature's nervous system is fully and systematically studied. In this experiment illustrating learning in Aplysia, when its siphon is touched gently, its gill contracts, with the extent of contraction proportional to the force of touching, as illustrated in experiment B1. In experiment B2, scientists locate a nerve ganglion (a group of several neurons) at the abdomen of Aplysia, and only removed this ganglion at step 8, and then the contraction response vanished, showing that this response is initiated and controlled by this particular ganglion. 

#### 1.4.1 Short term learning: habituation and sensitization

![](/images/aplysia_short_term.png)

Short term learning is illustrated by the above figure. In experiment A, scientist exert the same amount of force onto the siphon, however, the maximum response of the gill contraction drops as we repeat this experiment, as if the aplysia becomes "numb" to the simulation. Not until a rest of two hours, can a response of original intensity can be again observed when touching the siphon with the original force. This "numbing" is called **habituation** to the stimulus, and its most direct and probable cause is the depletion of vesicles that contains neurotransmitters outlined in section 2.3.

Experiment B shows the phenomenon of **sensitization**. After the aplysia has habituatied to the stimulus, scientists at exert a highly obnoxious stimulus to the siphon (e.g. poke its siphon or head with a needle instead of gently touching), it can resets the magnitude of the gill contraction response. Sensitization hence serves as a protection mechanism, such that when in danger, aplysia can "de-habituate" from the enviornment and restore its alertness. You might ask "how can sensitization be achieved if there is a shortage of vesicles?" This is a fantastic question and there are multiple way to do this. One source of modulation comes from its motor neurons that releases seretonin, which helps boost up vesicles avaliable.

#### 1.4.2 Long term learning in Aplysia

![](/images/aplysia_long_term.png)

When we repeat the short term learning experiment multiple times and let Aplysia to get habituated, amazingly long term learning occurs, and the response is shown above. For each training, we touch the siphon gentlely multiple times until habituation, allows the aplysia to rest, and repeat the training process. We see that the initial response of each training iteration is decreasing rapidly, showing a kind of long term adaptation. This diminishing response is only "forgotten" after a whole 14 weeks, when the scientists test it again on day 26. (Recall that habituation only lasted less than 2 hours) This is mediated by LTP mechanisms and I would say that this is a primitive form of memory: we have identified a cellular mechanism for which the aplysia is able to "remember" that it has receieved a lot of the same stimulus in the past few days!

### 1.5 Neural Plasticity

Neuroscientists use the word plasticity to describe the easiness of changing configuration and connections of neurons. **Synaptic plasticity** refers to the ability to change synaptic efficacy, and it can be either short term, or long term depending on whether structure changes are involved. On a much larger scale across thousands of synapses, **cortical plasticity** describes the ability to rewire neuron connections on a massive scale. We will revisit the idea of plasticity in later posts with a canonical example on Barn owls, but the take away point here is that learning done in brain can be interpreted as exercising the plasticity, rewiring and reconfiguring the connections according to the tasks we faced and our experiences with the world.

- - -
## 2. ML: Learning as optimization

![](/images/robot.png)

### 2.1 Model, parameter, estimator, inference

You must have heard the term "mathematical modeling" a lot growing up. To my understanding, a **model** is our understanding of a phenomenon and it is our try to describe it. For example, when understanding the outcomes of the tosses of a fair coin, our model is that it has $50\%$ chance giving us a head, or we could say that the probability of the fair coin showing head is $0.5$. What if the coin is not fair? Let's say the coin I have has probability of $p$ showing a head in one toss, we call this $p$ a **parameter** of our model. More rigorously, a model is a family of distributions $ M = {f_{\theta}: \theta \in \Theta }$, with each density parameterized by some parameter $\theta$ in the parameter space $\Theta$. In this coin toss example, $M = {f_p \sim \text{Bernoulli}(p): p \in [0,1]}$.

My friend, Jim, would like to play a game with me. If the coin shows up heads, he wins and I pay him 1 dollar, and else he would lose and pay me 1 dollar. In order to know whether the game is favorable, I would like to know the value of $p$. The same as the situation we face in reality, we would like to know the value and gain information about the parameter(s) of our model so that we can better understand what we are dealing with. The procedure of estimating the best values of parameters and gaining more information about them so that the data can be better explained is called **inference**.

In order to get a better idea of the coin, I propose to Jim that before we enter the game, we should do $10$ trial rounds of ten flips with outcomes $\{ F_1, F_2, \ldots, F_{10} \}$. My idea is that, if I count how many heads showed up, I could roughly calculate $p$ in the following way:

$$\hat{p} = \frac{\text{# heads showed up}}{\text{# of total flips}}$$

Note that I decided that I would guess $p$ using this formula _before_ I actually do the $10$ trials. This formula for my guess of $p$ is called an **estimator** for parameter $p$, and an estimator is always a function of data, whose value can be computed once the experiment is carried out, and this value is called an **estimate**. Note that we add a little "hat" to the parameter we would like to estimate to denote an estimator for that parameter.

Now our kind Jim agrees and flipped the coin $10$ times, and the outcomes are H,T,T,H,H,T,T,T,H,T. So using my formula, I estimate $p = 0.3$. I believe that my method of estimating $p$ makes perfect sense, and although I understand that the lack of heads may be due to chance, but I would still repectfully decline his invitation to play his game. 

This coin filp example might be too simple, let us look at another inference problem. Let us suppose that I am a school teacher,
and Jim is the only students who missed his final. However, I do have all midterm and final scores of other students, and I think that I can predict Jimmy's final score using his midterm score. To achieve this, I assume a linear model as follows:

$$\text{final_grade} = k \cdot \text{midterm_grade} + b$$

I have two parameters, $k$ and $b$, and the objective of my inference problem is to find the most suitable values of $k$ and $b$, such that I could predict Jim's final score as accurately as possible. If you have studied linear regression, you would know that this problem has a analytical solution. But let's look at a more universal and general way by which optimal parameters can be obtained!

### 2.2 Gradient based learning

#### 2.2.1 Loss function 

Following the question of estimating $k$ and $b$ in predicting Jim's final grade, the immediate question is: how should we define "the most suitable" values for them? To this end, we introduce the idea of an "objective function", and the set of parameter values are "the most suitable" if they minimize the objective function if the objective is a cost, or they maximize the objective function if the objective is a gain. In the realm of supervised (we will explain this soon) prediction problems, we usually use a loss function to describe how far away our prediction is off.

Mathematically, a loss function is a function from the parameter space to the real line that is strictly non-negative, with zero achieved where predictions match the outcomes exactly.

$$L: \Theta \rightarrow \mathbb{R}$$

Now let's look at some canonical choices of loss functions. Suppose that we have $D$ data pairs, $(x_1, y_1), \cdots, (x_D, y_D)$, where all $x_i$'s are observations and $y_i$'s are outcomes, or we call the **labels**. Then we can define loss function as follows:

- Squared loss:

$$L((k,b)) = \frac{1}{2}\sum_{i=1}^D (y_i - \hat{y_i})^2 = \frac{1}{2} \sum_{i=1}^D (y_i - (kx_i + b))^2$$

The half multiplied at the front is only for computation easiness -- when you take derivatives, the two in the power comes down and cancels with this half.

- Absolute loss:

$$L((k,b)) = \sum_{i=1}^D |y_i - \hat{y_i}| = \sum_{i=1}^D |y_i - (kx_i + b)|$$

Note that both losses are the summation of non-negative terms and hence overall non-negative. We choose a suitable loss function according to the problem's context, and the learning objective is to find a set of parameters that achieves the minimum of the loss function, and thereby rephrasing the learning problem as a optimization task.

#### 2.2.2 Gradient descent algorithm

So how do we find this optimum exactly? Naturally we resort to calculus and derivatives when we are trying to find the max or min of a function. In particular, the derivatives, or gradients in a more general, multi-dimensional setting, gives us the direction in which the value of our function is increasing most rapidly. Hence, we should take a small step in that opposite direction such that we can obtain a pair of parameters that would give us lower loss than the previous set of parameters. 

Mathematically, for a loss function $L$ and vector of parameters $\mathbf{\theta}$, the gradient is a vector with each entry the partial derivative with respect to $\theta_i$:

$$\nabla L(\mathbf{\theta}) = \bigg( \frac{\partial L}{\partial \theta_1}, \frac{\partial L}{\partial \theta_2}, \ldots, \frac{\partial L}{\partial \theta_n}\bigg)$$

The gradient descent algorithm says:

$$\mathbf{\theta}^{t+1} = \mathbf{\theta}^t - \eta \nabla L(\mathbf{\theta}^t)$$

Where we call $\eta$ the **learning rate**, which describes how big the step should we take towards the fastest descending direction. Imagine that you are on a hill, and the geometry of this hill you are standing on is fully described by your loss function. Note that this "hill" does not have to be three dimensional. You can be in a very high dimensional space if you have multi-dimensional parameters. But no matter how many dimensions are there, each set of specific parameter values $\mathbf{\theta}$ would give you the height of the hill at this coordinate, which is $L(\mathbf{\theta})$. 

![](/images/GD.png)

Therefore, with the above visualization, you can imagine the gradient descent process as follows: You start from a random point on the hill, and the objective is to reach the valley, the lowest point on this **landscape**. At each timestep $t$, you find the fastest descending direction $\nabla L(\mathbf{\theta}^t)$ by taking the gradient of the loss function and evaluate at current set of parameters, and walk towards that direction with step size $\eta$. You repeat this process until you reach the bottom of the valley. 

#### 2.2.3 Problems and issues with GD
Your first natural question might be how to determine the learning rate. Indeed, determining a suitable learning rate might be hard, and the choice will affect optimization performance. Observe that if your learning rate is too large, that you take too huge a step for every update, then you will end up oscillating half way down the valley and unable to reach the bottom, while too small a learning rate will result in very slow training speed, and more updates are required to reach the optimum. Learning rate is one of the many hyperparameters that need to be tuned, and we will revisit this question when we talk about hyperparameter tuning in the future posts.

Apart from learning rate, we can spot two more problems:
- This process is greedy, where it is only possible for us to move to a point in the parameter space where the loss is strictly less than before, which would probably trap us in a local minima of the function instead of a global one.
- The loss landscape might be much, much more complicated than this simple quadratic case, as an example shown below:

![](/images/landscapes.png)

The combination of those two problems presents great challenge to our gradient descent algorithm in fairly complex setttings. In the case where our initial guess is bad and we have a highly non-convex landscape, it is very easy to be trapped in a local minima. However, there are many clever excape plans that gives us a chance to hop out, which we would not go into detail here in this post.


### 2.3 Backpropagation

This section probably has the most tedious math parts of all in this blog series, so hereby I summarized the essense of this section as follows:

> Backpropagation algorithm allows us to compute gradients of parameters (the weights) in a neural network very efficiently while being biologically implausible.

Let me share an anecdote to show how classic and import backpropagation algorithm is. In my junior year I took CS281, which is the graduate level machine learning class at Harvard. The lecturer was a senior researcher from Oracle, and he said: "I asked the faculty chairs what I should cover in this class, and they told me I could teach any topic I want, as long as I derive backpropagation once at some point." So here I present you a derivation for backpropagation! How exciting:)


Consider a neural network with activation function $\sigma (\cdot)$. We take the $j^{th}$ neuron in an arbitrary layer other than the input layer, and recall that this neurons activation $a_j$ can be written as:

$$z_j = \sigma\bigg(\sum_{i=1}^n w_{ij}b_i\bigg) = \sigma(a_j)$$

where $b_i$ is the activation of neuron $i$ in the previous layer, and $w_{ij}$ is the weight between neuron $i$ in previous layer and neuron $j$ in current layer. Our ultimate goal is to compute the gradient $\frac{\partial L}{\partial w_{ij}}$ for all $i$. By chain rule:

$$\frac{\partial L}{\partial w_{ij}} = \frac{\partial L}{\partial a_j}  \frac{\partial a_j}{\partial w_{ij}}$$

- Let $\delta_i = \frac{\partial L}{\partial a_j} $, this term is called the **error**. 
- Since $a_j = \sum_{i=1}^n w_{ij}b_i$, $\frac{\partial a_j}{\partial w_{ij}} = b_i$.

Thus:

$$\frac{\partial L}{\partial w_{ij}} = \delta_ib_i$$

which is the error term multiplied by the activation of the input neuron of this weight, and this activation value can be stored during forward computation of the neural network. Now we only need to figure out the error term. With chain rule again:

$$\delta_j = \frac{\partial L}{\partial a_j} = \sum_{k=1}^N \frac{\partial L}{\partial a_k} \frac{\partial a_k}{\partial a_j} = \sum_{k=1}^N \delta_k \sigma '(a_j) w_{jk} = \sigma '(a_j)\sum_{k=1}^N \delta_k  w_{jk}$$

where $k$ denotes a neuron which neuron $j$ sends a connection to in the next layer. Therefore, we see that we can iteratively write the error term of neuron $j$ in terms of the previously calculated error term of neuron $k$ in the next layer and the weights between them, which means that we can calculate the error terms backwards starting from the last layer, and hence the name backpropagation!

Therefore, when performing gradient descent, at each iteration $t$, we:

1. Forward pass: compute activations of neurons at each layer from the 1st layer to the last using currnt values of the weights;
2. Backward pass: compute error term at each neuron from the last layer to the front;
3. Update: Evaluate gradient (error multiplied by outgoing neuron's activation) and take a step in negative direction of gradient for each parameter.

Again, revising the point in the last post about GPU computation, since the operations in both forward pass and backward pass involves extensive matrix multiplication, we can take gradients swiftly and efficiently, storing them locally at each neuron, also avoiding repeated calculations.

### 2.4 Regimes of learning in ML

After discussing methodology of optimization, let us come back to the main focus of this post -- what is learning. So far, we have treated machine learning as an optimization problem (and in fact, we can have different perspectives, which will be discussed towards the end of this post). But within optimization, the problem of getting to the optimum can be phrased with vastly different approaches. Now let's examine some of the most important distinctions.

#### 2.4.1 Supervised VS Unsupervised 

The term supervised describes whether you know the ground truth in training data. For example, when we try to predict the score Jim would get on final, we trained on the midterm and final scores of other students, the final score of other students would be the ground truth in this context. If we are classifying images, this task would be supervised, because each training image is accompanied by the true class label.

Hence, you as my smart readers would realize that the typical forms of loss function that I introduced in the previous sections would only make sense in a supervised regime, because the tru label $y$ is involved in the loss function formulation (we would not be able to compute those losses if we do not know y). 

You might wonder at this point: How would unsupervised learning possible then? How do we formulate a loss function without knowing the truth and what we are aiming for? The answer is that in some tasks, we can still define a meaningfull objective function. And we should shift our viewpoint a bit. In the supervised realm, we might be interested in predicting the output, but in the unsupervised realm, we are more interested in **describing our data** in general. 

For example, maybe we have a dataset of all detailed course selection information for all students in a dorm. We can run unsupervised clustering algorithms that groups students together. For example, we can group students according to how many classes they have chosen in common. In this sense, we are essentially describing this student dataset, and we can still do predictions such as a student's concentration, because students of the same concentration are likely to take the same subset of classes.

#### 2.4.2 Probablistic VS deterministic

Let us discuss this in the context of predicting final grade again. With a deterministic approach, we are basically saying that there are no sampling from a random variable in the model, and everytime you train afresh from the dataset and run the predictions on the test set, it will give you the _exact_ answers to everything. 

For example, predicting final score using regression would be a deterministic approach, and the slope parameter has a analytically solution 

$$\hat \beta = (\mathbf{X}^T\mathbf{X})^{-1}\mathbf{X}^T\mathbf{y}$$

which is fully specified once we see training data $\mathbf{X}$ and labels $\mathbf{y}$.

On the other hand, a probablisic approach involves sampling from random variables, and re-running the experiment would give a slightly different result due to random sampling.


#### 2.4.3 Parametric VS Non-parametric

It is extremely tempting to think that non-parametric means that there are no parameters. Quite the opposite, non-parametric means that we have infinite dimensional parameter space and subsequently the number of parameters is infinite. 

Let us revisite the idea of a model in section 2.1. A parametric model is formally a family of distributions parameterized by $\theta$ in parameter space, however, this means:

- the type of problems that any parametric model can describe is limited due to the finite dimensional parameter space.
- any parametric model involves a set of assumptions for the problems, embedded in the specific choice of the family of distributions.

Therefore, non-parametric methods triumph in the sense that it is not making any assumption about underlying distributions and hence have the potential of reaching less systematic errors (I'm planning to having an additional post specifically on error decompositions and empirical risk minimization). Here's an example for non-parametric method: suppose we would like to estimate the whole cumulative distribution function (CDF). In this case, the empirical cumulative distribution, ECDF, would be a non-parametric estimation of the CDF, since it does not have any model assumption, and only utilizes the data.

It seems for now that non-parametric methods are superior in the sense of making less assumptions, so why are we still using parametric methods? The answer is that when we have reasonlbly strong information about the problem at hand, making some suitable parametric assumption would make the inference problem much, much easier. For example, if I would like to describe the fairness of a coin, making the parametric assumptions that each toss the coin has probability $p$ of landing heads make perfect sense because it captures the essence of coin tosses. All we need to do is to estimate parameter $p$. 

- - - 

Now we have briefly visited learning in both biological neurons and in neural networks. Congratulations for making it through! In the second part of the post, we are going to introduce two more interpretations of learning in statistics and machine learning, and discuss similarities and differences in all approaches.


