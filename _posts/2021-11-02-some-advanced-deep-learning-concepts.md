---
layout: post
title: Some advanced deep learning concepts
subtitle:  
image:
---

## The TLDR:

Here's a nested list of topics that might be interesting to you if you're tired of seeing the same "intro to deep learning" explanation of AlexNet for cats and dogs and want to dive deeper into some slightly more niche areas of deep learning:

1. Probability calibration
    1. temperature scaling
2. Recreating simple machine learning models in deep learning frameworks
    1. Linear and logistic regression are just neural nets with 1 hidden layer
    2. Softmax regression
3. Debiasing models
4. Model efficiency
    1. Distillation
    2. Student-teacher architecture
    3. Quantization
    4. EfficientNet
5. Data augmentation
    1. beyond rotation, translation, etc
    2. MixUp
    3. CutMix
    4. Cutout
    5. AugMix
6. Graph neural networks
7. Bayesian neural networks
8. Normalization
    1. batch vs layer vs group norm
9. Special optimizers and learning rate schedulers
    1. Ranger
    2. LRFinder
    3. One-cycle fitting
10. Regularization
    1. beyond dropout and weight decay
11. Semi-supervised learning
12. Self-supervised learning
13. One shot and zero shot learning
    1. Siamese networks
    2. Transfer learning
14. Genetic algorithms
    1. aka "look mom, neural nets without gradient descent!"
15. Active learning
    1. Closely related: Cleaning up your dataset with the help of your model
    2. (typically this requires performing probability calibration)
16. Online learning
17. Federated learning
18. Computer vision beyond classification
    1. Object detection
    2. Semantic segmentation
    3. Instance segmentation
19. Special convolutional layers
    1. gated temporal convolutions
    2. depthwise separable convolutions
20. Homomorphic encryption
21. Generative adversarial networks (GANs)
22. Special loss functions
    1. focal loss
23. Reinforcement learning
    1. Multi-agent reinforcement learning
    2. Environments with partial observability
24. Transformers (self-attention)
    1. Linear transformers
    2. Vision transformers
25. Neural architecture search
26. Hyperparameter tuning paradigms
    1. Random search
    2. Bayesian optimization
    3. Hyberband
    4. BOHB (Bayesian optimization hyperband)

Note: I will add links to future blog posts as well as fill in more details and examples over time.

## Why is this important to anyone? Who is this for?

It's important to have a target audience in mind while writing anything or giving a presentation. I still remember my PhD advisor being really upset with me when I gave an internal progress update talk about my research with a bunch of intro slides as if I was talking to a general audience with no concept of the background and motivation of the lab's research. The time spent on those slides was a waste of every single lab member's time. I've imagined extrapolating that sentiment out into the context of the global landscape of the internet's machine learning content and audience. It would be easy to rehash and subtly tweak [deeplearning.ai](http://deeplearning.ai) and [fast.ai](http://fast.ai) material (as examples, not that those are the only quality sources of the same information). However, that wouldn't really serve many people at this point. There is a glut of intro to machine learning and intro to data science material out there. I think there's no point in an individual adding another introductory level explanation of these topics unless it's for the purpose of helping them learn or they seriously think that they can explain it substantially better than deeplearning.ai, fast.ai, 3Blue1Brown, Statquest, etc. For me, personally, I think there are very few concepts covered by these resources that I could explain with greater clarity as succinctly.

There's still a valley of despair, however, separating this overwhelming volume of redundant introductory material and reading papers from arxiv yourself on a daily basis.

As such, I thought it might be nice to give a bird's-eye-view of some of the topics that I've come across over a few years of reading machine learning papers and following machine learning researchers on Linkedin, Twitter, and Youtube.

## Why did you structure this blog post in such a strange way?

I recently read a great book, but I found myself really frustrated at points by the structure. For now I won't name the book, because I think there's more that's good about it than bad about it. (Also, I've never written a book, so take all of this with a grain of salt.) Like most technical textbooks, each chapter started with pieces and built up from there. We might call this a bottom-up approach. By contrast, many people point to [fast.ai](http://fast.ai) as a good example of a top-down approach to teaching machine learning. I think this is the terminology Jeremy Howard himself uses when describing the two different extremes of how to teach and learn topics, but it's been a couple years since I watched the lectures.

Suffice it to say, this bottom-up approach is common to STEM textbooks. So far so good, only the simplifications made along the way weren't explained to be simplifications, and better ways to do things were explained much later in the book. If you're trying to get everything you can from the book in a single pass, this is likely to frustrate you, because you spent a lot of effort trying to understand in detail suboptimal methodologies.

In addition, there were several cases where it wasn't obvious why something was being explained until near the end of the chapter. You had to trust the authors and be patient and hope that your lingering questions would be explained eventually and that different choices were made for good reasons.

However, this isn't the first time I've had similar frustrations. I've felt some degree of this with nearly every textbook I've ever read. In fact, I think it's no small part of what makes reading most textbooks so painful for most people. 

I think it's much more difficult to sustain interest and a vision for the narrative arc with the bottom-up method of teaching than it is with the top-down method of teaching. I find myself fighting the urge to skip ahead with most textbooks. I think this is because I want to get to the parts that I care about because it's unclear to me why I should care about the component pieces. Sometimes I can't resist this urge and I skip ahead only to then return to the skipped sections once the motivation is clear to me.

So I wanted to experiment with writing my next several blog posts the way I think I would hope for things to be written. I'll start with the essence of what I want to communicate and then go into successively more detail from there. Thus, if at any point someone has exhausted their interest with the post, they'll have walked away at any exit point with (hopefully) the most salient points I was trying to communicate.

## Waxing poetic about top-down teaching and learning:

To analogize to learning about cars (which is perhaps dangerous since I don't own a car and I'm not a mechanic): 

You don't start caring about cars or start studying cars by first learning how a catalytic converter works. Chances are, if you care enough to understand a catalytic converter, you're already invested in understanding all the components of a car. However, many people just want to know what a car is and what you can do with a car. What is a car? What kinds are there? Where can I get one? What can I do with it? How do I drive a car? A dramatically smaller subset of people will care enough to dive into car history and the mechanics of car parts after having that level of information.

Similar analogies are used for explaining the utility of object oriented programming. If all I want to do is drive a car, but never build one, I don't need to understand how a catalytic converter works for you to teach me how to use the pedals and steering wheel.

Put another way: If you teach me why I should care about cars, maybe I'll become so interested that I'll want to learn about car parts. Conversely, I'm extremely unlikely to care about cars just because you taught me about car parts.

To get slightly more philosophical about things, the sheer volume of information created by mankind makes it unsustainable to teach everything from the ground up. Regardless of how much of a polymath you aspire to be, you will never understand most things from bare basics along with the entire history of the failed experiments it took to arrive at the modern incarnation of the things you consume. As a point example, you likely use a microwave daily without truly understanding how it and all its various components work. If you do, then I'm sure you can imagine for yourself plenty of different examples.

For every subject and person, there's an individual and arbitrary depth of knowledge that's sufficient for that subject based on what they hope to do. Very few people want or need to build a microwave from scratch and that shouldn't prevent most people from using microwaves. I think that the median knowledge level in STEM would increase if we switched our teaching methods from bottom-up to top-down. I think we'd lose a lot fewer people because they stopped prematurely and never saw the pay-off for learning about seemingly obscure components and the history of a field they were never convinced of the utility of from the onset.