---
title: "Neuro & AI: Introduction and schedule"
comments: false

categories:
  - Neuro&AI
tags:
  - Neuroscience
  - Deep Learning
  - Neural Network
published: true

excerpt: "Quick introduction over the content and aim of this blog series"
header:
  overlay_image: /images/header2.png

---
Welcome to the first blog post of the Neuro & AI series! 

Since 2012, deep learning has revolutionized the world in numerous aspects, changing our lives in almost every way possible. However, I found most of the machine learning and deep learning tutorials online focuses too much on the practical aspect. Most of them lack the mathematical intuition, and most importantly, none of them mentioned neuroscience at all.

In short, our brain and an artificial neural network(ANN) can be infinitely alike or infinitely dissimilar, depending on your abstraction levels. Despite the fact that ANNs drew inspirations from biological neurons, one can also make a reasonable case that this as the only connection between ANN and our brain. But is this true? Does the similarities stop there? 

This blog series would love to introduce you to the basic ideas in deep learning, and in particular, focus on the intersection between neuroscience, cognitive science and deep learning. I wrote all the blogs with the mindset that everyone, regardless of background and former training, should be able to read my blog. I'm intending to introduce some rigorous math here and there, but they should have no impact for the whole line of story telling. Through the blogs, I hope to share:

- Basic understandings about human brain organizations and functions, with the emphasis on vision, attention and memory. 
- An introduction to deep learning and understandings for similarities and differences between modes and rules of learning in human and deep neural networks.
- Familiarity to classic, commonly used deep learning models such as the convolutional neural networks, Recurrent neural networks and their variants, with some mathematical intuitions.
- A candid discussion into the future of deep learning: how can neuroscience and deep learning help each other? What might be the fundamental obstacle towards general intelligence?

Hereby I post my intended plan for this blog series, extending to 10 posts:

### I. Brain and Neural Nets
- Brain as the pinnacle of human evolution
    - Brief history of neuroscience
    - Gross neuroanatomy
    - How is human brain special?
- Introduction to Neural Network
    - Nueral network basics, universal approximator
    - History of neural network
    - Rise of deep learning

### II. What is learning: Goals and Rules
- Learning in the brain
    - Neuron 101: cell structure and chemical synapse
    - Neurons: Short term learning by changing synaptic efficacy
    - Neurons: Long term learning by making structrual change
    - Case study: Aplysia
    - Neural plasticity
- Learning as an optimization problem
    - Model, parameter, estimator, inference
    - Gradient based learning
    - Backpropagation
    - Regimes of ML
- Learning as updating conditional probabilities
    - The Bayes Theorm
    - Updating posteriors
    - Perception as inference
- Statistical learning theory
    - Formal framework
    - PAC learning
    - Empirical risk minimization

### III. Classification: understanding representation
- Representation in human
    - Correct classification requires forms of representation
    - Firing patterns of neurons as representations of concept
    - Topographical maps in cortical organization
- Classification with algorithms
    - Decision boundary: goal of classification
    - Metric for performance: Confusion matrix
    - Perceptron algorithm
    - Feature engineering

### IV. Vision 1: Human vision
- Early visual system anatomy
- Neuron tuning and receptive field
- Visual system hierachy
- The way we see is learnt: Insights from early visual development
- Demystifying subconsciousness in vision

### V. Vision 2: Machine vision
- Convolutional Neural Network
    - Convolution and filters
    - Convolutional, fully connected, pooling layers
    - Representations in convolutional layers
- Model training 101
    - What is learnable and what is not
    - Hyperparameter tuning
    - Recap: Loss function and its design
    - Overfitting and underfitting
- Case study: Classification with dogs and cat (intended to be code inclusive)

### VI. Vision 3: Brain and machine in comparison
- Discussion: Similarities and differences
    - Neuron as abstractions
    - Layers in CNN compares to brain regions
    - Bottlenecks in both human visual system and in CNN
- View from neural development:
    - Axon guidance
    - Intrinsic activities and activity dependent sculpting
    - Case study: Barn owls
- Discussion: To what extent is biological realism the future for AI models?

### VII. Memory
- Memory in human
    - Types of memory
    - Storage and formation of long term memory
    - Case study: Patient HM
    - Hippocampus: beyond memory
- Memory in machines: Recurrent Neural Networks(RNN)
    - The context of sequence modeling
    - Long-short term memory networks(LSTM): all the gates!
    - Case study: Machine translation (intended to be code inclusive)

### VIII. Attention
- Human visual attention
    - Broadbent, Treisman, and the start of cognitive science
    - Visual capacity and working memory
    - Attention as a resource allocation mechanism
- Attention in deep learning
    - Attention as weights in sequence modelling
    - Attention mechanisms in CNN: a survey of methods
    - Case study: Alibaba's DIN recommendation system
- Discussion: Are attention in neuroscience and DL talking in the same sense?

### IX. Specialzation vs Generalization
- Specialization: What can machines do, and we cannot?
    - Finding correlation
    - Cutting edge developments in industry in the following fields:
        - Image classfication
        - Object detection and multi-object tracking
        - Applications on radiology: Is it better than expert radiologist?
- Generalization: What can we do, and machines cannot (so far)?
    - Limitations from machines mode of learning
    - Case study: Taxonomy study from Stanford on transfer learning
    - Case study: Block tower study on intuition
    - Imagination: pink elephant with two trunks?
    - Discussion: How might we enable machines to generalize?

### X. Towards general intelligence
- Interpretability
    - Adversarial attacks
    - Case study: Google's Deepdream
    - Fairness in machine learning and deep learning models
- Back to biological realism
    - Discussion: Should we always strive fore more bio-alike models?
    - Forget gradient descent: Direct feedback alignment
- Discussions:
    - Is GI achievable?
    - Is GI good: Efforts in AI safety


The above tentative schedules are subject to minor chages, and I hereby extend my invitation to all of you wonderful readers to actively engage in my blogs by commenting below. If you found a mistake in my blog, or know an answer to a question, please do not hesitate to let us know! I hope that it would be an educative, interactive, and most importantly, an inspiring journey!

