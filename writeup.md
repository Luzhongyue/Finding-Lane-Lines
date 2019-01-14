1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.
   My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I use gaussian fitler to blur the image and eliminate the noise.Nextly,I use Canny Edge Detection to extract lines in the image.Then  I define the interested region, and make the region out of the interested region to black.Then,I transform the image to Hough Space to fine the Lane lines.Finally,I add the the image which has beeb processed to the original image.
   In order to draw a single line on the left and right lanes, I modified the draw_lines() function by separating line segments by their slope ((y2-y1)/(x2-x1)) to decide which segments are part of the left line vs. the right line.  Then, I average the position of each of the lines and extrapolate to the top and bottom of the lane.Finally, I make a two line through the top and bottom of the lane respectively.



2. Identify potential shortcomings with your current pipeline
   The code can only work in good condition,and the region and other parameters are constant,which will result in error when work in complex enviroment.So the code is unstable. 

3. Suggest possible improvements to your pipeline
   The parameters and the region of interest should be variable.The problem of the challenge vedio can be solved by modify the paremeters.But I don't know how to make the code work in any conditions.

  