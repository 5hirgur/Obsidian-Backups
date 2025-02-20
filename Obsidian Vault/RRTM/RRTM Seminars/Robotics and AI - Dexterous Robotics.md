#RRTM 
Lecture on **19-09-2024** by Prof Nathan Lapora

Making humanoid hands are harder than building humanoid robots. Humanoid robots are excellent for social engagement with humans however, the end effectors - their hands need to be engineered to do actual human like work. In this lecture we also briefly touched base with [[AGI]] this was not a part of the presentation or agenda, however it is an interesting topic to keep in mind for my dissertation.

The image below is of a Homunculus.
![[80UqULWK4p.png#center]]
The Homunculus above is an image of a person where the face, lips and especially the hands are enlarged, to reflect on the relative size of the areas of the brain's motor and sensory cortex devoted to each of these body parts. Notice how the hands have the largest concentration.

To develop a mechanical sense of touch this lab as developed tactile sensors - these sensors are of very high resolution, the higher the resolution the more "sense of touch" can be expressed. 

# How do you make a robot hand behave like a humans?

Here professor Nathan draws parallel between the Shadow Hand manufactured by the Shadow Robot Company which was trained by Open AI and the SoftHand developed by QB Robotics. The Shadow Hand has 24 motors where as the SoftHand has just one motor, the manufacturing cost of the Shadow Hand is  $200,000 (apt considering there were 5,000 high caliber GPUs involved )where as the SoftHand was manufactured with a $10,000 budget. Both hands have incredible dexterity, the SoftHand demonstrates a level of dexterity almost similar to the Shadow Hand, from a pragmatic point of view the SoftHand is clearly, a better manufacturing alternative. 

![[firefox_fXb8CZImAV.gif#center]]

Professor Nathan's lab works towards development of effective tactile sensing dexterous robotic hands, the design of which is based on that of the SoftHand with the addition of another motor. Recall that the original SoftHand had only one motor but could perform complex dexterous tasks like wrapping its fingers around objects because of its adaptive design - inspired by the tendons of the human hand giving it properties of elasticity, the SoftHand has elastic bands on the back of the fingers which pull the hand back into an open position when the motor is switched off. This is an ineffective design -  this is where the additional motor in Professor's design comes in, this motor works against the first motor and works to wards opening the hand. 

![[Pasted image 20240928225347.png#center]]
<p align = "center">Robotic hand developed at the BRL</p>

![[fI7NuoFdio.png#center]]

This design adds another paradigm to the functioning of the robotic hand, my activating both motors at the same time the robot hand introduces a concept called *variable stiffness*. We use this concept all the time for example when we have to hold something very securely but not break it, or pull on one tendon at a time accurately.    ^611304


# How do you give the robot hand a human like sense of touch?

The Tactip.
Professor's Lab also develops tactile sensors that give these hands or any other robotic contraption a sense of touch. The design is inspired by that of the human skin where the dermal papillae act as mechanical amplifiers of contact. ^f8df95

![[Pasted image 20240928230846.png#center]]

The biometric tactile sensors developed at the lab as shown in the image above have little *leaver* like structures on them, these fingers also have a camera embedded in them which, in combination with the the leavers and computer vision give a sense of contact to the hand.   ^f9ff35

![[qi3E71LvVt.png#center]]

```
Insight - Question presented to the professor. 

These are very high resolution touch sensors, in order to use these with bionics/prosthetics the feedback needs to be sent back to biological neurons. These biological neurons are of low resolution, interfacing these are a challenge. 

There is research in this field - helping people with prosthetics regain their sense of touch, however, to reiterate interfacing electrical wires with actual neurons is a serious challenge. 
```

^ See [[Neurorobotics and Neuroprosthetics]].

![[Pasted image 20240928232118.png#center]]

The above image is a demonstration of how the sense of touch can be effectively used as a feedback mechanism to perform complex tasks, in this instance pouring liquid from a cup.

# Adding Intelligence 

OpenAI had trained the Shadow Hand purely using vision, this was not scalable, not practical and cumbersome. This is how the entire setup looked like:

![[Pasted image 20240929114214.png#center]]

Meta as recently as last year developed tactile sensors using [[Tactile Soft, Compliant Robotic Manipulators|GelSight]], these tactile sensors were trained using deep reinforcement learning algorithms and were able to achieve a high level of dexterity on their fingertips. 

![[Pasted image 20240929114515.png#center]]

This learning was done using simulation - sim to real approach. 

https://www.bristolroboticslab.com/dexterous-robotics

