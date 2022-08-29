---
layout: post
title:  "Using a Convolutional Neural Network (CNN) to Create User-specific Symbols for Navigation"
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

![1D CNN]({{site.baseurl}}/assets/images/model.png)

<br>

<h5>Examples & Demonstrations</h5>
<h6 style="font-size:120%">Mazes</h6>
The maze generation algorithm developed through this project is able to create a maze of easy, medium, or hard difficulty. The mazes draw from a subset of tiles that allow for increasingly more freedom of movement. For example, easy difficulty is contrained to right-angle turns and straight movements, whereas medium difficulty introduces diagonal movements. The starting point is indicated by a green circle, while the end is marked by a blue circle.

Easy                    |  Medium            | Hard                  
:-------------------------:|:-------------------------:|:-------------------------:
<img src="{{site.baseurl}}/assets/images/easy_maze.png" width="500" /> |  <img src="{{site.baseurl}}/assets/images/medium_maze.png" width="500" /> | <img src="{{site.baseurl}}/assets/images/hard_maze.png" width="500" />

<br><br>

<h6 style="font-size:120%">Real-life Trials</h6>
Below are demonstrations of the data collection process using a randomly generated maze of easy difficulty. The chart overlays shown in the videos represent the input the user is providing through the SNP sensor.

<h6>Author</h6>
<video width="1080" controls>
  <source src="{{site.baseurl}}/assets/images/author_demo.mp4" type="video/mp4">
Your browser does not support the video tag.
</video>

<br>

<h6>Other User</h6>
<video width="1080" controls>
  <source src="{{site.baseurl}}/assets/images/other_demo.mp4" type="video/mp4">
Your browser does not support the video tag.
</video>

<br>

## Next Steps
- Easy difficulty was the only one tested during this project. Further testing is needed to confirm pipeline is working for medium and hard difficulties.  
- Add contextual information (e.g., point cloud data) to allow user more flexibility with symbol creation. E.g., an input is given in advance in a hallway, but the robot waits for the next opening to turn.  
- Create dynamic maze curriculum that allows user to differentiate between similar symbols. Mazes designed to differentiate between similar symbols will be auto-generated until clear distinction is achieved.  

<a class="repo-link" target="_blank" rel="noopener noreferrer" href="{{ site.baseurl }}/MSR_Final_Project">Docs</a>
