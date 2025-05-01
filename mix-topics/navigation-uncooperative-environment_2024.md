# Robot navigation when lighting, weather, and geometry won't cooperate
[MIT Robotics](https://www.youtube.com/watch?v=oelXylttvS4)

by Tim Barfoot (University of Toronto) (18 October 2024)

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

Semi-supervise approach: used a network to learn masking all the outliers from the radar --> dICP (differential ICP), assigned weights to every point in the point cloud.
📑[Pointing the way: refining radar-to-lidar licalization using learned ICP weights](https://arxiv.org/abs/2309.08731#:~:text=The%20learned%20weights%20facilitate%20ICP,real%2Dworld%20autonomous%20driving%20data.)

🧠 Interesting thought: how can we know our localization will work along a particular route?
📑 [Toward Certifying Maps for Safe Localization Under Adversarial Corruption](https://arxiv.org/abs/2309.04251), RAL'24

## Going offroad

**Visual Teach & Repeat (VT&R)**: framework that allows a robot to navigate using only vision in unstructured environments

📑 Key paper: [Visual teach and repeat for long-range rover autonomy](https://onlinelibrary.wiley.com/doi/abs/10.1002/rob.20342) Journal of Field Robotics, 2010.

- teach --> user drives the robot once and it stores sparese visual info in a relative pose graph
- repeat --> robot localizes by matching live visual data to map and steers to stay on path
(no GPS, no IMU, no DNN, no global map, no semantics/structure)

Now working on avoiding obstacles during the repeat trajectories that weren't there in the teaching trajectory with simple obstacle detection and local sample-based motion planner + MPC to refine the planner. It'd be cool for this is to avoid the use of vocabularies, **"open-vocabulary terrain assessment"** (, i.e., knowing that something is an obstacle without knowing what that obstacle is).

> Tim's getting back to work on space robotics (since 2010 when his lab did its last work with CSA).

## Global Optimizality Certificates

📑key read: [An efficient global optimality certificate for landmark-based SLAM](#) by Holmes and Bargoot (RAS/IROS'23)

We typically set up our localization problem as a (nonconvex) optimization problem. The cost function canquite often have local minima; a good initial guess is needed ot avoid them. _How do we know if our solution is global or local?_

One way is by using **convex relaxation**. 

Pioneering works on **global optimization in robotics**:

- [Rotation syncrhonization](https://openaccess.thecvf.com/content_cvpr_2018/papers/Eriksson_Rotation_Averaging_and_CVPR_2018_paper.pdf) by Eriksson, Olsson, Kahl, and Chin. CVPR 2018
- [Pose-graph optimization](https://arxiv.org/abs/1612.07386) by Rosen, Carlone, Bandeira, and Leonard. IJRR 2019
- [Robust pointcloud](https://arxiv.org/abs/2001.07715) alignment by Yang, Shi, and Carlone. TRO 2020
- Extrinsic calibration [1](https://arxiv.org/abs/1809.03554) and [2](https://arxiv.org/abs/2005.08298) by Giamou, Ma, Peretroukhin, Kelly. RAL 2019 and MFI 2020.

🧠 Interesting thought from Tim at the end:
> Field robotics is a bif of thankless endeavor. The hardest part is doing the experiments in a way that they don't come across as **anecdotal**. I want people to believe I was thorough enough in my experiments that the results and the conclusions that I drew from the experiments were definitive. This is hard. Have you designed a broad-enough set of experiments that you are gonnna get a comprehensive answer to the A-is-better-than-B kind of conclusion?

In T-RO there is a specific set of papers called "Field Reports" meant for people to submit papers based on stress-testing other people's algorithms not on presenting a new algorithm. The novelty come from the way you stress-tested the algorithm(s) and what were the limitations. "Data papers" in IJRR are another avenue for this kind of works. 

