#robotics #kinematics #linearalgebra #vectors #math 

Differential relations define a relationship between a tools configuration and space velocity. 

The tip location in joint space is represented by joint angles as follows: 

$$ \large
\theta = \begin{bmatrix} \theta_1 \\\theta_2\\ \theta_3 \\.\\.\\\theta_n\end{bmatrix}
$$
The relation between joint angles with respect to their forward and inverse kinematic functions is as follows: 
![[Pasted image 20240825203204.png#center]]

Robot path planning is done in the tool-configuration space and the robot motion is controlled at joint space. 

# Differential Relationship 

Consider the following forward kinematics relationship: $x = w(q)$ 
(this is the same relation as x = FK($\theta$) described above)
where, 
x is the tool configuration vector
w is the tool configuration function
q is the set of [[Kinematic Parameters#^58dbb3|joint variables]]

Partial differentiation of the above equation yields $\huge \dot x = \frac{\partial w_k(q)}{\partial q_j}$  
Now we define a matrix known as the **Jacobian Matrix**, it is a 6x6 matrix that represents the relation between a joint's linear and angular velocities with respect to the rate of change of their joint variables. We define the Jacobian matrix as so:  ^86fce2

$$\huge
\dot x = J(q)\dot q
$$
where, $\huge J_{jk} = \frac{\partial w_k(q)}{\partial q_j}$ where $1 \le k\le 6$ and  $1 \le j\le n$

![[Pasted image 20240825212345.png#center]]
The above matrix displays the linear and angular velocities of the joints. $\dot x$ ,$\dot y$, $\dot z$ are the linear velocities of the joint in cartesian space and $\omega_x, \omega_y,\omega_z$ are angular velocities of the joint about their respective axes. J(q) is the Jacobian matrix.

k and j are the corresponding rows and columns and n is the [[Rudimentary Robotic Architectures and DoFs#Degrees of Freedom|DOF]]. 
For a rotary manipulator, [[Kinematic Parameters#^bd3d2f|where the only joint angle is the only defined parameter]], the Jacobian is defined as: 

$$\huge
\dot x = [J(\theta)] \dot \theta
$$
$$\huge
\therefore \dot \theta = [J(\theta)]^{-1}\dot x
$$

$\dot \theta$ is the top velocity in joint space and $\dot x$ is the tip velocity in cartesian space. 


![[3VFDD0WlN1.png#center]]

**Example:** 
Consider this planar robot:

![[Pasted image 20240915134109.png#center]]

# Singularities 

For the equation $\large \dot \theta = [J(\theta)]^{-1} \dot x$  the Jacobian might not be invertible for all values of $\theta$. At certain cartesian points in joint space the Jacobian loses it's rank, i.e there is a reduction in the number of independent rows and columns.  The points where the Jacobian loses rank are called *joint space singularities.* 

In the gif below, notice how the joints below re-orient themselves when the end effector or the tip of the robot tries to move in a straight line with a constant velocity, effectively slowing it down at the position where joint space singularities are triggered. 

Mathematically, in order for the end effector to move in a straight line as needed some of the joints need to have infinite velocity which is not physically possible. This can be a problem in operations like welding etc. There are many different types of singularities such as wrist singularities, shoulder singularities, elbow singularities etc. 

![[firefox_PVTXyeUCRG.gif]] 

This one DOF manipulator below is a perfect example of a velocity based singularity, where the tip tries to move with a constant velocity.


![[firefox_WMgyfede9T.gif]]

The first graph on the top is the plot of the output velocity, where as the one below is of the required joint velocity, notice how the required joint velocity reaches infinity when the output (or actual) velocity is zero, this is because there is no motor velocity in the world that can physically achieve this output. 

We can measure if a manipulator is close to singularity by calculating its *dexterity*.

$$\large dex(q) = det[J^TJ]$$
for n<= 6 the Jacobian is less than full rank if and only if the nxn matrix $\large J^TJ$ is singular, i.e the singularity occurs for robots with 6+ axes. The Jacobian is of full rank as long as *q* (the[[Kinematic Parameters#^58dbb3 | joint variables]]) is not a joint space singularity.  Redundant manipulators have n>6 hence, the determinant of the 6x6 matrix $\large J^TJ$ must be used. 

Joint space singularity occurs only when $dex(q) =0$ . High dexterity implies that the robot has greater range of motion, as the dexterity tends to zero for specific values of q (again, the joint variables), i.e specific positions in its workspace the robot becomes less movable, eventually hitting singularity at $dex =0$. Dexterity mapped to a workspace is called a dexterous workspace.    

There are some unique singularities such as boundary and interior singularities, discussed below.

# Boundary Singularities 

When $dex(q) = 0$, the arm is stretched out at the boundary of the workspace. 

![[Pasted image 20240915143139.png#center]]

# Interior Singularities 

Troublesome, formed when two or more axes form a straight line, the effects of rotation about one axis may be cancelled due to counteracting rotation about the other axes. Tool configuration will remain the same even when there is a change in joint space/variables. 

# Generalized Inverse 

For $\large \dot \theta = [J(\theta)]^{-1}\dot x$  inverse is not defined when the number of axes n is arbitrary - i.e the J matrix needs to be square. 

![[Pasted image 20240915144342.png#center]]
# Pseudo Inverse 

A pseudo inverse, also called the *Moore-Penrose inverse* satisfies all the stipulations for a generalized inverse mentioned above. Its is denoted as $A^+$. (When in terms of joint variables not joint space)

$A^+ = A^T(AA^T)^{-1}$  for m<=n
$A^+ = A^{-1}$  for m=n 
$A^+ = (A^TA)^{-1}A^T$   for m>=n

in the context of a mxn matrix.

# Resolved Motion Rate of Control 

For a mapped trajectory which does not go through any singularities, J(q) is the 6Xn tool configuration Jacobian matrix where n<=6. 

$$\large
\dot q = [J(q)^TJ(q)^{-1}J^T(q)\dot x] 
$$
$$
\large \therefore \dot q = J(q)^+\dot x
$$
$\dot q$ is joint specific unlike $\dot \theta$ which is a whole matrix for the tip velocity in joint space. 





