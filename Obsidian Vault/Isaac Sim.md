#IsaacSim #robotics 

This document is a personal documentation of Nvidia's Isaac Sim, methods, shortcuts and techniques to optimize robotic simulation workflows.

# Basics 

Source: https://docs.isaacsim.omniverse.nvidia.com/latest/introduction/quickstart_index.html

Launch IS by running 
```bash
cd ~/isaacsim
./isaac-sim.selector.sh
```

A new scene can be created by clicking $file > new$ , you can add a ground plane by clicking $Create > Physics > Ground \ Plane$. A light source can be added by going to $Create > Lights > Distant \ Light$ . 

# Transformations and Translations

The gizmos for manipulating an object is on the left hand side toolbar.

![[Pasted image 20250217170759.png#center]]

1. Press “W” or click on the Move Gizmo to drag and move the object. You can move it in only one axis by clicking on the arrows and drag, in two axes by clicking on the colored squares and drag, or in all three axes by clicking on the dot in the center of the gizmo and drag.
    
2. Press “E” or click on the Rotate Gizmo to rotate the object.
    
3. Press “R” or click on the Scale Gizmo to scale the object. You can scale it in one dimension by clicking on the the arrows and drag, two dimensions by clicking on the colored squares and drag, or in all three dimensions by clicking on the circle in the center of the gizmo and drag.
    
4. Press “ESCAPE” to Deselect the object.

You can also make more precise modifications to the Cube through its **Property** panel by typing in the exact numbers in the corresponding boxes. Click on the blue square next to the boxes to reset the values to default.

![[Pasted image 20250217171026.png#center]]


# Physics and Collision 

Common Physics Properties are mass and inertia matrix — the properties that allow the object to fall under gravity. Collision Properties are the properties that allow the object to collide with other objects.

Physics and Collision properties can be added separately, so you can have an object that collides with other objects but does not fall under gravity, or falls under gravity but does not collide with other objects. But in many cases, they are added together.

1. To add physics and collision properties to the object, first find the object (“/World/object”) on the stage tree and highlight it.
    
2. Then go to the **Property** panel on the bottom right of the Workspace. In the **Property** panel, click on the **Add** button and select **Physics** on the dropdown menu. This will show a list of properties that can be added to the object.
    
3. Select **Rigid Body with Colliders Preset** to add both physics and collision meshes to the object.
    
4. Press the **Play** button to see the object fall under gravity and collide with the ground plane.

![[Pasted image 20250217172158.png#center]]






