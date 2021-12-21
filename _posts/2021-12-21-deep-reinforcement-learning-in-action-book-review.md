---
layout: post
title: Deep Reinforcement Learning in Action - book review
subtitle:  
image:
---

I recently read the book "Deep Reinforcement Learning in Action".

## What did I think about the book?

I enjoyed the book and thought it was a great introduction to deep reinforcement learning. It uses PyTorch, not some framework that was made specifically for the book. This is a huge benefit if you already know PyTorch or want to learn it.

It provides formal math, string diagrams, and Python code for many concepts. Seeing the same concept presented multiple ways not only allows you to understand it more easily based on your level of comfort with with each mode of expression, but it also allows you to become more comfortable with the ones that currently require more effort for you.

I hesitate too be too critical of any book, since I haven't written one myself and I'm sure it's a monumental endeavor. That said, there are some things that I didn't like. The book didn't cite many sources. Some Googling of different details in the book show that some of the examples in the book were very clearly modeled after papers that weren't cited. Presumably this was an oversight and not intentional. Decisions in the code weren't always explained and the same thing was accomplished multiple ways in different chapters of the book. I've been refactoring and extending the notebooks in [a fork of the repo](https://github.com/Jack-Etheredge/DeepReinforcementLearningInAction), but it's still a work in progress. 

The book covers several topics, starting with the basics.

Here are some of the topics covered:

1. dynamic programming
2. multi-arm bandit
    1. epsilon-greedy
    2. softmax selection policy
3. constructing a DQN in PyTorch
4. counteracting catastrophic forgetting with experience replay
5. target network to stabilize learning
6. on-policy vs off-policy learning (Q learning)
7. model-based vs model-free algorithm
8. Policy network and policy gradients
    1. REINFORCE algorithm
    2. n-step learning
9. actor-critic methods
    1. distributed training as an alternative to experience replay buffer for batch updates
    2. distributed advantage actor-critic (DA2C)
10. evolutionary algorithms
11. distributional DQN
12. curiosity
    1. inherent curiosity module
13. multi-agent reinforcement learning
    1. mean field Q-learning
14. attention (transformer) RL models

While explaining these topics, the book also has some brief asides and high level introductions to graphs. Some of the asides in the book seem a bit meandering and it can take a while to understand how they eventually tie back into the topic of the chapter at hand. I found myself frustrated with the book a few times for this reason, but it's possible this is a personal thing.

## Why did I read the book and why do I care about reinforcement learning?

There are a few areas of deep learning that I've been intending for a long time to read about, understand, and do some small projects with to deepen my understanding and give me practical experience using them. Among these subjects are deep reinforcement learning, generative models (particularly GANs, VAEs, DDPMs, and generative transformer models), and graph neural networks. I've actually read and made notes on a large number of generative model papers in addition to reading a great book on generative deep learning, but I've yet to do any substantial projects with them, which is something I should remedy soon.

Reinforcement learning and generative models seem particularly relevant to creating artificial general intelligence. Reinforcement learning is how humans learn (sort of, and some of the time) and the way that we process information is to constantly predict the future and use the errors in our predictions to learn how to make a better mental model of the world*. Graph neural networks appear to be a way to make sense of data with many different structures, which seems to me like they'd probably help as well. That said, of the three subjects, I understand graph neural networks by far the least at present. Perhaps my enthusiasm for them will dramatically increase or decrease with more studying.

For much of my life so far I've had trouble focusing and prioritizing because I find so many things interesting. I feel pulled in a million directions constantly by the number of things that one can learn or do. I already felt this when I was still studying biology, but with the explosion of machine learning as a field in recent years, it's difficult not to overwhelm yourself with the dizzying pace and volume of different models. It's impossible to be an expert in the entire field of machine learning now because the field is too large with too many subdomains and research directions. That said, throughout the many things I’ve wanted to be during my life, I’ve always been passionate about human health and environmental conservation.

Why care about artificial general intelligence, then? I think it could help us with both. An artificial general intelligence might help us solve human problems much faster.

I've been fascinated with reinforcement learning for a long time and have studied it off and on over the past few years. I watched the original youtube videos for the 2018 UCL x Deepmind deep reinforcement learning course and did some additional reading to understand multi-arm bandits, AlphaGo, AlphaStar, and AlphaFold. The UCL x Deepmind course made me aware of the Rainbow DQN  paper ([Rainbow: Combining Improvements in Deep Reinforcement Learning](https://arxiv.org/pdf/1710.02298v1.pdf)) about a year after it was published. Hado van Hasselt taught the class and he was one of the authors on the paper. After reading the Deep Reinforcement Learning in Action book it occurred to me just how much one would have to understand if they went on a deep dive through Rainbow DQN as a starting point for learning reinforcement learning and recursively read more papers until a good grasp of all the components that went into Rainbow.

## Some Final Thoughts

I've started reading the book "Foundations of Deep Reinforcement Learning: Theory and Practice in Python", which also seems like it's going to be quite good. I'm not far enough in to make a good comparison yet, though. I also have a copy of "Grokking Deep Reinforcement Learning". There will presumably be a lot of overlap in the books, but I'm hoping that seeing the same information presented different ways and with different emphasis from the different authors will be useful. I also assume there's rapidly diminishing returns to this approach. Time will tell if I find this approach useful and return to reading papers exclusively instead of the other books.

I previously wrote an extremely terse post about what I consider the best resources for early career machine learning engineers or data scientists. Eventually I'll write posts about some of my favorite resources for different math, machine learning, and computer science topics that's more extensive with my thoughts on the particular strengths of the various books, courses, and other types of resources I've found valuable. 

*These statements are gross oversimplifications, but are generally true per my current understanding of human neuroscience.