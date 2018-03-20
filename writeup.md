# **Finding Lane Lines on the Road** 

[//]: # (Image References)

[gray_solidWhiteCurve]: ./test_images_output/gray_solidWhiteCurve.jpg "Grayscale"
[blur_solidWhiteCurve]: ./test_images_output/blur_solidWhiteCurve.jpg "Gaussian blur"
[canny_solidWhiteCurve]: ./test_images_output/canny_solidWhiteCurve.jpg "Canny edge detection"
[roi_solidWhiteCurve]: ./test_images_output/roi_solidWhiteCurve.jpg "Region of interest mask"
[hough_solidWhiteCurve]: ./test_images_output/hough_solidWhiteCurve.jpg "Hough transform"
[lines_solidWhiteCurve]: ./test_images_output/lines_solidWhiteCurve.jpg "Lines drawn"
[solidWhiteCurve]: ./test_images_output/solidWhiteCurve.jpg "End product"

[sdc_p1_drawing]: sdc_p1_drawing.jpg "Drawing solution"

---

### Reflection

### 1. Process image pipeline

The pipeline to process image consisted of a total of 6 steps.

#### Grayscale
Firstly, I converted the input frame to grayscale in order to significantly reduce the computational complexity. 
![alt text][gray_solidWhiteCurve] 

#### Gaussian blur
Next I applied gassian blur to the image that takes the pixels close to eachother, and sets the value of the pixel to be the average of the surronding pixels. 
![alt text][blur_solidWhiteCurve] 

#### Canny edge detection
After blurring together the pixels, we make it easier for our next step which is edge detection. We can now apply Canny algorithm, which uses the blurred pixel to detect edges on the image. 
![alt text][canny_solidWhiteCurve]

#### Region of interest
We are only interested in the lines of the image, and since we know where the lines will be relative to the image, we can cut away uninterested information and only focus on the region of interest.
![alt text][roi_solidWhiteCurve]

#### Hough transform
Now we can move on to the final part, which is to detect the lines in the image. The hough transformation uses the edges detected by the canny to find aligned points that together form a line. To do this, the hough transforms the points in imagespace into something called the Hough Space. In hough space, each points are represented as lines, and at the point where the lines crosses forms the function mx + b in image space.

![alt text][hough_solidWhiteCurve]

#### Extrapolate, splitting into right and left lane
As seen on the last image, the lanes are now successfully marked, however we want to merge the lines into a single right and left lane. We do this by calculating the slope of every line where the ones with positive slope belonging to the right lane, and negative slope left lane. We collect all the points for a certain lane, and calculate the polynomial function for this line. Using this function we can now select the starting and end point of the lines ourself, where each point is simply calculated using the function. To decide the starting and endpoint I drew up what the x value would have to be in both cases to make the lanes be drawn from beginning of image (or y = 0). 

![alt text][sdc_p1_drawing]

As seen in this drawing I chose the x-value 0 left lane starting point with the maximum point as stop point. With the right lane going opposite direction (negative slope) the start-point is maximum x-value and stop x-value equal to image width. With these values we now have two long lanes drawn as shown in the following function.

![alt text][lines_solidWhiteCurve]

#### Merged lines image with original image
Added the calculated lines on top of original picture, showing the lines nicely drawn
![alt text][solidWhiteCurve]

### 2. Identify potential shortcomings with your current pipeline

The current solution will only work the the lines have one straight line, and therefore struggle when the road turns. When tuning the parameters, I also notices that some parameters worked very well for some situations and bad for others, so it is difficult to find the perfect parameters for all situations, and thereby not a solid solution.
Also, this system will struggle more when the lanes are poorly marked, or even at night when it is dark.


### 3. Suggest possible improvements to your pipeline

One possible improvement is to implement a memory system that correlates the different frames in an image with eachother. Using the slope difference from each frame to decide which lanes to include. Especially when working on the challenge video I noticed how I was able to tune the parameters to make the lane run smoothly most of the time, but in some frames the lanes where jumping all over the place. Implementing a memory that compared the slope of the previous lanes could prevent the lanes jumping around on the image, making it more smooth and stable.

Also another suggestion to improve the lanes in a line could be to instead of having the lane extrapolation in 1d line, try to draw a curved line to fit better especially in turns.

