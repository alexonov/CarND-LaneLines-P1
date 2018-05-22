# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of few steps. First, I converted the images to grayscale, then I used smoothing, then canny transform to detect edges.
After that I identified a region of interest as a low part triange of the image - this is where the lines would be extracted. I extracted lines using
Hough transformation. Next step was to make 2 single lines out of all the extracted ones. 
First I have calculated slopes of all the lines and filtered out the obvious outliers (slopes of flat or greater than 45 degrees). I have also split them into 2 groups - left and right (depending if slope was greater than 0 or not). Now the last step was to average these groups into 2 lines. I have tried using geometry at first and calculate average slope and intercept but decided that drawing a regression line trough all of the points was simpler and more robust.


![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline


Main shortcoming is that the pipeline is not stable and highly sensitive to noise. Also it does not care about the color of the lines it sees.


### 3. Suggest possible improvements to your pipeline

One obvious improvement would be to take into account the color of the lanes - that way the noise would be reduced and it wont be fooled by another cars.
Another good improvement should be cmaking the algorithm aware of the lanes detected in the past. That way sudden changes due to noise won't happen. So for example currently detected lane could be averaged with few previous ones weighted accourding to how far in the past they were. Last few ones should be enough to make it more stable
