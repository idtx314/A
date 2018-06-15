---
layout: project
title: Probabilistic Milling Interface
date: June 15, 2018
image: mill.png
permalink: "project-7.html"
---

## Overview

|Components                     ||Concepts|
|:------------------------------||:-----|
|    Hobbyist Milling Machine     ||    Linux    |
|    Linux Laptop  ||    Embedded Microprocessors    |
|    Sensor Array      ||    Trajectory Generation    |
|    Mill Microcontroller       ||    Computer Vision    |
|                               ||    Python    |
|||    Rviz    |
|||    ROS    |
|||    Receding Horizon Control    |




## Summary

The objective of this project is to produce a robust interface via which a user can operate a hobbyist milling machine. The machine and interface will be used to demonstrate the nature and potential of atypical trajectory generation for object manufacturing in 3 dimensions in a way that can be more intuitively understood by an untrained viewer. In particular, it will be used to support exploration of ergodic controllers (Prabhakar et al, 2017). Ideally the project will also include a machine vision component to allow a receding horizon control method.  

The project will consist of a simulation component and a hardware component. The simulation will accept a time dependent trajectory and output a visualization of that trajectory's effect on a simulated stock material, allowing quick validation of trajectory performance.  

![Display Mode](../public/images/mill_sim.gif){: height="231px" width="300px"}

The hardware component will consist of a hobbyist milling machine with 3 or more axes of motion, paired with a machine vision sensor system, and operated through a simple gui or terminal interface. The interface will accept the same input as the simulator and translate it into a machine executable toolpath. The mill will partially execute that toolpath, at which point the sensor rig will evaluate the actual effect on the stock material and output geometric data representing the material's current shape. It is expected that this data will then be used to automatically re-generate the trajectory to account for deviations from the expected effect, with the interface then being given this new trajectory to follow. This adaptive process will be iterated until the material geometry closely matches the expected output.



The project will be written primarily in Python, with ROS being used for modularity in communication between components. The code is currently not available for public viewing.


References
1. Prabhakar, Ahalya, et al. "Autonomous visual rendering using physical motion." arXiv preprint arXiv:1709.02758 (2017).
