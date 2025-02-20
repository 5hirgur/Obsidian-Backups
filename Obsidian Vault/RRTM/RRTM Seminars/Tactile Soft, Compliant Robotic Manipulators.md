#RRTM 
Video seminar available on 23-09-2024 by Sandra Q. Liu, MIT. 

*Why touch and compliance are important for robotics*

End effectors and robotic systems are designed for specific tasks, soft end effectors help generalize their use cases. Dr.Sandra's lab developed a unique GelSight based tactile sensor.

![[Pasted image 20240923174321.png#center]]

The surface of the GelSight surface has aluminum "cornflakes" on them.

![[Pasted image 20240923174518.png#center]]

There are flatter and globular pieces on the surface, the flatter pieces have a perfect reflectance parameter which gives us sharper details. The globular pieces have a scattered light parameter which gives us a smooth gradient. 

![[Pasted image 20240923174818.png#center]]

We want our soft robot hands to have tactile or touch sensing capabilities so that we can get a feedback from them. 



# GelFlex Finger

Camera based 2D proprioception, exoskeleton based finger and a neural network that leverages a camera to determine the size and profile of simple objects. 

![[Pasted image 20240929124014.png#center]]

A cable chain is used for manufacturing, made out of soft silicone , the gaps in the cable chain is where the camera resides and there is a string under the cable chain mechanism.


### Proprioception 

As the finger bends, angles relative to the assembly were calculated and images of the object were taken at different angles. This data is then fed to the neural network to get a sense of the size and shape of the object. 

![[Pasted image 20240929124352.png#center]]

As you see in the image labled "Predicted Finger" - this approach is very accurate. 

## Tactile Sensing 

A different neural network is used for tactile sensing, this network is trained to differentiate between boxes and objects of a cylindrical nature. The Gel Flex finger is now able to get a sense of the nature of the objects using only one camera. 

The limitation here is that the cable chain construction of the Gel Flex finger makes it difficult to grab smaller objects, there is no force tracking and depth perception. 

# GelSight FinRay

^51e463

This new contraption was developed being inspired by a novel FinRay gripper. It is a soft robot finger with rich touch sensing and proprioception, it has marker tracking which enables it to have force sensing.

![[Pasted image 20240929125254.png#center]]

A Fin Ray design does not have space for a camera, and does not allow LEDs to bend and flex. Hence, to create the GelSight Fin Ray a hollowed out structure was used.

![[Pasted image 20240929125553.png#cente r]]


To mitigate the issues with LED flexion the surface of the actuator has a acrylic piece under the silicone and the sides are painted with green and red paint, blue LEDs are used at the end littered across yellow florescent dots. 

![[Pasted image 20240929125822.png]]

The black dots are markers used for tracking shear forces. 

# GelSight EndoFlex

![[Pasted image 20240929130747.png]]

Integrating the technology designed above,  GelFlex finger and GelSight Fin Ray inspired. 

![[Pasted image 20240929130900.png]]

These fingers are able to safely interact with a human hand without hurting it and is able to simultaneously able to hold heavy objects.

One grasp of an object is able to detect the nature of the object. 

![[Pasted image 20240929131100.png#center]]


# GelPalm 

This is a tactile sensing palm, gives greater dexterity to the hand assembly because sensing is not limited to the fingers now. 

![[Pasted image 20240929131454.png#center]]

![[Pasted image 20240929131613.png#center]]



• Developed a low-cost, flexible lighting system to enable high-resolution tactile sensing for soft robots
• Design of a fully high-resolution tactile sensing hand
• Novel dual-compliant palm design
• Modular fingers and palms to explore future soft-rigid hands with tactile sensors