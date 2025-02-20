#RRTM
Lecture by Paul O' Dowd on 10-10-2024

# Emergence

Emergence is a concept which displays the ''emergence'' of collective behavior in a colony. Take a ant or termite colony for example an individual ant would not know the grand plan or structure of the anthill, but collectively through emergence very complex structures are built according to environmental factors such as density of oxygen, sunlight etc. 

![[Pasted image 20241027164126.png#center]]
## Flocking

![[firefox_w1IF44FghD.gif]]

Notice this flock of birds, they move as a collective mass without knowing the destination or a directive. How do we mimic this behavior in robotics?
We can get this intelligent behavior by following three rules - ![[Pasted image 20241027164626.png]]

Aggregation, Dispersal and alignment results in flocking. 
Aggregation is positive feedback, Dispersal is negative feedback and alignment is randomness. 
It is extremely difficult to work out the rules to go from collective behaviors back to individual behaviors.
This is where centralized control comes in. 

# Centralized Control

Centralized control is an alternative to flocking, drone shows usually use centralized control. 

Why not use a swarm? (CC is not a swarm)
- Swarms demonstrate stochastic behavior (randomness with a probability) 
- Swarms rely on their environment
- Difficult to prove they are safe
- Difficult to design and engineer, centralized is cheaper and easier

Why use swarms then: 

![[Pasted image 20241027165713.png#center]]

Centralized control depends on a single computer, might be susceptible to bottlenecks and has one point of failure. 

# Swarms vs Centralized Control

Robots in centralized control do not talk to each other exclusively and try to be autonomous. Multiple computers talk to a centralized computer that talks back to other robots. 
![[OyTzMZCMxu.png#center]]
Hybrid systems also exist they use swarms in tandem with centralized control.