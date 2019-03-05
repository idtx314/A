---
layout: project
title: Mag-Sense Wearable Device
date: March 23, 2018
image: mag_sense/glove_prototype.jpg
permalink: "project-1.html"
---

<!-- 
TODO:

-->


<!-- Tags and Video -->
<!-- Line before a table should be blank -->

|Key Skills & Tools          ||                              |
|:---------------------------||:-----------------------------|
|Microcontrollers (Arduino)  ||Sensor Fusion                 |
|Programming (C, Python)     ||Communications (Serial, I2C)  |



## Repository
[Arduino Code](https://github.com/idtx314/gloveduino)  
[ROS Code](https://github.com/idtx314/rosglove)  
[CAD Files](https://cad.onshape.com/documents/59f6b9e68d51d87d17f218b7/w/08135ad5edb522fb621632bc/e/02c82a1bae2817e4d66146ec)  
<br />
<br />
<br />



## Introduction
In this project I created and proposed the project concept of a device that would allow a user to "feel" magnetic fields; selected a microcontroller, IMU, and motor; soldered and wired together the electronic components; designed wearable hardware in CAD; fabricated prototypes with 3D printing; wrote software in C to read from sensors, apply motor control, estimate state using sensor fusion, and communicate state estimates over serial; wrote software in Python to visualize state estimates using ROS and Rviz; and refined the hardware and software through failure analysis and user testing.
<br />
<br />
<br />



## Hardware
Hardware for this project is divided into a set of wearable mounts and the onboard electronics.
<br />
<br />
>
>#### Wearable Mounts
>Two small mounts secure all the project components into a complete package, which is designed to be worn on a user's person. A ring holds the sensor and feedback motor, while all other components are mounted onto a plate, which is secured to the forearm with velcro straps. My design allows the user to focus all their attention onto the finger when attempting to "feel" a magnetic field while minimizing the perceived weight of the package. All CAD modeling for these components was done in Onshape, an online sister product of Solidworks. Prototypes were 3D printed from PLA plastic.

<img src="./public/images/mag_sense/ring.png" alt="IMU Ring" style="display: inline-block; max-width: 49%; max-height: 49%;" />
<img src="./public/images/mag_sense/forearm.png" alt="Forearm Plate" style="display: inline-block; max-width: 49%; max-height: 49%;" />

><br />
><br />
>
>#### Electronics
>The electronics for this project consist of an Arduino microcontroller PCB, a logic converter PCB, an MPU-9250 9-axis IMU (with accelerometers, gyros, and magnetometers), a motor driver PCB, and an Eccentric Rotating Mass (ERM) motor for haptic feedback.
>The IMU and motor are mounted on the ring mount. The Arduino, logic converter, and motor driver boards are mounted on the forearm mount. Soldered connections between these components use multi-stranded wiring for flexibility and are reinforced with heat shrink tubing and adhesive. Power and serial communications are provided by the USB port on the Arduino.
<br />
<br />
<br />



## Software
The software for this project performs four primary functions: IMU calibration, data collection and state estimation, motor control, and state visualization. Most functions are handled on the Arduino microcontroller, with visualization being performed by a ROS node intended to run on an attached Linux system.
<br />
<br />
>
>#### IMU Calibration
>The IMU calibration algorithm is written in C on the Arduino, and runs during the microcontroller's initialization. The algorithm calculates bias values for the accelerometers and gyros using at rest readings, then performs hard iron and soft iron calibration of the magnetometer's hall sensors to co-locate the reading centers and normalize the reading surface to an ellipsoid.  
>Instructions on when and how to move the IMU during calibration are provided over serial, and will be printed to the terminal if received by the ROS node made to handle serial communications.  
>Significant portions of the calibration code were provided by Kris Winer, whose libraries were helpful for learning to use the IMU.

<img src="./public/images/mag_sense/calibration.jpg" alt="Before Cal" style="display: inline-block; max-width: 33%; max-height: 33%;" />
<img src="./public/images/mag_sense/calibration2.png" alt="After Hard Iron" style="display: inline-block; max-width: 33%; max-height: 33%;" />
<img src="./public/images/mag_sense/calibration3.png" alt="After Soft Iron" style="display: inline-block; max-width: 33%; max-height: 33%;" />

><br />
><br />
>
>#### Data Collection and State Estimation
>The state estimation algorithm is written in C on the Arduino, as part of the looping program. Data from the gyro, accelerometer, and magnetometer registers is read from the IMU using I2C communications protocol.  
>The gyro data is integrated over time to produce an estimated change from the initial orientation of the IMU. Accelerometer data is used to estimate roll and pitch based on the direction of gravity, and these estimates are combined with the gyro values using a complimentary filter in order to correct for the compounding error created by integration.  
>The final estimated orientation is broadcast using Serial protocol over the USB port, along with the magnetometer readings.
><br />
><br />
>
>#### Motor Control
>The motor control algorithm is written in C on the Arduino, as part of the looping program. Vibrations of different frequency and pattern are commanded based on the magnitude of the magnetic field detected by the IMU, in order to indicate the approximate strength of the field to the user.
><br />
><br />
>
>#### State Visualization
>The magnetic field and IMU data is visualized using a pair of ROS nodes programmed in Python, and intended to run on a computer connected to the Arduino via USB.  
>The first ROS node listens for serial communications containing orientation data over the USB port and translates the contents into a ROS message. The second ROS node receives that message and uses the data to publish visualization markers for the magnetic field strength and direction, and the orientation of the IMU compared to its initial position. These markers can then be visualized using Rviz.

<img src="./public/images/mag_sense/visualization.png" alt="Visualizer" width="500" style="display: block; margin-left: auto; margin-right: auto; padding: 10px;"/>

<br />
<br />
<br />



## Relevant Links
* [JohnChi Example Sketch](https://playground.arduino.cc/Main/MPU-6050)
* [Kris Winer MPU9250 Algorithms](https://github.com/kriswiner/MPU9250)
* [Sparkfun Haptic Motor Driver Library](https://www.sparkfun.com/products/14538)
* [Sparkfun IMU Library](https://www.sparkfun.com/products/13762)

