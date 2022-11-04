# lib_meyeni
This is a library for Blender with a few useful and random shader and geometry node groups, some focused on a 3d printing workflow.

![Nodes Example](https://github.com/Trainraider/lib_meyeni/blob/main/pictures/geo_nodes.png?raw=true)
## Geometry Nodes
### Displacement
![Displacement Node](https://github.com/Trainraider/lib_meyeni/blob/main/pictures/displacement.png?raw=true)    
This is a displacement node very similar to the one available as a shader node.
The displacement node is used to displace the surface along the surface normal, to add more detail to the geometry.
Both procedural textures and baked displacement maps can be used. The new X, Y, Z inputs can be used to remove displacement componenents in each axis.
Removing the Z component can be very useful for texturing 3d prints.

### Falloff
![Falloff Node](https://github.com/Trainraider/lib_meyeni/blob/main/pictures/falloff1.png?raw=true)
![Falloff Curves](https://github.com/Trainraider/lib_meyeni/blob/main/pictures/falloff.png?raw=true)    
The Falloff node is meant to be connected into the scale input of the displacement node.
It will gently lower the displacement scale to 0 as it approaches in proximity,
the edges of the mesh supplied to the "target" input of the falloff node. Generally you would supply
a simple mesh with few edges to the falloff node, and the same mesh but subdivided to the displacement node.
This node is usefull for applying textures to parts of 3d prints where the texture could otherwise create problematic geometry or interfere with pieces
fitting together properly if geometry past the edge is affected.

* Higher strength makes the falloff more sudden
* Factor controls the amount of falloff. At <1, the edges will still receive some amount of displacement.
* Smooth toggles between two falloff functions shown above, based on arctangent and cosine. With smooth on, the falloff is less abrubt at the edge.
Both have more appropriate uses.

### PCB Texture
It's just a procedural texture that looks kind of like Printed Circuit Board (PCB). It requires either a Position node or some other source of coordinates.

### Quad/Tri from Verticies
These two nodes make a face from verticies supplied as vectors. Flip normal can flip the face if needed.
The Quad will not exist if the 4 verticies are not coplanar.

## Shader Nodes
### Overhang Shader
![Overhang Shader](https://github.com/Trainraider/lib_meyeni/blob/main/pictures/overhang_shader.png?raw=true)    
This shader node colors a mesh depending on how printable the overhangs are. It's designed for FDM 3d printing.
The layer height and extrusion width inputs are used to calculate the maximum printable overhang angle.
This node can be used to find optimal 3d print positions to reduce supports, find optimal print settings, and it's
useful for designing custom supports for problem areas.

### Vase Overhang Shader
![Vase Overhang Shader](https://github.com/Trainraider/lib_meyeni/blob/main/pictures/vase_overhang_shader.png?raw=true)    
Same as the Overhang Shader, except it shades in a way appropriate for printing in vase mode,
meaning overhangs that would normally otherwise be fully supported by internal infill are also colored if they're too steep.
