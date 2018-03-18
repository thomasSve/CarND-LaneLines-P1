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

First, I converted the images to grayscale.
![alt text][gray_solidWhiteCurve] 

I added gaussian blur with kernel size 5
![alt text][blur_solidWhiteCurve] 

Next I performed edge detection using Canny with low threshold equal to 50 and high threshold 150.
![alt text][canny_solidWhiteCurve]

Applied region of interest, cutting away uninterested information to focus on only current lines.
![alt text][roi_solidWhiteCurve]

I performed hough transform that drew the lines
![alt text][lines_solidWhiteCurve]

Added the calculated lines on top of original picture, drawing a nice overlook over the images
![alt text][solidWhiteCurve]

![alt text][sdc_p1_drawing]


### 2. Identify potential shortcomings with your current pipeline

The current solution will only work the the lines have one straight line, and therefore struggle when in a turn. 

One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...
