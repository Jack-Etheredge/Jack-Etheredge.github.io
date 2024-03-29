---
layout: post
title: Machine learning project lessons I've learned
subtitle: Mistakes to avoid
image:
---

Here are some of the lessons I've learned so far in my career as a machine learning engineer and from doing machine learning projects. This is advice I'd try to impress upon my younger self if I could send a message back in time.

1. Always use pipelines and data generators.
   
   Shortcuts here will cost more in the long run. Pipelines eliminate drift between training and inference preprocessing steps and dramatically reduce the number of steps to keep track of regarding which manipulations you've performed on various slices of your data. Scikit learn pipelines are great, but are not the only option. For deep learning, there's also Tensorflow Transform (part of Tensorflow Extended aka TFX). Keras has special stateful transformation layers that can be incorporated directly into your model as well. KerasClassifier and KerasRegressor exist as part of Tensorflow and allow you to use Keras models with scikit learn pipelines. Skorch is a Python package that solves that fulfills the same end for PyTorch. If you have complicated data augmentation steps or training data generation paradigms, it will pay dividends to create data generators for your model(s) early on in your project rather than having to keep track of data manipulations separate from your model.
2. Stop using notebooks and creating several variants of that notebook.
   
   Write scripts and write logs. Ideally also write tests. Again, shortcuts here will cost more in the long run. I use RStudio and then Jupyter notebooks when I was learning bioinformatics and machine learning. Neither one instilled in me good software engineering best practices. I would create duplicates of notebooks endlessly and keeping track of my versions and train of thought during and after a project was a nightmare. If this sounds familiar, please do yourself a favor and switch to writing scripts. Read a little bit about software engineering best practices. Look at some code from open source software that you personally use if that helps you. Using notebooks less and treating projects more like building software was an inevitable side effect of being employed as a machine learning engineer rather than a data scientist, but it's also been one of the most if not the single most important changes that has caused me to grow in the space. Most production code is not written in notebooks. Most maintainable code is not written in notebooks. Notebooks can be a great way to blend code with exploratory data analysis and visualizations, but they don't lend themselves naturally to version control and writing good software.
3. Maximize learning and automation. Minimize grinding.
   
   Spend more time learning better ways to do things well rather than frantically cobbling stuff together. If you find yourself grinding away at something, it's probably worth stepping back and seeing if there's a fundamentally better way you can learn to do something. It's easy to get stuck in the mindset of just seeing something across the finish line, but learning more efficient methodologies and tools will pay dividends on your current project and all your future work as well. I have a post it note on my desk to remind me of this that simply says "Maximize learning and automation. Minimize grinding."
4. Start with GPUs as early as it makes sense to.
   
   When does it make sense to you? Once your code runs without error on CPU and the training time has become the bottleneck. Before then, you'll move as slow or slower on a GPU as you would a CPU, and it will cost you far more if you're paying for cloud instances. However, once the CPU becomes the bottleneck, you can pay less for the total training time on a GPU, because you could get a 10x or 20x speedup. Getting GPU training set up initially can be a pain due to finicky CUDA driver installation and tightly coupled driver and deep learning framework versions, but after maybe an hour of debugging at most in most cases, you'll reap some serious benefits. Thus, to reiterate, it's worth switching the moment the training time is the bottleneck.
5. Use tensorboard.
   
   This one is a bit more up to personal taste, and still a bit aspirational for me. Tensorboard is quite easy to use with both TensorFlow and PyTorch (and thus Fastai), but I never remember to use it until I'm already deep into a new project. It can help quite a bit, particularly when you want to determine how several different models are performing relative to each other quickly and visually.
6. Use hyperparameter tuning tools early.
   
   Switch to using random search or bayesian hyperparamater optimization as quickly as possible after identifying the most important hyperparameters, including architecture. It's too easy to get sucked into obsessively watching your model training and hand testing different hyperparameters. This is a giant waste of your life. That time is better spent learning ways to hand this task over to the computer and then with all of the personal time you've regained after that initial investment, reading deep learning papers, napping, playing video games, teaching, or whatever else enriches your life the most.

*This post is a work in a progress.*