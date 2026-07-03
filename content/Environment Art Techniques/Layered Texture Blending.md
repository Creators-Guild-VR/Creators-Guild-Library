(Page is Unfinished)

Layered texture blending is a method we can use to texture typically large environment objects. In my case, I use it to texture the runway and terrain. Some other user cases of this technique include:
- Cars in Cyberpunk 2077
- Buildings in Arma Reforger

The fundamental of this method is that we're going to take several texture sets, and blend them together based on another texture.

The method allows us to take several tiling textures and blend them smoothly together. 

![[Wide Shot.jpg]]
This image shows a world I build using this texturing method. It was used for the landscape and runway materials.

One unity material you can use to layer blend is orel's shader:
https://shaders.orels.sh/
It's capable of using a single mask image to blend between 5 different materials.

But this is a technique that you can use many different shaders with. Or even make your own.

### Fundamental Concept:
The goal with layered texture blender is to mix together multiple tiling textures, within a single material. It's regularly used by many AAA games in order to have buildings with a high detail level but also the ability for the artist to paint onto the mesh (as opposed to tiling a single texture).

The reason we want to do this, is because compared to just assigning different textures to mesh parts we can use a texture to blend the edges between materials. It also might offer a performance boost because it's 1 material instead of however many. 

Here's an example image:

![[EdgeBlend.png|697]]

In this image the blend between each surface is handled by a texture. The grass, concrete, sand, asphalt.

### The Mask:

In this case, I'm using an image to blend the textures. We can do this because the image has 4 channels of information that can be separated. The red, green, blue and transparency.

But we can actually get 5 channels out of it because the absence of any data can also be considered a channel.

This is the mask debug view of this area:

![[MaskDebugView.png]]

This is a raw view of how the blending texture looks, in this case:
- Blue = sand
- Red = concrete
- Black = grass
- Green = Asphalt

![[RunwayMap.png]]
This is the actual map that's used to blend the textures. I'm getting creative with my UV unwrapping by lining up each area with the corresponding blend I want to achieve.

If you're familiar with the technique, I'm using it in the same way as I would use [[Trim Sheets]].

Otherwise, you can just paint a texture however you see fit.


### Step by Step

