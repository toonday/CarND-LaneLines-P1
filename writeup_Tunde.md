# **Finding Lane Lines on the Road** 

## Writeup Tunde Oladimeji

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

My pipeline consisted of 5 steps.
* I selected only colors in the image I cared about (bright colors since lane lines are usually either yellow or white)
* I converted the color filtered image to grayscale
* When selecting tuning parameters, I used percentages of the image dimensions rather than absolute values to help with different image resolutions
* I detected edges in the image using canny's algorithm
* I applied a mask so I can only focus on edges in my region of interest
* I used the hough lines algorithm to detect edges that make up a line
* I merged the averaged extrapolated line image generated from my custom hough algorithm onto the orignal image passed
* I returned the results

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by:
* grouping the lines detected into 2 groups (left and right) which can be identified by the slope of the line
* ignoring horizontal lines (lines with a low absolute value for slope)
* finding the average line of the lines in each group
* extrapolating each of the average lines to the top and bottom planes using the numpy polyfit function to get the equation of the line



### 2. Identify potential shortcomings with your current pipeline

* My current pipeline seems decent enough
* I made some comments below about scenarios of lane lines over actual traffic flow lines, but seems like a good start to me!
* My color selection might be an issue in night environments as the lane lines might be a lot darker at night, maybe I can do some filtering as to comparing brightest and darkest images in the pixel to define what the bright color threshold should be.
* I also noticed that more weird lines are included when the gravel on the raod is light grey which causes some jitters as well.
* Overall, testing my pipeline in scenarios in which the lane lines could blend into the environment or has similar properties with other elements in the environment would be useful.




### 3. Suggest possible improvements to your pipeline

* I got some jittery movements initially with my results.
* This was mainly has a result of horizontal lines being detected as well.
* It would be interesting to figure out how to recognize irregular lane lines due to construction e.t.c and how to detect the actual flow of traffic lines.
* I think my extrapolation function can be improved, it seems a bit longer than I would have liked, there are probably libraries out there that do something similar faster.
* Also I took average of all the lines, I might get better results if I took average points for the top of the line above a certain threshold and perform the same thing for averaging the points at the bottom of the line.
