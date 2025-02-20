#robotics #kinematics #linearalgebra #vectors #math 

The inverse kinematics problem is to find the position and orientation of the robot's joints in order to reach an object in space. Generalized solutions do not exist, unique solutions are rare and multiple solutions exist for an inverse kinematics problem.

Given the desired position vector *p* and the orientation **R** for the end effector we find values for the joint variables *q* which satisfy the [[Forward Kinematics#Arm Equation|arm equation.]]  ![[Pasted image 20240810173741.png]]

We need to establish a forward kinematics relation in order to define an inverse kinematics solution. 

Recall the [[Forward Kinematics#Arm Matrix| arm matrix]] where the elements of the matrix are 12 equations and *n* unknowns. (n = 6 for a 6 axis robot since we deal with 6 total sets of [[Kinematic Parameters#^58dbb3|joint variables]]) The rotation matrix matrix *R(q)* has 9 equations and the position vector *P(q)* has 3.  ^418ed3

Here, the three equations for the position vector $p(q) = (p_x,p_y,p_z)$ are independent and the equations in the rotation matrix for [[Kinematic Parameters#Normal, Sliding & Approach Vectors|normal, sliding and approach vectors]] 9 in total are **not** independent.  

However, we can derive the following 3 independent equations from this specific relation: 

![[Pasted image 20240810174941.png#center]]
**$\therefore$ There are 6 independent equations for the resulting arm matrix.**

# Necessary Conditions

A manipulator is solvable for an inverse kinematics problem if all sets of [[Kinematic Parameters#^58dbb3|joint variables]] can be found corresponding to a given end effector location. The necessary conditions are: 

- The tool must be within the workspace
- $n\ge6$ (dof $\ge$ 6) to have any arbitrary orientation of the tool
- Tool orientations must not violate joint limitations. 

When the above conditions are satisfied, we have two types of solutions.
1. **Closed from solutions/ Analytical expressions**
   
   For an [[Inverse Kinematics]] problem to be solved with a close form solution, the **sufficiency condition** must be satisfied i.e - *Three adjacent joint axes must intersect OR be parallel to each other.* 
    ^d9d43b
2. **Numerical solutions/ Iterative search** 
   
   Time consuming method. 

# Uniqueness of Solutions: Multiple Solutions

There can be multiple solutions for an [[Inverse Kinematics]] problem, the nature of these duplicate solutions are as follows: 

- Kinematically redundant robots
  
  In the context of a 6DOF robotic arm: 
  When $n\geq6$ , we have to make assumptions for say - $\theta_7,\theta_8$ and for each such value we need to solve for $(\theta_1.....\theta_6)$ which are the values that actually define the position and orientation of the robot in 3D space. The robot thus has more DOF than are necessary for this task, making it kinematically redundant.

- Elbow up or elbow down configurations. 
![[Pasted image 20240825190141.png#center]]

# Closed Form Solutions

Refer above: [[#^d9d43b|closed form solutions]] 
There are two approaches to closed form solutions, the Geometric Approach and the Algebraic Approach. Here we only discuss the Algebraic Approach.

Algebraic Approach: 

1. Obtain at most [[#^418ed3|12 scalar equations]] from the homogenous transformation matrix.
2. Leverage trigonometric identities to combine two equations to eliminate certain variables. 
3. We can also use the following substitution to convert the trigonometric equations into polunomial equations: 
   
   $$\huge \mu = tan(\theta/2) $$$$\huge \therefore cos(\theta) = (1 - \mu^2)/(1 + \mu^2)$$$$ \huge sin(\theta) = 2\mu/(1+\mu^2)$$

4. Use  $\theta  = Atan2(sin(\theta_i),cos(\theta_i))$ function with $sin\theta$ and $cos\theta$ of joint angles. (Atan is not Arctan! Atan2 also specifies the quadrant )

   ![[Pasted image 20240825194503.png#center]] 

Examples:

Consider a 2 DOF robot as shown: 

![[Pasted image 20240825193243.png#center]]



Form it's [[Forward Kinematics]] solution, we get these relationships: 

$P_x = l_1cos(\theta_1)+l_2(\theta_1+\theta_2)$ and $P_y = l_1sin(\theta_1)+ l_2cos(\theta_1 + \theta_2)$ 

The inverse kinematics problem needs us to solve $\theta_1$ and $\theta_2$ for a specific position vector $P$
Now, adding the squares of the above two equations we get - 
![[Pasted image 20240825193840.png#center]]

*(Here, S is sin and C is cos)*
Instead of doing a cos inverse to get the value of $\theta_2$ we try to find out the value of $sin(\theta_2)$. 
We use $sin(\theta_2) = \pm\sqrt{1 - cos^2(\theta)}$ to obtain this value. We can now leverage the Atan2 function to get the value of $\theta_2$ , buy using this approach instead of using a cosine inverse we get the quadrant information of the angle and its value over $[-\pi, \pi]$. 

This is a simple example, but actual practical renditions are much more complex. 







