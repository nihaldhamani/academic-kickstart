+++
# Project title.
title = "Seeker Vision"

# Date this page was created.
date = 2019-07-16T12:00:00

# Project summary to display on homepage.
summary = "A NASA Johnson Space Center funded mission using open-source machine learning and computer vision tools for autonomous vision-based navigation in space. Final system launched on Cygnus NG-11 in April 2019 with a mission date of July 2019."

# Tags: can be used for filtering projects.
# Example: `tags = ["machine-learning", "deep-learning"]`
tags = ["deep-learning", "computer-vision", "cubesats"]

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
url_pdf = "seeker_utrw_poster.pdf"
# url_slides = ""
# url_video = ""
# url_code = ""

# Custom links (optional).
#   Uncomment line below to enable. For multiple links, use the form `[{...}, {...}, {...}]`.
# links = [{icon_pack = "fab", icon="twitter", name="Follow", url = "https://twitter.com/georgecushen"}]

# Featured image
# To use, add an image named `featured.jpg/png` to your project's folder. 
[image]
  # Caption (optional)
  caption = "Credit: NASA Johnson Space Center"
  
  # Focal point (optional)
  # Options: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight
  focal_point = "Smart"
+++

## Quick Overview
* Seeker is a NASA Johnson Space Center CubeSat Mission hoping to demonstrate capabilities relevant to on-orbit, free-flying inspection of space vehicles.
* [Texas Spacecraft Laboratory](https://sites.utexas.edu/tsl/seeker/) contracted by JSC to develop a novel visual navigation system for Seeker-1 that provides azimuth and elevation of a target spacecraft using only a monocular camera
* While serving as the ML/CV lead, our team trained CNN's, wrote computer vision algorithms, and integrated everything into a flight-ready system.
* Launched on Cygnus NG-11 in April 2019. Mission to be carried out in July 2019.
* Research was presented at UT Research Week's poster session in April 2019 and won the 1st-place audience favorite award. You can find our poster [here](seeker_utrw_poster.pdf)


<center>{{< figure src="seeker-deep-space-tracking.gif" title="Tracking Cygnus with a uniform backdrop" >}}</center>



## A More Detailed Overview
I served as the Machine Learning & Computer Vision lead, overseeing 6 student developers and researchers in the Texas Spacecraft Laboratory working on the Seeker Vision project. The goal of the project was to use low-cost COTS hardware and open-source ML tools to enable NASA's Seeker CubeSat to detect, identify, and localize a target spacecraft ([Cygnus](https://en.wikipedia.org/wiki/Cygnus_(spacecraft))) while in orbit. Our team trained Convolutional Neural Networks and wrote Computer Vision algorithms which were then integrated with the flight software. The measurements taken by the system are then used in real-time in the guidance, navigation, and control of the Seeker-1 CubeSat.

Our "intelligent camera" was selected for integration on the flight unit among competing solutions. The Seeker-1 CubeSat will validate and test the vision system for vision-based navigation during its mission in July 2019.

<center>{{< figure src="seeker-earth-tracking.gif" title="Tracking Cygnus against a noisy backdrop" >}}</center>

### Seeker CubeSat Mission Overview
[Seeker](https://roundupreads.jsc.nasa.gov/pages.ashx/991/QA%20Seeker%20and%20NASA%20shall%20find) is a NASA Johnson Space Center mission funded as an International Space Station project to develop an ultra-low cost approach to highly automated extravehicular inspection of crewed or uncrewed spacecraft.

<center>{{< figure src="seeker-kenobi.png" title="Seeker (left) & its 'translator' Kenobi (right). Credit: NASA JSC" >}}</center>

The [Texas Spacecraft Laboratory](https://sites.utexas.edu/tsl/), with UT Aerospace Engineering and Engineering Mechanics professor Dr. Maruthi Akella serving as Principal Investigator, was funded to develop a vision system for the Seeker-1 technology demonstration mission that launched in April 2019. Seeker-1 is a 3U CubeSat that will be deployed from an Orbital ATK Enhanced Cygnus ISS resupply spacecraft following the completion of its resupply mission in July 2019. The Seeker-1 CubeSat will perform a 60-minute mission consisting of proximity operations around the Cygnus spacecraft. 


### Project Requirements and Challenges
* Our vision system had to be capable of detecting and calculating relative bearing estimates at 1Hz on an Intel Joule 570x (not that powerful)
  - Low computing power and time constraints eliminated many solutions viable for Earth-based systems
* Cygnus was 'non-cooperative'
  - had no fiducial markers and could not communicate its position during the mission
* The space environment presented us with additional challenges
  - Clouds and complex features on the Earth introduced noise
  - Lighting was varied and very inconsistent
  - Radiation could disrupt camera sensors producing noisy images
* Camera system needed to be commandable to change camera parameters in real-time

### Detection and Localization
Google's MobileNet SSD v1 architecture provided us with a framework for training and tuning object detection models. The lightweight object detector was extensively tested and proved to be resilient and met our 1Hz requirements during hardware-in-the-loop testing.

<center>{{< figure src="example-cygnus-detection.png" title="An example of Cygnus detection" >}}</center>

### Synthetic Image Generation
In order to train a robust model, we needed a dataset of images with varied backgrounds conditions and orientations. As a result, we focused on generting high-fidelity synthetic imagery using Unreal Engine and Microsoft's AirSim.

<center>{{< figure src="simulated-cygnus-2.png" title="A synthetically-generated image of Cygnus" >}}</center>

### Relative Bearing Calculation
In order to obtain the centroid (needed to calculate the relative bearings) of the Cygnus body, many different contouring algorithms were tested. Ultimately, a classifer was developed to determine the backdrop condition (deep space, noisy Earth, uniform Earth) and the contouring algorithm that was the best for each condition was applied

<center>{{< figure src="seeker-contouring.png" title="An example of Cygnus contouring" >}}</center>

## Ongoing Work

The Seeker team at JSC has chosen to fund continued research in order to develop a system capable of computing relative pose using a monocular camera.