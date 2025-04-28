# Robotics Worldwide Workshop 2025
[MIT Robotics](https://www.youtube.com/watch?v=0OdOvkm5Xi4)

Organied by Luca Carlone (MIT) and Amanda Prorok (University of Cambridge) (4 April 2025)

## Perception, mapping, and navigation

Different ways of representing in 3D:
- Pointclouds
- Meshes
- Occupancy
- *Distance fields* --> cube of distances to the surface
**Distance fields** can be useful since collision checks in 3D require only a single look-up (we can collision check compex shapes quickly) --> for +info check the work from Helen Oleynikova (ETHZ)

On the topic of reconstruction, interesting work 📑: *SiLVR - NeRF with Lidar and uncertainty*, by Maurice Fallon (Oxford University)

[Spiking neural networks](https://medium.com/@deanshorak/spiking-neural-networks-the-next-big-thing-in-ai-efe3310709b0): they seem to work well with the innate nature of event cameras (aka Neuromorphic Computing) --> for +info check the work from Tobias Fisher (QUT Centre for Robotics)

Really cool way of visually representing where errors are coming from (by Jiajun Wu (Stanford University))
![image](https://github.com/user-attachments/assets/60d7f574-7514-4ea9-b00b-9f9aceae217f)

## Collaborative and interactive robotics

Challenges:
- life-long autonomy
- team composiition changes (e.g., roles, members)
- changes in robots (e.g., failures, payload) --> can robots learn about the strengths and weaknesses of their teammates? (aka group introspection) --> for +info check the work from Hao Zhang (University of Massachusets Amherst)
- environment (e.g., dust, snow, obstacles, vegetation)

## Grasping, manipulation, and dexterity

Interesting thoughts by Nima Fazeli (University of Michigan)
- 20XX-2020: first principles vs learning methods. 
- 2021 - ???: learning is here to stay --> raw sensory feedback (tightly coupled) vs abstract features (loosely coupled) ?
- Raw pixels are a very poor representation for dexterous manipulation --> geometry, force, and contact should be the "languaage" used.

GelSight --> vision-based tactile sensor that use optical design to trasnfer contact geomtery into color patterns in the ouput image --> for +info check the works from Wenzhen Yuan (UIUC)

## 🧠 Panel thoughts

**Q: Are data-driven approaches making robots more robust and reliable? Is hybrid the key?**
- the future appears to be hybrid (safe, trust, guaranteed, ... what do these terms really mean?)
- data-driven methods appear to be more robust against SMALL changes in the environment (an object shows up, lighting changes, etc.)
- there might be 3rd way of thinking about hybrid where instead of purely hybrid we start to think about how data is actually structured in the first place
- data-driven methods seem to be reaching a point where some of their fundamental issues aren't solvable with just scaling
- the issue with traditional (planning-based or model-based) methods is that the assume a perfect representation of the enviroment, and that's never the case. Learning approaches are much more capable of dealign with corrupted or imperfect data.
- plannign has a big role in generating data in simulations for priviledge learning
- there is still so much more to do on the policy architecture to make the action representation better and more efficient

**Q: how do you foresee the interplay between innovation in SW and HW over the next decade?**
- is hardware holding back a lot of the software development? (e.g., how can we do large-scale data collection?) 


