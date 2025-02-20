#mechanics #design #assembly #robotics 

# Mechanical Advantage
*Torque V/S Rotational Velocity*

In robotics we generally favor torque over speed, with the exception of servos and high torque motors (which have built in gearboxes) commercial available motors do not have a favorable speed to torque ratio.  

By using different diameters of gears together, we can exchange rotational/translational velocities with torque: 
$$
Old\ \ Torque \; \cdot Old\ \ Velocity = New \ \ Torque \; \cdot New\ \ Torque
$$
We get get the *old torque* and *old velocity* form a motors datasheet. 
We use [[Statistics and Dynamics]] to decide on a reasonable torque and speed for our robot assembly. 

# Gear Ratio

Larger gears move slower than smaller ones, however they have more torque. 
The gear ratio is the value at which we change the velocity and torque. 

If our gear ratio is $m/n$ then:

$$
New\ \ Torque = (m/n)*\ Old \ \ Torque
$$
$$
New\ \ Velocity = (n/m) *Old \ \ Velocity  
$$
Example:  ^f8eec7

![[Pasted image 20240731220649.png#center]]

If you wanted a simple gearing ratio of say 2 to 1, you would use two gears, one being twice as big as the other. It isn't really the size as much as the diameter ratio of the two gears. If the diameter of one gear is 3 times bigger than the other gear, you would get a 3/1 (or 1/3) gearing ratio. You can easily figure out the ratio by hand measuring the diameter of the gears you are using.

For a much more accurate way to calculate the gearing ratio, calculate the ratio of teeth on the gears. If one gear has 28 teeth and the other has 13, you would have a (28/13=2.15 or 13/28=.46) 2.15 or .46 gearing ratio.

# Gear Efficiency 

By using gears the machines unput to output efficiency is reduced. Due to friction, misalignment of pressure angles, lubrication, gear backlash, angular momentum etc. 

Different gear setups have different efficiencies, to get the *True Output* for a particular setup we multiply the *New Velocity* and the *New Torque* by the known efficiency percentage.

Continuing the above [[Gears#^f8eec7|example:]]

![[Pasted image 20240731221733.png#center]]
# Gear Chains

Since two consecutive gears rotate in opposite directions, for a odd number of consecutive gears the first and the last gears rotate in the same direction while an even number of gears are counter rotational. 

When multiple gears are organized in succession forming a chain, the gear ratio is calculated by ignoring all other gears in between the first and last gears. The gear ratio would be:

**(*diameter of the 1st gear*)/(*diameter of last gear*)** 
\
The total efficiency of the gear chain would be: ![[Pasted image 20240731222415.png#center]]

# Compound Gears

Compound gears are two gears on the same shaft, their velocities would be the same. 

![[Pasted image 20240731222549.png#center]]

To calculate the torque for this setup we leverage [[Statistics and Dynamics]].

```
radius_gear1 * torque_gear1 = radius_gear2 * torque_gear2

In this example, what minimum torque does the motor need to pull the weight up?

writing down the equations:  
torque_motor * radius_gear1 = torque_gear2 * radius_gear2  
torque_gear2 * radius_gear2 = torque_gear3 * radius_gear3  
torque_gear3 * radius_gear3 = weight * radius_gear3

simplifying, we get:  
torque_motor * radius_gear1 = weight * radius_gear3

so therefore the minimum required motor torque is  
torque_motor = weight * radius_gear3 / radius_gear1

Now what if you wanted the weight to lift at 2 feet/sec. What rotations per second and direction must the motor rotate at?

writing down the equations:  
rps_motor * radius_gear1 = rps_gear2 * radius_gear2  
rps_gear2 = rps_gear3  
rps_gear3 * 2*pi*radius_gear3 = velocity_weight  

simplifying, we get:  
rps_motor * radius_gear1 = rps_gear3 * radius_gear2  
or  
rps_motor * radius_gear1 = velocity_weight / (2*pi*radius_gear3) * radius_gear2

so therefore the required motor rps is  
rps_motor = 2 ft/sec * radius_gear2 / (2*pi*radius_gear3 * radius_gear1)
```

# Gear Pitch 

When selecting your gears, the three most important numbers you must know are **pitch**, **pitch diameter**, and **number of teeth**.

![[Pasted image 20240731223900.png#center]]
                                *Representation of pitch diameter*

Pitch = (number of teeth)/ (pitch diameter)

For example, a gear with 72 teeth and a 1.5" pitch diameter is 48 Pitch. Gears that mesh must both have the same pitch and pressure angle (usually 20 degrees).

# Common Gear Types 

| Name                      | Efficiency | Image                                                                                                                                                                                                                                                                                                                                                    |
| ------------------------- | ---------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Spur Gears                | 90%        | ![[Pasted image 20240731224220.png]]                                                                                                                                                                                                                                                                                                                     |
| Helical Gears             | 80%        | ![[Pasted image 20240731224304.png]]                                                                                                                                                                                                                                                                                                                     |
| Sproket Gears with Chains | 80%        | ![[Pasted image 20240731224602.png]]<br><br>Note: Two gears with a chain can be considered as three separate gears. Since there is an odd number, the rotation direction is the same. They operate basically like spur gears, but due to increased contact area there is increased friction (hence lower efficiency). Lubrication is highly recommended. |
| Bevel Gears               | 70%        | ![[Pasted image 20240731224641.png]]                                                                                                                                                                                                                                                                                                                     |
| Rack and Pinion           | 90%        | ![[Pasted image 20240731224703.png]]                                                                                                                                                                                                                                                                                                                     |
| Worm Gears                | 70%        | ![[Pasted image 20240731224725.png]]                                                                                                                                                                                                                                                                                                                     |
| Planetary Gears           | 80%        | ![[Pasted image 20240731224852.png]]                                                                                                                                                                                                                                                                                                                     |


