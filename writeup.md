**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./test_images_output/solidWhiteCurve.jpg "final output"

---

### Reflection

### 1.pipeline description

My pipeline consists of 6 steps. 
1) First, I converted the images to grayscale.

2) Then images were smoothened using gaussian_blur function

3) Then canny function was run on images to detect edges of the lane

4) Then a region of interest(RoI) to fimd lanes was defined

5) Then using hough transform all the line segment found in the RoI was detected
   
   draw_lines function is modified to detect only two lane lines as follows,
	The initial seperation of right vs left lane was done using slopes of each line segment detected
	Then slopes of left and right lanes were added and averaged seperately
	To expolate the line segment line equation , x = x1 +(y-y1)/m was used
	Since this equation requires slope as well as one point, the point was found using averaging all the points
	for both lines. For corresponding two y values ,x values were found and plotted using cv2.line function

6) The detected lines were plotted on the inital image using weighted_img function


![alt text][image1]


### 2.Potential shortcomings with the current pipeline

It will be hard to detect if the lane lines are very faded due to old road conditions

Unable to detect, if the road has a sharp turn, since straight line is used instead of curved lines

Lane line detection is susceptible to noise in the frame due to various factors like weather, lighting conditions etc.       

### 3. Suggest possible improvements to your pipeline

A possible improvement would be to use curved line fitting to detect lane lines

To better the lane detection, data from a set of previous frames ie.average slope and intercepts should be stored 
to find or predict the lanes in the current frame. This stratergy will be robust against any noise in the images
and better fitting of line to the lane 
