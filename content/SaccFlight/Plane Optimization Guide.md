---
description: A bunch of objectives to strive for to improve performance and development time
---
# The goal
## 2 Meshes
- 1 for the transparent parts of the canopy (or the entire canopy, your choice)
- 1 for the opaque parts of the plane (airframe, whatever is not transparent)
	- No extra objects, everything that is not transparent should stay the same mesh

^ Technical "why"
Doing it this way you can set LOD1 or LOD2 for the canopy to remove it completely, cutting on something called overdraw (making the GPU shade the same pixels multiple times)

 Allows for setting LOD1 or LOD2 on the opaque mesh to include a fake non-transparent canopy
 
 You can sell the effect by using reflection effects to pretend like the light bouncing off the canopy at a distance makes it look opaque

## 1 Armature
- Works with the most GPU-efficient workflow of having 1 mesh for all the opaque sections of the plane
- Save up on redundant logic
	- You won't be disabling "just the left aileron" or "just the right landing gear", or having LODs or occlusion culling for each part of the plane, most probably you are going to want to apply the same logic to the whole plane, those Mesh Renderers are not needed
- Better workflow
	- Working with bones allows grouping several parts of the plane together, makes it easier to set up accurate pivot points and makes positioning more visible

### 2 Materials
- 1 for the transparent sections
- 1 for the opaque sections
	- Using a non-transparent-enabled shader allows the GPU to use early depth rejection (Early-Z), it looks into the depth buffer, figures out "every pixel behind this is not worth rendering" and skips it, otherwise it will render everything behind it regardless and then overwrite those pixels with opaque sections, as transparent layers don't write to the depth buffer, wasting performance

### Add an Armature to your mesh

- Leave the first bone as a way to move your whole plane, general good idea to leave it at the center of the plane
	- This is the root bone
	- Make sure every bone on the plane is parented to this one
		- Extrude bones from this one using E or press Shift + A to add a new bone on the 3D cursor's position, then shift-click the root bone and Ctrl + P > Keep Offset to parent it
- Add one bone to each control surface
	- Use vertex snapping to align the bone, the pivot point of the bone is at the base (the short and fat end, the pointy end is the end of the bone)
- Name any bones on one side with ".R" or ".L" suffix according to their side, you can later right click and Symmetrize to save time (blender will create a copy on the other side or update the already existing one)
- Doing this first allows you to merge objects more easily

## Merge all separate objects

- Add an Armature modifier to the main mesh
- For each object
	- Add a Vertex Group with the name of the bone you want to control it (if it's just part of the main body, name it after the root bone)
	- Go into Edit mode (press Tab)
	- Select all vertices on the object (press A)
	- Click on the Vertex Group, select assign and make sure Weight is set to 100%

- Landing gear parts, control surfaces, everything opaque needs to be merged to the main body of the plane, everything will be controlled with bones
- Keep in mind how much a user will see, ex you can probably strip away most parts of the landing gear, the user will not be seeing that, as long as it's a strut with wheels you're fine

>[!info] Jet engine nozzle control
>Jet engine nozzles can also be controlled using bones but you will have to place a bone at the center of the circle and give it weight over the outer edge of the nozzle, then scale the bone to control it
>
>For more granular and simpler in-Unity control use blendshapes (called shape keys in Blender), as they will show up in Unity as a nice slider to adjust instead
>
>The performance hit it has is minimal considering it's at most 2 nozzles per-plane

## Join Materials

- 1 material for opaques (airframe, landing gear)
- 1 material for transparents (canopy, landing lights possibly)