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
![IMG-3769](https://github.com/FirasBDarwish/Localization-System/assets/94559551/b431d923-eabe-47f6-a16f-5ae6ef0d2ef4)

There are several moving parts that we had to account for while designing the set-up.
In order not to disrupt the lab space and to offer us the flexibility to adjust our tracking space (depending on experimental needs), we opted out of fixing the base stations to the walls and selected two tripod extensions. The recomended minimum height for basestation placement is 6ft 6in.

The Central computer houses most of the software behind our position tracking operation. There are specific hardware requirements for this computer that are listed [here](https://www.vive.com/us/product/vive-pro2/specs/). Make sure to meet the minimum requirements listed for the Vive Pro 2.

### Software to be installed to facilitate set up:
* Steam
* SteamVR
* VIVE Console
* Visual Studio
* "Localization_System_(Data_Upload_and_Pre_Processing).ipynb"
* samples_vs2017.sln *(for tracking HMD)*
* OpenVRTrackingExample.sln *(for tracking controllers)*

## 4. Software

### For tracking HMD:
Once your hardware is set up and you have steamVR and VIVEconsole running, do the following carefully:
1. Run Visual Studio as administrator
2. Open Solution and select the file 'samples_vs2017.sln' (also accessible without github compression [here](https://drive.google.com/drive/folders/1IMe8gzdmaPh613JaygjoRtgVKjA9-ax6?usp=sharing))
    - NOTE: DO NOT CHANGE THE FILE WHATSOEVER. ALL HELPER FUNCTIONS HAVE BEEN CONFIGURED AND WRITTEN FOR YOU.*
3. Build both 'hellovr_dx12' and 'hellovr_opengl' from the solution explorer.
4. Click 'Local Windows Debugger'

If everything is configured properly, you should be able to see your console print your HMD's position and rotation. Save/export debug/output console.

Once you've saved/exported a .txt file of your debug/output log in Visual Studio, make sure to clean your .txt file manually before moving on to data processing and analysis. This removes any lines in the output log that are related to set-up/system initialization and/or system termination. See the *sample* .txt files in the folders "input (before_cleaning)" and "output (after_cleaning)" for how the .txt files should be edited.

Then, follow the instructions in "Localization_System_(Data_Upload_and_Pre_Processing).ipynb" found in the GitHub repo to process the .txt file to a Pandas Dataframe and conduct some exploratory analysis.

### For tracking controllers:
Once your hardware is set up and you have steamVR and VIVEconsole running, do the following carefully:
1. Run Visual Studio as administrator
2. Open solution and select the file 'OpenVRTrackingExample.sln' (accessible [here](https://drive.google.com/drive/folders/1La5g4xWDrm0M61xHiKC8yMNwjrBg1I6u?usp=drive_link).
    - NOTE: DO NOT CHANGE THE FILE WHATSOEVER. ALL HELPER FUNCTIONS HAVE BEEN CONFIGURED AND WRITTEN FOR YOU.
3. Build 'OpenVRTrackingExample' from the solution explorer.
4. Click 'Local Windows Debugger'

If everything is configured properly, you should be able to see your console print your left and right controller's position. Save/export console.

*NOTE: it is preferred to change the VR headset's power management settings so that the headset display turns off after 5 minutes, see [instructions here](https://forum.htc.com/topic/6186-htc-vive-tracker-how-to-stay-awake-when-no-movement-for-a-long-while/), as the controller's tracking will pause if HMD is not awake.

## 5. Processing and Transforming:

See Professor Gilbert Strang [Lecture on Orthogonal Procrustes Problem](https://www.youtube.com/watch?v=0Qws8BuK3RQ&t=315s) for overview of what we are attempting to achieve with this step as well as [Orthogonal Procrustes Problem overview](https://en.wikipedia.org/wiki/Orthogonal_Procrustes_problem) for how we will derive the solution to approximate matrix B to matrix A using an orthogonal matrix.

In the context of our position tracking problem, this allows us to standarize coordinate frames.

Given {M, N}, two finite size point sets in a finite-dimensional real vector space R^3 which contain M and N points respectively, if M != N, then we cannot directly use the solution to Orthogonal Procrustes Problem and will require simultaneous pose and correspondence registration, see discussion [here](https://stackoverflow.com/questions/51333836/procrustes-analysis-with-unequal-number-of-points).

This provides us with two underlying mechanisms for mapping a set of points N to a reference set of points M:
1. Filter N's concentration to match M, such that a solution to the Orthogonal Procrustes Problem can be calculated using scipy.linalg.orthogonal_procrustes
2. Employ iterative closest point to match each point in N to a point in M. Still exploring different Python implementations.

### Why is that important?
This is ultimately a tool to conduct experiments and extensions where accurate and precise 3D tracking in space is needed. We can't simply compare the results of one runtime of this experimental setup to another. We need to geometrically minimize the difference between two point clouds to properly compare them.

## 6. Extensions:
Use of any inverse kinematics tool to map motion in 3D space generated by point cloud to joint configurations needed to move robot. See [overview](https://www.mathworks.com/help/robotics/inverse-kinematics.html) by Mathworks.

## Items Still Pending:
* Creating pipeline to fix size of output matrices (for each trial run in an experiemnt) to be able to use the [procrustes solution](https://docs.scipy.org/doc/scipy/reference/generated/scipy.spatial.procrustes.html) offered by scipy.
    * The logic here is to scale the rate at which inputs are mapped to output matrix for the larger matrices so that it matches smaller matrix.
        * If A is 15x3 and B is 60x3, scale B by accepting a point every 4 points (filtering to scale).
* In case fixing size of output matrices is not possible or--*more importantly*--correspondences are hazy and noisy, I need to explore the use of [iterative closest point algorithms](https://en.m.wikipedia.org/wiki/Iterative_closest_point). These generalize better to 3D point clouds.
* Using [libsurvive](https://github.com/cntools/libsurvive) for vive tracker and controller position tracking (facilitates tracking process).
