# Finding Lane Lines on the Road

[*Video1*](https://github.com/Luzhongyue/Finding-Lane-Lines/blob/master/test_videos_output/solidWhiteRight.mp4)\
[*Video2*](https://github.com/Luzhongyue/Finding-Lane-Lines/blob/master/test_videos_output/solidYellowLeft.mp4)
## Conclution

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I use gaussian fitler to blur the image and eliminate the noise.Nextly,I use Canny Edge Detection to extract lines in the image.Then  I define the interested region, and make the region out of the interested region to black.Then,I transform the image to Hough Space to fine the Lane lines.Finally,I add the the image which has beeb processed to the original image.
In order to draw a single line on the left and right lanes, I modified the draw_lines() function by separating line segments by their slope ((y2-y1)/(x2-x1)) to decide which segments are part of the left line vs. the right line.  Then, I average the position of each of the lines and extrapolate to the top and bottom of the lane.Finally, I make a two line through the top and bottom of the lane respectively.
But the code can only work in good condition,and the region and other parameters are constant,which will result in error when work in complex enviroment.So the code is unstable. 



  
