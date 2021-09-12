---
layout: post
title: Thoughts on "Early Convolutions Help Transformers See Better"
subtitle: Alternate title - Transformers outperform CNNs . . . when you add convolutions to them 
image:
---

A work friend I used to have weekly virtual meetings with to discuss machine learning papers messaged me a couple weeks ago saying "There's another idea we had that turned out to be a good one," along with a link to a paper that had been uploaded to arXiv the day before.

After checking the title and abstract, I responded with "Yeah. Story of my life."

A month ago, FAIR and UC Berkley came out with the paper "Early Convolutions Help Transformers See Better" ([arXiv](https://arxiv.org/abs/2106.14881) ). 

Since their introduction in the 2017 paper "Attention Is All You Need" ([arXiv](https://arxiv.org/abs/1706.03762)), transformers have taken over NLP to the point that they've all but completely replaced GRUs and LSTMs in that space. Lately transformers have been coming after CNNs too with the vision transformer (ViT) architecture first introduced less than a year ago in the paper "An Image is Worth 16x16 Words: Transformers for Image Recognition at Scale" ([arXiv](https://arxiv.org/abs/2010.11929)).

However, pairing CNNs for feature extraction with RNNs has been common for years, so it was a natural thought to imagine when seeing vision transformer that perhaps ditching the cheap convolution operations entirely might not be optimal, a thought which I had voiced to my friend when ViT came onto the scene. Transformers have been replacing RNNs, by and large, but CNNs have remained state of the art for vision until quite recently<sup>*</sup>. Even for sequence data, convolutional layers are still frequently paired with LSTMs or GRUs. Thus, it was surprising, honestly, not to see the CNN + Transformer architecture appear in the literature, since it seems like the next logical step if you reductionistically consider Transformers as "better RNNs" in your mental landscape of deep learning architectures.

One option to combine CNNs and ViT would be to use the CNNs for feature extraction and then feed the features output by the CNN to the "vanilla" ViT using the standard patchify operation. It turns out this isn't the first time this has been conceived of (see [here](https://openreview.net/forum?id=M1VznPOV5jV)). In fact, going back to the original ViT paper, a "hybrid architecture" was proposed that also does exactly this - passing the raw image through a CNN and then feeding the feature map from the CNN to the patchify operation.

CNNs are translation invariant, meaning that you can shift something around in the image and it will still be classified the same, which is a feature of CNNs that arises from pooling operations. (Invariance and equivariance to scale and rotation aren't naturally a result of the convolution or pooling operations, and are instead frequently part of data augmentation regimes to make the model more robust to input variations of this nature.) 

ViT is not inherently translation invariant, as the transformer is instead permutation invariant. Transformers are built with sequences in mind, which means that ViT uses a sequence of image patches.

This new paper "Early Convolutions Help Transformers See Better" replaces the patchify operation in ViT with convolutions. Patchify in the original ViT paper uses non-overlapping patches, while this CNN+ViT paper uses standard convolutions, which normally have a stride smaller than the kernel, and thus operations are being performed on overlapping patches.

The focus of this paper was on the optimization behavior of the network. They claim that ViT is a bit finicky to optimize, and is sensitive to learning rate and weight decay (~ L2 regularization) choices, converges slowly, works with AdamW, but not SGD, and that their CNN+ViT architecture fixes all of these shortcomings. An additional point that is particularly interesting to me is that this architecture achieves state of the art (SOTA) results on ImageNet, which makes me think that this paper might be the turning point where transformers might begin wrestling with CNNs for computer vision task supremacy.

Both the architecture change and the core results of the paper are summarized in Figure 1 of the paper. The rest of the paper goes on to detail the experiments, including some ablation tests and the stability of larger models.

It's always possible with deep learning papers that part of the magic sauce is in the exact training paradigm, including the data augmentation used and the exact set of hyperparameters tested, but the fact that the focus of this paper was specifically to test the optimization behavior of the architecture, several different learning rates and weight decay values were used, so this may alleviate a substantial amount of the concern on this front. The data augmentation was compared directly to the that of the Data-efficient image Transformers (DeiT) paper "Training data-efficient image transformers & distillation through attention", which employs a lot of recent data augmentation tricks ([arXiv](https://arxiv.org/abs/2012.12877)).

I'm excited by this architecture and want to play with it soon. I might implement it myself as a fun project, particularly since the code isn't associated with the paper at present. Update: I implemented this paper [here](https://github.com/Jack-Etheredge/early_convolutions_vit_pytorch). 

The world is a big place. There are 7 billion people. Information is abundant on the internet. Chances are, if you have a great idea, someone else does too. If you don't do it, someone else will. There are two ways to look at this: 1) one in which you must do every good thing that comes to your mind because if you don't, someone else will beat you to it, or 2) one in which you allow yourself to let go of the ambition to do everything you're interested in seeing done in the world. The latter is how I managed to let go of being a wet lab biologists doing bench science. The former is how I feel daily looking at the influx of machine learning publications.

Stuff went wrong in my PhD and I will likely never recover from that in some respects. I got extremely sick and didn't end up with first author publications for multiple reasons, not least of which being the aforementioned sickness. I'm healthy now and happier for having traded wet lab experiments at the bench for machine learning and working at a computer. I've also matured a lot in the interim, as one would hope and expect. Fortunately, I like machine learning and my current job quite a bit. Unfortunately, I might never be able to break into ML research and publish in that field either. But survivor bias in academia and the cold start problem of trying to contribute to a research group when you don't already have publications are topics for another day. Here's hoping I'm wrong, though, because there is no shortage of exciting work being done in the field that constantly inspires plenty of ideas for research I'd love to do.

<sup>*</sup>As of today, a look at ImageNet classification performance shows that EfficientNets (a type of CNN first introduced in "EfficientNet: Rethinking Model Scaling for Convolutional Neural Networks" ([arXiv](https://arxiv.org/abs/1905.11946v5))) were still in the lead until a pair of Google Brain papers were uploaded to arXiv on June 8th and June 10th 2021 which use transformers ("Scaling Vision Transformers" ([arXiv](https://arxiv.org/abs/2106.04560v1)) and "Scaling Vision with Sparse Mixture of Experts" ([arXiv](https://arxiv.org/abs/2106.05974v1)), respectively).

Acronyms:
- CNN: convolutional neural network
- DeiT: Data-efficient image transformer
- FAIR: Facebook AI research
- GRU: gated recurrence unit (a type of recurrent neural network)
- LSTM: long short term memory (a type of recurrent neural network)
- NLP: natural language processing
- ViT: vision transformer

Update 9/12/21: Added link to my paper implementation (PyTorch). Fixed typo.