---
layout: post
title: Using Keras with multi-GPU with TensorFlow backend
subtitle: tutorial blog post
thumbnail-img: images/post_link_photos/maxime-rossignol-266384-unsplash.jpg
---

So you've got Keras running fine one one GPU either using a personal system or AWS (likely a p2.xlarge instance), but you'd like to have more power.

The next largest instance on AWS is the p2.8xlarge, which has 8 times as many K-80s (8 of them instead of 1).

Fortunately, Keras' performance is nearly linear with the number of GPUs, until 16 GPUs if I recall correctly. (I'll update this after I hunt down the articles again so that I can reference them).

Also fortunately, the p2.8xlarge costs exactly 8x what the p2.xlarge does. That means that if you really need the speed boost to get your training done quickly, you can pay the same amount for the same amount of training but do it 8 times faster.

It was surprisingly difficult to piece together how to actually achieve this from online searching, but it's rather simple once you know how to do it:

First off, add this import:
```python
from keras.utils.training_utils import multi_gpu_model
```

After you've defined your model's architecture, add this line:
```python
with tf.device('/cpu:0'):
   Omodel = model
model = multi_gpu_model(Omodel, gpus=8) # update this to the number of GPUs you ACTUALLY have; it's 8 for the p2.8xlarge
```
I've hard-coded the number of GPUs here. There is a way to determine the number of GPUs programmatically and variablize this snippet, but if you read my side notes below you'll see why I did away with that option as a "better safe than sorry" decision.

Assuming you've been showing the model summary after defining the architecture, you'll now need to switch out the name of the model you're pulling the summary from. Otherwise you'll get a silly summary that basically just informs you that you're splitting the jobs across 8 GPUs.
```python
Omodel.summary(line_length=150)
```

Also, if you're not already doing so, you can determine how much you're utilizing your GPU(s) by running in bash:
```bash
watch nvidia-smi
```

Now you can increase your batch size 8-fold. If your architecture/data are massive, as in the case of my last project involving segmentation of 3D MRI volumes, this might just mean going from a batch size of 1 to a batch size of 8, but that will make a world of difference.

----

Some side notes:

If you're running on AWS, I recommend getting your model running on 1 GPU first (the p2.xlarge) and doing your debugging in that instance, then adding these little snippets of code and switching the instance type to the p2.8xlarge.

AWS has a few GPU compute instance options. There are more powerful instances than the p2 instances, including the p3 instances. I wasn't able to get access to them, but if you can, then that's great, because the p2 uses K-80 GPUs, which are getting a bit dated now.

Most of the features of Keras work fine with multi-GPU, although I've had some issues with certain callbacks, like save_best_weights. This can be gotten around by using an epoch of 1 in a for loop. It's not ideal, but it works fine.

Many people have had issues with multi_gpu_model if they run this code:

```python
from tensorflow.python.client import device_lib
print(device_lib.list_local_devices())
```
As such, I recommend running it only to check your devices the first time, but don't run it before you're actually going to train the network.

If you're using batch normalization layers, GPUs can sometimes introduce NaNs if they are not given training examples. This can happen if your number of training samples isn't divisible by your number of GPUs, since on the last training batch of each epoch, some GPUs will get samples and some won't. There are two obvious solutions to this problem: 1) don't use batch normalization layers if you don't really need them, 2) drop a few examples to make the dataset divisible by the number of GPUs. Most non-biological datasets have tons of training data, so dropping less than 8 examples will be trivial. Otherwise, you could find a clever way to randomly exclude x-number of examples such that all data is used, just not every epoch.

Enjoy.

----    
