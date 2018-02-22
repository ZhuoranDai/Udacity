# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

The image processing pipile consists of following steps:

**1**
Try to mark only white/yellow pixels in the image and turn all other pixels to black

**2**
Convert the image to grayscale

**3**
Apply Gaussian filter

**4**
Canny edge detect

**5**
Select the region of interest and apply a mask

**6**
Use Hough transform to detect line segments

The pipeline continues with following additional steps in order to draw a single line on the left and right lanes:

**7**
Calculate the slope of each line segment and divide lines segments into two groups, left group with negative slope and right group with positive slope

*For each of the groups
**8**
Remove gross outliers based on knowledge of the expecting slope range
**9**
Apply a linear fit to all points constituting remaining valid segments, and use this linear fit as the common lane
**10**
Extend the common lane to the border of our region of interest

**11**
Finally draw the lanes and blend with the original image

### 2. Identify potential shortcomings with your current pipeline


There are fews things I really don't like in the current pipeline:

**1**
Lot of settings are hard coded, this includes the color mask, region of interest and expected slope range.
The color mask probably won't be appropiate under a different light/weather condition, for example at night.
The region of interest and expected slope range are highly dependent on the orientation of the vehicle, as well as the road condition. Those definitely will be broken when we try to make a turn.

**2**
The lane detection using simple linear fit is not very consistent and we do observe glitch or jump from clip to clip, especially on the dashed lane.

### 3. Suggest possible improvements to your pipeline

I believe significant improvement can be achieved if we try to leverage the continuity of the video content, it's very unlikely to observe a dramatical change on lane color, slope and shape between consecutive frames.
