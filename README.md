# SFND 2D Feature Tracking

<img src="images/keypoints.png" width="820" height="248" />

The idea of the camera course is to build a collision detection system - that's the overall goal for the Final Project. As a preparation for this, you will now build the feature tracking part and test various detector / descriptor combinations to see which ones perform best. This mid-term project consists of four parts:

* First, you will focus on loading images, setting up data structures and putting everything into a ring buffer to optimize memory load. 
* Then, you will integrate several keypoint detectors such as HARRIS, FAST, BRISK and SIFT and compare them with regard to number of keypoints and speed. 
* In the next part, you will then focus on descriptor extraction and matching using brute force and also the FLANN approach we discussed in the previous lesson. 
* In the last part, once the code framework is complete, you will test the various algorithms in different combinations and compare them with regard to some performance measures. 

See the classroom instruction and code comments for more details on each of these parts. Once you are finished with this project, the keypoint matching part will be set up and you can proceed to the next lesson, where the focus is on integrating Lidar points and on object detection using deep-learning. 

## Dependencies for Running Locally
* cmake >= 2.8
  * All OSes: [click here for installation instructions](https://cmake.org/install/)
* make >= 4.1 (Linux, Mac), 3.81 (Windows)
  * Linux: make is installed by default on most Linux distros
  * Mac: [install Xcode command line tools to get make](https://developer.apple.com/xcode/features/)
  * Windows: [Click here for installation instructions](http://gnuwin32.sourceforge.net/packages/make.htm)
* OpenCV >= 4.1
  * This must be compiled from source using the `-D OPENCV_ENABLE_NONFREE=ON` cmake flag for testing the SIFT and SURF detectors.
  * The OpenCV 4.1.0 source code can be found [here](https://github.com/opencv/opencv/tree/4.1.0)
* gcc/g++ >= 5.4
  * Linux: gcc / g++ is installed by default on most Linux distros
  * Mac: same deal as make - [install Xcode command line tools](https://developer.apple.com/xcode/features/)
  * Windows: recommend using [MinGW](http://www.mingw.org/)

## Basic Build Instructions

1. Clone this repo.
2. Make a build directory in the top level directory: `mkdir build && cd build`
3. Compile: `cmake .. && make`
4. Run it: `./2D_feature_tracking`.

## My changes in the Forked repo from Udacity Origin source

## Project rubic points:

1- Data Buffer :

I have used verctor Insert method to push element from back and pop first element(First Come First Serve) to optimize the data storage.
<img src="images/1.png" width="820" height="248" />
2-Keypoints detection:

the first step is to get the Key points in the input Image so we can use those key points to find matches with the following images. 
Using opencv Lib. I have Implement many key points detector (HARRIS, FAST, BRISK, ORB, AKAZE, and SIFT detectors).


By expermentaion:
* the Fast detector was the quickest in keypoint detection.
* SIFT detector was the slowest

<img src="images/2.png" width="820" height="248" />

the output from this step will be like this:

<img src="images/keypoints.png" width="820" height="248" />

As our Interest is to get the Time to Collision so I focused on the front car by removing any key point outside the car 
box by comapring the points Indecies with car box coordenadas.

<img src="images/3.png" width="820" height="248" />

3-Descriptors:

Using opencv Lib. I have Implement many key points Descriptors (BRIEF, ORB, FREAK, AKAZE and SIFT Descriptors).
By expermentaion:
* the BRISK Descriptors was the quickest with FAST key points detector.
* SIFT detector was the slowest with FAST key points detector.

<img src="images/4.png" width="820" height="248" />


After we get the Keypoint and It's Enviroment we step the matching by using the K-nearest or Nearest neighbor.

<img src="images/5.png" width="820" height="248" />

the out from matching step will be like that:

<img src="images/6.png" width="820" height="248" />

##TEST Results:

based on the test result:
top 3 are:
1-FAST+BRISK
2-FAST+ORB	
3-FAST+BRIEF	
