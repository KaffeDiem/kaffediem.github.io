---
layout: post
title: Rendering tile-based isometric maps in LÖVE2D
---

There is not a whole lot of information out there on rendering tile-based
isometric maps in general, and even less so in LÖVE2D, thus I decided to write
a small article on the subject.

This guide assumes that the reader is known with the [LÖVE2D](https://love2d.org)
game engine as well as Lua. I will try to keep it as general as possible for
other frameworks and engines as well. 

First and foremost we must define the expected input and outout to measure some
critera for success.

### Defining the input

The input should be some table defining a map. Let us say that we have got
below tileset which is a spritesheet containing 4 images.

![Tileset as a spritesheet][1]

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
well.

```lua
waterAndWood = {
  {1, 3, 1},
  {1, 3, 1},
  {1, 3, 1},
}
```

The goal is then to generate below result from above input.

![Water with wood cutting trough][2]

### Loading the quads 

[1]: images/2021-isometric/tilesheet.png "Tileset"
[2]: images/2021-isometric/water_with_bridge.png "Water bridge"
