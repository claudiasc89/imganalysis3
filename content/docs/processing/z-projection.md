---
title: Z-projections, finding the best focused plane
weight: 1
draft: false
---
When it comes to capturing intricate intracellular structures or achieving the sharpest focus in microscopy images, acquiring Z-stacks is crucial. Z-stacks allow us to collect a series of images at different focal planes, providing a comprehensive view of the specimen. When processing these images, we have several options: we can select the best-focused slice or create a Z-projection to reconstruct our structure of interest.

Manually selecting the best Z-plane can be tedious, especially when it varies across images. However, there's good news! This process can be automated, making it faster and more precise, ensuring that each image benefits from the optimal Z-stack.
You can find the full script for this process in my [GitHub repository](https://github.com/claudiasc89/imganalysis3_scripts/blob/main/csc_ip001.py).

## How do we find the best focused plane?

To automatically detect the best-focused plane, we rely on the mathematical parameters of our image. The strategy choosen will differ depending on whether we're working with fluorescent images or brightfield.

### Fluorescent images

For fluorescent images, the standard deviation (SD) of pixel intensities is a reliable indicator. SD measures how spread out the values are in a dataset—in this case, the pixel intensities. In a perfectly focused image, the boundaries of structures are sharp, resulting in a significant difference in intensity between pixels in the background and those within the cell, which leads to a higher SD for the entire image. Conversely, if the image contains blur, pixels near the edges of structures will have more averaged intensities, resulting in a lower SD for the image.

{{< figure src="media/SD_fluor.png" alt="Image showing change of SD in z-stacks" caption="Figure 1: Different z-stacks of a GFP fluorescent cell, demonstrating how the standard deviation (SD) varies with focus. Each stack shows a detailed view of the cell's border, illustrating how pixel intensities differ more sharply when the image is in better focus." >}}

#### Key code for focus detection
In this section, we focus on the critical parts of the code used to identify the best-focused plane within a 3D image stack. The following explanation breaks down the approach used to achieve this:

Given a 3D image with dimensions specified as ('z', 'x', 'y'):
```python
image.shape # Example output: (5, 2048, 2048)
```
Here, image.shape indicates that image is a multi-dimensional array with 5 stacks, each with dimensions 2048x2048 pixels.

1. **Calculating Standard Deviation**
To determine the focus quality of each z-stack, we first compute the standard deviation of pixel values across the x and y dimensions for each z-slice:
```python
sd = image.std(axis=(1, 2))  # 'z' is located at index 0, so x and y are flattened
```
-Explanation: By specifying axis=(1, 2), we compute the standard deviation for each z-slice by flattening the x and y dimensions. This results in an array of standard deviation values, where each value corresponds to a z-stack. The standard deviation measures the contrast or sharpness of the z-stack, with higher values indicating better focus.
The output will be an array containing as many sd as z-stacks contains the image.

2. **Finding the best-focused slice**
Next, we determine which z-stack has the maximum standard deviation:
```python
maxsd = sd.argmax()
```
-sd.argmax() returns the index of the z-stack with the highest standard deviation. This index represents the slice with the best focus, as it shows the highest contrast compared to other z-stacks.

#### Key code for projections
Once we have identified the best-focused slice, we can proceed to create projections from the image stack. The script offers three projection types: selecting the best-focused slice, and computing average or maximum projections.

First, we determine the range of z-slices to include in the projection based on the user-defined stack_step parameter. This range accounts for slices above and below the best-focused slice. The script is designed to handle cases where the best focus might not be centered within the stack and adjusts the range to avoid exceeding the image boundaries. For a complete view of the script, refer to the [full code on GitHub](https://github.com/claudiasc89/imganalysis3_scripts/blob/main/csc_ip001.py).
Here’s a breakdown of how the script performs these projections:

1.**Selecting the best focused slice**
```python
 img_proj = img.take(maxsd, axis=dimensions_indices['z'])
```
-Explanation:The maxsd variable holds the index of the slice with the highest standard deviation, which corresponds to the most focused image. The img.take() function extracts this specific slice along the z-axis (depth) of the image.

2.**Average or mean projection**
 ```python
 img_proj = np.mean(img_z, axis=dimensions_indices['z'], dtype=np.uint16)
```
-Explanation: For the average projection, np.mean() computes the mean pixel value across the specified range of z-slices. This range is centered around the best-focused slice and extends a number of slices above and below it. The axis=dimensions_indices['z'] argument tells NumPy to average along the z-dimension. The dtype=np.uint16 ensures that the resulting image maintains the same data type as the original.

3.**Maximum projection**
```python
 img_proj = np.max(img_z, axis=dimensions_indices['z'])
```
-Explanation: For the maximum projection, np.max() identifies the maximum pixel value along the z-dimension for each pixel location. This highlights the brightest features across the selected z-slices, making it useful for visualizing structures that may be more prominent in certain slices.

Congratulations if you are still here! Did you find this explanation useful? Do you follow a different strategy for image processing? Feel free to reach out with any questions or to share your own methods!


<script src="https://giscus.app/client.js"
        data-repo="claudiasc89/imganalysis3"
        data-repo-id="R_kgDOMqW3fg"
        data-category="Announcements"
        data-category-id="DIC_kwDOMqW3fs4CiXHG"
        data-mapping="pathname"
        data-strict="0"
        data-reactions-enabled="1"
        data-emit-metadata="0"
        data-input-position="top"
        data-theme="light_protanopia"
        data-lang="en"
        crossorigin="anonymous"
        async>
</script>

