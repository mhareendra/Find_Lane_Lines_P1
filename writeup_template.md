# **Finding Lane Lines on the Road** 

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image0]: ./test_images_output/0gray_solidYellowLeft.jpg "Grayscale"
[image1]: ./test_images_output/2masked_edges_solidYellowLeft.jpg "Masked Edges"
[image2]: ./test_images_output/3lines_solidYellowLeft.jpg "Extrapolated Hough lines"
[image3]: ./test_images_output/4output_solidYellowLeft.jpg "Output"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of multiple steps.  
1. Validate size of image, resize if necessary
2. Convert image to grayscale
3. Apply Gaussian Blur with kernel size of 7x7
4. Perform Canny edge detection with low threshold = 120 and high threshold = 180
5. Extract the region of interest using a 4-sided polygon mask defined by vertices
6. Detect lane lines using hough transform

In order to draw a single line on the left and right lanes, I extrapolated the detected Hough lines by using 'polyfit' to fit a line.
I then used 'poly1d' to compute y values corresponding to min and max x values (obtained from vertices that define the polygon region of interest). These x and y values provided the bounds between which lines have to be drawn. An additional validation step is to ensure that the computed y values are within the region of interest (defined by vertices).

Sample images that represent the pipeline: 

1.  ![alt text][image0]             2.  ![alt text][image1]

3.  ![alt text][image2]             4.  ![alt text][image3]

### 2. Identify potential shortcomings with your current pipeline


Potential shortcomings:

1. Illumination differences, like driving during low visibility or nght time or very bright/sunny conditions, would reduce acccuracy since the thresholds for Canny edge detection would be invalid
2. Curved roads would require a different approach since line detection would not produce good results
3. Bad road conditions would affect the appearance of lane lines
4. Non-centered driving would require a wider region of interest mask
5. Vehicles immediately in front of our camera would block majority of the visible lanes 


### 3. Suggest possible improvements to your pipeline

Possible improvements:

1. Use location of detected lanes in previous frames to contribute to detection in current frame
2. Use Machine learning to train an algorithm to recognize various types/shapes/colors of lane lines under different conditions
3. Interpolate lane line locations to fill in for frames where detection is not possible
4. Use a linear function to generate thresholds for edge detection that are different for different parts of the image, since the lines closer to the camera would appear brighter than the farther lines.  

