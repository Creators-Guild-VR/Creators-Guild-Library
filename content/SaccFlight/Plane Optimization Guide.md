---
description: A bunch of objectives to strive for to improve performance and development time
---
^Lemon note: this guide does not yet consider Saccflight UI elements, it is possible that another material needs to be added per UI element like MFD, HMD and HUD, all the stuff mentioned here is strictly from the basic mesh requirements vs visuals and what affects computer performance. If somebody else expands it, please delete this note.
# The goal
## 2 Meshes, 2 Materials, 1 Material per Mesh
- 1 for the transparent parts of the canopy (or the entire canopy, your choice)
- 1 for the opaque parts of the plane (airframe, whatever is not transparent)
	- No extra objects, everything that is not transparent should stay the same mesh

### Technical FAQ

#### Why not more meshes?
Using more [[Mesh|meshes]] for control surfaces is unnecessary any logic will most probably only be applied to the whole plane (you won't be hiding just an aileron or such, you will hide the whole plane), this means the [[CPU]] will have more [[Mesh Renderer|mesh renderers]] to go through before passing them to the [[GPU]]

#### Why not 1 mesh?
TLDR: When making it 1 [[Mesh|mesh]] you will still need 2 [[Material|materials]], if you have 1 mesh you miss out on using [[LOD]] to remove the canopy as a whole

Here are the possible cases:
##### 1 whole transparent material
Using 1 transparent ([[Alpha Blending|alpha blended]]) material will for the whole plane, means the whole plane won't write to the [[Depth Buffer|depth buffer]], this means no [[Easy-Z]], so whenever you're looking down at the cockpit, everything behind it is also being rendered

This also means sometimes things will render on top of your plane when they shouldn't
##### 1 whole opaque material
You will have to have no canopy glass geometry at all (no reflections or refraction)
You could use a cutout shader to make the canopy transparent but it will be 100% transparent, pixels from it will not be rendered

##### 2 materials, 1 mesh
You can assign 2 different materials in the same mesh, you'd have saved up one mesh (not a big deal) but for the GPU changing materials is more expensive than changing meshes, so in the end you win nothing by this but now you can't use [[LOD]] to remove the canopy entirely when far away, this is still the second best option though, as the canopy from far away will be a few pixels at most


>[!warning] Performance destroyer:  TREES 🌳
>Avoid crowds of transparent foliage like trees or bushes with transparent shader planes for branches
>
>Depending on how many you put and how much they overlap on screen, this could turn into an [[Overdraw|overdraw]] nightmare
>
>If you want to use trees like that make sure they use a cutout shader instead ([[Alpha Clipping|alpha clipping]])
>
>You can still use [[LOD]] to increase definition if the player chooses to go near them (cutout shaders look like ass from up close) but in those cases you can just use an opaque [[Mesh|mesh]]

## 1 Armature
- Works with the most efficient workflow of having 1 mesh for all the opaque sections of the plane
- Better workflow
	- Working with bones allows grouping several parts of the plane together, makes it easier to set up accurate pivot points for them and makes positioning more visible

## 2 Materials
- 1 for the transparent sections
- 1 for the opaque sections


# The steps to reach the goal
## Add an Armature to your mesh

- Leave the first bone as a way to move your whole plane, general good idea to leave it at the center of the plane
	- This is the root bone
	- Make sure every bone on the plane is parented to this one
		- Extrude bones from this one using E or press Shift + A to add a new bone on the 3D cursor's position, then shift-click the root bone and Ctrl + P > Keep Offset to parent it
- Add one bone to each control surface
	- Use vertex snapping to align the bone, the pivot point of the bone is at the base (the short and fat end, the pointy end is the end of the bone)
- Name any bones on one side with ".R" or ".L" suffix according to their side, you can later right click and Symmetrize to save time (blender will create a copy on the other side or update the already existing one)
- Doing this first allows you to merge objects more easily

## Merge all separate objects

- Add an Armature modifier to the main mesh and to the canopy object (yes, they will use the same armature)
- Keep the canopy (or canopy glass) a separate object so that you can assign the transparent material on it
- For each object
	- Add a Vertex Group with the name of the bone you want to control it (if it's just part of the main body, name it after the root bone)
	- Go into Edit mode (press Tab)
	- Select all vertices on the object (press A)
	- Click on the Vertex Group, select assign and make sure Weight is set to 100%
	- Make sure to still assign a Vertex Group for the canopy

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