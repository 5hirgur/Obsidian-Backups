#linearalgebra #kinematics #robotics #vectors #geometry 

To characterize the position and orientation of a point in on an object with respect to the fixed frame we need *pure* rotations and translations. 

While rotation can be represented in the form of a 3x3 rotation matrix, translation cannot. Hence, we need a higher dimensional space of homogenous coordinates. (4D space)

## Homogeneous Coordinates

Consider a point *p* in $\mathbb{R}^3$ where F is the orthonormal coordinate frame for $\mathbb{R}^3$. Here $\sigma$ is the non zero scaling factor.  

The homogeneous coordinates of *q* with respect to **F** denoted as $[q]^F$ are:


$$\huge
[q]^F = [\sigma q_1,\sigma q_2,\sigma q_3,\sigma]
$$ 
 The scaling factor is usually considered as 1 for convivence. 

## Homogeneous Transformation Matrix

^451ebb

The following matrix includes, rotation and translation applications, defined as: 

$$ \huge
T = \begin{bmatrix} R & P \\η^T &\sigma \end{bmatrix}
$$



Here, T is the homogeneous transformation matrix, where - 

R is the 3x3 rotation matrix
P is the 3x1 Translation vector
η is 1x3 the perspective vector, usually set to zero
$\sigma$ is the scaling factor, set to 1 

If scaling is to be included, the matrix would be : 
$$ \huge
T = \begin{bmatrix} SR & P \\η^T &\sigma \end{bmatrix}
$$ 
Where S would be a diagonal matrix representing scaling factors 
![[Pasted image 20240702131037.png]] 
But for further discussions we will assume that the space has no scaling and perspective changes and hence the last row of the transformation matrix will  be $[0 \\0 \\0 \\1]$  where the 0 0 0 is the perspective vector and 1 is the scaling factor, meaning there is no perspective distortion, and the transformation is affine.

For a robotic arm , P (Translation Vector) could represent the position of it's end effector and R (Rotation Matrix) it's orientation. Therefore, representation of a point *p* with respect to the fixed frame F is done in the same way defined in [[Basic Coordinate Transformations#^58a376 |Coordinate Transformation Matrix]] , but with the Homogeneous Transformation Matrix instead :

$$
\huge [p]^F = [T]\cdot[p]^m
$$

where $[p]^F$ and $[p]^m$ are represented as [[#Homogeneous Coordinates]].

Fundamental rotations and translations can be represented in terms of the Homogenous Transformation Matrix as fundamental rotation and fundamental translation matrices. 

Other types of important transformations are [[Screw Transformation]] and [[Screw Pitch]].

### Fundamental Homogeneous Rotation Matrix

^a493dd

To exclusively represent rotation in the form of [[#Homogeneous Transformation Matrix]] set the translation vector to 0. Hence the resulting matrix will be : 


$$\huge  Rot(\phi ,k) = \begin{bmatrix} R_k(\phi) &  &  & 0 \\  &  &  & 0 \\  &  &  & 0 \\ 0 & 0 & 0 & 1 \end{bmatrix} $$

Where $Rot(\phi,k)$ is the Kth fundamental homogenous rotation matrix (rotation about Kth axis by $\phi$ degrees).

![[Pasted image 20240702135811.png]]

### Fundamental Homogeneous Translation Matrix 

^2ce76b

To exclusively represent translation in the form of [[#Homogeneous Transformation Matrix]] set the rotation matrix to an Identity matrix $I$. Hence the resulting matrix will be : 

![[Pasted image 20240702135943.png]]

here P1, P2 and P3 are the part of the translation vector. 

Also represented by this function:  T(Kth axis of movement, number of units moved).


## Inverse Homogeneous Transformation Matrix

^4e3f33

For a homogenous transformation matrix, if the perspective vector η is 0 and the scaling factor $\sigma$ = 1, (meaning the last row is $[ 0 0 0 1]$) then it's inverse transformation is: 

$$
\huge
T^{-1} = \begin{bmatrix} R^T &  &  & -R^TP \\  &  &  &  \\  &  &  &  \\ 0 & 0 & 0 & 1 \end{bmatrix} $$


## Composite Homogeneous Transformations

Here, when multiple transformations such as rotations and translations are given for a mobile frame, we follow the same algorithm described in [[Basic Coordinate Transformations#^1dbc85 |Composite Rotations]]. 
Refer to the following example : 

![[Pasted image 20240702140227.png]]

Refer to [[Basic Coordinate Transformations#Rotations |Rotations]] to see how the rotation matrix was formed. 













