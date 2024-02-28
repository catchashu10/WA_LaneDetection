# WA Perception Coding Challenge: Lane Detection

Note: For detailed description of the implementation and methodology please follow along the comments and output in the Jupyter Notebook located at `./WA_perceptionChallenge.ipynb`

## Final Output

The result of the detection and analysis process is illustrated in the image below, located at `./answer.png`.

![Final Output](answer.png)

## Methodology

The project follows a structured approach to detect red objects within an image:

1. **Image Preprocessing**: The image is loaded and converted to the HSV color space to simplify the color detection process.
2. **Color Detection**: Two ranges for red color in the HSV space are defined to account for its circular nature in HSV. A binary mask is then created to isolate red objects.
3. **Noise Reduction**: Morphological operations (dilation followed by erosion) are applied to the binary mask to remove noise.
4. **Object Detection**: Contours are identified in the cleaned-up mask, and the centers of these contours are calculated using the object properties.
5. **Center Filtering and Sorting**: Centers that do not meet certain criteria are filtered out. The remaining centers are sorted and divided into left and right paths based on their positions.
6. **Path Analysis**: Lines are fitted through the center points of the leftmost and rightmost objects to analyze potential paths.
7. **Visualization and Output**: The processed image, with detected objects and path lines, is saved and displayed.

## Challenges and Solutions

### What Did You Try?

- **Color Space Conversion**: Initially struggled with accurately detecting red objects due to the wide variation in shades of red and lighting conditions. 
- **Noise in the Detection**: Small, irrelevant objects were being detected as red objects, adding noise to the analysis.
- **Outlier Detection**: Some detected objects were outliers, not fitting into the expected pattern of left and right paths.

### Why It Did Not Work

- **HSV Color Space**: The direct translation of RGB to HSV did not initially account for the circular nature of red hues in HSV, leading to incomplete detection.
- **Morphological Operations**: The initial choice of kernel size and iterations was not optimal for all test images, leading to either too much noise or the removal of relevant objects.
- **Outlier Filtering Hack**: The hack based on y-coordinate filtering is not robust, as it relies on specific image dimensions and object placements.

## Libraries Used

The project utilizes the following libraries:

- **OpenCV (cv2)**: For image processing tasks, including color space conversion, morphological operations, contour detection, and line fitting.
- **NumPy**: Used for efficient array manipulations, especially for operations on image matrices and color ranges.
- **Matplotlib**: For visualizing the images and results at various stages of processing.