analog following, digital communication 
analog sensor values are calibrated and uncalibrated. 
digital sensors are calibrated too using discharge time. 
#robotics
# Abstract 

This study presents the design and implementation of a leader follower system for the Pololu 3Pi+ robots. The Pololu 3Pi + has seven IR sensors - two bump horizontal IR sensors and five vertical IR sensors for line following functionality. We only leverage the two bump horizontal bump IR sensors along with dynamic speed control and PID control. The leader robot emits infrared light, which is detected by the follower robot using a combination of forward-facing bump sensors. By integrating calibrated analog and digital sensor readings, the system achieves enhanced distance and angle tracking. Dynamic closed-loop PID control ensures real-time adjustments in the follower's speed and trajectory, enabling accurate alignment with the leader robot.

Key innovations include the hybrid sensor fusion technique - strategically combining the use of both digital and analog sensors readings. This balances the resolution and speed trade-offs of sensor readings, and an efficient communication protocol of operating at 100Hz with a minimal 10 microsecond delay. Experimental results demonstrate significant improvements in tracking performance, with reduced distance error, smoother motion, and better responsiveness compared to traditional threshold-based approaches. The system successfully demonstrates handing of straight trajectories with robustness and adaptability. 

This research contributes to advancements in autonomous robotics, with potential applications in swarm robotics, warehouse automation, and cooperative robotics systems. Future work will focus on optimizing sensor fusion, scaling to multi-robot scenarios, and improving communication protocols for even higher performance.

# Introduction 

In robotics, a leader-follower systems are critical for applications requiring coordination and collaboration between multiple autonomous agents. These are the building block of swarm robotics, search and rescue operations and industrial automation, where precise alignment and synchronization between robots is paramount. The primary challenge in designing such systems lies in ensuring accurate tracking of the leader robot by the follower robot, which must dynamically adjust its movement based on real-time data.

The 3Pi+ is equipped with RC type reflectance sensors, model QTR-1RC, which are typically used for line following tasks by detecting infrared light. These sensors are effective for basic line following and bump sensing tasks and hence, present significant limitations to be used in a leader follower system. Their functionality is limited when compared to TSOP IR sensors, which are designed for robust IR detection in dynamic and noisy environments. Adapting the QTR-RC sensors for leader-follower tasks presents unique challenges that require significant optimization.

These sensors are downward-facing, optimized for detecting surface reflectance rather than forward-facing IR emissions from a leader robot, without calibration, QTR-RC sensors can be sensitive to environmental interference, requiring robust calibration and processing. QTR-RC sensors excel in digital output, their data must be carefully processed to infer both distance and angular alignment.

This research leverages the advantages of QTR-RC sensors to design and implement a robust leader-follower system. The sensors' ability to provide fast, sensitive, and parallel data readings is utilized to dynamically track the leader's position. Calibrated discharge time readings are used to estimate the distance and orientation of the leader robot.

The proposed system showcases the potential of QTR-RC sensors for advanced robotics applications. Experimental evaluations demonstrate improved tracking performance, reduced alignment errors, and robust adaptability to the leader's motion, even under dynamic conditions.

Distance is directly proportional to discharge time, distance is also directional proportional to calibrated  analog values of the IR sensors. However, distance and transmitting frequency is inversely proportional. An increase in the robots angle also results in an increase in the calibrated angle value. This study aims to demonstrate solutions to implement a robust directional leader follower system by optimizing these constraints.

# Hypothesis 
This study hypothesizes that the performance of a directional leader follower system using QTR-RC sensors can be optimized by understanding and leveraging key relationships between sensor and physical parameters. 

- **Distance and Sensor Response:**
    
    - The discharge time of the QTR-RC sensors is directly proportional to the distance between the leader and follower robots.
    - Similarly, the calibrated analog values of the IR sensors decrease with increasing distance, indicating an inverse relationship.
      
- **Distance and Transmitting Frequency:**
    
    - The IR transmitting frequency is inversely proportional to the distance. Higher frequencies enhance the perceived IR intensity, improving the detection range and reducing noise.
      
- **Angle and Calibrated Values:**
    
    - The calibrated sensor values increase with the misalignment angle between the leader and follower. This directional relationship can be exploited to correct angular alignment dynamically.

This study aims to validate these relationships and optimize the system by calibrating sensor readings to balance sensitivity and environmental noise. Implementing a dynamic control system that integrates discharge time, calibrated analog values, and angular measurements to maintain optimal alignment and distance. Developing a robust leader-follower system that accounts for the inverse relationship between distance and transmitting frequency, ensuring consistent performance over varying conditions.

By addressing these constraints through sensor calibration, fusion, and adaptive control, this study seeks to demonstrate the feasibility of implementing an efficient and precise leader-follower system using cost-effective QTR-RC sensors.


# Methodology 

The methodology for this study involves a systemic approach to designing, implementing and testing this leader follower system using QTR-RC reflectance sensors. This process can be broken down into several phases - Sensor Calibration, Sensor Fusion and Data Processing, Control Algorithm Development and Experimental Evaluation. Each phase, focuses on addressing novel implementations and challenges posed by leveraging the OTR-RC sensors and optimizing their performance for directional tracking. 



## Sensor Calibration 

Calibration of the QTR-RC sensors is a crucial step. These sensors, are sensitive to various environmental factors such as ambient light and surface reflectivity. The follower robot will perform a $720 \degree$ rotation to perform calibration and scaling, the leader robot does not need to perform any such routine because it is the emitter.


![[Untitled Diagram.drawio.png#center]]


Here we observe that after calibrating and scaling the values the scaled IR values increase from 0.13 to 0.76 when we increase the distance. ![[Pasted image 20241130183228.png#center]]

The graph below shows the performance of the IR sensor before and after calibration as a function of distance, the distance here is raw distance measured in millimeters. 
The blue lines represent the sensor output without any calibration. This data, exhibits significant variability over a much larger range, caused by environmental factors, noise or non-linear sensor behavior. The red line represents sensor values post calibration. This graph is scaled by a factor of  30 for readability. Calibration reduces sensor variability resulting in more consistent and predictable values over a range of -1 to 1. The graph demonstrates the effectiveness of the calibration process in normalizing sensor data, essential for applications requiring accurate and consistent readings in real time. 

![[calibrated-vs-uncalibrated.jpg#center]]

We observe the same behavior, and flesh out this context by making a logarithmic plot of IR sensor values vs distance. The green line represents the sensor's scaled and calibrated values plotted against distance. The data shows fluctuations at shorter distances due to rapid sensor response in this range. As distance increases, the values become stable and follow a logarithmic trend. The logarithmic scale highlights the drop in sensor values as distance increases, common for sensors whose signal strength diminishes over distance.

![[log.png#center]]


## Sensor Fusion and Data Processing

Once the sensors are calibrated, the next step is to combine data from both the analog and digital modes to estimate both the distance and the angular alignment between the leader and follower robots.  Two IR sensors and the robot's two motor encoders work in tandem, as the sender emits an IR signal at a preset frequency of $100Hz$ and at a predefined speed of $0.4mm/ms$. The receiver robot compares this incoming data with a predefined threshold. when the incoming calibrated analog data is between $-0.02$  to $0.4$ the robot goes backwards, otherwise when the values are between $0.4$ to $0.88$ the robot moves forward. 


### Communication

The QTR-RC on the 3Pi+ has a small working reflectance area which results inability to receive distorted and wide spectrum IR signals. Because of the capacitor in the output line there is a discharge time between the high and low states of the IR transmitter.


![[Pasted image 20241130191028.png#center]]

Due to this discharge time, there is a delay between transmission and reception of data, which limits the setup to efficiently communicate using QTR-RC sensors. To mitigate this, we estimate a transmission frequency which allows us to effectively transmit data between two robots without being hindered by the capacitors discharge time. The graph below demonstrates this behavior against distance. 

![[WhatsApp Image 2024-11-30 at 17.20.39(1).jpeg#center]]

This graph has a generally increasing trend: as the distance increases, the discharge time also increases.
Now we establish a relation between calibrated analog values and the robot's angle. In the graph below we observe that as the angle of the receiving robot with respect to the emitting robot tends to go from $-60\degree$ to between $-20\degree$ and $0\degree$ the analog values tend to become zero.  An increase angle of the robot decreases the transmission efficiency. This calls for development of control measures as discussed in the following section. 

![[WhatsApp Image 2024-11-28 at 23.15.43(1).jpeg]]
## Control Algorithm Development 

To ensure that the follower robot maintains an appropriate distance and angular alignment with the leader, a **closed-loop PID control** algorithm is implemented. This algorithm continuously adjusts the motion of the follower based on the real-time sensor readings and the desired behavior (distance and angle).

### Dynamic Speed Control & Closed Loop Control (PID)
Calibrated analog values between -1 to are mapped to o to 0.5 to get the dynamic speed values. These values are passed to a PID function for control.  Leader robot travels at a constant speed, follower tries to maintain a constant distance with the leader. The speed is dynamically adjusted to maintain this distance. This is true for angle too, angle has a threshold and will adjust the follower robot to stay aligned with the leader. This setup allows the robot to travel forwards as well as backwards. The angular alignment between the leader and follower is determined by comparing the left and right sensor readings. A significant difference in sensor readings indicates that the follower is misaligned with the leader.



## Experimental Evaluation
The final phase involves extensive testing and evaluation of the leader-follower system under different conditions to assess its performance. Several experiments are conducted to test the system's robustness and accuracy in maintaining both distance and alignment with the leader. The evaluation includes:

**Straight-Line Following:**  
The leader robot follows a straight path while the follower attempts to maintain a fixed distance and angular alignment. The performance of the PID controller is evaluated by measuring the deviation in distance and angle over time.

**Variable Speed Following:**  
The leader robot changes its speed during the experiment, and the follower must adapt its motion accordingly. This tests the adaptability of the PID controller and the sensitivity of the sensors in responding to changes in the leader's behavior.

**Environmental Variations:**  
The tests are conducted under different lighting conditions and on different surface types to evaluate the robustness of the calibration and sensor fusion techniques. This ensures the system can perform reliably in real-world environments.



# Results and Conclusion 

# Future Potential 


