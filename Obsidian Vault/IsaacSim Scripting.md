#IsaacSim #linux #programming #robotics #python 

# Useful Imports
A list of useful imports that can be used for scripting with [[Isaac Sim]].

## omni.usd
^55cc07
[here](https://docs.omniverse.nvidia.com/kit/docs/omni.usd/1.12.11/Overview.html) is the official documentation for additional reference.

This is an API written in C++ sits on top of omniverse kit core, USD, and omniclient library. Application functionality includes: 
- Events/Listeners
- Selection handling
- Access to the Omniverse USD Audio subsystem
- Access to the Omniverse Client Library, and handling of Omniverse Assets/URIs
- USD Layer handling
- A USDContext which provides convenient access to the main USDStage and its layers, as well as various Hydra, Renderer and Viewport related services
- MDL support
- Python bindings to all of the above, using the Python-3 async API in most cases

## pxr 
^46cfe1
Usecase : `from pxr import Usd, UsdGeom, Gf`
Here, we import some classes from the `pxr` library:
- `Usd`: Provides functionality for working with the USD stage, which is the container for your scene.
- `UsdGeom`: Contains classes related to geometric transformations, like creating transforms or manipulating geometry. ^125fc3
- `Gf`: A library that provides mathematical types and operations, such as `Vec3d` for 3D vectors.

# Useful Functions 

## [[IsaacSim Scripting#^55cc07|omni.usd]]

### omni.usd.get_context().get_stage()

^4ad346

This retrieves the current stage, which is the container for all the objects in the USD scene. It's like the "world" where everything in the scene exists.

```python 
stage = omni.usd.get_context().get_stage() # Get the current stage`
```

## [[IsaacSim Scripting#^46cfe1|pxr]]

### Gf.Vec3d(x_position, y_position, z_position)

^39430f

Gf.Vec3d is an object which is a basic vector type for three doubles. [constructor initialisation](https://openusd.org/release/api/class_gf_vec3d.html#af09c5e33053cf2c0f6175ae82a2f5d74)

```python
# example usage, appends position vector to positions list, ideally should be done recursively 
positions = []
position = Gf.Vec3d(x_position, y_position, z_position)
positions.append(position)
```

### stage.DefinePrim(prim_path, "Xform")

^90ffb5

[This creates a new `Xform` (transform) prim at the specified path](https://openusd.org/release/api/class_usd_stage.html#a6151ae804f7145e451d9aafdde347730). The `Xform` prim is used to store transformation operations like translation, rotation, and scaling. A prim is essentially a building block in USD, and an `Xform` type represents a transform node in the scene (which can include translation, rotation, and scale).
```python 
prim = stage.DefinePrim(prim_path, "Xform")
#prim_path is the path of the usd asset to be loaded 
```

stage is populated using [[IsaacSim Scripting#^4ad346|get_stage()]]. The `prim` variable now needs references to be able to interact with the scene. 

```python  
asset_reference = prim.GetReferences().AddReference(asset_path)
```

**Reference in USD terminology means that instead of embedding the actual content of the asset (like the 3D geometry) directly into the scene, you're linking to the asset file. This allows multiple scenes or prims to share a common asset without duplicating the asset data.**

#### GetReferences()
`GetReferences()` is a method that retrieves a reference to the list of external assets (references) that are attached to this particular prim. In USD, you can attach external references to a prim, meaning that the prim will refer to other assets in the scene, such as 3D models, textures, or other objects.

Now, the `prim` does not have an external asset linked to it. In other words, the prim would exist in the scene, but it would not represent any geometry or 3D object (like a box). It would essentially be an empty transform node with no visual representation. There ins't any actual object associated with the `prim`. 

`AddReference` links the prim to a specific asset, without it, the prim would remain a blank `Xform` (transform) node with no mesh or geometry.
#### AddReference(asset_path) 
The purpose of `AddReference` is to attach a 3D model (asset) to a prim. Without this link, the prim exists, but it doesn't represent any 3D object. This is useful if you want to have the object appear in the scene. `AddReference(asset_path)` adds an external reference to this prim. It tells USD that this `prim` should reference an external asset located at `asset_path`. The `asset_path` is a string that points to a file, in this case, the asset file representing a 3D object like a box (e.g., "box_2.usda"). 

### Xform API 

The **`xform_api`** handles the transformation stack of the `prim` (the object). You can chain multiple transformations together, such as **translation, rotation, and scaling**.

The order of operations matters.

If we first rotate and then scale, the scale operation will apply to the rotated object. If we scale first and then rotate, the rotation will happen on the scaled object.****
#### UsdGeom.Xformable(prim)

Creates an **Xform API (Application Programming Interface)** for the `prim`. The prim is to be instantiated using [[IsaacSim Scripting#^90ffb5|stage.DefinePrim]]. [Here](https://openusd.org/release/api/class_usd_geom_xformable.html) is the C++ reference. 

In USD, a `prim` can have various attributes (e.g., geometry, material). The `Xformable` API is used for operations related to transforming the `prim`. In other words, it allows us to manipulate the position, rotation, and scale of the `prim`.

The `Xformable` class is specifically designed for handling **transformations** in 3D space. This class is part of the `UsdGeom` module (which stands for **USD Geometry**), meaning it’s focused on transforming the geometry in the scene.

By creating this API, we can access transformation operations (e.g., translation, rotation, scaling) for the `prim` that will affect the object linked to it

```python
xform_api = UsdGeom.Xformable(prim)
```

##### ClearXformOpOrder()
Clears any existing transformation operations that may be applied to the `prim` before applying new ones.
Dont forget to initialise the [[IsaacSim Scripting#^125fc3|xform api]].
```python
xform_api.ClearXformOpOrder()
```

When spawning or transforming objects in USD, there may be residual transformation operations from previous transformations that can conflict or override the intended new transformation. By clearing the existing operations, you ensure that only the intended new transformation operations are applied (like translation or scaling).

##### AddTranslateOp
Dont forget to initialise the [[IsaacSim Scripting#^125fc3|xform api]].
```python
xform_api.AddTranslateOp().Set(value=Gf.Vec3d(x,y,z))
```
`AddTranslateOp()` is a method provided by the `Xformable` class (which `xform_api` is an instance of). This method **adds a translation operation** to the transformation chain of the `prim`.

The `Set`method is used to actually **apply the translation** operation with the specified values and it expects values in [[IsaacSim Scripting#^39430f|Gf.Vec3d]]. 

##### AddRotateXYZOp
Applies Euler rotation on the object specified by the prim. 
```python
# Apply rotation (e.g., rotating by 45 degrees around the Y-axis)
rotation = [0, 45, 0]  # Rotation angles in degrees
xform_api.AddRotateXYZOp().Set(value=Gf.Vec3f(rotation[0], rotation[1], rotation[2]))
```
##### AddScaleOp 
Just like translation and rotation, scaling is applied through the `Xformable` API. You can scale an object uniformly (i.e., same scale on all axes) or non-uniformly (i.e., different scales along different axes).
```python 
# Apply scaling (e.g., scale by 2x on the X axis, 1x on the Y axis, and 3x on the Z axis)
scaling = [2.0, 1.0, 3.0]  # Scale factors for X, Y, Z axes
xform_api.AddScaleOp().Set(value=Gf.Vec3f(scaling[0], scaling[1], scaling[2]))
```




# Example Uses

## Spawning an object 
The following script spawns set of boxes on a pallet in IsaacSim, The boxes are tightly packed together. 

![[Pasted image 20250416145726.png#center]]

```python 
import omni.usd
from pxr import Usd, UsdGeom, Gf
import os
def spawn_multiple_objects(asset_name, parent_path="/World/PickAssets/Final_Row/Box_2_Assets/Pallet_Box_2"):
    stage = omni.usd.get_context().get_stage()  # Get the current stage
    # Dimensions of the boxes
    box_x = 36  # Box width (x direction)
    box_y = 20  # Box depth (y direction)
    box_z = 14	  # Box height (z direction)
    # Pallet dimensions (world coordinates)
    pallet_x_min = 325
    pallet_x_max = 480
    pallet_y_min = -83
    pallet_y_max = 90
    pallet_z_height = 22  # Height of the pallet
    # Layer count (3 layers of boxes)
    layers = 3
    # Calculate the number of boxes that fit along each axis
    num_boxes_x = (pallet_x_max - pallet_x_min) // box_x
    num_boxes_y = (pallet_y_max - pallet_y_min) // box_y
    # Create a list to store positions
    positions = []
    # Loop through the x, y, and z axes to calculate the positions
    for layer in range(layers):
        for x_idx in range(num_boxes_x):
            for y_idx in range(num_boxes_y):
                # Calculate the x and y positions based on the index and box dimensions
                x_position = pallet_x_min + (x_idx * box_x)  # Center the box in the x-direction
                y_position = pallet_y_min + (y_idx * box_y)  # Center the box in the y-direction
                # Calculate the z position for each layer
                z_position = pallet_z_height + (layer * box_z)  # Stack boxes with a height offset
                # Define the position in world coordinates
                position = Gf.Vec3d(x_position, y_position, z_position)
                positions.append(position)
    # Get the user's home directory dynamically
    user_home_dir = os.environ.get('HOME')  # This will get the home directory of the current user
    # Asset and scene directories relative to the user's home directory
    scene_directory = os.path.join(user_home_dir, "kinisi/kinisi_ros/ros/kinisi_isaac/assets/environments")
    asset_directory = os.path.join(user_home_dir, "kinisi/kinisi_ros/ros/kinisi_isaac/props/cybership")
    # Compute the relative path from the scene directory to the asset directory
    asset_path = os.path.relpath(os.path.join(asset_directory, asset_name), scene_directory)
    # Ensure the asset exists relative to the assets directory
    if not os.path.exists(os.path.join(scene_directory, asset_path)):
        print(f"Error: Asset file {os.path.join(scene_directory, asset_path)} does not exist.")
        return
    # Now spawn the boxes at the calculated positions
    for i, position in enumerate(positions):
        prim_path = f"{parent_path}/box_{i}"
        # Create a new Xform (transform) prim for the object at the specified prim path
        prim = stage.DefinePrim(prim_path, "Xform")
        # Load the asset (e.g., a box) into the scene using the relative asset path
        asset_reference = prim.GetReferences().AddReference(asset_path)
        # Create a transformation for the object to position it in the scene
        xform_api = UsdGeom.Xformable(prim)
        # Clear any existing transformations
        xform_api.ClearXformOpOrder()
        # Add a translation operation to the xform
        xform_api.AddTranslateOp().Set(value=Gf.Vec3d(position[0], position[1], position[2]))
        print(f"Spawning box at {position}")  # For debugging
# Example usage:
# Specify the asset name for the box and spawn boxes on the pallet
spawn_multiple_objects("box_2.usda")  # Adjust the asset name to match the relative path
```


