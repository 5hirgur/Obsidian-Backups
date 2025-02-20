#robotics #kinematics #linearalgebra #geometry #vectors 

The forward kinematics gives us the joint variables and the link lengths (essentially the [[Kinematic Parameters]] also called the DH parameters interchangeability) with goal being to find the position of the end effector. 

# Arm Matrix 

The arm matrix is a [[Homogeneous Transformations#^451ebb|homogenous transformation matrix]] that maps the coordinates of frame *k* to *k-1* 

![[Pasted image 20240729185607.png#center]]


We take the following steps in order to align the *K-1th* frame to the *Kth* frame: 

1. Rotate the $k-1^{th}$ frame by $\theta$ about the $Z^{k-1}$ axis.
2. Translate the $k-1^{th}$ along  $Z^{k-1}$ by $d_K$.
3. Translate the $k-1^{th}$ along  $Z^{k-1}$ by $a_K$
4. Rotate the $k-1^{th}$ frame by $\alpha$ about the  $Z^{k-1}$ axis.

Since, all these transformations are with respect to its own mobile frame (K) and not it's base frame (K-1), we [[Basic Coordinate Transformations#^1dbc85 | post multiply]] based on the rules of composite rotations. 

Hence, the resulting [[Homogeneous Transformations#^451ebb|homogenous transformation matrix]], called the arm matrix is:

$$\huge
T_{k-1}^k(\theta_k,d_k,a_k,\alpha_k) = R(\theta_k,3)Tran(d_k,3)Tran(a_k,1)R(\alpha_k,1)
$$

Here k-1 is the source frame, and k is the destination frame
A generalized form:

$$\huge
T = R(\theta,z)Tran(d,z)Tran(a,x)R(\alpha,x)
$$
Since we know exactly what axes are being used for their appropriate transformations we [[Basic Coordinate Transformations#^1dbc85 | post multiply]] the [[Homogeneous Transformations#^a493dd|fundamental homogenous rotation matrix]] and [[Homogeneous Transformations#^2ce76b|fundamental homogenous translation matrix]] accordingly and compute the composite rotations with the solution resulting to be:

![[Pasted image 20240730003516.png#center]]

Here C is cosine and S is Sine. 
This is the [[Basic Coordinate Transformations#^58a376 |coordinate transformation matrix]] between two adjacent frames. 

It's inverse would be: 
![[Pasted image 20240730004759.png#center]]

This matrix is derived from the [[Homogeneous Transformations#^4e3f33|inverse homogenous transformation matrix]]. 
The arm matrix is also called the DH matrix. 

# The Forward Kinematics Problem 

Consider the following robotic arm arrangement: 

![[Pasted image 20240730133331.png#center]]

In a forward kinematics problem, our goal is to find the position of the end effector when the [[Kinematic Parameters#^58dbb3 |joint variables]] for each joint are are given.

Consider the set of all joint variables to be $q_1,q_2.q_3,.....q_n$ in the cartesian plane of the robot base/fixed frame. 
Therefore, we multiply successive [[#Arm Matrix|arm matrices]] to get the base frame ($L_o$) homogenous configuration as:

$$\large
T_o^n(q_1,q_2,q_3,....q_n) 
$$

$$\huge
\therefore T_o^n(q) = T_0^1(q_1)\cdot T_1^2(q_2) \cdot T_2^3(q_3) .... \cdot T_{n-1}^n(q)
$$

***q*** being the joint variables of the final joint. 
A generalized form: 

$$ \huge
T_{base}^{tool}(q) = T_{base}^1(q_1) \cdot T_1^2(q_2) \cdot T_2^3(q_3) .... \cdot T_{n-1}^{tool}(n) 
$$



Once we get this final [[Homogeneous Transformations#Homogeneous Transformation Matrix |homogenous transformation matrix]], or [[#Arm Matrix]] we can extract the coordinates of the position vector **P** with respect to the base frame.

# Arm Equation 

Once we have the resulting arm matrix as defined in the [[#The Forward Kinematics Problem]] above: 
![[Pasted image 20240730135515.png#center]]

We represent the position vector of the end effector as $P(q)$ and the tool orientation as $R(q)$.
$R(q)$ is represented as cartesian coordinates through [[Kinematic Parameters#^34fee2|normal, sliding and approach vectors]] 

$$
\huge
R(q) = \begin{bmatrix}N_x &S_x &A_x\\N_y&S_y&A_y\\N_z&S_z&A_z \end{bmatrix}
$$



