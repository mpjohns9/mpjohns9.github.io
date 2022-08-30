---
layout: post
title:  "Using a Convolutional Neural Network (CNN) to Create User-specific Symbols for Navigation"
subtitle: "Final Project"
subsubtitle: "MS in Robotics &#8212 Northwestern University | Advised by: Matthew Elwin, PhD & Ola Kalinowska"
categories: [ Machine Learning, Python, ROS, Gazebo, Computer Vision, Simulation]
image: assets/images/sp_thumb.png
gif: assets/images/sp_thumb.png
repo: "https://github.com/mpjohns9/MSR_Final_Project"
when: June - August 2022
featured: false
hidden: false
---
The primary objective of this project was to classify [sip-and-puff (SNP)](https://www.orin.com/access/sip_puff/#Sip/Puff%20Breeze) signals into user-defined symbols to generate an intuitive set of controls. The application of this technology would be particularly useful to someone who lacks the ability to use their hands. This project allows for the creation of a custom set of controls using an SNP sensor in a short amount of time. 

<h5>The Process</h5>

1. To begin, a user must complete a set of simulated mazes that can be viewed through RViz and/or Gazebo.   
*Note: Though the user feels as if they are in control of the robot, the robot control is predefined based on the maze generated. Future development would allow for the user to affect robot behavior as they progress through the maze curriculum.*
2. The inputs a user provides to complete this maze are collected to train a neural network sepcific to that user. The data is auto-labelled based on tags applied to sections of the maze during the generation process.
3. User data is augmented to increase the size of the dataset, reducing the need for a more time intensive data collection process with the user. 
4. The augmented dataset is used to train a 1-dimensional convolutional neural network (CNN) to classify SNP inputs into discrete movement actions (forward, left, right, stop).
5. Using the trained network, the user can navigate the Gazebo world freely, and eventually, real life.

<h5>The Model</h5>
This project uses a 1-dimensional convolutional neural network (1D CNN) to classify user inputs into movement actions: forward, left, right, and stop. For each user, a new model is trained to make predictions specific to that user. The 1D CNN is trained on actual data collected from the user, as well as augmented data derived from the initial SNP input signals.  

<img src="{{site.baseurl}}/assets/images/model.png" width="50%"/>

<br>

<h5>Data Augmentation Process</h5>
The data augmentation process randomly applied transformations to the real data collected from a user until the desired number of data points was achieved. For this project, that number was 20,000 (starting from 20 original samples; 5 from each class).  

1. Center &mdash; Separates noise and signal and centers signal in time. This first step was applied to each data point.  
2. Apply one of the following:  
    - Compress &mdash; Compresses signal and adds noise in its place.  
    - Expand &mdash; Expands signal by taking mean of consecutive data.  
    - Shift Left/Right &mdash; Shifts signal either earlier or later in time.

<h5>Examples & Demonstrations</h5>
<h6 style="font-size:120%">Mazes</h6>
The maze generation algorithm developed through this project is able to create a maze of easy, medium, or hard difficulty. The mazes draw from a subset of tiles that allow for increasingly more freedom of movement. For example, easy difficulty is contrained to right-angle turns and straight movements, whereas medium difficulty introduces diagonal movements. The starting point is indicated by a green circle, while the end is marked by a blue circle.  

Easy                    |  Medium            | Hard                  
:-------------------------:|:-------------------------:|:-------------------------:
<img src="{{site.baseurl}}/assets/images/easy_maze.png" width="350" /> |  <img src="{{site.baseurl}}/assets/images/medium_maze.png" width="350" /> | <img src="{{site.baseurl}}/assets/images/hard_maze.png" width="350" />

<br><br>

<h6 style="font-size:120%">Trials & Results</h6>
This section highlights both the data collection and testing processes. After collecting sip and puff data from a user, the data was augmented and a model was trained. Using the trained model, the user was required to navigate a maze similar to the one used for data collection (also randomly generated). This time, however, their input was fed into the model and classified as one of the four movement actions (stop, start, left turn, right turn). Having control over the turtlebot, the user was asked to complete the maze. Results of these trials are discussed below.  

<h6>Data Collection</h6>
Below are demonstrations of the data collection process using a randomly generated maze of easy difficulty. The chart overlays shown in the videos represent the input the user is providing through the SNP sensor.  

<video width="720" controls>
  <source src="{{site.baseurl}}/assets/images/author_demo.mp4" type="video/mp4">
Your browser does not support the video tag.
</video>

<br>

<video width="720" controls>
  <source src="{{site.baseurl}}/assets/images/other_demo.mp4" type="video/mp4">
Your browser does not support the video tag.
</video>

<br>

<h6>Live Testing</h6>
This video shows a user navigating a maze using their own set of symbols created through the data collection and model training phases. In this trial, the model achieved 100% accuracy. Overall, the accuracy for this user was 91% (See User 1 below).  

<video width="720" controls>
  <source src="{{site.baseurl}}/assets/images/manual_demo.mp4" type="video/mp4">
Your browser does not support the video tag.
</video>

<br>

After collecting data using the process demonstrated above, a model was trained and tested live. As an example, a graphical representation of one set of symbols created by each user is shown below, along with results and qualitative commentary from the trials. Accuracy was determined by comparing user's intended action and the actual movement of the robot resulting from the model's prediction.  

<img src="{{site.baseurl}}/assets/images/results_table.png" width="95%"/>

Users 1-4 were profiles created by the author to test the robustness of the pipeline. User 5 was not the author and was given no instructions other than to use the sip and puff device to guide the robot through the simulated maze. In both cases, the data augmentation process outlined above was used to generate more data. In every trial, the trained model was able to successfully predict movement actions from sip and puff inputs; the user was able to easily navigate a maze using their custom set of symbols.  

## Next Steps
- Easy difficulty was the only one tested during this project. Further testing is needed to confirm pipeline is working for medium and hard difficulties.  
- Add contextual information (e.g., point cloud data) to allow user more flexibility with symbol creation. E.g., an input is given in advance in a hallway, but the robot waits for the next opening to turn.  
- Create dynamic maze curriculum that allows user to differentiate between similar symbols. Mazes designed to differentiate between similar symbols will be auto-generated until clear distinction is achieved.  

<a class="repo-link" target="_blank" rel="noopener noreferrer" href="{{ site.baseurl }}/MSR_Final_Project">Docs</a>
