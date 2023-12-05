# Ninkyo-Dantai-II

# Development Manual

_This document contains useful information for development of Ninkyo Dantai II. We explain why we do certain things, the way we do it._

## 3D Models - Game Object Sprite Masks

All object masks must be marked in text and they must be a multiple of 2. 64x64, 128x128, 256x256 ... etc

## **3D Models - Exporting from Sketchup 2021**

When exporting 3D models ensure you select and tick all the 'OBJ export options'.

![image](https://github.com/TeamCS1/Ninkyo-Dantai-II/assets/84191027/6c5096fe-5819-42a0-9cf5-61e0259afd06)

## **Order of 3D Batch Drawings**
The order of the 3D draw transformation events also matters:

```
d3d_transform_set_identity();
d3d_transform_add_rotation_x(0);
d3d_transform_add_rotation_y(0);
d3d_transform_add_rotation_z(0);
d3d_transform_add_scaling(1,1,1);
d3d_transform_add_translation(x,y,0);
draw model...
d3d_transform_set_identity();
```

> [!NOTE]
> Highlights information that users should take into account, even when skimming.

## Rendering 3D Game Models

Waypoint coronas - All 3D Objects must use a depth of 0! When looking through corona's you can see the object. For whatever reason you don't want to see an object through the corona, set it to negative. Below 0, not 0.
All 3D Solid textures must use the tick 3D model box in the Sprite Menu and must be a multiple of 2.

## World Game Object

Some Objects must only be used once, which are found inside the world spawn object. These are 'fired' for specific niche events only.

## **Debug - Keys**

You can now change floor texture using the mousewheel
Change render distance using + and -

## Google Sketchup stuff

Converting everything into polygons, removes all visual glitches with the objects. They also must be triangulated.
All Sketchup models must be centred to the middle and rotation must be at 0 degrees 

A plugin called _**Chris Fullmer Tools**_ is used for centering models. (*However, this is now built into the d3d tool yay!)

Green Left, Red Right. (Fixes object normals)

## UV Mapping
Everything must be UV mapped after using _**Ultimate Unwrap 3D Pro**_.

## Post UV Mapping Convert from .OBJ File to .D3D File

Always click snap to ground first.

Next click on normals, and select either flat or smooth depending on how you want the effect. In most cases I click on flat normals.

Click on Assets and load a texture file in .PNG format.

Click on materials and load the UV map that was created when you went through the texturing process.

Once you have finished UV Mapping, use the obj converter to convert models from .obj to .d3d format, which is found on my website.

## Game Engine Related
Engine Version - Updated to GM 1.4.9999





