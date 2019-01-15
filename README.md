# Finding Lane Lines on the Road
---
![](https://github.com/Luzhongyue/Finding-Lane-Lines/blob/master/Images/1.png)

[*Video1*](https://github.com/Luzhongyue/Finding-Lane-Lines/blob/master/test_videos_output/solidWhiteRight.mp4)\
[*Video2*](https://github.com/Luzhongyue/Finding-Lane-Lines/blob/master/test_videos_output/solidYellowLeft.mp4)

Overview
---

When we drive, we use our eyes to decide where to go.  The lines on the road that show us where the lanes are act as our constant reference for where to steer the vehicle.  Naturally, one of the first things we would like to do in developing a self-driving car is to automatically detect lane lines using an algorithm.

In this project it will detect lane lines in images using Python and OpenCV.  OpenCV means "Open-Source Computer Vision", which is a package that has many useful tools for analyzing images. 

## Pipeline description 
---

The following techniques are used:
* canndy edge detection
* region of interest selection
* hough transform line detection

### Conversion to Grayscale

Applies the Grayscale transform, this will return an image with only one color channel

![](https://github.com/Luzhongyue/Finding-Lane-Lines/blob/master/Images/2.png)

### Gaussian Blurring

To supress noise and spurious gradients Gaussian smoothing is applied. By experiments, kernel of size 5 was chosen. 

![](https://github.com/Luzhongyue/Finding-Lane-Lines/blob/master/Images/3.png)

### Edge Detection

To detect edges, we can use popular Canny algorithm. The algorithm will first detect strong edge (strong gradient) pixels above the high_threshold, and reject pixels below the low_threshold. Next, pixels with values between the low_threshold and high_threshold will be included as long as they are connected to strong edges. The output edges is a binary image with white pixels tracing out the detected edges and black everywhere else.

![](https://github.com/Luzhongyue/Finding-Lane-Lines/blob/master/Images/4.png)

### Region of Interest Selection

When finding lane lines, we don't need to check the sky and the hills. So we can filter out unnecessary objects in the image, the region of interest is defined.In this case, I'll assume that the front facing camera that took the image is mounted in a fixed position on the car, such that the lane lines will always appear in the same general region of the image. Next, I'll take advantage of this by adding a criterion to only consider pixels for color selection in the region where we expect to find the lane lines.

![](https://github.com/Luzhongyue/Finding-Lane-Lines/blob/master/Images/5.png)

### Hough Transform Line Detection

Using an OpenCV function called HoughLinesP that takes several parameters to detect lines in the edge images.
* rho and theta: the distance and angular resolution of our grid in Hough space. Remember that, in Hough space, we have a grid laid out                  along the (Θ, ρ) axis. You need to specify rho in units of pixels and theta in units of radians.
* threshold: specifies the minimum number of votes (intersections in a given grid cell) a candidate line needs to have to make it into                the output. 
* min_line_length: the minimum length of a line (in pixels) that you will accept in the output.
* max_line_gap: the maximum distance (again, in pixels) between segments that you will allow to be connected into a single line.

![](https://github.com/Luzhongyue/Finding-Lane-Lines/blob/master/Images/6.png)
### Averaging and Extrapolating Lines
In order to draw a single line on the left and right lanes, I modified the draw_lines() function by separating line segments by their slope ((y2-y1)/(x2-x1)) to decide which segments are part of the left line vs. the right line.  \

Then, I average the position of each of the lines and extrapolate to the top and bottom of the lane.Finally, I make a two line through the top and bottom of the lane respectively.

![](https://github.com/Luzhongyue/Finding-Lane-Lines/blob/master/Images/7.png)



  
