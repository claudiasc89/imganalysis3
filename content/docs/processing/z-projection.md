---
title: Z-projections, finding the best focused plane
weight: 1
draft: false
---
When it comes to capturing intricate intracellular structures or achieving the sharpest focus in microscopy images, acquiring Z-stacks is crucial. Z-stacks allow us to collect a series of images at different focal planes, providing a comprehensive view of the specimen. When processing these images, we have several options: we can select the best-focused slice or create a Z-projection to reconstruct our structure of interest.

Manually selecting the best Z-plane can be tedious, especially when it varies across images. However, there's good news! This process can be automated, making it faster and more precise, ensuring that each image benefits from the optimal Z-stack.

## How do we find the best focused plane?

To automatically detect the best-focused plane, we rely on the mathematical parameters of our image. The strategy choosen will differ depending on whether we're working with fluorescent images or brightfield.

### Fluorescent images

For fluorescent images, the standard deviation (SD) of pixel intensities is a reliable indicator. SD measures how spread out the values are in a dataset—in this case, the pixel intensities. In a perfectly focused image, the boundaries of structures are sharp, resulting in a significant difference in intensity between pixels in the background and those within the cell, which leads to a higher SD for the entire image. Conversely, if the image contains blur, pixels near the edges of structures will have more averaged intensities, resulting in a lower SD for the image.

{{< figure src="media/SD_fluor.png" alt="Image showing change of SD in z-stacks" caption="Figure 1: Different z-stacks of a GFP fluorescent cell, demonstrating how the standard deviation (SD) varies with focus. Each stack shows a detailed view of the cell's border, illustrating how pixel intensities differ more sharply when the image is in better focus." >}}

#### Key code components for focus detection
In this section, we focus on the critical parts of the code used to identify the best-focused plane within a 3D image stack. The following explanation breaks down the approach used to achieve this:

Given a 3D image with dimensions specified as ('z', 'x', 'y'):
```python
image.shape # Example output: (5, 2048, 2048)
```



In this section, we highlight the key parts of the code for processing fluorescent images. This script performs projection operations on 3D or 4D image stacks. 
For the full executable script, please visit my [GitHub repository](https://github.com/claudiasc89/imganalysis3_scripts/blob/main/csc_ip001.py).





