---
title: Z-projections, finding the best focused plane
weight: 1
draft: true
---
When it comes to capturing intricate intracellular structures or achieving the sharpest focus in microscopy images, acquiring Z-stacks is crucial. Z-stacks allow us to collect a series of images at different focal planes, providing a comprehensive view of the specimen. When processing these images, we have several options: we can select the best-focused slice or create a Z-projection to reconstruct our structure of interest.

Manually selecting the best Z-plane can be tedious, especially when it varies across images. However, there's good news! This process can be automated, making it faster and more precise, ensuring that each image benefits from the optimal Z-stack.

## How do we find the best focused plane?

To automatically detect the best-focused plane, we rely on the mathematical parameters of our image, which differ depending on whether we're working with fluorescent images or brightfield.

# Fluorescent images

For fluorescent images, the standard deviation (SD) of pixel intensities is a reliable indicator. In a perfectly focused image, the boundaries of structures are sharp, resulting in a significant difference in intensity between pixels in the background and those within the cell, which leads to a higher SD for the entire image.

Conversely, if the image contains blur, pixels near the edges of structures will have more averaged intensities, resulting in a lower SD for the image.
