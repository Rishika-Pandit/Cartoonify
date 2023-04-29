

# Cartoonify Image

This code aims to transform an input image into a cartoon-like image by applying various image processing techniques. 

## Required Libraries

* `cv2`: OpenCV library for computer vision
* `numpy`: Library for working with arrays
* `matplotlib`: Library for data visualization

## Steps

1. Load the input image using `cv2.imread()` and convert the color space from BGR to RGB using `cv2.cvtColor()`.
2. Create an edge mask of the image using `cv2.adaptiveThreshold()` and `cv2.medianBlur()`.
3. Reduce the color palette of the image using k-means clustering algorithm implemented using `cv2.kmeans()`.
4. Reduce the noise in the image using bilateral filtering using `cv2.bilateralFilter()`.
5. Combine the edge mask with the quantized image using `cv2.bitwise_and()`.

## Functions

### `read_file(filename)`

* Inputs: 
  * `filename` (str): The path to the input image file
* Outputs: 
  * `img` (numpy array): The RGB image array

This function loads the input image and converts its color space from BGR to RGB using `cv2.cvtColor()`. It then displays the image using `matplotlib.pyplot.imshow()`.

### `edge_mask(img, line_size, blur_value)`

* Inputs: 
  * `img` (numpy array): The RGB image array
  * `line_size` (int): The size of the edges to be detected
  * `blur_value` (int): The value of the median blur applied to the image
* Outputs: 
  * `edges` (numpy array): The edge mask of the input image

This function converts the input image to grayscale using `cv2.cvtColor()`. It then applies median blur using `cv2.medianBlur()` and adaptive threshold using `cv2.adaptiveThreshold()` to create an edge mask of the image.

### `color_quantization(img, k)`

* Inputs: 
  * `img` (numpy array): The RGB image array
  * `k` (int): The number of colors to be quantized
* Outputs: 
  * `result` (numpy array): The quantized image array

This function converts the input image to a numpy array using `np.float32()` and reshapes it using `numpy.reshape()`. It then applies k-means clustering algorithm using `cv2.kmeans()` and returns the quantized image array.

### `cartoon()`

* Outputs: 
  * Displays the cartoonized image

This function combines the quantized image with the edge mask using `cv2.bitwise_and()` and displays the cartoonized image using `matplotlib.pyplot.imshow()`. 

## Example Usage

```python
filename = "/content/cartoonify.jpg"
img= read_file(filename)

line_size, blur_value= 5,7 
edges= edge_mask(img, line_size, blur_value)

img = color_quantization(img, 9)

blurred = cv2.bilateralFilter(img, d=3, sigmaColor= 200, sigmaSpace= 200)

cartoon()
```
