
# **Finding Lane Lines on the Road** 

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[original]: ./writeup_images/original.png
[gray]: ./writeup_images/gray.png
[color_selected]: ./writeup_images/color_selected.png
[blured]: ./writeup_images/blured.png
[cannied]: ./writeup_images/cannied.png
[masked]: ./writeup_images/masked.png
[hough]: ./writeup_images/hough.png
[combined]: ./writeup_images/combined.png

---

### Reflection

### 1. Pipeline Description
<!-- Describe your pipeline. As part of the description, explain how you modified the draw_lines() function. -->

My pipeline consists of 7 steps.

original image

![alt text][original]

1. Convert images to grayscale.

![alt text][gray]

2. Extract the pixels of the image with higher value since the yellow and white lane is relatively white in grayscale.

![alt text][color_selected]

3. Apply gaussian blur to remove noise in the image.

![alt text][blured]

4. Apply canny edge detection to find the edge of lanes in the image.

![alt text][cannied]

5. Mask by polygon to extract roughly where the lanes are.

![alt text][masked]

6. Apply probabilistic Hough transform to find straight line segments to draw.

![alt text][hough]

7. Combine drawn lines and the original image.

![alt text][combined]


In order to draw a single line on the left and right lanes instead of many segments, I made the following modification to the
draw_lines() function.
1. Calculate 'a' and 'b' for the segments found by hough line transform in terms of y = ax + b where 'a' and 'b' means slope and intersection on y axis.
2. Check if 'a' (slope) is larger than 0.3 or smaller than -0.3. If it is neither, exclude the segument from the later step of 
calculation since too flat line is not the lane line we are looking for and set the weighted average line off.
3. Multiply a and b by the length of the segment. This is for putting more weights on longer segments than shorter segments when it calculates the weighted average of a and b.
4. Group each 'a' and 'b' into left lane and right lane.
5. Take the weighted average of 'a' and 'b' in left lane and right lane group. 
6. Draw two lines for left and right lane from the bottom of the image to the 2/5 of the image hight using y = ax + b calculated by the above steps.


### 2. Identify potential shortcomings with your current pipeline

As my method crops out the bottom half of the image by the trapezoid, I imagine the outputed lines will be much off from the actual lane in the more real-life image since the given test video and images were under the almost best condition such as the straight lane, sunny day, and no shade on lanes. 

My algorithm always represents lanes as two straight lines no matter what. Apparently this cannot be sufficient when a car encounter a quick curve.

In bad weather or road with shade, the grayscale value of each pixel could be much lower, which results that the lanes are corpped out through the current color masking.

### 3. Suggest possible improvements to your pipeline

To adapt the different light condition, I would suggest use HSB space instead of RGB space for color masking. Since it's easier to select similar color with different brightness. That is, specifing small range of hue and somewhat wider range of saturation and brightness would easily extract the pixel of a cirtain color.
