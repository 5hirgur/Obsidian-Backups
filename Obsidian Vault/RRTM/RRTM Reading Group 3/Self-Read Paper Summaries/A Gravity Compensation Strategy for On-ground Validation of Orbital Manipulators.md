#RRTM

Week 3 

https://ieeexplore.ieee.org/document/10161480

Orbital manipulators perform servicing tasks like assembly, maintenance, repair and orbital debris removal. These manipulators however, operate in zero gravity while being validated under the effect of gravity which is impractical because joint torque limits can be reached quite easily for certain configurations when gravity is actively compensated by the joints. This paper proposes a strategy to simulate gravity compensation for an orbital manipulator arm on the ground. 

The experimental results validate the effectiveness of the method on the DLR CAESAR space robot, which uses a cable suspended system as external carrier to track the desired gravity compensation force, resulting from the proposed method.

A direct compensation of gravitational force at the joint level on ground can negatively affect the workspace of the robotic arm. 

Several methods can be used to compensate for gravity to validate these robotic arms.
- Air Bearing 
- 0-G Parabolic Flights
- Neutral Buoyancy
- Hardware in The Loop Simulations 
- Cable Suspended Systems



AI EXPLANATION BELOW: 

Here a modeling framework for a generic manipulator-carrier system (Similar to cable suspended system setup includes dynamic [[Robotics and AI - Dexterous Robotics#^611304 |variable stiffness?]]) aimed at achieving gravity compensation for robotic arms like the CAESAR manipulator. They formulate an optimization problem to optimally distribute gravitational torques between the manipulator's internal joint torques and the external forces applied by a carrier system, ensuring that the control tasks are not disturbed. The dynamics of the system are captured through equations that incorporate the inertia and Coriolis matrices, gravitational torques, and the external wrench, leading to a solution that balances the gravitational load while respecting torque limits across various configurations. 

The method employs weighting matrices to optimize the control of joint torques and external wrenches, demonstrating flexibility by varying the application points of forces and the capabilities of external carriers. Results indicate that the proposed method effectively reduces gravitational torques to within allowable limits, achieving full gravity compensation and satisfying predefined constraints,