---
title: The image, an array of pixels
weight: 3
---
What is an image? In image analysis, an image is a collection of data that represents visual information. When imported into a coding environment, this visual information is converted into an array of pixels. Each pixel in this array has a specific intensity value that represents the brightness at that point in the image.

## Pixel intensity values

For 8-bit images, the pixel values range from 0 to 255. In microscopy, we usually work with 16-bit images because they offer a higher bit depth. In other words, the pixel values range from 0 to 65535, allowing for finer gradations of intensity. 

{{< figure src="media/pixels_fig.png" alt="Image of a pixel array" caption="Figure 1: Schema of pixel intensities in a digital image. Each square represent a pixel which its intensity value." >}}

## Image dimensions

For simple 2-dimensional (2D) image, the array has two dimensions -height and width. We can inspect the dimensions of an image using code.

{{< figure src="media/ia_arrayshapeIN1.png" alt="Image of a pixel array" caption="" >}}

The output would be

{{< figure src="media/ia_arrayshapeOUT1.png" alt="Image of a pixel array" caption="" >}}

However, in microscopy images are often multi-dimensional to include additional information such as time, z-stacks or different fluorescent channels. These multi-dimensional images are represented as arrays of arrays. For instance, a 3D image might have the shape (z, height, width) and a 4D images might have the shape (time, z, height, width). 


## Did you enjoy? Then share this post:

<div class="social-share">
  <a href="https://twitter.com/share?url={{ .Permalink }}&text={{ .Title }}" target="_blank">Share on Twitter</a> |
  <a href="https://www.linkedin.com/shareArticle?mini=true&url={{ .Permalink }}&title={{ .Title }}" target="_blank">Share on LinkedIn</a> |
  <a href="https://www.facebook.com/sharer/sharer.php?u={{ .Permalink }}" target="_blank">Share on Facebook</a>
</div>