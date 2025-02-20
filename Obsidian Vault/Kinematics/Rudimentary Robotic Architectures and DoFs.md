#linearalgebra #kinematics #robotics #vectors #geometry 

# Degrees of Freedom 

The degree of freedom for a robot is the number of directions a robot can move it's set of joints and links. It is the minimum number of coordinates needed to represent the configuration of a robot. 

- An object that has all 6 degrees of freedom is called Holonomic.

- An object that has fewer controllable degrees of freedom than the total degrees of freedom is called Non-Holonomic.

- An object with more controllable degrees of freedom that the total degrees of freedom is called Redundant. 

A door hinge has only 1 DOF because it's configuration can be represented by only one value - $\theta$ , that is the angle of the door made by it's hinges. 

Similarly, a cartesian point has 2 DOFs - $(x,y)$ .

A *Planar* rigid body is a flat body in the x-y plane and has 3 DOFs  - $(x,y)$ and $\theta$  , i.e two dimensional parameters and one angular parameter. 
A *Spatial* rigid body has 6 DOFs  - $(x,y,z)$ and *roll, pitch and yaw*. 

For [[Robotic Arm]]s the end effectors positioning is represented in 3 DOFs in 3D space either obtained by rotation or displacement, represented in (x,y,z) and their orientation also is represented in 3 DOFs  represented using roll, pitch and yaw. 

![[Untitled 1.jpg]]


```
Degrees of Freedom = (sum of freedoms of the points) - (number of independent constraints)
```

Constraints in robot are defined by its [[#Joints and Links]] and 1 link is always assumed to be grounded. 

To calculate the DOF of a robot, use the following table of spatial and planar constraints in relation to common type of joints :

| Joint Type  | DOF (*f*) | Planar Constraints | Spatial Constraints |
| :---------: | :-------: | :----------------: | :-----------------: |
|  Revolote   |     1     |         2          |          5          |
|  Prismatic  |     1     |         2          |          5          |
|   Helical   |     1     |         X          |          5          |
| Cylindrical |     2     |         X          |          4          |
|  Universal  |     2     |         X          |          4          |
|  Spherical  |     3     |         X          |          3          |

![[Pasted image 20240707193232.png]]

Now that we know the degree of freedoms of each individual joint we can leverage the Grublers Formula to calculate the total degree of mobility of our robot (DoF and DoM are often used interchangeably but they are not the same, DoM is a more accurate description of this formula): 

$$\huge
Dom= m(N - 1-J) +\sum_{i =1} ^{J} f_i
$$
Where, 
***m*** is a constant - 6 for spatial and 3 for planar bodies
***N*** is the number of links 
***J*** is the number of joints
***$f_i$*** is the freedoms provided by joint *i*

```
NOTE:
for this formula to be valid the constraints provided by joints must be independent, and grublers formula provides a lower bound DOF for configuration space singularities arising in CLOSED CHAINS.
```

![[Untitled.jpg]]

# Joints and Links 

^fa62f3

Joints provide a robot with relative motion.
Links  are rigid members between joints. 

![[Pasted image 20240707191418.png]] ^cd76f2

A robot is usually divided into a *body and arm assembly* and a *wrist assembly*

![[Pasted image 20240707191559.png]]


# Robot Architectures

The combination and disposition of different kind of joints that make up a robot's kinematic chain. 

Common Body and Arm Configurations :

1. Polar Coordinate Body and Arm (RRP)

   ![[Pasted image 20240707194423.png]]

2. Cylindrical Body and Arm (RPP)
   
   ![[Pasted image 20240707194511.png]]
3. Cartesian Coordinate Body and Arm (PPP)

   ![[Pasted image 20240707194552.png]]

4. Jointed Arm Body and Arm (RRR)
   
   ![[Pasted image 20240707194639.png]]

5. Selective Compliance Assembly Robot Arm (SCARA) (RPP
   
   ![[Pasted image 20240707194747.png]]



