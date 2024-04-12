# Ninkyo-Dantai-II

# About

This project has been marked as legacy, because the game development has been moved to Unity 3D due to a number of GameMaker Studio engine constraints.

The new project can be found here - https://github.com/TeamCS1/Ninkyo-Dantai-II-Tanpen

# Developement Constraints

- GameMaker Studio 3D is limited to 8 hardware lights. I also had a few bugs where some of them were not being switched off/on.
- GameMaker Studio 3D .d3d format is slow.
- GameMaker Studio 3D distance based LODs bugs (may be a me issue here).
- Hard to edit, despite my own built 3D Editor

# Development Manual

_This document contains useful information for development of Ninkyo Dantai II. We explain why we do certain things, the way we do it._

## 3D Models - Game Object Sprite Masks

All object masks must be marked in text and they must be a multiple of 2. 64x64, 128x128, 256x256 ... etc

## **Code Short Circuiting**

A neat trick is to utilize GML’s short-circuiting. Short-circuiting is how GML decides to stop reading your conditionals when a false value is reached. For example, given the following code:

```javascript
if (1 + 1 == 3) && (instance_place(x, y, obj_enemy))
{
  // stuff
}
```
Due to the fact that 1 + 1 is not 3, GameMaker won’t even bother reading the instance_place call. Since you are saying both statements must be true, there is no way that the conditional could return true if the first part is false. Use this to your advantage when ordering your conditionals. If you have checks that are more performance-heavy than others, put the lighter ones first! And additionally, keep in mind which conditionals are most likely to be false -- having five conditionals that will almost always be true, followed by one that will almost always be false, is a waste of time to process.

## **Profiling**

About profiling, yeah wasn't in GM 8 yet. They first implemented it in GM:S 1.3, but it still tells you the fps at least.

If you want to know how much time certain code needs exactly you can make a timer that measures time before and after the code has run, the difference is the time needed.
step event or draw event.

Step Event
```javascript
t = current_time;
// >

// test code here

// >
t = current_time - t;

```
Draw Event
```javascript
draw_text(20, 20, "time: " + string(t) + " ms");
```
current_time measures in milliseconds, if you want something precise use get_timer(), that one is in microseconds. If your game runs at 60 fps, you have 16.67 ms per step, if your game needs more than that, it slows down.

## **Sketchup Scaling Guide**

HEIGHT (ONE STORY) - 50M
WIDTH AND DEPTH - 100m

HEIGHT (TWO STORY) - 100M
WIDTH AND DEPTH - 100m

## **3D Models - Exporting from Sketchup 2021**

When exporting 3D models ensure you select and tick all the 'OBJ export options'.

![image](https://github.com/TeamCS1/Ninkyo-Dantai-II/assets/84191027/6c5096fe-5819-42a0-9cf5-61e0259afd06)

## Rendering Projection Specifics

NOTE: In GMS2, setting the projection differs from 1.4 – by default, it now does a conversion to right-handed coordinate space to stay consistent with 2D, but this inverts the up vector. 

To make the projection act like 1.4 and before and use left-handed space and make the up-vector act as expected. In GMS2 you must make the fov and ratio values negative.

![image](https://github.com/TeamCS1/Ninkyo-Dantai-II/assets/84191027/32a88392-4b5b-432f-ac5e-4aa2c72a3b18)

## **Order of 3D Batch Drawings**

> [!TIP]
> Read carefully...
> 
The order of the 3D draw transformation events also matters:

```javascript
d3d_transform_set_identity();
d3d_transform_add_rotation_x(0);
d3d_transform_add_rotation_y(0);
d3d_transform_add_rotation_z(0);
d3d_transform_add_scaling(1,1,1);
d3d_transform_add_translation(x,y,0);
draw model...
d3d_transform_set_identity();
```

## World Game Object

Some Objects must only be used once, which are found inside the world spawn object. These are 'fired' for specific niche events only.

## Rendering 3D Game Models

Waypoint coronas - All 3D Objects must use a depth of 0! When looking through corona's you can see the object. For whatever reason you don't want to see an object through the corona, set it to negative. Below 0, not 0.

All 3D Solid textures must use the tick 3D model box in the Sprite Menu and must be a multiple of 2.

## Greyboxing the World

A relatively new technique I am playing around with circa December 2023.

The approach to city-level design is making the city building blocks made from grey untextured models.

To start with you'll need an appropriate grey texture:

+ RGB(128, 128, 128): This represents a mid-grey colour. Each component is set to half of the maximum value (255), resulting in a neutral grey.

+ RGB(192, 192, 192): This is a lighter grey, with each component set to three-quarters of the maximum value.

+ RGB(64, 64, 64): This is a darker grey, with each component set to one-quarter of the maximum value.

## **Debug - Keys**

You can now change floor texture using the mouse wheel
Change render distance using + and -

## Google Sketchup stuff

Converting everything into polygons, removes all visual glitches with the objects. They also must be triangulated.
All Sketchup models must be centered to the middle and rotation must be at 0 degrees.

A plugin called _**Chris Fullmer Tools**_ is used for centering models. (*However, this is now built into the d3d tool yay!)

![image](https://github.com/TeamCS1/Ninkyo-Dantai-II/assets/84191027/f6208ca9-2922-4fbf-9a74-ee6a34c68afd)

> [!TIP]
> Read carefully...

It is still important to center models in the Sketchup step as it is good practice and is a method used to keep all models uniform and consistent across projects.

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





