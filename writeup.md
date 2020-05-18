## Advanced Lane Finding Project

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

[image1]: ./examples/undistort_output.png "Undistorted"
[image2]: ./test_images/test1.jpg "Road Transformed"
[image3]: ./examples/binary_combo_example.jpg "Binary Example"
[image4]: ./output_images/binary_warped.png "Warp Example"
[image5]: ./examples/color_fit_lines.jpg "Fit Visual"
[image6]: ./examples/example_output.jpg "Output"
[video1]: ./project_video.mp4 "Video"
[image7]: ./output_images/window7.png "Visualizing Window"
[image8]: ./output_images/lane_result7.png "Lane Boundary"
[image9]: ./output_images/final.png "Final"
[image10]: ./output_images/0.jpg "Final_0"
[image11]: ./output_images/1.jpg "Final_1"
[image12]: ./output_images/2.jpg "Final_2"
[image13]: ./output_images/3.jpg "Final_3"
[image14]: ./output_images/4.jpg "Final_4"
[image15]: ./output_images/5.jpg "Final_5"
[image16]: ./output_images/5.jpg "Final_6"
[image17]: ./output_images/5.jpg "Final_7"


## [Rubric](https://review.udacity.com/#!/rubrics/571/view) Points


### Step 1: Camera Calibration


The code for this step is contained in the first code cell of the IPython notebook located in "Advance-Lane-Finding.ipynb"  

I start by preparing "object points", which will be the (x, y, z) coordinates of the chessboard corners in the world. Here I am assuming the chessboard is fixed on the (x, y) plane at z=0, such that the object points are the same for each calibration image.  Thus, `objp` is just a replicated array of coordinates, and `objpoints` will be appended with a copy of it every time I successfully detect all chessboard corners in a test image.  `imgpoints` will be appended with the (x, y) pixel position of each of the corners in the image plane with each successful chessboard detection.  


I then used the output `objpoints` and `imgpoints` to compute the camera calibration and distortion coefficients using the `cv2.calibrateCamera()` function.   


### Step 2:  Calibrate, Undistort and Warp images


I applied distortion correction using the `cv2.undistort()` function and perspective transform using the `cv2.getPerspectiveTransform() ` and `cv2.warpPerspective()` functions in `cal_undistort()` to the test image and obtained this result:

![alt text][image1]


### Step 3: Create Binary Tresholded Image

I used a combination of color and gradient thresholds to generate a binary image in `sobel_treshold()` function. Here's an example of my output for this step. 

![alt text][image4]

### Step 4 : Detect Lane Pixels

In `find_lane_pixels(binary_warped)` function, I detected line pixels using histogram. With windowing and `np.polyfit()` got left and right lane polynoms.

### Step 5: Visualize Sliding Window

I defined `visualizeSlidingWindow()` function to visualize windows on lane and test in on test image obtained result:

![alt text][image7]

### Step 6: Detect Lane Pixels and Fit to Find the Lane Boundary

I defined `search_around_poly()` function to fit lane pixels to find lane boundaries, applied to test image and obtained result:

![alt text][image8]

### Step 7: Warp the Detected Lane Boundaries Back Onto the Original Image.

I defined `DrawLine()` function to unwarp the binary image, combined it with original image applied to test image and obtained result:

![alt text][image9]



###  Step 8: Determine the Curvature of the Lane and Vehicle Position With Respect to Center

I defined `measure_curvature()` function to calculate curvature and radius of the lane.

### Step 9 : Define Pipeline

I defined a `pipeline()` function to combine all functions mentioned above. I takes and image, calibrates camera, udistort and make perspective transfrom on it. After this, it converts the warped image to binary image using sobel operator, HSL transform and tresholding. With binary image, it finds lane pixels and calcuates curvature and raidus of lane. Result of pipeline on test images: 

![alt text][image10]
![alt text][image11]
![alt text][image12]
![alt text][image13]
![alt text][image14]
![alt text][image15]
![alt text][image16]
![alt text][image17]

---

### Pipeline (video)

#### 1. Provide a link to your final video output.  Your pipeline should perform reasonably well on the entire project video (wobbly lines are ok but no catastrophic failures that would cause the car to drive off the road!).

Here's a [link to my video result](./project_video_output.mp4)

---

### Discussion

#### 1. Briefly discuss any problems / issues you faced in your implementation of this project.  Where will your pipeline likely fail?  What could you do to make it more robust?

Here I'll talk about the approach I took, what techniques I used, what worked and why, where the pipeline might fail and how I might improve it if I were going to pursue this project further.  
