#RRTM 
Lecture by B.Ward Cherrier on 09-10-2024

*Merging robotic perception with biological systems.* 

# Why Prosthetics?

There are 2 million upper limb amputees worldwide, technology could help semi paralyzed patients regain some independence (250K - 500K people a year suffer from spinal chord injury).
# Touch 

^f26af0

```
Computer vision has been around for decades but research on touch is relatively new. 
Touch is a very important sense and an equally complex one at that, recall the Harlow's monkey experiments:

Harlow's monkeys were apparently hungry for something other than food: They were literally starving for a warm, comforting touch. With these studies, Harlow was the first to show that intimate body contact, and not feeding, was the most important factor in mother-child bonding.
```

The sense of touch is much more nuanced that what is initially thought of. There are four main mechanical types of sensing,:
- constant pressure
- dynamic changes in pressure
- vibration 
- skin stretching
![[Pasted image 20241026233727.png#center]]
# Spikes

^1397c3

Spikes is the format of the data that is used by the human nervous system, the data is formatted as spikes and transmitted from neuron to neuron. Everything happening in the brain is encoded in spikes. If the goal is to integrate non biological sensors with the brain for perception the must record or encode the data they collect in spikes. 
# Sensors: How is Touch Transduced by the Skin

## The NeuroTac 
The NeuroTac is a sensor similar to the [[Robotics and AI - Dexterous Robotics#^f8df95|TacTip]] but differs from it because its traditional camera is swapped out for an event based camera. This event based camera records information in events, not frames. This enables us to encode information in [[Neurorobotics and Neuroprosthetics#^1397c3|spikes]].  

![[Pasted image 20241027000524.png#center]]

The camera essentially only captures changes in the image, this is similar to how the brain and the retina work, the retina captures information about change in the images which is why human vision is very sensitive to movement. 

![[firefox_Ku3EeYeI2Q.gif#center]]

Poking the NeuroTac above, the camera uses computer vision to capture changes in images. 
# Perception: How Does the Brain Perceive Sensory Information 

When the NeuroTac goes over a surface it develops a raster plot, then spiking neural networks are leveraged.

![[Pasted image 20241027010509.png#center]]

Spiking neural networks are specialized neural networks where the activation function of each node of a neural network receives a number, say if you are moving forward in time every time steps receives a number. If that number is above a certain threshold value it sends another number to another neuron. There is propagation of information through the network. There is no backpropagation with spiking neural networks.

In the context of the NeuroTac the data sent through the network is either a 1 or nothing, if there is no new information detected nothing is broadcasted over the network and, instead of using activation function on neurons - abstraction of the [Hodgkin-Huxley neuron model](https://en.wikipedia.org/wiki/Hodgkin%E2%80%93Huxley_model) is used. 

```
Does this methodology give complete sense of mechanical touch and how? refer to the four types of mechanical touch neurons. Does each type requre a seperate Spiking neural network? or does the hodgkin huxley neuron model integrate all of it together? 
```

There are many avenues in the field of perception in this case, detecting texture, working with slip ,sensing braille, etc. 

## Organoid Intelligence 

Taking biology itself, FinalSpark's lab grown brains (organoids) are used for studying/exploring sensing and computation. The goal for a current BRL project is to read data from a tactile sensor, and simulate/compute the data in a real organoid.

![[Pasted image 20241027011901.png#center]]

The organoids learning capability has to be proven yet.
# Feedback to a Prosthetics User

Now that we have the tactile information we compute it on board the prosthetic, but we also need to give the user feedback. 
## Non Invasive Techniques

Vibration motors outside of the skin are used to give a sense of contact, these motors are higher up the arm and respond to touch of each finger separately. 
![[Pasted image 20241027115340.png#center]]

# Invasive Techniques

Microsimulation, recall the [[Neurorobotics and Neuroprosthetics#^f26af0| four different types of touch ]] ,these nerve endings are constituted by various afferents. A tactile sensor gathers data in spike form, pushes it down a neural network and that is transmitted through a specific afferent to the brain for the user to get a sense of touch. For this, a tiny needle is guided by ultrasound to target an individual afferent. 

![[Pasted image 20241027115637.png#center]]







