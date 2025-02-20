#linearalgebra #kinematics #robotics #vectors #geometry 

Geometry of motion, branch of classical mechanics used heavily in robotics in conjunction with its mathematical counterpart [[Linear Algebra]]. Kinematics describes the motion of a robot and their manipulators. Not to be confused with dynamics which describes interpretation of load balancing of external and internal loads acting on a stationary or mobile robot or its manipulator. 

# Object Location and Motion 

*For an object in the physical world, how do you describe its position and orientation? 
And when in motion how do you describe the change in its position and orientation?*

## Coordinate frames

^62a969

Consider *p* to be a vector in a n- dimensional Euclidean space $\mathbb{R}^n$ and $X = \{x1,x2,x3....xn\}$
be the [[orthonormal]] set of $\mathbb{R}^n$. In other words, $X$ is a set of axes in the n dimensional space.
The coordinates of vector *p* with respect to $X$ is denoted as $[p]^x$, which is defined as:  

$$
\huge p = \sum_{k=1}^n [p]_k^x x^k
$$

Note that because the space is [[orthonormal]] and not [[orthogonal]], unit axes are being multiplied by the vector and all the resulting vectors are being added to obtain it's coordinates. 


## Coordinate Transformations

^8f1290

*The coordinate transformation problem is to find the coordinate's of a point on an object with respect to the **fixed frame** when the coordinates of said point with respect to the **mobile frame**is known.*

Consider an object in a three dimensional space, with a fixed frame *f* and a mobile frame *m*.

![[Pasted image 20240626123304.png]]

When we rotate this object the coordinates of point *p* on the object with respect to the mobile frame *m* never changes, however these coordinates change with respect to the fixed frame *f* ,also notice that the mobile frame is attached to the object rotates with the object itself. 

The position of point *p* with respect to the mobile frame *m* : 
$$
p^m = \begin{Bmatrix} p.m1\\p.m2\\ p.m3\end{Bmatrix}
$$
*(the two frame of references are orthonormal)*
Similarly, the position of point p with respect the the fixed frame *f* :
$$
p^f = \begin{Bmatrix} p.f1\\p.f2\\ p.f3\end{Bmatrix}
$$

### Coordinate Transformation Matrix

^58a376

Consider a fixed coordinate frame $f = \{f1,f2,f3 ... f_n\}$ and a mobile frame $m = \{m1,m2,m3 ...m_n\}$ in a *n* dimensional space $\mathbb{R}^n$.

Then for each point *p* on an object in $\mathbb{R}^n$ :
$$
\huge [p]^f = A[p]^m
$$

The Matrix A is called the **Coordinate Transformation Matrix**.

Where matrix *A* is defined as $A_kj = f^k.m^j$ for 1 <= k ; j <= n
for example, in a 3D space the matrix A would be:

$$
A = \begin{bmatrix}   f1\\f2\\f3\end{bmatrix} . \begin{bmatrix}m1 & m2 & m3\end{bmatrix}
$$

$$\huge
\therefore A = \begin{bmatrix}   f_1.m_1& f_1.m_2 & f_1.m_3\\f_2.m_1 & f_2.m_2 & f_2.m_3\\f_3.m_1 & f_3.m_2 & f_3.m_3   \end{bmatrix}
$$

When the frame *f* and *m* are aligned, the the matrix is an Identity matrix :
*(assumed 3D space in the image below)*

![[Pasted image 20240626185225.png]]

### Inverse Coordinate Transformations

```
CONDITION : The origin must be same for the fixed frame f and mobile frame m
```

If the above condition is true, then $A^-1 = A^T$, and hence: 
$$
\huge [p]^m = A^T[p]^f
$$
### Rotations

^a191db

To specify the position and orientation of an object in terms of a fixed frame *f*, coordinate transformation involving both rotations and translations are required. 

When a body is rotated along with its mobile frame along a unit vector of the fixed frame, the resulting [[#Coordinate Transformation Matrix]] is known as the **Fundamental Rotation Matrix**.

Consider a 3 dimensional space $\mathbb{R}^3$ where with the fixed frame  $f = \{f1,f2,f3\}$ and the mobile frame  $m = \{m1,m2,m3\}$ where the mobile frame is rotated along the $f1$ axis. 

  ![[Pasted image 20240626212349.png]]  
  
  The angle of rotation here is $\phi$. 
  the new axes of the mobile frame are $m1',m2',m3'$. 
  The fundamental rotation matrix along $f1$ will be : 
  
$$
\huge
R_1(\phi) = \begin{bmatrix}   f_1.m_1'& f_1.m_2' & f_1.m_3'\\f_2.m_1' & f_2.m_2' & f_2.m_3'\\f_3.m_1' & f_3.m_2' & f_3.m_3'   \end{bmatrix} = \begin{bmatrix} 
1 &0 &0\\
0 & cos(\phi) & -sin(\phi)\\
0 & sin(\phi) &cos(\phi)
\end{bmatrix} 
$$

Similarly,
the fundamental rotation matrices along the $f2$ and $f3$ axes respectively would be : 

$$
\huge
R_2(\phi) = \begin{bmatrix} 
cos(\phi) &0 &sin(\phi)\\
0 & 1 & 0\\
-sin(\phi) &0  &cos(\phi)
\end{bmatrix} 
$$
$$\huge
R_3(\phi) = \begin{bmatrix} 
cos(\phi) &-sin(\phi) &0\\
sin(\phi) & cos(\phi) & 0\\
0 & 0 & 1
\end{bmatrix} 
  $$
#### Composite Rotations

^1dbc85

Sequence of rotation about the unit vectors. 
The algorithm to find the final rotation matrix is :

1. Initialize the rotation matrix R to an Identity matrix such that, R = I, 
   which corresponds to *f* & *m* being coincident. 
   
2. When *m* is rotated along $\phi$ about the Kth vector of ***f*** then perform **pre-multiplication** 
   where : $\large R_k(\phi)\ -> [R_k(\phi). R ]$ 
   
3. When *m* is rotated by $\phi$ about its **own** Kth vector then perform **post-multiplication** 
   where: $\large R_k\ -> [R.R_k(\phi)]$ 
   
4. If more rotations remain, go back to step 2
   
5. The resulting matrix maps *m* to *f*

Example:

![[unnamed.jpg]]