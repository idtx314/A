---
layout: project
title: Starbax Program for Baxter
date: March 23, 2018
image: starbax/baxter.jpg
permalink: "project-2.html"
---

## Overview

|Components                     ||Concepts|
|:------------------------------||:----------------------|
|Rethink Robotics Baxter robot  || ROS                   |
|Keurig Coffeemaker             || Python                |
|Assorted cups and k-cups       || Trajectory Planning   |
|                               || Group coordination    |



<!--
Todo:
    Get this project working on my station and collect images
    Get video of my section of the project working. I know can use and rely on it.  
-->

## Repository
The git repository for this project is available [here](https://github.com/Laurenhut/ME495-final-project).


## Introduction
Coffee making is a necessary, but highly repetitive process. So when tasked with demonstrating our skills with the Robot Operating System (ROS) and robotics, my group of 4 students (Kashish Goyal, Lauren Hutson, Solomon Wiznitzer, and I) decided that we would automate the coffee making process.  

We selected the Baxter robot as the platform for our project. To bring the scope of the project in line with our time frame we set the goal of having Baxter operate a Keurig coffee maker and accompanying items like cups and pods. We set an additional goal of having the robot use visual processing to identify the objects in its workspace, allowing them to be placed anywhere.  

Over the course of 2 weeks we used a combination of color recognition and AR tag tracking to accomplish object recognition, created nodes and services for trajectory planning and execution, tied our individual work together into a functioning whole, and presented our project to students and faculty.


## Hardware
The Baxter robot was produced by Rethink Robotics for research and academic use. The platform consists of two arms and a swivel mounted "head", all three of which are equipped with a sensor suite including a color camera. The arms can mount a selection of grippers, and the robot's API is reasonably well documented by the manufacturer. Baxter was selected as the project platform both because it met all hardware requirements for the project and because it was the most likely to be available for use at any given time, allowing more freedom in development scheduling. The most significant drawback of the platform was that it used series elastic actuators, which are known to be less precise in their motions.  
With only two weeks to complete the project, it was decided to limit the scope of the problem where possible and then expand if time allowed. By using a Keurig single serve automatic coffee maker, the project outsourced some of the most complicated aspects of coffee making and was able to focus on a smaller set of motions and interactions.  



## Software



![Chassis](../public/images/starbax/baxter_press.gif)
![Chassis](../public/images/starbax/baxter_open.gif){: height="415px" width="300px"}
![Chassis](../public/images/starbax/baxter_close.gif){: height="297px" width="300px"}
