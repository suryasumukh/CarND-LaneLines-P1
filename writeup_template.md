# **Finding Lane Lines on the Road**
---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report  

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

The pipeline consists of a series of transformation applied to recognize lanes
in images. The input image with RGB channels it converted to a grayscale image
using the grayscale helper function. This grayscale image is processed by the
canny edge detection function. A polygon is used to pick the bottom
part of the image where the lanes occur most of the time. Hough transformation is
applied to this image to get a set of lines that outline the lanes. The draw_function
takes the lines from the hough transform and computes the slope and intercept.
slopes with absolute value less than 0.2 are discarded since they mostly describe
horizontal lines. Lanes with positive slope are part of right lanes and those with
negative slope form parts of the left lane. The slopes and intercepts are averaged
to describe a single left and right lane. Since we want the lanes to drawn from
bottom of the image, the y coordinate is the height of the image. This y value is
used to calculate the x coordinate using the averaged slope/intercept line
expression for both lanes. The top end of the lanes is calculated the same way.
The y value is maximum of y coordinates of set the lines from hough transform.
These points are used to draw lanes on the image with the opencv lines function.
This image is superimposed on the original image to depict the extrapolated lanes.

### 2. Identify potential shortcomings with your current pipeline

 * This pipeline cannot be used to detect lanes when making turns. Since the focus
is on the bottom part of the image, information to the right and top left for right
left turns respectively are lost.
 * Distinction between lane types is not possible
 * Traffic signs are ignored
 * Can be hard to draw lanes at intersections. Lines with horizontal slopes are ignored


### 3. Suggest possible improvements to your pipeline

Use Convolutional Neural Networks to overcome some of the shortcomings
