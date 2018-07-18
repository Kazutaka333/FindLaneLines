# **Finding Lane Lines on the Road** 
[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)

<img src="examples/laneLines_thirdPass.jpg" width="480" alt="Combined Image" />

Overview
---

When we drive, we use our eyes to decide where to go.  The lines on the road that show us where the lanes are act as our constant reference for where to steer the vehicle.  This project was the very first step in developing a self-driving car is to automatically detect lane lines using in images using Python and OpenCV.


How to Run the Program
---

**Step 1:** Set up the [CarND Term1 Starter Kit](https://classroom.udacity.com/nanodegrees/nd013/parts/fbf77062-5703-404e-b60c-95b78b2f3f9e/modules/83ec35ee-1e02-48a5-bdb7-d244bd47c2dc/lessons/8c82408b-a217-4d09-b81d-1bda4c6380ef/concepts/4f1870e0-3849-43e4-b670-12e6f2d4b7a7)

**Step 2:** Open the code in a Jupyter Notebook

`> jupyter notebook`

Click on the file called "P1.ipynb".  Another browser window will appear displaying the notebook.  

How the Program Works
---

[//]: # (Image References)

[original]: ./writeup_images/original.png
[gray]: ./writeup_images/gray.png
[color_selected]: ./writeup_images/color_selected.png
[blured]: ./writeup_images/blured.png
[cannied]: ./writeup_images/cannied.png
[masked]: ./writeup_images/masked.png
[hough]: ./writeup_images/hough.png
[combined]: ./writeup_images/combined.png

The program mainly consists of 7 parts.

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

### 2. Potential Shortcomings with the current program

As my method crops out the bottom half of the image by the trapezoid, I imagine the outputed lines will be much off from the actual lane in the more real-life image since the given test video and images were under the almost best condition such as the straight lane, sunny day, and no shade on lanes. 

My algorithm always represents lanes as two straight lines no matter what. Apparently this cannot be sufficient when a car encounter a quick curve.

In bad whether or road with shade, the grayscale value of each pixel could be much lower, which results that the lanes are corpped out through the current color masking.

### 3. Possible Solution

For the shaI would suggest use HSB space instead of RGB space for color masking. Since it's easier to select similar color with different brightness. That is, specifing small range of hue and somewhat wider range of saturation and brightness would easily extract the pixel of a cirtain color.
