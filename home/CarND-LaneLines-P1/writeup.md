
# **Finding Lane Lines on the Road** 

## Project Writeup

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Construct a pipeline that finds lane lines on the road; 
* Reflect on the construction process in a written report

[//]: # (Image References)

[image1]: ./examples/laneLines_thirdPass.jpg "Grayscale"
[image2]: ./test_images_blur/solidWhiteRight.jpg "Blurred"
[image3]: ./test_images_canny/solidYellowLeft.jpg "Canny"
[image4]: ./test_images_hough/solidYellowLeft.jpg "Hough"
[image5]: ./test_images_merged/whiteCarLaneSwitch.jpg "Merged"
[image6]: ./test_images_region/solidWhiteRight.jpg "Region"

---
### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.
##1. Pipeline Steps:

Our first step is to convert our input images to grayscale for easier identification of lane lines using OpenCV's `cvtColor()` function. We then apply
 a 9x9 Gaussian Filter to reduce noise within the image. 
 
 [image2]: ./test_images_blur/solidWhiteRight.jpg "Blurred"
 
 Our next step is to apply Canny Edge Detection algorithim to remove redundant information from the images. 
 
 [image3]: ./test_images_canny/solidYellowLeft.jpg "Canny"
 
 With image edges detected, we next pass the images and chosen vertices to our `region_of_interest()` function which returns an image with a mask applied leaving only our specified area of interest remaining.  
 
 We then apply the Hough Line Transform for detection of straight lines in the images.
 
 [image4]: ./test_images_hough/solidYellowLeft.jpg "Hough"
 
 We next extrapolate the detected line segments returned by the Hough Line Transform function to map out the full extent of lanes on images using our `draw_lines()` function. 
 
 [image6]: ./test_images_region/solidWhiteRight.jpg "Region"
 
 Our final step is to merge our original images with the images containing projected lane lines.
 
 [image5]: ./test_images_merged/whiteCarLaneSwitch.jpg "Merged"
 

ReThe `draw_lines()` function was modified to find the linear fit to the coordinates in each group by looping over the detected lines and calculating their slope. Those lines with calculated slopes greater than 45 degrees were retained; otherwise If a line's calculated slope is greater than 45 degrees, it is retained; otherwise, it is discarded. This approach produced images with lanes well identified but failed to perform adequately on the test videos.


### 2. Identify potential shortcomings with your current pipeline


One major shortcoming is the pipeline's performance on the challenge video. I believe the poor performance can be attributed to the source and destination points used for the warping and unwarping of each video frame not being calibrated to the video's dimensions. After selecting coordinates specific to the dimensions of the video, the performance is likely to improve. This is a challenge I will work on tackling in the coming days.  


### 3. Suggest possible improvements to your pipeline

There are many possible improvements to be made to the pipeline. One such improvement would be to automate the source and destination coordinate selection process using machine learning (perhaps a CNN?). Another future improvement is to use semantic segmentation for likelihood of pixels belonging to specified classes such as road, car or sign. Generally, the goal is to increase the robustness of the model rendering it capable of handling a multitude of test cases. 





```python

```
