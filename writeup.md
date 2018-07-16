
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

My pipeline consists of 7 steps.

1. Convert images to grayscale.
2. Extract the pixels of the image with higher value since the yellow and white lane is relatively white in grayscale.
3. Apply gaussian blur to remove noise in the image.
4. Apply canny edge detection to find the edge of lanes in the image.
5. Mask by polygon to extract roughly where the lanes are.
6. Apply probabilistic Hough transform to find straight line segments to draw.
7. Combine drawn lines and the original image.

In order to draw a single line on the left and right lanes instead of many segments, I made the following modification to the
draw_lines() function.
1. Calculate 'a' and 'b' for each segment in terms of y = ax + b where 'a' and 'b' means slope and intersection on y axis.
2. Check if 'a' (slope) is larger than 0.3 or smaller than -0.3. If it is not, exclude that 'a' from the later step of 
calculation since flatter line is not the lane line we are looking for and set the weighted average line off.
3. Multiply a and b by the length of the segment. This is for putting more weights on longer segments than shorter segments when
it calculates the weighted average of a and b.
4. Group each 'a' and 'b' into left lane and right lane.
5. Take the weighted average of 'a' and 'b' in left lane and right lane group. 
6. Draw two lines for left and right lane from the bottom of the image to the 2/5 of the image hight using y = ax + b calculated
by the above steps.


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...
