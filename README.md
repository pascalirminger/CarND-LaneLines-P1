# **Finding Lane Lines on the Road**

[//]: # (Image References)
[imageAfterStep1]: ./demo/1_gray_scale.png "Step 1"
[imageAfterStep2]: ./demo/2_blurred.png "Step 2"
[imageAfterStep3]: ./demo/3_canny_edge.png "Step 3"
[imageAfterStep4]: ./demo/4_masked.png "Step 4"
[imageAfterStep5]: ./demo/5_hough_lines.png "Step 5"
[imageAfterStep6]: ./demo/6_merged.png "Step 6"
<img src="examples/laneLines_thirdPass.jpg" width="480" alt="Combined Image" />

## **Overview**

This repo contains the code written to complete the first project on [Udacity Self-Driving Car Nanodegree Program](https://www.udacity.com/course/self-driving-car-engineer-nanodegree--nd013) (Term 1). This project aggregates algorithms to identify and mark lane lines on the road. The algorithms work for images and videos which are taken from a camera at the center of a vehicle.

## **Description**

The pipeline consists of six steps:
1. Converts the image into a gray scaled version using the ```cv2.cvtColor()``` function.
2. Applies a Gaussian blur to the image using the ```cv2.GaussianBlur()``` function.
3. Uses a Canny transformation to find edges on the image using the ```cv2.Canny()``` function.
4. Applies an image mask to keep only the region of interest using the ```cv2.fillPoly()``` function as well as the ```cv2.bitwise_and()``` function.
5. Uses a Hough transformation to find the lines on the masked image using the ```cv2.HoughLinesP()``` function. It also draws these lines onto a black image (all black) of the same size as the original image using the ```cv2.line()``` function.
6. Merges the output of the last step with the original image to represent the found lines on it using the ```cv2.addWeighted()``` function.

In order to draw a single line on the left and right lanes, I modified the ```draw_lines()``` function (part of step 5) by adding a decision whether a line segment is part of the left lane or the right lane. The decision contains two parts. First, the slope ```((y2-y1)/(x2-x1))``` must be either positive or negative. Second, the positions of ```x1``` and ```x2``` must both be either on the left or on the right side of the image. The functions ```numpy.polyfit()``` and ```numpy.poly1d()``` are being used to average and extrapolate the line segments.

| Step | Output                       |
|:----:|:----------------------------:|
| 1    | ![alt text][imageAfterStep1] |
| 2    | ![alt text][imageAfterStep2] |
| 3    | ![alt text][imageAfterStep3] |
| 4    | ![alt text][imageAfterStep4] |
| 5    | ![alt text][imageAfterStep5] |
| 6    | ![alt text][imageAfterStep6] |
