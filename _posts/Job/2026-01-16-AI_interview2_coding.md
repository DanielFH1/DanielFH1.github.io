---
title: "Preparing ML/DL CODE interview"
date: 2026-01-16
toc: true
toc_sticky: true
use_math: true
categories:
  - job
published : false
---

# 1. Can you implement a 2D Convolution operation from scratch using Python (assuming input is a 2D array)? Also, how do you calculate the output size?

## Code 

$$ \text{Output}_{\text{size}} = \frac{\text{Input} - \text{Kernel} + 2 \times \text{Padding}}{\text{Stride}} + 1 $$

To keep it simple for this implementation, I will assume stride = 1, and no padding.

```python 
def convol2d(image, kernel):
    # 1. Get dimension
    i_h , i_w = len(image), len(image[0])
    k_h , k_w = len(kernel), len(kernel[0])

    # 2. Calculate Output dimensions
    o_h = i_h - k_h + 1
    o_w = i_w - k_w + 1

    ouput = [ [0]*o_w for _ in range(o_h)]

    # 3. Perform convolution
    for y in range(o_h):
        for x in range(o_w):
            # Calculate sum of element-wise product
            val = 0
            for ky in range(k_h):
                for kx in range(k_w):
                    val += image[y+ky][x+kx]* kernel[ky][kx]
            output[y][x] = val
    return output
```

I'll implement a basic 2D convolution with stride 1 and valid padding. 
The time complexity is $O(H \times W \times k^2)$ based on the formula. 
First, I calculate the output height and width by subtracting the kernel size from the image size and adding 1.

Then, I'll use nested loops to slide the kernel over the image.
For each position, I perform an element wise multiplication between the image patch and the kernel, then sum the results to get a single pixel value for the feature map. 

