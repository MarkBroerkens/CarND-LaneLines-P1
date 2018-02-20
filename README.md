This is my submission for the Udacity Self-Driving Car Nanodegree Lane Detection Project. You can find my code in this [Jupyter Notebook](https://github.com/MarkBroerkens/CarND-LaneLines-P1/blob/master/P1.ipynb). 

## Summary

The pipeline takes a video of a street as input and outputs it with the lane markers highlighted.
<img src="https://raw.githubusercontent.com/MarkBroerkens/CarND-LaneLines-P1/master/readme_images/0_original.jpg" width="400">
<img src="https://raw.githubusercontent.com/MarkBroerkens/CarND-LaneLines-P1/master/readme_images/6_result.jpg" width="400">

## Finding Lane Lines on the Road ##

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps:
1. convert the images to grayscale
2. apply Gaussian smoothing in order to reduce the noise in the image
3. detect edges using canny edge detection algorithm
4. select the region of interest by applying a mask
5. apply the hough transformation in order to identify the lines

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by 
1. identifying the right and left lines by analyzing their slope
2. filtering out lines that are obviously not lane lines
3. interpolation of the lines to the full length betwwen the bottom of the image and the horizon
4. calculate the median values of the left and right lines

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be that the pipeline draws straight lines which obviously cannot follow curves.

Another shortcoming could be that the input image is not sufficient for detection of the lanes so that we either get randon lines that do not follow the lane lines or we do not get any lane lines at all.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to consider the position of the lane lines in previous images in order to validate and influence the  calculation of the current results. Since the speed of the car is limited, we can assume that the street doesn't change dramatically between two images.
