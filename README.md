## Advanced Lane Finding
[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)
![Lanes Image](./examples/example_output.jpg)

In this project my goal was to write a software pipeline to indentify the lane boundaries in a video. 
First of all I calibrate the camera by using buil-in opencv camera calibration functions. Laterly I use some customised binary threshold function to highlight lines and use perspective transformation to bird-view. After this I use sliding window or searching near previously finded polyline to find position of the lane in image. After all of these I compute car position on the lane and lane curvature and visualise lane and its features on image. 


---

### Camera calibration

this stage is located under heading **camera calibration** in my "AdvancedLineFinding" ipython notebook.

Because of some defects in camera lenses there are geometrical distortion and we need to correct them to use camera images to truly undestand forms of the real objects.

We use simply recogniseble patern as chessboard (regular secuenses of black and white squares) situated on a flat surface. We use 9x6 pattern. Take many pictures of it and find chessboar couners of it by cv2.findChessboardCorners. As we assume that patter is on a flat surfate we know that all line should be strate. We use cv2.calibrateCamera function which retuns mtx and dist coefficiets which further used to undistort images by cv2.undistort function.

Here is the result of the camera calibration for the chessboard image.
![Chessboard](./output_images/distUndist.png)

---

### Pipeline (single images)

First of all undistort our real images.
Here is the example.
![Real image undistortion](./output_images/realDistUndist.png)

Later in section **finding threshold** I try different color spaces like rgb, hls and hsv to find out which is the best to highlight lines on image, also I try different  gradients as x, y, magnitude and directional.
Finaly I used combined threshold which consists of v channel from hsv, s channel from hsl and complex gradient threshold (**final threshold** section)

Here is the result of my threshold function.
![Threshold](./output_images/Thresholded.png)




A great writeup should include the rubric points as well as your description of how you addressed each point.  You should include a detailed description of the code used in each step (with line-number references and code snippets where necessary), and links to other supporting documents or external references.  You should include images in your writeup to demonstrate how your code works with examples.  

All that said, please be concise!  We're not looking for you to write a book here, just a brief description of how you passed each rubric point, and references to the relevant code :). 

You're not required to use markdown for your writeup.  If you use another method please just submit a pdf of your writeup.

The Project
---

The goals / steps of this project are the following:

* Compute the camera calibration matrix and distortion coefficients given a set of chessboard images.
* Apply a distortion correction to raw images.
* Use color transforms, gradients, etc., to create a thresholded binary image.
* Apply a perspective transform to rectify binary image ("birds-eye view").
* Detect lane pixels and fit to find the lane boundary.
* Determine the curvature of the lane and vehicle position with respect to center.
* Warp the detected lane boundaries back onto the original image.
* Output visual display of the lane boundaries and numerical estimation of lane curvature and vehicle position.

The images for camera calibration are stored in the folder called `camera_cal`.  The images in `test_images` are for testing your pipeline on single frames.  If you want to extract more test images from the videos, you can simply use an image writing method like `cv2.imwrite()`, i.e., you can read the video in frame by frame as usual, and for frames you want to save for later you can write to an image file.  

To help the reviewer examine your work, please save examples of the output from each stage of your pipeline in the folder called `output_images`, and include a description in your writeup for the project of what each image shows.    The video called `project_video.mp4` is the video your pipeline should work well on.  

The `challenge_video.mp4` video is an extra (and optional) challenge for you if you want to test your pipeline under somewhat trickier conditions.  The `harder_challenge.mp4` video is another optional challenge and is brutal!

If you're feeling ambitious (again, totally optional though), don't stop there!  We encourage you to go out and take video of your own, calibrate your camera and show us how you would implement this project from scratch!

## How to write a README
A well written README file can enhance your project and portfolio.  Develop your abilities to create professional README files by completing [this free course](https://www.udacity.com/course/writing-readmes--ud777).

