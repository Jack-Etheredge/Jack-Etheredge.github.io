---
layout: post
title: Brain tumor segmentation with 3D UNet CNN
---

For my final Metis project, I decided to tackle brain tumor segmentation. My Github repo for the project: https://github.com/Jack-Etheredge/Brain-Tumor-Segmentation-3D-UNet-CNN

I achieved this using Keras with Tensorflow as the backend.

This UNet was built for the MICCAI BraTS dataset: https://www.med.upenn.edu/sbia/brats2018/data.html

I achieved a dice score of 0.78 and weighted dice score of 0.67. I treated both tumor types (LGG and HGG) together. Papers that separate the task for each tumor subtype can perform better

The UNet was based on this paper: https://arxiv.org/abs/1802.10508 

I heavily modified code from two sources to get this project to work:

- Original code for building the UNet was from this repo: https://github.com/ellisdg/3DUnetCNN
- Original code for the data generator: https://stanford.edu/~shervine/blog/keras-how-to-generate-data-on-the-fly.html

The model was based on that used by Isensee 2017.

I achieved a 0.78 whole-tumor test dice score. The dice score is simply the percentage of pixels that are the same for the ground truth and predicted segmentation masks. In the case of 3D images, it's more accurate to say that we're checking the voxel-wise accuracy rather than pixel-wise accuracy, since we're truly dealing with voxels (volume element, the 3D analogue of a pixel). 

This was my first time dealing with MRI data, so I had several things to learn.

Also, even though my PhD is in neuroscience and developmental biology, this was my first time really doing much with human brain data. I've always dealt in model organisms before.

Future (tenuously) related project ideas:
Cartoon machine: upscaling, colorizing, and style-transforming low resolution black and white cartoons. This is a rather ambitious project idea, and I think going all out would include feeding a transcript and producing audio in the voice of different voice actors.

