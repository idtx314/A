---
layout: project
title: Receding Horizon CNC Interface
date: June 15, 2018
image: mill.png
permalink: "project-7.html"
---

## Header/ major project components

|Components                     ||Concepts|
|:------------------------------||:-----|
|    grbl Controller     ||    Linux    |
|    Laptop  ||    Embedded Microprocessors    |
|    USB Camera      ||    ROS    |
|    X-Carve Mill       ||    Computer Vision    |
|                               ||    C++, Python    |
|||    Rviz    |
|||    GCode    |
|||    Receding Horizon Control    |


<iframe width="560" height="315" src="https://www.youtube.com/embed/ua0gecTH6jU" frameborder="0" style="display: block; margin-left: auto; margin-right: auto;" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


## Github Repo
[https://github.com/idtx314/mill_controller](https://github.com/idtx314/mill_controller)


## Project Introduction
The motion of robots is generally stiff and repetitive, often carried out with little regard for the current context of the machine. The reasons for this are rooted in the way that robotic motion plans are generated and executed. Most motion planners generate trajectories using very formulaic algorithms. Robots execute those trajectories very rigidly by matching specific positions at specific times, often blindly and with no sense of an underlying goal.
In an effort to improve this situation and produce more adaptive, even graceful robots, Ahalya Prabhakar carries out research on novel methods of information based trajectory generation and receding horizon control systems that can modify planned motions based on the success of preceding ones. 
After promising studies carried out with two dimensional systems, Ahalya now wants to begin performing experiments with a three dimensional platform. The goal of this ongoing project is to build her that platform.  
This page documents my contributions to this effort during the Spring and Fall of 2018. By the end of my time on the project I had outlined a two dimensional "Phase 1" of project development, constructed an experimental platform, built a simulator element, developed the receding horizon control software, and produced documentation on installation and operation so that future students can continue to develop the project into a full fledged three dimensional experiment platform.


## Hardware
The experimental platform is based on an X-Carve CNC mill and X-Controller, all purchased as a kit from Inventables. I modified the platform by attaching an articulated arm to the back. The arm can be easily configured to reach various heights and mount a variety of sensors over the carving bed.

<a href="https://imgur.com/a/Qnw8pum">
    <img src="./public/images/xcarve/platform_1.jpg" alt="X-Carve" width="500" style="display: block; margin-left: auto; margin-right: auto; padding: 10px;border: 0;"/>
</a>

#### Significant Design Choices
###### Carving/Printing
A mill was selected over alternative CNC platforms on the rationale that removing material would allow trajectories to be generated with the least constraint in the base scenario. This was in comparison to other methods like 3d printing, which would require that any trajectories produce a structurally stable product from nothing.
###### Axis Count
After researching available milling platforms, I selected a 3-axis X-Carve CNC system that was among the existing lab equipment rather than purchasing a full 5-axis system. The 3-axis system was expected to be significantly easier to control, and thus more suitable for an initial prototype. It was also immediately available, removing the need to order and assemble a new sysem.
###### Sensor Selection
A variety of cameras and depth cameras were examined while choosing the sensor for the platform. A Logitech C270 color USB camera was selected for use in the initial prototype, which only required color recognition. To accomodate the expected switch to a depth camera later in the project's development, I designed the image processing algorithms to work with point cloud data as well.
###### Sensor Mounting
A motorized camera mount was briefly considered to allow all relevant sides of the material to be imaged. Because mill systems that can carve more than one side of a material typically move the material rather than the end tool, I concluded that moving the camera would also be uneccesary.



## Software
The control software is designed as an interface between Ahalya's prototype trajectory generators and the experimental platform. To make future development as easy as possible, I prioritized modularity in the design.  
Individual functions of the controller are split out into separate ROS nodes, which can be replaced or modified at will with little fear of compromising the rest of the system. This also permits any given node to be written in either Python or C++, granting access to the libraries and features available to both languages.  
There are three primary functions: trajectory parsing, gcode sending, and image processing.

<a href="https://imgur.com/a/f9RgvEO" >
    <img src="./public/images/flowchart_project.png" alt="Full Chart" width="500" style="display: block; margin-left: auto; margin-right: auto; padding: 10px;"/>
</a>

###### Trajectory Parsing
To maximize ease of use with Ahalya's existing data formats, the system can parse a variety of input types into a 3 dimensional, time dependent trajectory. This data is then translated into a GRBL compatible G-code file for execution on the X-Controller.
###### G-Code Sending
The sending nodes communicate with the X-Controller through a serial over USB connection. After preparing the X-Carve for use, the sending node streams the G-Code file line by line and receives confirmations from the X-Controller. Streaming will continue until the trajectory ends or the time horizon has been exceeded.
###### Vision Processing
The vision processing nodes use OpenCV, the Point Cloud Library, and the Octomap library to process sensor data from a Logitech C270 USB camera into a variety of output formats. These outputs are a three dimensional representation of how the experiment material has changed as a result of the end-effector following the input trajectory. Ahalya's trajectory generation software can use this information to alter the planned trajectory for future timesteps in order to better achieve the intended final outcome.



## Future Development Outline
* Reconfigure the software to operate as a state machine with a central control node and GUI.
* Add color thresholding to the vision processing.
* Add the end mill and configuring the machine for milling.
* Replace the camera with a depth camera.
* Complete the transition into 3D milling.
* Automate imaging calibration process.
