---
layout: project
title: Quadrotor Chassis and Mixed-Autonomy Controller
date: March 23, 2018
image: Quad.jpg
permalink: "project-3.html"
---

## Overview

|Components                     ||Concepts|
|:------------------------------||:------|
|    MPU-9250 9-Axis IMU    ||  PID Feedback Control  |
|    PWM Board  ||    Embedded Microprocessors  |
|    ERC      ||    Motor Control  |
|    Raspberry Pi Zero    ||    Feedback Based Position and Orientation Control  |
|                               ||  3D Position Data  |
|||    C Programming  |
|||  Group Workflow and Project Management  |



<!--
Todo:
    Add detailed hardware section
    Add detailed software section
    Add future work?
    Reconfigure images and video appropriately. Produce some better gifs.
-->

<iframe width="560" height="315" src="https://www.youtube.com/embed/VJnbBmU5wRM" frameborder="0" style="display: block; margin-left: auto; margin-right: auto;" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Repository

The project is written mostly in C. The final codebase is available on my github repository [here](https://github.com/idtx314/ME-495-Quadcopter).

## Introduction

Quadcopters have become common platforms for research, industry, and leisure. Some of this ubiquity is surely due to their stability and ease of use, and it might suprise many to learn that these properties aren't inherent to the design. The eerie grace of a well designed quadcopter is actually a result of its intricate control algorithms, and building such a platform is an opportunity to learn about these algorithms first hand.
The goal of this project is to assemble and program the control software for a small quadcopter that will respond to control input from the user, but hover in place when left to operate autonomously.
This project course was tackled in groups of two. Over a ten week period, Drew Warren and I followed the guidance of the course material to produce an air worthy chassis and program control code that responded well to user input over a wireless network. Horizontal autonomous position holding was accomplished using fusion of onboard sensor data and positional information provided by a Vive lighthouse observing the flight.





## Implementation Summary
The quadcopter chassis was made of carbon fiber and steel parts, which were provided by the class. The electronics involved were an ESC board and a PWM board to regulate the motors, a Raspberry Pi Zero to control the assembly, a Lithium Polymer battery to power the drone, and a USB wireless card attached to the Pi so that we could send commands and data from a laptop over wireless SSH connection. A 9-axis IMU provided accelerometer and gyroscope data. A set of Vive sensors mounted on top of the quad allowed us to determine yaw and position in cartesian space based on signals from a lighthouse. User control was provided through a USB video game controller connected to the laptop.

![Chassis](../public/images/Chassis.png){: height="224px" width="300px"}

Code was written in C, with instructors providing low level initialization and management functions for the motors, vive, and controller. This allowed us to place our focus on higher level operation and control of the quadcopter itself. The control script calculates pitch and roll of the quadcopter using a complementary filter of accelerometer and integrated gyroscope data. PID controllers use that information to adjust motor speed as needed to maintain a target orientation. The target orientation is set by a weighted combination of the control input from the user and the output of more feedback control loops, which use positional data provided by the Vive sensors to adjust target orientation and negate horizontal drift.

<img src="./public/images/quadcopter/control_test.gif" alt="Testing roll controls" width="500" style="display: block; margin-left: auto; margin-right: auto; padding: 10px;"/>


