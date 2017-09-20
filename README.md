## Self-Driving Car Engineer Nanodegree

## Project 1: Finding Lane Lines on the Road

Project Jupyter Notebook: P1.ipynb

Notebook HTML snapshot: P1.html

Test Images:

![solidWhiteCurve](https://github.com/ongchinkiat/SDCND-Project1/raw/master/solidWhiteCurve.jpg "solidWhiteCurve")


![solidWhiteRight](https://github.com/ongchinkiat/SDCND-Project1/raw/master/solidWhiteRight.jpg "solidWhiteRight")

![solidYellowCurve](https://github.com/ongchinkiat/SDCND-Project1/raw/master/solidYellowCurve.jpg "solidYellowCurve")

![solidYellowCurve2](https://github.com/ongchinkiat/SDCND-Project1/raw/master/solidYellowCurve2.jpg "solidYellowCurve2")

![solidYellowLeft](https://github.com/ongchinkiat/SDCND-Project1/raw/master/solidYellowLeft.jpg "solidYellowLeft")

![whiteCarLaneSwitch](https://github.com/ongchinkiat/SDCND-Project1/raw/master/whiteCarLaneSwitch.jpg "whiteCarLaneSwitch")

Video Files: 

1. solidWhiteRight.mp4

2. solidYellowLeft.mp4

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps.

First, I converted the images to grayscale, then I applied Gaussian smoothing to clean up any noise.

Next, Canny thresholding is applied to identify the edges in the image. Then I apply a polygon mask to remove the "unwanted" areas in the image which are not likely to contain the target lane lines.

Finally, Hough transform is applied to identify the lane lines.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by grouping the lines into 2 groups: those with positive gradient and those with negative gradient.

For each group, the average (x1,y1) and (x2,y2) are computed, then they are extrapolated to y1 = height of image, y2 = 320 (far end of the road, value decided base on visual inspection of the test images).



### 2. Identify potential shortcomings with your current pipeline


The pipeline will fail to identify the lane lines if

1. there are some markings in the middle of the lane.

2. bright sun light shines on the road, causing the contrast of the road and lane markings to reduce.

3. the car is making a sharp turn, there may not be enough lane markings for identification.

4. 2 or more lines are identified on either side of the lane.

5. there is a vehicle in front, or at the side blocking the lane markings.

### 3. Suggest possible improvements to your pipeline

Possible improvements:

1. Check if there are 2 or more lines which are not close together on either side of the lane. Discard the lines that are too far away to the side, or too near to the middle.

2. Add some "memory" to remember the identified lane marking lines from the previous frame(s), to filter out those lines that are too far off the previous lines.
