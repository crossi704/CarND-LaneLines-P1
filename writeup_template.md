**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1. Describe the pipeline

My pipeline consisted of 8 steps:
1) Convert image to grayscale for easier manipulation
2) Apply Gaussian Blur with kernel size 5 to smoothen edges
3) Apply Canny Edge Detection on smoothed gray image
4) Crop Region Of Interest and discard all other lines identified before outside the cropped region
5) Perform a Hough Transform to find lanes within our cropped region.
6) Separate left and right lines by its angle in radians (using math.arctan(theta) we can avoid slope = 0)
7) Calculate the line's average 2 Points (x1,y1,x2,y2) composing it and its angle in radians.
8) Calculate the average X and Y from the remaining (x1,y1,x2,y2) and using the average angle, draw a single line for the left lane and single line for the right lane.


![alt text][image1]


### 2. Potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when you have a white or yellow car just in front of your self-driving car.
The lane lines could be be mistaken by the color of the car, and if the car is very near, region cropping could fail to filter it.
Hopefully some of these lines detected would not pass on the lines angle filter that I included (from 20 to 45 degrees).


### 3. Possible improvements to your pipeline

A possible improvement would be to implement some past frame analysis if line detection in current frame fails.
In challenge video for example, using my algorithm, there are some frames where no lines were detected,
maybe tweaking my angle filter and combining it with "line memory" from previous frame would solve this issue.

