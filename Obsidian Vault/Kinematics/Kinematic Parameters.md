#kinematics #robotics #geometry #vectors

Kinematic parameters of a robot describe the position and configuration of the robot, especially the tool-tip or the end effector, which outlines the [[Forward Kinematics]] problem. 

These parameters make up the **joint variables** and are mainly:  ^58dbb3

- [[#Joint Angle ]] $\theta$
- [[#Joint Distance]] *d*
- [[#Link Length]] *a*
- [[#Twist Angle]] $\alpha$

By [[Rudimentary Robotic Architectures and DoFs#^cd76f2|convention]] joints and links are numbered separately starting from the fixed base, numbered 0. The last link is the end effector. There are (n+1) links for an n axis robot.

# Joint Parameters

^486ed9

Joint parameters describe the relative position and orientation of two successive links. 

![[Pasted image 20240722141140.png]]

Joint K connects link K to link (K-1). The parameters associated with joint K are represented with $Z^{k-1}$ , aligned with the axis of joint K. 

## Joint Angle   

The Joint angle ($\theta$) is the rotation about $Z^{k-1}$ needed to make the axis $X_{K-1}$ parallel to $X^k$ (ignore the subscript/postscript discrepancy here, they are in accordance to the diagram )
## Joint Distance

The Joint distance ($d_k$) is the translation needed along $Z^{k-1}$ needed to make the axis $X_{K-1}$ intersect with axis $X^k$.


```
For each joint one of these two parameters must be constant, while the other variable. 
```

For example the joint angle $\theta$ for a prismatic joint would be zero and the joint distance (d) would be zero for a rotary joint.  ^bd3d2f

# Link Parameters

These parameters define the position and orientation of two successive joints. 

![[Pasted image 20240722143847.png]]

$Z^k$ and $Z^{K-1}$ are joint axes and link K connects joints K and K-1 together. $x^K$  is the common normal between the axes of joints K and K-1, all the parameters associated with link K are defined with respect to this axis)

## Link Length

The Link length $a_k$ is the translation along  $x^k$ needed to make axis $Z^{k-1}$ intersect $Z^k$ 

## Twist Angle

The twist angle $\alpha_k$ is the rotation about $x_k$ needed to make axes $Z^k$ and $Z^{k-1}$ parallel. 



![[Pasted image 20240722145211.png#center]]


# Normal, Sliding & Approach Vectors

^34fee2

The normal, sliding and approach vectors help us define the orientation of the end effector in terms of joint coordinates by using the YPR convention (Yaw, Pitch, Roll). Hence, the orientation of the end effector can also be represented as cartesian coordinates in the form of a [[Basic Coordinate Transformations#^a191db |rotation matrix]].

$$
\large
R = [r^1,r^2,r^3]
$$
![[Pasted image 20240722183427.png#center]] 

Notice that r1 is the normal, r2 is sliding and r3 is the approach vector.

Expanding on the rotation matrix: 

$$
\huge
R = \begin{bmatrix}N_x &S_x &A_x\\N_y&S_y&A_y\\N_z&S_z&A_z \end{bmatrix}
$$

yaw, pitch and roll are rotations about the normal, sliding and approach vectors. 
When the end effector is aligned with the base frame this matrix is an Identity matrix, because there is no change in orientation of the end effector with respect to the base frame, recall the [[Homogeneous Transformations#^2ce76b| Fundamental Homogenous Translation Matrix]]]






