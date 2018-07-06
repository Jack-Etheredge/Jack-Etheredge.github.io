---
layout: post
title: Brain tumor segmentation with 3D UNet CNN
description: project blog post
image: assets/images/pic06.jpg
---

For my final Metis project, I decided to tackle brain tumor segmentation. My Github repo for the project: https://github.com/Jack-Etheredge/Brain-Tumor-Segmentation-3D-UNet-CNN

This was my first time dealing with MRI data, so I had several things to learn.

Also, even though my PhD is in neuroscience and developmental biology, this was my first time really doing much with human brain data. I've always dealt in model organisms before.

I achieved this using Keras with Tensorflow as the backend.

This U-Net was built for the [MICCAI BraTS dataset][BraTS].

This U-Net was based on the one constructed in [this paper (Isensee 2017)][Isensee 2017].

I achieved a dice score of 0.78 and weighted dice score of 0.67. The dice score is effectively the percentage of pixels that are the same between the prediction and the ground truth segmentation masks. More accurately these are "voxels" (volume elements) in the case of 3D volumes.

Ground Truth:               |  Prediction:
:-------------------------:|:-------------------------:
![ground truth](/images/Ground_Truth_Example.png){:class="img-responsive"}  |  ![prediction](/images/Prediction_Example.png){:class="img-responsive"}

Remove this redundancy:
I achieved a 0.78 whole-tumor test dice score. The dice score is simply the percentage of pixels that are the same for the ground truth and predicted segmentation masks. In the case of 3D images, it's more accurate to say that we're checking the voxel-wise accuracy rather than pixel-wise accuracy, since we're truly dealing with voxels (volume element, the 3D analogue of a pixel).

There are different grades of glioma. The BraTS dataset is separated into low-grade glioma (LGG) and high-grade glioma (HGG, also known as glioblastoma). I treated both tumor types (LGG and HGG) together. Papers that separate the task for each tumor subtype can perform better with respect to the dice score, but this is less appropriate for automation, because having different models for different tumor subtypes requires prior physician annotation to work correctly.

It is worth mentioning that a 3D U-Net is not the only way to tackle this problem. It could be done slice by slice with a 2D U-Net, or even without a U-Net using a more traditional convolutional-deconvolutional segmentation network without the concatenation between the convolution and deconvolution steps that are the defining element of a U-Net.

Future (tenuously) related project ideas:
- Cartoon machine: upscaling, colorizing, and style-transforming low resolution black and white cartoons. This is a rather ambitious project idea, and I think going all out would include feeding a transcript and producing audio in the voice of different voice actors.

I heavily modified code from two sources to get this project to work:

- Original code for building the U-Net was from this repo: [https://github.com/ellisdg/3DUnetCNN](https://github.com/ellisdg/3DUnetCNN)
- Original code for the data generator: [https://stanford.edu/~shervine/blog/keras-how-to-generate-data-on-the-fly.html](https://stanford.edu/~shervine/blog/keras-how-to-generate-data-on-the-fly.html)

[Isensee 2017]: https://arxiv.org/abs/1802.10508
[BraTS]: https://www.med.upenn.edu/sbia/brats2018/data.html
