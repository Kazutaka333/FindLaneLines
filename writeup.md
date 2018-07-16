
# **Finding Lane Lines on the Road** 

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1. Pipeline Description
<!-- Describe your pipeline. As part of the description, explain how you modified the draw_lines() function. -->

My pipeline consisted of 7 steps. First, I converted the images to grayscale, then I extracted whiter part of the image
using cv2.inRange() since the lane is either yellow or white, which is relatively white in grayscale. After that, I applied 
gaussian blur to remove noise in the image, and applied canny edge detection to find the edge of lanes in the image.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by ...

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...
