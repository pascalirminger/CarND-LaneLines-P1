# **Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road.
* Reflect on your work in a written report.

[//]: # (Image References)
[imageAfterStep1]: ./demo/1_gray_scale.png "Step 1"
[imageAfterStep2]: ./demo/2_blurred.png "Step 2"
[imageAfterStep3]: ./demo/3_canny_edge.png "Step 3"
[imageAfterStep4]: ./demo/4_masked.png "Step 4"
[imageAfterStep5]: ./demo/5_hough_lines.png "Step 5"
[imageAfterStep6]: ./demo/6_merged.png "Step 6"

## **Reflections**

### **Description**

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

### **Potential shortcomings and possible improvements**

* I was confronted with pretty bad shaking of the extrapolated red lines. Therefore, I added some filters to the ```draw_lines()``` function to ignore "false-positive" line segments. Now, I got several frames with either the left or the right line missing.
* At the moment, the frames are ignorant of the outcomings of the previous frames. A moving average or something even smarter (e.g. Kalman filter) would help smoothing out the line changes frame-by-frame and the impact of noise.
