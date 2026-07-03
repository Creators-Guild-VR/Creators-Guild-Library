(Page is Unfinished)

Layered texture blending is a method we can use to texture typically large environment objects. 

Some user cases of this technique include:
- Cars in Cyberpunk 2077
- Buildings in Arma Reforger

The fundamental of this method is that we're going to take several [[Texture Set]]s and blend them together based on another texture (called a mask in this case). This allows us to use texture sets, without fully giving up on the ability to control our placement of textures via painting.

![[Wide Shot.jpg]]
This image shows a world I build using this texturing method. It was used for the landscape and runway materials.

One unity material you can use to layer blend is orel's shader:
https://shaders.orels.sh/
It's capable of using a single mask image to blend between 5 different materials.

But this is a technique that you can use many different shaders with. Or even make your own.

### Fundamental Concept:

In this break down we're going to blend together several [[Texture Set]]s according to the mask.

The mask is they key ingredient here, it allows us to have a smooth, or textured edge between our different texture sets. Under a normal circumstance without a blend, you would only be able to assign a texture to the geometry. This would result in a hard edge.

Here's an example image showing the smooth edge:

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
- Green = asphalt

![[RunwayMap.png]]
This is the actual map that's used to blend the textures. I'm getting creative with my UV unwrapping by lining up each area with the corresponding blend I want to achieve.

If you're familiar with the technique, I'm using it in the same way as I would use [[Trim Sheets]].

![[UV Unwrap Example.png]]

Otherwise, you can just paint a texture, you would do this by figuring out in advance what you would want each area to be, and then painting them RBG.

