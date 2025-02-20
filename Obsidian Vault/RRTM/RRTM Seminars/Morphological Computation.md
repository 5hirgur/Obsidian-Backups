#RRTM 
Lecture by Helmut Hauser on 30-09-10

Morphology is a design principle which suggests that building intelligent smart robots its body needs to be taken under consideration and not just its "brains".

![[Pasted image 20241023175734.png]]

The goal of morphological robotics when it comes to interfacing between body and the environment is for improving interaction, for example this jellyfish robot made from FinRays developed by Valentina Lo Gatto  ([[Tactile Soft, Compliant Robotic Manipulators#^51e463|finray example]]) ![[firefox_IovIqFpCsj.gif]]

On the other hand we can develop sensors to reduce the complexity of the system before it gets to the brain structure/processor. This helps facilitating learning and control in the robotic system. For exapmle this sensing skin developed by Euan Judd :

![[Pasted image 20241023180553.png]]

This is a soft sensing skin which liquid channels filled with salt water, surrounded by electrodes measuring varying levels of impedance. When the skin is pressed down the impedance around that area changes, these measurements can be used with AI and ML to accurately determine where the contact has been made. Other sensing approaches is this spider web developed by Martin Garrad, spiderwebs are naturally occurring morphological structures, spiders sit on their webs sensing vibrations to detect danger or prey. 

![[Pasted image 20241023181027.png]]

This is a spiderweb based vibration sensor whose displacement(vibrations) are measured by a laser. 

![[Pasted image 20241023181318.png]]

The interfacing between the brain or controller and the morphological body has a lot of scope for introducing machine learning, ideally for this approach the first layer of a neural network must be morphological, this is optimal for developing spiking neural networks too and is fit for neuromorphic computation. 

An ideal morphological robot would have bodily adaption, where it is made out of some smart material which can learn from its experience by interacting with the environment. So far, this has only been largely simulated, however from simulations we observe that we can throw the genetic code developed for a morphological machine into different environments to get different experiences resulting in different morphologies. 

Consider this simulation: ![[firefox_gJXK1Rp9ef.gif]]

Here a tadpole is simulated, then given the morphological body of a forglet. It remembers its movement patterns and adapts a new policy which is later inherited by the morphological body of a  fully formed frog with the task of finding food (green sphere).

