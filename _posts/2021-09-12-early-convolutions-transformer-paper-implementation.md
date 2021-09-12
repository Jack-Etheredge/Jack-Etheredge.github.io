---
layout: post
title: Implementing "Early Convolutions Help Transformers See Better" in PyTorch
subtitle:  
image:
---

As I discussed in my previous blog post, the paper ["Early Convolutions Help Transformers See Better"](https://arxiv.org/abs/2106.14881) replaces the patchify operation in the original vision transformer paper with convolutions.

Here's the code to replace the patchify operations: 
```python
n_filter_list = (channels, 48, 96, 192, 384)  # hardcoding for now because that's what the paper used

self.conv_layers = nn.Sequential(
    *[nn.Sequential(
        nn.Conv2d(in_channels=n_filter_list[i],
                    out_channels=n_filter_list[i + 1],
                    kernel_size=3,  # hardcoding for now because that's what the paper used
                    stride=2,  # hardcoding for now because that's what the paper used
                    padding=1),  # hardcoding for now because that's what the paper used
    )
        for i in range(len(n_filter_list)-1)
    ])

self.conv_layers.add_module("conv_1x1", torch.nn.Conv2d(in_channels=n_filter_list[-1], 
                            out_channels=dim, 
                            stride=1,  # hardcoding for now because that's what the paper used 
                            kernel_size=1,  # hardcoding for now because that's what the paper used 
                            padding=0))  # hardcoding for now because that's what the paper used
self.conv_layers.add_module("flatten image", 
                            Rearrange('batch channels height width -> batch (height width) channels'))
```

Of course, these many hardcoded values could/should be updated to variables if you wanted to experiment with kernel sizes, strides, and filter numbers different from those used in the paper. I'll likely update the code soon to make these default values instead of having them hard coded.

The `out_channels=dim` part of the 1x1 conv takes care of making sure that the number of channels matches the input dimension of the transformer blocks.

One thing that wasn't immediately obvious to me when I went to implement this is that the output of the 1x1 conv is still not correct to be fed into the transformer blocks. I debugged by calculating what the outputs would be and then using hooks to confirm. `Rearrange('batch channels height width -> batch (height width) channels')` takes the (batch, channels, height, width output) from the 1x1 conv and both rearranges the axes and flattens the outputs to a rank-3 tensor with dimensions (batch, height*width, channels).

Also, if you're more familiar with tensorflow.keras, the way that PyTorch specifies the number of filters in convolution layers is a little different. In Keras, you specify the filter number per layer explicitly with `filters`, while in PyTorch you have `in_channels` and `out_channels`. Of course, the `out_channels` is equal to the number of filters.

Apart from the block of code above, the rest of the architecture is a vanilla transformer encoder block, so you could use whatever fancy linear transformer you wanted or [the original O(n**2) transformer](https://arxiv.org/abs/1706.03762).

References:
- "Early Convolutions Help Transformers See Better" ([arXiv](https://arxiv.org/abs/2106.14881))
- "Attention Is All You Need" ([arXiv](https://arxiv.org/abs/1706.03762))
- "An Image is Worth 16x16 Words: Transformers for Image Recognition at Scale" ([arXiv](https://arxiv.org/abs/2010.11929))
