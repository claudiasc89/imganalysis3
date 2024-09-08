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

#### Code for fluorescent images
In this section, we highlight the key components of the script used for processing fluorescent images. This script performs projection operations on 3D or 4D image stacks, allowing users to visualize and analyze specific aspects of their data. For the full executable script, please visit my [GitHub repository](https://github.com/claudiasc89/imganalysis3_scripts).

##### Global Variables

The script utilizes global variables to manage various aspects of image processing. These include:

- **`proj_type`**: Specifies the type of projection (e.g., 'best', 'mean', 'max').
- **`maxsd`**: Index of the z-slice with the highest standard deviation.
- **`filename`**: Name of the input image file.
- **`stack_step`**: Number of z-slices to include in the projection.
- **`dimensions`, `dimensions_map`, `dimensions_indices`**: Metadata about image dimensions and their indices.

##### Projection Functions

The script includes functions to perform different types of projections on 3D or 4D image stacks:

- **`projection_3D(img)`**: 
  This function applies a projection to a 3D image stack. It supports:
  - **Best Projection**: Selects the z-slice with the highest standard deviation.
  - **Mean Projection**: Computes the mean of a specified number of z-slices around the most focused slice.
  - **Max Projection**: Computes the maximum value across the specified z-slices.

  **Key Steps**:
  - Determine the range of z-slices to be included based on the projection type.
  - Calculate the appropriate projection (mean or max).
  - Save the projected image and log the details.


#### Usage

1. **Prepare Image Data**:
   Ensure your input image data is in the correct format and dimensions required by the script.

2. **Set Parameters**:
   Adjust the global variables and function parameters to suit your specific dataset and projection needs.

3. **Run the Script**:
   Execute the script to perform the projection and save the results. The script will generate output files and log files containing the details of the projection.

By understanding these components, you can effectively use the script to analyze and visualize fluorescent images, tailoring the projections to your research needs.

For a complete and executable version of this script, please refer to my [GitHub repository](https://github.com/claudiasc89/imganalysis3_scripts).



