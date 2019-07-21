+++
# Project title.
title = "Highway Lane Finding"

# Date this page was created.
date = 2019-07-19T12:00:00

# Project summary to display on homepage.
summary = "A Computer Vision pipeline to identify the highway lane boundaries in a video"

# Tags: can be used for filtering projects.
# Example: `tags = ["machine-learning", "deep-learning"]`
tags = ["computer-vision"]

# Optional external URL for project (replaces project detail page).
# external_link = ""

# Slides (optional).
#   Associate this project with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references 
#   `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
# slides = ""

# Links (optional).
# url_pdf = ""
# url_slides = ""
# url_video = ""
url_code = "https://github.com/nihaldhamani/CarND-Advanced-Lane-Lines"

# Custom links (optional).
#   Uncomment line below to enable. For multiple links, use the form `[{...}, {...}, {...}]`.
# links = [{icon_pack = "fab", icon="twitter", name="Follow", url = "https://twitter.com/georgecushen"}]

# Featured image
# To use, add an image named `featured.jpg/png` to your project's folder. 
[image]
  # Caption (optional)
  caption = "Credit: Udacity Self Driving Car Nanodegree"
  
  # Focal point (optional)
  # Options: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight
  focal_point = "Smart"
+++


## Project Overview
The goal of the project was to write a computer vision pipeline using OpenCV to identify the lane boundaries from a dashcam video. The pipeline was written in Python using the OpenCV Computer Vision library.

<center>{{< figure src="lane-finding.gif" title="Example video output from a dashcam video" >}}</center>

The following steps were taken in order to achieve the goals of the project:



* Compute the camera calibration matrix and distortion coefficients given a set of chessboard images.
* Apply a distortion correction to raw images.
* Use color transforms gradient thresholds to create a thresholded binary image.
* Apply a perspective transform to rectify binary image.
* Detect lane pixels and fit to find the lane boundary.
* Determine the curvature of the lane and vehicle position with respect to center.
* Warp the detected lane boundaries back onto the original image

### Camera Calibration
I start by preparing "object points", which will be the (x, y, z) coordinates of the chessboard corners in the world. Here I am assuming the chessboard is fixed on the (x, y) plane at z=0, such that the object points are the same for each calibration image. I used these object points and corresponding image points that would exist to calculate the distortion. Luckily OpenCV provides methods such as cv2.calibrateCamera() to make this easier

<center>{{< figure src="chessboard.png" title="Chessboard camera calibration" >}}</center>

### Detecting Lane Lines and Curvature
Using a combination of color and gradient thresholds, I was able to generate a pretty decent looking binary image. The binary image is then masked remove excess noise and then warped using a perspective transform to achieve a birds-eye view of the lane lines. Finally I was able to use the histogram method to detect points along curved lines and used those points to fit a polynomial.

Here are some examples from the intermdiate steps: 

<center>{{< figure src="binary.png" title="Before and after binary thresholding" >}}</center>
<center>{{< figure src="masked.png" title="Masked output of binary image" >}}</center>
<center>{{< figure src="warped.png" title="Birds-eye perspective transform of masked image" >}}</center>


### Failures and Future Work
There are a lot of fluctuations in my pipeline. One thing to note is I tried implementing search based on previous poly fits but that caused the fluctuations to worsen. Additionally, I tried implementing smoothing as well but that showed no significant improvement. Future work involves implementing a solution to search around the already found lane lines as opposed to finding them for each frame. Furthermore, in order to make my pipeline more robust, I could implement better sanity checking that would make the overall output smoother.







