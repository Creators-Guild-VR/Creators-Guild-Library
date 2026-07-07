(Page is Unfinished)
---


Layered texture blending is a method we can use to texture typically large environment objects. 

Some user cases of this technique include:
- Cars in Cyberpunk 2077
- Buildings in Arma Reforger

The fundamental of this method is that we're going to take several [[Texture Set]]s and blend them together based on another texture (called a mask in this case). This allows us to use Texture Sets without fully giving up on the ability to control our placement of textures via painting.

![[Wide Shot.jpg]]
his image shows a world I built with layered texturing. It was used for the landscape and runway materials.

One Unity material you can use to blend layers is Orel’s shader:
https://shaders.orels.sh/
It’s capable of using a single mask image to blend between 5 different materials, but you can find many other shaders that support this or even make your own.


---
### Break down

In this section we’ll blend together several [[Texture Set]]s according to the mask.

The mask is they key ingredient here. It allows us to have a smooth or textured edge between our different Texture Sets. Under a normal circumstance without a blend, you would only be able to assign a texture to the geometry. This would result in a hard edge.

Here’s an example image showing a smooth edge:
![[EdgeBlend.png|697]]

The blend between each surface (grass, concrete, sand, and asphalt) is handled by a texture mask.

### The Mask:

In this case, I’m using a mask to blend the different textures. The method I'll be showing seperates the mask into 4 color channels: red, green, blue, and transparency (alpha).

But we can actually get 5 channels out of a regular image because the absence of any data can also be considered a channel.

Here is the mask debug view of this area:

![[MaskDebugView.png]]

This is a raw view of how the texture blending looks in scene, in this case:
- Blue = sand
- Red = concrete
- Black = grass
- Green = asphalt

![[RunwayMap.png]]
This is the actual masking map that is used to blend the different textures. I’m getting creative with my UV unwrapping by lining up each area with the corresponding blend I want to achieve.

If you're familiar with the technique, I'm using it in the same way as I would use [[Trim Sheets]].

![[UV Unwrap Example.png]]

Otherwise, you can just paint a texture. You can do this by figuring out in advance where you want each area to be and then painting them on separate channels.

**Painting a unique texture for blending:**

For this example I will be creating a new texture for a cube, importing it into Unity, and then showing how I use this new texture mask with Orel’s shader.

In blender, I'm using this default cube:
![[Painted Texture.png|697]]

I created a new black texture in blender and used the texture painting mode to paint on the different layers where I want my materials to be.

In this case, it's important that I when painting each layer on set the colour to either 100% R, G or B.

![[Colour Selector.png]]

After I painted on my different colour channels, I exported the texture and mesh into unity, as well as several tiling textures to use for demonstration purposes. 

Here’s the cube I just made with Orel’s layered shader:

![[Orel's Layered Breakdown.png]]

In this case, I'm using a layer count of 3 (because I didn’t paint anything for a 4th channel).

The most important things to pay attention to when using Orel’s shader are:

1. Layer count - bear in mind, this is counting from 0 not 1, because the absence of any layer will apply the "base layer".
2. Mask type - normally vertex colours, in this case we want to use texture
3. Mask texture - in this area we input our mask texture we created for this specific mesh
4. Texture input - the input of a specific texture for that texture layer
5. Mask channel - you can choose per layer which part of the texture that layer should sample, in our case it's red green and blue 
6. Tiling - this controls the tiling for the layer

If you want different tiling for your layers compared to your, you can either use the triplanar version of the material, or use a 2nd UV channel for the mask.


**NH's note:**

This is the first page I wrote for the guild wiki, and it was more difficult than I thought to wrap this entire concept up into a page. Mostly because of the large amount of pre-requisite knowledge.

Please write to me on discord about what further information would be of use and what's missing.
Hope it helped!