#RRTM 
Lecture by Basaran Bahadir Kocer  on 30-09-2024

# Tethered Perching with Aerial Robots 
![[firefox_lipj1MPqDH.gif#center]]

Autonomous tensile perching, the drone moves back and forth to achieve sufficient momentum to wrap a tether around a structure. It can also perch on a structure, turn off its rotors in a way where it is able to collect information about the surface by climbing up and down the tether, as shown.

![[Pasted image 20241024173913.png#center]]


![[Pasted image 20241024173639.png]]
![[Pasted image 20241024173954.png]]

The above graph shows that wrapping a tether with momentum is inefficient hence there was a need to develop a design for a tether that has more efficient wrapping. See new implementation below: 

![[Pasted image 20241024174103.png]]

![[Pasted image 20241024174209.png]]

can perch with the drone or with the tether independently, this slightly increases the energy requirement however gives us the following perching modalities:

![[Pasted image 20241024174259.png]]

# Adding Vision Based Perception 

## Vision based crown loss estimation for individual trees with remote aerial robots:

![[Pasted image 20241025125729.png]]

Unity is used to generate synthetic images along with unity's "entry" plugin this is used to train a model called *real time crown loss estimation*. By using different thresholds two main characteristics are identifies - the density of the green in the tree and the density of the background. With this data another model called *two stage crown loss ranking* is trained, this model compares the densities of the trees in single frame, and estimates the absolute crown loss values using *real time crown loss estimation*. Because this data is being captured from afar we need to get closer to the trees, resulting in- 

## Leaf Disease Detection and Severity Estimation:

![[Pasted image 20241025130222.png]]

Detecting ash disease, this is how the generative model works: 

![[Pasted image 20241025130528.png]]

![[Pasted image 20241025130628.png]]

Notice the 400 iteration model (standard, left) vs the fine tuned generative model with 2600 iterations (right).