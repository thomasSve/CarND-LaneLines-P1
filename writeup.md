# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[gray_solidWhiteCurve]: ./test_images_output/gray_solidWhiteCurve.jpg "Grayscale"
[blur_solidWhiteCurve]: ./test_images_output/blur_solidWhiteCurve.jpg "Gaussian blur"
[canny_solidWhiteCurve]: ./test_images_output/canny_solidWhiteCurve.jpg "Canny edge detection"
[roi_solidWhiteCurve]: ./test_images_output/roi_solidWhiteCurve.jpg "Region of interest mask"
[lines_solidWhiteCurve]: ./test_images_output/lines_solidWhiteCurve.jpg "Hough transform"
[solidWhiteCurve]: ./test_images_output/solidWhiteCurve.jpg "End product"

# Drawing
[sdc_p1_drawing]: sdc_p1_drawing.jpg "Drawing solution"

---

### Reflection

### 1. Process image pipeline

The pipeline to process image consisted of a total of 6 steps.

Firstly, I converted the input frame to grayscale
![alt text][gray_solidWhiteCurve] 

Next I added gaussian blur to 
![alt text][blur_solidWhiteCurve] 

Next I performed edge detection using Canny with low threshold equal to 50 and high threshold 150.
![alt text][canny_solidWhiteCurve]

Applied region of interest, cutting away uninterested information to focus on only current lines.
![alt text][roi_solidWhiteCurve]

Next I performed hough transform that drew and colored the lines nicely. When drawing these lines I splitted the lines into right and left lane. I calculated the slope of the lines, making the lines with negative slope belonging to left lane and positive slope belonging to right lane. I then added all these together, and used polyfit to draw one line over these point. For each line I used poly1d to get the polynomial function for the two lanes so I could select the starting point of each lane when x was 0 for left lane and x was equal to lane width as demonstrated in the drawing below.

![alt text][sdc_p1_drawing]

Which resulted in the following lines

![alt text][lines_solidWhiteCurve]

Added the calculated lines on top of original picture, showing the lines nicely drawn
![alt text][solidWhiteCurve]

### 2. Identify potential shortcomings with your current pipeline

The current solution will only work the the lines have one straight line, and therefore struggle when the road turns. When tuning the parameters, I also notices that some parameters worked very well for some situations and bad for others, so it is difficult to find the perfect parameters for all situations, and thereby not a solid solution.  
Also, this system will struggle more when the lanes are poorly marked, or even at night when it is dark.


### 3. Suggest possible improvements to your pipeline

One possible improvement is to implement a memory system that correlates the different frames in an image with eachother. Using the slope difference from each frame to decide which lanes to include. Especially when working on the challenge video I noticed how I was able to tune the parameters to make the lane run smoothly most of the time, but in some frames the lanes where jumping all over the place. Implementing a memory that compared the slope of the previous lanes could prevent the lanes jumping around on the image, making it more smooth and stable.

Also another suggestion to improve the lanes in a line could be to instead of having the lane extrapolation in 1d line, try to draw a curved line to fit better especially in turns.

