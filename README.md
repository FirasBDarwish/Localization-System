# Localization-System
Developed as part of Research Assistantship work with the Laboratory of Computer-Human Intelligence headed by Professor Tuka Alhanai.

We are developing a localization (position and rotation tracking) system for use in experimental set-ups and to generate point clouds of fixed 3D euclidean space. 

## Aim of Project
To employ a streamlined method for object localization and detection in 3D space using a sensor-based system. Through tracking the absolute position of an object, this system can map various features of that object’s movement to specialized settings (3D position to robot motion and planning). We hope to provide a proof-of-concept for the selected method against other researched set-ups, as well as use the system to collect, process, and analyze different motion-based, 3D data. 

## Some of the fundamental tasks and overarching objectives of the project:
1. Literature Review: Conduct a wide and thorough evaluation of (a) current, (b) deployable, and (c) streamlined methods for localization.
2. Hardware Selection: Select appropriate hardware and approach.
3. Set Up: Set up hardware for localization system in laboratory setting and prepare instructions for replicating the experimental set-up.
4. Software: Develop a pipeline for receiving and processing 3D data from Vive.
5. Processing and Transforming: data using Procrustes Orthogonal Problem to standarize coordinate frames.
6. Extension: Apply experimental set-up to mapping problems (diluting 3D euclidean space to control robothand motion).

## 1. Literature Review
We surveilled different types of technologies that are in use to determine which methods are available for plug-and-play implementation today. This allows us to lay down a proof-of-concept for our selected approach by comparing it to our assessment of these other techniques.

A synthesis of these other methods and their respective literature sources can be found [here](https://docs.google.com/document/d/1ux5NU3kCQx4bAz_PhazY3dFVRATjMM7p3F19Rx_DHok/edit).

## 2. Hardware Selection
The selected, out-of-the-box system is to employ 2 Vive base stations alongside Vive trackers to configure the motion of the trackers based on emitted infrared pulses from the base stations. When compared against other methods along the parameters of cost, ease of access, and accuracy/precision, this external and internal sensor set-up is the most appropriate to the purposes of this study.

## 3. Set Up
![IMG-3769](https://github.com/FirasBDarwish/Localization-System/assets/94559551/04646a9f-37dc-41b2-a562-b0cd88848325)

There are several moving parts that we had to account for while designing the set-up.
In order not to disrupt the lab space and to offer us the flexibility to adjust our tracking space (depending on experimental needs), we opted out of fixing the base stations to the walls and selected two tripod extensions. The recomended minimum height for basestation placement is 6ft 6in.

The Central computer houses most of the software behind our position tracking operation. There are specific hardware requirements for this computer that are listed [here](https://www.vive.com/us/product/vive-pro2/specs/). Make sure to meet the minimum requirements listed for the Vive Pro 2.

### Software to be installed to facilitate set up:
-Steam
-SteamVR
-VIVE Console
-Visual Studio

