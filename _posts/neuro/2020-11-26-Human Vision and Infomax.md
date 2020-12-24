---
title: "Neuro & AI (IV): Human Vision and Infomax"
comments: true

toc: true
toc_label: "Table of Contents"
toc_icon: "cog"

categories:
  - Neuro&AI
tags:
  - Neuroscience
  - Computational Neuroscience
  - Information Theory

published: false

excerpt: "Human early visual system and math derivation for RGC receptive fields"
header:
  overlay_image: /images/header_vision.png
---


<!-- ### IV. Vision 1: Human vision and Infomax
- Human visual system
    - Early visual system anatomy
    - Neuron tuning and receptive field
    - Visual system hierachy
    - The way we see is learnt: Insights from early visual development
    - Demystifying subconsciousness in vision
- Infomax and receptive field
    - What is computational neuroscience?
    - Mathematical modeling of early visual system
    - Infomax derivation of receptive field -->

Congratulations on making through the four previous posts that gives an overview about the content, philosophy and methodology of neuroscience and machine learning. Starting from this post, we will finally dive into more specific domains and talk about the applications of deep learning models there. 

Firstly, let's talk about biological vision in the first section. It is not only because that it is a topic close to my heart, but also because it is highly pertinent to our first major model, the convolutional neural network, whose invention was very much inspired by the structure of the human visual system. In the second section, I am going to introduce you some ideas from information theory and show you how amazingly and beautifully can we derive the shape of receptive field that aligns with empirical results, with few reasonable assumptions. Although those theories are developed with those assumptions and is far from reality, it still provides a potentially illustrative explanation for why our visual system has evolved to have the functions it has nowadays.

## 1. Human Visual System

![](/images/eye_anatomy.png)

### 1.1 Early visual system anatomy

As the saying goes, eyes are the windows to our hearts. Retina that sits at the back of our eye, is considered as part of the central nervous system. As the photon enters through iris, refracted by cornea and lens, and shines onto our retina, huge amounts of unprocessed information is picked up by our photoreceptor cells on retina.

![](/images/retina.png)

The structure of retina is conterintuitive as shown in the figure above. The photoreceptor cells are actually located at deeper locations at the back of retina. Light shines through the initial layers into the deep layers, and those signals picked up by photoreceptor cells then travels back in the opposite direction to the surface of retina, eventually reaches the retinal ganglion cells, which are connected to optic nerves that conveys the signals into our brain. 

![](/images/rods_and_cones.png)

There are two types of photoreceptors: rods and cones. The rods are very sensitive to photons and is in charge of detecting light intensity, while the rods are responsible for color vision. We have three types of cones that are sensitive to red, green and blue light respectively, and we can think of them as the three color channels. This is also the reason why we use RGB.

![](/images/wavelength.png)

The theory is that the mammals used to have more channels than three (possibly 7?), and has larger visible range of frequencies. However, during the time of dinausours, the mammals were forced to live undergroud, and hence, having better colored vision did not make the species more fit to the environment. As time passed by, the early mammals, mainly small rodents, started to lose channels and eventually only retained three of them. Hence, our color perception is most likely a story of devolution rather than evolution.

![](/images/early_visual.png)

After the visual signals 
