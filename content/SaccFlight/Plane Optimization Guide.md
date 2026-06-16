---
description: A bunch of objectives to strive for to improve performance and development time
---

## The mesh

The main aim here is to have 1 mesh per plane, no separate objects
This improves draw time and therefore performance

### Add an Armature to your mesh

- Leave the first bone as a way to move your whole plane, general good practice to leave it at the center of the plane
- A bone's pivot point

## Merge all separate objects

- Before merging something, if it needs to move make sure there's a Bone for it and that the Bone's Vertex Group has 100% weight on the entire object, then you can merge
- Landing gear parts, control surfaces, the canopy, everything needs to be merged to the main body of the plane, everything will be controlled with bones
- Keep in mind level of detail necessary, the user will not be looking at the landing gear when they're in the plane, odds are nobody will ever be close enough to see the landing gear go down, you can safely skip most details and nobody will ever notice, apply this logic to everything the user might not see, if it goes unseen 70% of the time, remove it or scale down the level of detail as much as you can

>[!info]
>Jet engine nozzles can also be controlled using bones but you will have to scale that bone
>
>For ease of use it's a better idea to use blendshapes for this (called shape keys in Blender), as they will show up in Unity as a nice slider to adjust instead
>
>The performance hit it has is minimal considering it's at most 2 nozzles per-plane

