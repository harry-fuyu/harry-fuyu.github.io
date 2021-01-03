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

published: True

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

The structure of retina is conterintuitive as shown in the figure above. The **photoreceptor cells** are actually located at deeper locations at the back of retina. Light shines through the initial layers into the deep layers, and those signals picked up by photoreceptor cells then travels back in the opposite direction to the surface of retina, eventually reaches the **retinal ganglion cells (RGC cells)**, which are connected to **optic nerves** that conveys the signals into our brain. 

![](/images/rods_and_cones.png)

There are two types of photoreceptors: **rods** and **cones**. The rods are very sensitive to photons and is in charge of detecting light intensity, while the rods are responsible for color vision. We have three types of cones that are sensitive to red, green and blue light respectively, and we can think of them as the three color channels. This is also the reason why we use RGB.

![](/images/wavelength.png)

The theory is that the mammals used to have more channels than three (possibly 7?), and has larger visible range of frequencies. However, during the time of dinausours, the mammals were forced to live undergroud, and hence, having better colored vision did not make the species more fit to the environment. As time passed by, the early mammals, mainly small rodents, started to lose channels and eventually only retained three of them. Hence, our color perception is most likely a story of devolution rather than evolution.

![](/images/early_visual.png)

After the visual signals leaves eye via the optic nerves, they pass through the **optic chiasm**, which is like a cross road for the optic nerves, and separate themselves according to which part of the visual field that the signal is coming from. Notice that since light only travels in straight line (at least here there's not significant distortion due to gravity:D ), the left half retina of the left eye could only see what's on the right of our visual field, and the right half retina of the left eye is only looking at the left. The purpose of this reorganization is such that all signals corresponding to the left visual field go to the left side of the body at this cross road, and all signals from the right visual field go to the right. After the optic chiasm, the optic nerves reaches thylamus, which is a common relay for all sensory information. In particular, this thylamic neuclus is called the **Lateral geniculate neuclus (LGN)**. Note that by the reordering that occured in optic chiasm, each LGN only receives information from one side of the visual field. Then, the neurons sends signals from the LGN to the primary visual cortex (V1) in a radiating pattern.

### 1.2 Receptive field and neuron tuning

Because each RGC cell is only connected from a few photoreceptors, each optical nerve is only connected from a few RGC cells and so on, we see that a change restricted to a small part of the visual field would not be detected for all RGC cells and cells in V1. Hence, the **receptive field (RF)** of a neuron is the sensory space (e.g. visual field for vision) that the neuron is responsive to. 

![](/images/RGC_RF.png)

The RGC cells have a so called **center-surround** receptive field. For the illustration on the left, the cell would be greatly activated if light shines on the center of the receptive field, but its activity would be inhibited when the light shines on the sides, and no effect when the light falls outside of this RF. The illustration on the right also shows a center-surround receptive field but switched in its property, where the center becomes inhibitory and the surround becomes excitatory.

![](/images/orientation_tuning.png)

Another very important property of neuron is called tuning, and this corresponds to the neuron's feature if we think in terms of neural networks. Neurons in the primary visual cortex (V1) are very sensitive to the orientation. For a certain V1 orientation selecting cell, which is called a **simple cell**, it's levels of activities is a function of the orientation, as shown in the figure above. We see that this cell is the most responsive to vertical bars, and as the bar becomes more slanted towards horizontal, the level of activation would decrease, and the curve is pproximately Gaussian. Orientation tuning of V1 cells is first observed in cat by [Hubel and Wiesel](https://www.youtube.com/watch?v=8VdFf3egwfg&t=126s) back in the 1950s as a purely haphazard observation. 

![](/images/elongated_RF.png)

One interesting observation shown in the figure above is that **orientation tuning in V1 simple cells can arise from alignment of several center surround receptive fields**. One question that one might ask is that how can this be true if the retinal ganglion cells are not connected to V1 cells directly? To answer this question, we recognize that the cortex itself has layered structure. Usually the cortex has six layers, and in the case of V1, after the relaying neurons leave LGN, they enter the primary visual cortex in layer IV. For further propagation to layer III, the above pattern can be realized, and a layer III cell in V1 could then be orientation selective. This is one possible explanation for how orientation tuning is implemented in the brain, and in the second section of the post, we would discuss more detail about the theoretical justification for why our V1 cells appear to be orientation selective.


### 1.3 Visual system hierarchy

![](/images/visual_hierarchy.png)

#### 1.3.1 Hierarchy overview

After the visual signals reach V1, information is extracted in hierarchical and parallel manners. After V2, there are mainly two pathways for parallel processing. All information about location goes up to the parietal lobe, and this pathway in dorsal direction is called the **where stream**, or the **dorsal stream**. On the other hand, information about the object itself goes sideway to the temporal lobe, and is called the **what stream**, or the **ventral stream**.

![](/images/MT_LIP.png)

Visual areas higher up in the higher hierarchy have more complicated tuning properties that sometime are not as easily interpreted as those of V1. For example, cells in V5, or called the **Middle Temperal area (MT)**, are tuned to the directions of motion. Cells in V4 are sensitive for colors, and areas further up, like the **Lateral Interparietal area (LIP)**, has cells whose tuning properties can be modulated by current task of the individuals and hence strongly related to visual attention. Intriguingly, this hierarchical and parallel organization of the visual cortices is true in other sensory cortices, however, it is not exhibited in higher order association cortices that are responsible for higher order functions. 

#### 1.3.2 Example: Facial tuning
Now let us focus on one specific example of neuronal tuning up in the hierarchy. You might have heard the so called "Jennifer Aniston" cell, where the neuron is only excited when the famous American actress, Jennifer Aniston, enters the visual receptive field of your cell. This cell is the embodiment of how complicated the tuning property of a neuron could be. This neuron must be sitting there high up in the hierarchy, and listening to all information extracted by numerous downstream neurons in a parallelled manner. It is true that we have a face area, where **neurons in this area are tuned to the entire face, instead of specific facial features**. 

![](/images/facial_tuning.png)

This figure shows how neuron activation levels change with inversion of faces. Thatcherized means that the eyes and the brows are inverted on the face. We see that unsurprisingly, the normal face gives the highest level of activation marked in blue. Thatcherizing a normal face would cause a significant drop in activity, marked in red. However, if the face itself is inverted, then thatcherizing this inverted face has no inpact on the activation level, with the yellow (inverted) and green (thatcherized inverted) having approximatly overlapping curves. This shows that our selectivity for normal eyes and brows are lost if we invert the whole face, even though the thatcherized inverted face has correct orientation for eyes and brows although at a misplaced positition. Hence, this experiment provides strong evidence that our tuning for faces is holisitic, instead of partial. 

#### 1.3.3 The tethering hypothesis

One of the most important question in psychology and neuroscience is about what is innate and what is learned. Same question applies here: Is our brain following a strict genetic plan in cortical organization? How does a brain cell know which visual area it belongs to? How does plasticity comes into play? 

![](/images/tethering_hypo.png)

Buckner and Krienen proposed the tethering hypothesis back in 2013, arguing that the hierarchical organization of visual cortices is a product of both genetic programming and visual experience. They proposed that V1 and MT act as "anchors" and are hard-coded by genetic programs. Once those two areas are pinned down on the cortex, the other areas form automatically through our visual experiences. 

<!-- It is known that when babies are still in their mother's wombs, the retinas would send randomized activation signals through optical nerves and along up the hierarchy.  -->


