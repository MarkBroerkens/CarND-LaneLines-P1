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

## The Lane Line Detection Pipeline

My pipeline consisted of 5 steps:
1. convert the images to grayscale
<img src="https://raw.githubusercontent.com/MarkBroerkens/CarND-LaneLines-P1/master/readme_images/1_greyscale.jpg" width="400">
2. apply Gaussian smoothing in order to reduce the noise in the image
<img src="https://raw.githubusercontent.com/MarkBroerkens/CarND-LaneLines-P1/master/readme_images/2_blured.jpg" width="400">
3. detect edges using canny edge detection algorithm
<img src="https://raw.githubusercontent.com/MarkBroerkens/CarND-LaneLines-P1/master/readme_images/3_canny.jpg" width="400">
4. select the region of interest by applying a mask
<img src="https://raw.githubusercontent.com/MarkBroerkens/CarND-LaneLines-P1/master/readme_images/4_masked.jpg" width="400">
5. apply the hough transformation in order to identify the lines
<img src="https://raw.githubusercontent.com/MarkBroerkens/CarND-LaneLines-P1/master/readme_images/5_hough.jpg" width="400">

In order to draw the left and right lane lines, I modified the draw_lines() function by 
1. Assign the lines from the hough transformation to the right or left lane by analyzing the slope. 
2. Filtering out lines that are not lane lines. Only lines with a slope between 0.5 and 2 are considered as potential lane lines 
3. Extrapolation of the lines to the full length betwwen the bottom of the image and the horizon
4. Calculate the x value of the bottom and top end of the lane line by calculation of the median value of the set of right or left hough lines.
5. In order to handle situations where the pipeline is not able to produce a line line we simply use the precvious lane line coordinates.


## Results
[white] (https://youtu.be/Tgr6BCZZ_3g "Click to watch")

[yellow] (https://youtu.be/oSYKV15r19I "Click to watch")

[challenge] (https://youtu.be/r_DpWtK0Myg "Click to watch")



## Identify potential shortcomings with your current pipeline


One potential shortcoming would be that the pipeline draws straight lines which obviously cannot follow curves.

Another shortcoming could be that the algorithm in this pipeline uses coordinates of previous lane lines in case it is not able to detect the lane lines from the current image. For a real self driving car, this would be very dangerous, because the car would still think that it "sees" lane lines even though it is already driven off the road.


## Suggest possible improvements to your pipeline

A possible improvement would be to consider the position of the lane lines in previous images in order to validate and influence the  calculation of the current results. Since the speed of the car is limited, we can assume that the street doesn't change dramatically between two images. This could also trembling lane lines in the video.

Another improvement could be the integration of some algorithm that configures the parameters of the pipeline according to the quality and needs of the input video. 
