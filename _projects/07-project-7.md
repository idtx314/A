---
layout: project
title: Receding Horizon CNC Interface
date: June 15, 2018
image: mill.png
permalink: "project-7.html"
---

## Overview

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


## Header/ major project components

## Intro video/pictures


## Github Repo
[https://github.com/idtx314/mill_controller](https://github.com/idtx314/mill_controller)


## Project Introduction
The motion of robots is generally stiff and repetitive, often carried out with little regard for the current context of the machine. The reasons for this are rooted in the way that robotic motion plans are generated and executed. Most motion planners generate trajectories using very formulaic algorithms. Robots execute those trajectories very rigidly by matching specific positions at specific times, often blindly and with no sense of an underlying goal.
In an effort to improve this situation and produce more adaptive, even graceful robots, Ahalya Prabhakar carries out research on novel methods of information based trajectory generation and receding horizon control systems that can modify planned motions based on the success of preceding ones. 
After promising studies carried out with two dimensional systems, Ahalya now wants to begin performing experiments with a three dimensional platform. The goal of this ongoing project is to build her that platform.  
This page documents my contributions to this effort during the Spring and Fall of 2018. By the end of my time on the project I had outlined a two dimensional "Phase 1" of project development, constructed an experimental platform, built a simulator element, developed the receding horizon control software, and produced documentation on installation and operation so that future students can continue to develop the project into a full fledged three dimensional experiment platform.


## Hardware
#### Talk about what I selected and why
#### Milling/Printing Choice

## Software
#### Why ROS, critical functions
#### Trajectory Parsing
#### Gcode Sending
#### Image Processing

## Future Development Outline






































<img src="./public/images/mill_animated.gif" alt="Animated Mill" width="500" style="float: right;margin-right:auto; padding: 10px;"/>
In this project I created a ROS package to provide computer vision based feedback control for an X-Carve CNC mill. The mill was configured to operate as a pen plotter accepting time controlled x, y, and z input. The package accepts trajectories from csv files or in a variety of ROS message formats, which it then parses into gcode and transmits to the mill to be executed.
After running a trajectory for a given time period, the mill is instructed to stop operating and move the equipment away from the material. Images of the material are taken by a fixed usb camera and then processed to identify locations where the mill has drawn on the paper. This data is visualized in Rviz, and published to ROS topics in a variety of formats.  
The published data can be used to determine how well the mill has performed in executing the trajectory so far, and what alterations to the planned trajectory are necessary to achieve the desired end result of the trajectory planner.  
The motivation underlying the construction of this project is to support the ergodic trajectory research of Ahalya Prabhakar and the Neuroscience and Robotics Laboratory at Northwestern University. As part of the lab's ongoing mandate to explore neurology by implementing unusual behaviour in robotic platforms, Ahalya's research explores the remarkably life like results of using time sensitive x, y, and z trajectories to guide activities such as drawing and exploring. 

<iframe width="560" height="315" src="https://www.youtube.com/embed/BPGvnV0WLSQ" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


The project is written in C++ and Python, with ROS being used for modularity and flexibility in communication between components.
