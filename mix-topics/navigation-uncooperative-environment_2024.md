# Robot navigation when lighting, weather, and geometry won't cooperate
[MIT Robotics](https://www.youtube.com/watch?v=oelXylttvS4)

by Tim Barfoot (University of Toronto) (18 Ocotber 2024)

His group has traditionally made an effort to find and work on unconventional sensors, including:
- sun sensors, including "homemade" sensors
- star trackers --> good to give you the rotation matrix at night (tiny footprint)
- radar
- doople LiDars (per point radial velocity estimate per point in the cloud)

> "Not everything needs to be solved in software, some things are solved with better hardware."

Today they are working on Radar (Navtech RAS3/RAS6) and an Aeva Aeries II Lidar (doopler).

## Doopler odometry
Doopler is a slightly different ranging principle than conventional Lidar. Same as used in radar. Based on FMCW (frequency modulated continuous wave).

First thing done --> include the doopler velocity estimates as a new factor to include in the factor graph and then solve with non-linear least squares. Better estimates than ICP, particularly in degenerate environments (i.e., environments with lack of sufficient geometric features or distinct structures that allow for reliable pose estimation and mapping: long corridors, tunnels, or vast open fields). 

They expanded this concept to radar odometry, which seems to work well after RANSAC.

## Localization on the road

Boreas dataset --> 📑[Boreas: a multi-season autonomous driving dataset](https://journals.sagepub.com/doi/epub/10.1177/02783649231160195) IJRR'23. 






## Going offroad

## Global Optimizality Certificates

📑key read: [An efficient global optimality certificate for landmark-based SLAM](#) by Holmes and Bargoot (RAS/IROS'23)

What are these? 
