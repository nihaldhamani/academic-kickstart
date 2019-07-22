+++
# Project title.
title = "WAILA"

# Date this page was created.
date = 2019-07-16T12:00:00

# Project summary to display on homepage.
summary = "What Am I Looking At? (WAILA) is a real-time object detector Android app that predicts objects using Tensorflow and a model trained on the [COCO](http://cocodataset.org/#home) dataset. WAILA provides functionality to learn more about the object and to save it as a memory"

# Tags: can be used for filtering projects.
# Example: `tags = ["machine-learning", "deep-learning"]`
tags = ["android", "object-detection"]

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
# url_code = ""

# Custom links (optional).
#   Uncomment line below to enable. For multiple links, use the form `[{...}, {...}, {...}]`.
# links = [{icon_pack = "fab", icon="twitter", name="Follow", url = "https://twitter.com/georgecushen"}]

# Featured image
# To use, add an image named `featured.jpg/png` to your project's folder. 
[image]
  # Caption (optional)
  caption = "What Am I Looking At?"
  
  # Focal point (optional)
  # Options: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight
  focal_point = "Smart"
+++


## Android App Overview and Examples
The goal of the project was to create a functioning android app that was integrated with the Tensorflow API. 

The app performs the following functions:


  * Detects object from a video feed.
  * Draws bounding boxes on the object that can be clicked by the user.
  * Uses Wikipedia API to obtain more information about the object.
  * Saves detected object as a *memory* along with it's location.
  * Displays all memories that are stored on the cloud database.


### Authentication
Authentication is controlled through the Firebase Authentication service. 

The authentication fragment supports the following cases:

  * User login for existing account.
  * Anonymous user login.
  * Create new user account.

<center>{{< figure src="auth.png" title="Screenshot of authentication fragment" >}}</center>

### Detection from Video Feed
Once camera permissions are granted, the TensorFlow Object Detection intent is started. Here the user sees a live video feed from the phones camera and they can point it at any object. If its an object that the model recognizes, a bounding box is drawn around the object and a prediction is given. The user can learn more about the object by clicking anywhere within the bounding box of the object.

<center>{{< figure src="video.png" title="Model detecting a laptop with 97% confidence" >}}</center>

### Wikipedia Info and Memory Saving
Once the bounding box for the object is clicked, using Wikipedia’s API, WAILA return the details about what the object detected. It also returns another image from Wikipedia so that the user can relate the object they have seen with the picture.

Clicking *New Memory* allows the user to store this memory. If the user logs in with their credentials, they store the memory in their private database. However, if the user logs in anonymously, they store the memory in the open public database. 

Clicking *Past Memories* takes the user to a page where they can go look at their saved memories.

<center>{{< figure src="detected.png" title="Screen after detected object bounding box is clicked" >}}</center>


### Saved Memories
The image, location (if available), timestamp, and object title are all saved on a database hosted on the Firebase Database service. The memories are displayed on a custom RecyclerView. Clicking on a saved memory brings up the additional information saved along with a map of the location using the Google Maps API.

<center>{{< figure src="saved.png" title="Example of interactions with saved memories" >}}</center>


### Backend Processing
I think the most noteworthy thing about the way we deal with our database across our 5 different application activities. We have a Java class called PhotoManager that controls every interaction from our database. Since we want the same database reference across all the activities, we used a singleton design pattern to ensure that we always have the same database inference. PhotoManager has a lot of useful functions such as updating the current user, uploading a photo object to firebase, helper functions that convert to and from different data types and also a function that gets all the photo objects for a given user. Additionally, PhotoManager defines an interface getDataListener, that serves as a callback from when the RecyclerView wants to query the database.










