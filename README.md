# Image Processing for Object Isolation

This project demonstrates an image processing pipeline to isolate objects of a specific color range from an image using OpenCV. The workflow involves reading the image, blurring, color space conversion, color thresholding, morphological operations, contour detection, and filtering.

## Workflow

### Image Reading
The image `'redSeaBream.png'` is loaded using `cv2.imread()`, which reads the image in BGR format. BGR (Blue, Green, Red) is the default color format used by OpenCV.

### Image Blurring
A Gaussian blur is applied with a kernel size of `(5, 5)` using `cv2.GaussianBlur()`. This step reduces noise and smooths the image, which helps in improving the accuracy of subsequent processing steps.

### Color Space Conversion
The blurred image is converted from BGR to HSV (Hue, Saturation, Value) color space using `cv2.cvtColor()`. The HSV color space is more suitable for color-based segmentation compared to BGR.

### Color Thresholding
A color mask is created using `cv2.inRange()` to isolate pixels within a specific HSV range. The range corresponds to the orange color, defined by `lower_orange` and `upper_orange` boundaries. This mask helps in focusing on the desired color.

### Morphological Operations
- **Dilation**: Performed twice using `cv2.dilate()` to expand the white areas in the mask. This operation helps close small gaps and connect disjointed areas, enhancing the mask.
- **Erosion**: Performed three times using `cv2.erode()` to shrink the white areas. This step removes small noise and separates connected objects, making the final contours more distinct.

### Contour Detection
Contours are detected in the processed binary image using `cv2.findContours()`. The function focuses on external contours only, which are the outermost boundaries of objects in the image.

### Filtering Contours
Contours are filtered based on their area. Only contours with an area greater than 1000 pixels are retained. This filtering step helps remove small, irrelevant contours that are not of interest.

### Creating and Applying a New Mask
A new mask is created, and the filtered contours are drawn onto this mask using `cv2.drawContours()`. This new mask is used to isolate the desired objects from the original processed image.

### Displaying the Result
The final image, which shows only the isolated objects, is displayed using Matplotlib's `imshow()` function in grayscale. This allows for visual verification of the processing results.

## Requirements

- Python 3.x
- OpenCV (`cv2`)
- Matplotlib (`plt`)

You can install the required libraries using pip:

```bash
pip install opencv-python matplotlib
