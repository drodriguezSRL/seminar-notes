# Adaptive Robot Localization with Physics Informed Neural Networks
[UMA-SRL Seminars](#)

by Mauro Martini from Politecnico di Torino (25 April 2025)

What I hope to learn:
1. what's the approach adapting to?
2. what is the physics-informed part modeling?
3. what's PIC4SeR doing in the space robotics domain?

## [PIC4SeR](https://pic4ser.polito.it/) 

Interdepartmental Center for Service Robotics at PoliTo

Key application areas:
- precision agriculture
- service robotics for wellbeing (collab with Uni Sevilla)
- cultural heritage
- smar city, search and rescue
- underwater
- **space** --> collabs with ESA and JPL; have their own "space analogue" facility.

## Approach 1: end-to-end data-driven pose estimation

**Goal**: optimize wheel and inertial odometry to learn to correct the pose error to better estimate wheel-inertial odometry poses. 

On one side, we capture data from IMU and encoder for odometry estimation. 
On the other side, we record images for visual-inertial estimation --> use this estimation for online training of the NN that then corrects the odometry of the wheel-inertial odometry.

❓ Online learning --> how much does it affect bandwidth and latency?

📑 Ref paper
- Navone et al (2023) [Online learning of wheel odometry correction for mobile robots with attention-based neural netowrks](https://ieeexplore.ieee.org/document/10260407) (CASE 2023)

main limitations:
- interpretability and generalization

So to increase these --> approach 2

## Approach 2: physics-informed neural networks

model robot kinematics and dynamics and add the known differential equations directly into the loss function (as a *regularization term*) when training the NN

++interpretability by limit or constrain the predictions possible through the NN
++generalization by exploit this model to train NN with an extra term

- task 1: learn the robot dynamic model (w.o. gravity forces (_planar problem_))
- task 2: learning releveant physics coefficients to update the model

input: kinematic state (vx vy wz), accelerations (ax, ay, az) and commands (fx, fy, fz)
output: predicted sate of the robot 

applications: prediction models such as KF, MPC 

it could also be used for online ("adaptive") training as in approach 1.

📑 preprint to come in the coming weeks...

## 🧠 Thoughts...

This approach will work well if the data is generated in a simulator with the same dynamic model as the one used to train the NN.

But what happens when we transfer this to the real world (much more complex dynamics)? --> challenge they are working on.

What they are doing is more uncertainty estimation or quantificaton than explaining the output of the model.

They are using derivatives to compute the loss function (potentially using a numerical derivation method) this might introduce a lot of high frequency noise (as derivatives often do)..frequency of computation will be critical (how much might this be affected by env conditions and adaptability?)

Sensor noise would be a challenge when moving outside. 







 

