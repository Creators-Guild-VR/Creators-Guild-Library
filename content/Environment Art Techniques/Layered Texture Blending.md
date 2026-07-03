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

### Break down of the usecase.

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

**Painting a unique texture for blending:**

In this example, I am going to create a texture for a cube, import it into unity, and show how I can use Orel's shader with the layered blend.

Here's the cube:
![[Painted Texture.png|697]]

In this case I just created a new black texture in blender, and used the paint mode to paint on the layers. 

In this case, it's important that I when painting each layer on set the colour to either 100% R, G or B.

![[Colour Selector.png]]

After this, I simply exported the texture and file into unity. 

Here's I'm using the cube we just made, with orel's layered shader:

![[Orel's Layered Breakdown.png]]

In this case, we're going to use a layer count of 3 (because we didn't paint anything in for a 4th channel)

The important things to pay attention to when using orel's shader are:

1. Layer count - bear in mind, this is counting from 0 not 1, because the absence of any layer will apply the "base layer".
2. Mask type - normally vertex colours, in this case we want to use texture
3. Mask texture - in this area we input our mask texture we created for this specific mesh
4. Texture input - the input of a specific texture for that texture layer
5. Mask channel - you can choose per layer which part of the texture that layer should sample, in our case it's red green and blue 
6. Tiling - this controls the tiling for the layer


**NH's note:**

This is the first page I wrote for the guild wiki, and it was more difficult than I thought to wrap this entire concept up into a page. Mostly because of the large amount of pre-requisite knowledge.

Please write to me on discord about what further information would be of use and what's missing.
Hope it helped!