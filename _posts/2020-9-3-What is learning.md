---
title: "Neuro & AI (ii): What is learning?"
comments: true

categories:
  - Neuro&AI
tags:
  - Neuroscience
  - Deep Learning
  - Neural Network
published: true

excerpt: "Introduction to the concept of learning in neurons and in neural networks"
header:
  overlay_image: /images/header.jpg
---

Welcome to the second post in he series of Neuro & AI! This post covers one of my favorite topics, and to some extent even philosophical, about what the process of learning is. When we were kids and we were trying to learn how to ride a bike, what is the process going on in our brain? Is this process different when we associate a newly seen word "bike" to the object in front of us with two wheels? 

We mentioned several times even in the first post, and you might have known that neural network needs to be trained. If we were to teach the network, how is the network learning? What information, in what form, is retained during its learning? 

We are also interested in two philosophical points:
- How is learning in human brain different from learning in neural networks? On which abstraction levels are they similar, and on which level are they not? From this discussion, we are heading into one of the philosophical themes of the blog post series, which is about whether making neural networks more similar to human brains would always be beneficial for model performance.
- We will dive deeper in to statistics and talk about learning from a Bayesian perspective. We would first understand what is Bayesian thinking, and I will try to convince you that in the Bayesian world, learning is purely about updating conditional probabilities we call posterior. From here, we are heading into another major philosophical theme, which is that perceptions done by the brain can be treated as a statistical inference problem. (we will definitely discuss this in more detail)

<!-- Here's the bullet point agenda for today:
- Neuron 101: cell structure and chemical synapse
- Neurons: Short term learning by changing synaptic efficacy
- Neurons: Long term learning by making structrual change
    - Hebb's Rule
    - Long term potentiation and depression
    - Case study: Desensitization in Aplysia
    - Synaptic plasticity
- ML: Learning as an optimization problem
    - Model, parameter, estimator, inference
    - Loss function and loss landscape
    - Gradient based learning
    - Backpropagation
    - Regimes of ML
- Being Bayesian: Learning as updating conditional probabilities
- Discussion: perception as an inference problem -->

If you can't wait to find out to some of the questions above, great! Let's dive right into it!

![](/images/aplysia.png)

### 1. Neuron 101: Cell structure and chemical synapse

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


### 2. Neurons: Short term learning by changing synaptic efficacy

Finally we are equipped with the jargons and concepts to talk about learning. Learning can be very broadly categorized into short term learning and long term learning depending on how long they last. Short term learning does not involve structural change, but rather a change in synaptic efficacy. The effect usually last by on the order of seconds or minutes.

So how can the transient change in synaptic strength be achieved?

#### 2.1. Method 1: Releasing vesicles

As previously mentioned, the vesicles in presynaptic terminal that contains neurotransmitters. If there are more vesicles released from the presynaptic terminal, more neurotransimitter molecules would be released into the space between the pre- and post- synaptic terminals called the **cleft**, causing the concentration of those molecules in the cleft to increase. As the concentration rises, there is a higher chance for the receptors on postsynaptic membrane to catch a floating neurotransmitter molecule and cause a small depolarization in the postsynaptic terminal. Hence, releasing more vesicles can definitely elicit a stronger response from the postsynaptic neuron, thereby enhancing synaptic strength, but only temporarily, since the access neurotransmitters can be recycled by presynaptic terminal or diffuse into other places are are lost.

#### 2.2. Method 2: Facilitation

After the previous depolarization in the postsynaptic terminal, the electrical potential there would go back to its original state due to ions diffusing down their concentration gradient in and out of the postsynaptic cell. This means that the potential would decrease down slowly until it reaches the equilibrium at around -70mV, which is called the **resting potential**. This subsidizing process is slow: imagine a cup of hot tea set on a table in room temperature. The tea would cool down very fast at first, but the process of cooling slows down as the temperature of the tea gets closer to room temperature. Same thing happens here in the neuron, as the electrical potential restores towards the resting potential, the process of getting there gets slower. 

Hence, facilitation happens when another small depolarization happens before the previous depolarization has fully subsided, resulting in the second depolarzation to reach a more positive potential than the neurotransimitters could ever contribute, by piggy-bagging on the first depolarization. Here is a graphical illustration.

#### 2.3. (passive) Method 3: Vescicle depletion

As vescicle fuses with the presynatic membrane, more and more vescicles are being produced at another site by cutting off the infolding of the presynaptic membrane. In the situation where stimulus arrives quickly in succession, the speed of vescicle regeneration lag behind the rate of vescicle release, resulting in less vescicle fusions and less neurotransmitter release than it should have been. This passive mechanism would hence decrease the synaptic strength temporarily. If we allow a short period of time for the vescicles to regenerate, this effect would be no longer in place.

### 3. Long term learning by structrual change

#### 3.1 Hebb's postulate
Hebb's learning rule describes how structural change should be directed by learning activities. It can be stated succinctly in the following two sentences:

> Fire together, wire together.

> Out of sync, unlink.

This sentence states that the neurons firing simultaneously should have a permanent increase in synaptic strength, because the synchronization has a functional relavence, and the second statement states the opposite direction. Hebb's rule has direct biological evidence from neuron recordings, that the aquisition of new skills are achieved by the synchronized firing of a pattern of neurons.

- - - 
##### Mathematical formulation

(please feel free to skip)
Mathematically, if two neurons have activations $x_i$, $x_j$, then the weight $w_{ij}$ connecting those two neurons should have the value:

$$w_{ij} = x_ix_j$$

This says the the weight between two neurons are directly proportional to the activation of both neurons, elegantly capturing the idea of Hebb's postulate. This learning rule for the value of weights is called the **Hebbian learning rule** in computational neuroscience.

- - - 

#### 3.2. Long term potentiation (LTP)
LTP and it's opposite, long term depression (LTD), lies at the heart of long term learning, and these mechanisms are what allows the implementation of Hebb's rule. LTP is a viable candidate for the cellular mechanism for learning and memory!

![](/images/LTP.png)

LTP has a mechanism that involves the G-protein cascades that acts as a coincidence detector that is activated if both presynaptic activity and postsynaptic depolarzation happens simultaneously. If this coincidence detector is activated, then LTP changes the structure of this synapse by buiding and inserting more neurotransmitter receptors into the postsynaptic membrane, expanding current postsynaptic terminal, or even split current terminal into two for stronger response, as shown in figure above.

![](/images/LTP_example1.png)
![](/images/LTP_example2.png)

Now I'll try to convince you that LTP modulation on neuron is a frequent event and the structural change can be quite drastic. In the figure above, scientists imaged part of the mouse brain area that are responsible for whisket activities. The transient dentritic spines are marked in blue in the bottom row of images. We see that a brand new, large dentritic spine emerged on day 5, and completely dissappeared on day 6. There is also another spine marked in red that only appeared for three days.

### Case Study: Short term and long term learning in Aplysia








