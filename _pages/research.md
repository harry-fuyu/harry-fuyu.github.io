---
layout: archive
title: Research
permalink: /research/


defaults:
  - values:
      layout: single
      author_profile: true
      
---

<img src="/images/harvard.png" width="60"> 
### Sept 2018 - Present    
Research Assistant, Harvard Vision Lab, Harvard University

- #### Thesis Project: Multi-Object Tracking With Top-down Location Proposals
Currently conducting thesis research of combining top-down attention mechanism into object tracking networks such as Fast R-CNN and YOLO for better performance, since current region proposals in those networks are entirely decided bottom-up.

<!-- ![](/images/prototype.png) -->
- #### Project: Top-down Visual Attention In Convolutional Neural Networks
Investigated the distribution of neural representations in convolutional layers of Convolutional Neural Network (CNN) trained on classifying Cifar10 images, in order to design **category specific weights** used in modeling top-down visual attention. Discovered that similarity of image representation to category’s mean representation is not the criteria CNN is using for classification.

- #### Project: Learning Interpretable Representations in Intuitive Physics
<!-- ![Latent space extrapolation of VAE using RNN as encoder and decoder.](/images/latent.png) -->
    - Innovatively utilized Recurrent Neural Networks (RNN) as the encoder and decoder of a variational autoencoder (VAE) to explore what inductive bias could make VAE’s latent space more interpretable.
    - Implemented VAE in pytorch using pyro package to reconstruct projectile trajectories of particles and discovered that latent space is much more structured if vertically sliced trajectories are used as training data. 

<img src="/images/TUM.png" width="60"> 
### June 2020 - Aug 2020     
Research Assistant, Macke Lab, Technical University of Munich (TUM)

![](/images/sbi_HH_model.png)

- #### Project: Simulation Based Inference For Multiple Datapoints
    - Established pipeline for testing sbi, which performs systematic Bayesian inference when likelihood of model is intractable bytraining a neural network to map data onto parameter posteriors, for its performance when multiple i.i.d. data is observed, provided a valuable reference for sbi users on the trade-off between model and computational complexity when using sbi.
    - Designed suitable baseline tests for permutation invariance (PI) for multiple posterior density estimators, in particular variants of masked autoregressive flows, and identified average pooling on data embedding as a viable structure to achieve PI by performing baseline tests on data simulated from exponential family distributions.