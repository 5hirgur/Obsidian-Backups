#RRTM 
Lecture by Prof. Efi Psomopoulou on 23-09-2024

When it comes to developing robotic fingertips, control engineering problems have mathematics based solutions that result in smooth robot motion whereas, machine learning problems and challenges are solved by data driven solutions that ensure safe interaction of the robot with the environment. 

A prototype for stable grasping and in hand manipulation was developed at Kyushu University where the fingers demonstrated human like rolling motion of fingertips, it simplified this problem and generalised the solution well. However, the robot purely relies on joint angles and forward kinematics and has no [[Robotics and AI - Dexterous Robotics#^f9ff35|tactile sensing]].

Up until now the tactile sensors developed at the BRL [[Robotics and AI - Dexterous Robotics]] work by using computer vision and deep learning algorithms. These fingertips? developed by Efi at the lab get information about contact and force without data collection, cleaning and computer vision. 

# Controller Design 

The features of this controller are:
- Only proprioceptive and tactile
- No object knowledge
- Closed loop system stability proof
- Joint torque control

Refer to the equation below.

![[Pasted image 20240929213435.png#center]]
## Controller Limitations

The limitations of this controller are:

- Fingers need rolling capablity
- Equilibrium has to be within rolling distance
- Contact needs sufficient friction 
- Leverages joint torque control 

# Controller for Stable Pinching 

![[Pasted image 20240929213728.png#center]]

We get the angles $\phi$ and $\psi$ from the [[Pasted image 20240929213728.png|above equation]].

# Equilibrium Manifold

![[Pasted image 20240929214036.png#center]]

# Controller for Stable Pinching 

![[Pasted image 20240929214107.png#center]]






