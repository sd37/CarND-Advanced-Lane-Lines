##Writeup Template
###You can use this file as a template for your writeup if you want to submit it as a markdown file, but feel free to use some other method and submit a pdf if you prefer.

---

**Advanced Lane Finding Project**

The goals / steps of this project are the following:

* Compute the camera calibration matrix and distortion coefficients given a set of chessboard images.
* Apply a distortion correction to raw images.
* Use color transforms, gradients, etc., to create a thresholded binary image.
* Apply a perspective transform to rectify binary image ("birds-eye view").
* Detect lane pixels and fit to find the lane boundary.
* Determine the curvature of the lane and vehicle position with respect to center.
* Warp the detected lane boundaries back onto the original image.
* Output visual display of the lane boundaries and numerical estimation of lane curvature and vehicle position.

[//]: # (Image References)

## [Rubric](https://review.udacity.com/#!/rubrics/571/view) Points
###Here I will consider the rubric points individually and describe how I addressed each point in my implementation.  

---
###Writeup / README

####1. Provide a Writeup / README that includes all the rubric points and how you addressed each one.  You can submit your writeup as markdown or pdf.  [Here](https://github.com/udacity/CarND-Advanced-Lane-Lines/blob/master/writeup_template.md) is a template writeup for this project you can use as a guide and a starting point.  

You're reading it!
###Camera Calibration

####1. Briefly state how you computed the camera matrix and distortion coefficients. Provide an example of a distortion corrected calibration image.

Please see the notebook code cell 1, compute camera calibration for chessboard images for this.
I performed this on the test image provided by the ta in the lectures.

![alt text](./output_images/chessboard.png)


###Pipeline (single images)

####1. Provide an example of a distortion-corrected image.
Please refer to solution.ipynb code cell number 5-6 for this. Over there I have first undistorted the image and then performed the perspective transform.

Apt visulizations have been generated.
![alt text](./output_images/undistorted.png)


####2. Describe how (and identify where in your code) you used color transforms, gradients or other methods to create a thresholded binary image.  Provide an example of a binary image result.

Please refer to code cells 7-9 for this. I tried several thresholding scheme. In the end I used the color-grad threshold as visulized in cell 9.

![alt text](./output_images/thres-col-grad.png)

####3. Describe how (and identify where in your code) you performed a perspective transform and provide an example of a transformed image.

Please refer to solution.ipynb cell number 5-6 for this. Over there I have first undistorted the image and then performed the perspective transform.
The is similar to the one discussed in the lectures. It also describes what src and dst points I have used. This was recommended by some good people on the udacity forum.

Apt visulizations have been generated.

![alt text](./output_images/perspective.png)

####4. Describe how (and identify where in your code) you identified lane-line pixels and fit their positions with a polynomial?

Please refer to solution.ipynb code cells 9-10-11 for this. It is similar to the approach described in lectures and code is there in the cells.

![alt text](./output_images/poly-fit.png)


####5. Describe how (and identify where in your code) you calculated the radius of curvature of the lane and the position of the vehicle with respect to center.

Please refert to solution.ipnyb code cells 9 def_compute_radc() for this.


####6. Provide an example image of your result plotted back down onto the road such that the lane area is identified clearly.

Please see cell 15-16. Here lanes have been drawn on several test images.


![alt text](./output_images/lane_mapping.png)

---

###Pipeline (video)

####1. Provide a link to your final video output.  Your pipeline should perform reasonably well on the entire project video (wobbly lines are ok but no catastrophic failures that would cause the car to drive off the road!).

Here's a [link to my video result](https://github.com/sd37/CarND-Advanced-Lane-Lines/blob/master/project_video_soln_final.mp4)

There is a little wobble in the middle of the video when there is a huge shadow on the street, were it detects the railing as part of the lane.
It quickly is able to rectify this. Would love to know how this is solved.

---

###Discussion

####1. Briefly discuss any problems / issues you faced in your implementation of this project.  Where will your pipeline likely fail?  What could you do to make it more robust?

The pipeline would perform well on sunny days with moderate casting of shadows on the road.

Intially I tried performing search for lanes from scratch on every frame. This was very slow, ~1.0 iterations/sec. I was able to increase it to 1.6 iterations/sec by performing
a search in a margin around previously detected lane.

I also used the curvature of the detected lanes to sanitize it and compared it with the curvature of already detected lanes to decide whether to perform a full search or not.

I think implementation of smoothing approach discussed in the lectures and making use of the position of the vehicle for deciding to do the full search for lane can make the pipeline
more robust. Unfortunately, did not have time to invest in this.

Please let me know of other possible ways as well and references.
