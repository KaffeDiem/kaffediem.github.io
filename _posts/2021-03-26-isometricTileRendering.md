---
layout: post
title: Rendering tile-based isometric maps in LÖVE2D
---

[![YouTube preview of a tile-based isometric map](/images/2021-isometric/youtube_preview.png)]
(https://www.youtube.com/watch?v=3yU7wD8ITaw)

There is not a whole lot of information out there on rendering tile-based
isometric maps in general, and even less so in LÖVE2D, thus I decided to write
a small article on the subject. Also, above video should give you a good idea
of what I mean by tile-based and isometric. 

This guide assumes that the reader is known with the [LÖVE2D](https://love2d.org)
game engine as well as Lua. I will try to keep it as general as possible for
other frameworks and engines as well. 

First and foremost we must define the expected input and outout to measure some
critera for success. 

### Defining the input and expected output

The input should be some table defining a map. Let us say that we have got
below tileset which is a spritesheet containing 4 images.

![Tileset as a spritesheet][tileset]

In our code we will be loading this image once and then extract the 4 tiles,
which we will be rendering on the screen.

Next up is to define some way that the map should be layed out. Lets say that
we want a map only containing water in the dimensions `3x3`. The input should
then be a table containing the indexes of the tile which we want to draw. As
water is the first tile, the table is filled with ones. 

```lua
water = {
  {1, 1, 1},
  {1, 1, 1},
  {1, 1, 1},
}
```

Below example demonstrates three tiles of wood cutting trough the water as
well. We see the number 3 in the table representing the third images on the 
spritesheet.

```lua
waterAndWood = {
  {1, 3, 1},
  {1, 3, 1},
  {1, 3, 1},
}
```

Thus, our goal is to render below image from the above table as input.

![Water with wood cutting trough][water]

### Loading the image and extracting the quads 

```lua

tilesheet = love.grahpics.newImage('path_to_tilesheet')


```

[tileset]: /images/2021-isometric/tilesheet.png "Tileset"
[water]: /images/2021-isometric/water_with_bridge.png "Water bridge"
