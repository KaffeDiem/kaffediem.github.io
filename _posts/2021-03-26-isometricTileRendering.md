---
layout: post
title: Rendering tile-based isometric maps in LÖVE2D
---

[![YouTube preview of a tile-based isometric map](/images/2021-isometric/youtube_preview.png)](https://www.youtube.com/watch?v=3yU7wD8ITaw)

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
well. We see the number 3 in the table representing the third image in the 
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

### Loading the tilesheet and extracting the quads 

One thing worth noticing is that you should not load the image or the quads
more than once, thus we make sure that all the loading is done in love.load()
such that it is stored in the RAM.

```lua
function love.load()
  -- Load image in love.load()
  tilesheet = love.grahpics.newImage('path_to_tilesheet')
  tiles = fromImageToQuads(tilesheet, 32, 32)
  -- Draw the map from top point 200, 100
  mapX, mapY = 200, 100 -- Used in love.draw()
  map = { -- The map to draw
    {1, 3, 1},
    {1, 3, 1},
    {1, 3, 1},
  }
end

-- Where tilesheet is an image and tilewidth is the width
-- and height of your textures (32x32 in this case)
function fromImageToQuads(tilesheet, tileWidth, tileHeight)
  local tiles = {} -- A table containing the quads to return
  local imageWidth = tilesheet:getWidth()
  local imageHeight = tilesheet:getHeight()
  -- Loop trough the image and extract the quads
  for j = 0, imageHeight - 1, self.tileHeight do
    for j = 0, imageWidth - 1, self.tileWidth do
      table.insert(
        tiles,
        love.graphics.newQuad(
          i, j, tileWidth, tileHeight, imageWidth, imageHeight
        )
      )
    end
  end
  -- Return the table of quads
  return tiles
end
```

Above function will create a table containing all the quads to draw later.
If we index the table `tilesheet[1]` then it will be the quad containing
the water tile and `tilesheet[3]` will contain the tree tile. 

### Rendering the map

Rendering the map is the tricky part of drawing isometric maps. We will be
converting a 2D table into an isometric view.

![An illustration of the isometric view][illustration1]

Above figure shows how the conversion is done. Notice that the first row is
rendered from the top middle towards the right. 

![Isometric tiles as images][illustration2]

Even though tiles are isometric the image is still just a square and its
x and y coordinates are drawn from the top left corner. When rendering we will
have to increase the x coordinate as well as the y coordinate.

![Isometric rendering as squares][illustration3]

Above figure shows how we continually increases the x and y coordinates.
x is increased by half a tile and y is increased by a quarter of a tile.

When we also subtract half a tile from the x coordinate.

Putting all this increase and decrease together we have that:

```lua
function love.draw()
  for i = 1, #map do -- Loop trough rows
    for j = 1, #map[i] do -- Loop through cols in the rows
      if self.map[i][j] ~= 0 then -- If there is a tile to draw

        local x =
          mapX -- Starting point
          + (j * (tileWidth / 2)) -- The width on rows
          - (i * (tileWidth / 2)) -- The width on cols
        local y =
          mapY
          + (i * (tileHeight / 4)) -- The height on rows
          - (j * (tileHeight / 4)) -- The width on cols
        -- Draw the tiles
        love.graphics.draw(
          tilesheet, 
          tiles[map[i][j]],
          x, y,
        )
      end
    end
  end
end
```

And putting it all together we have now code the following code ready to run!

```lua
function love.load()
  -- Load image in love.load()
  tilesheet = love.grahpics.newImage('path_to_tilesheet')
  tiles = fromImageToQuads(tilesheet, 32, 32)
  -- Draw the map from top point 200, 100
  mapX, mapY = 200, 100 -- Used in love.draw()
  map = { -- The map to draw
    {1, 3, 1},
    {1, 3, 1},
    {1, 3, 1},
  }
end

-- Where tilesheet is an image and tilewidth is the width
-- and height of your textures (32x32 in this case)
function fromImageToQuads(tilesheet, tileWidth, tileHeight)
  local tiles = {} -- A table containing the quads to return
  local imageWidth = tilesheet:getWidth()
  local imageHeight = tilesheet:getHeight()
  -- Loop trough the image and extract the quads
  for j = 0, imageHeight - 1, self.tileHeight do
    for j = 0, imageWidth - 1, self.tileWidth do
      table.insert(
        tiles,
        love.graphics.newQuad(
          i, j, tileWidth, tileHeight, imageWidth, imageHeight
        )
      )
    end
  end
  -- Return the table of quads
  return tiles
end

function love.draw()
  for i = 1, #map do -- Loop trough rows
    for j = 1, #map[i] do -- Loop through cols in the rows
      if self.map[i][j] ~= 0 then -- If there is a tile to draw

        local x =
          mapX -- Starting point
          + (j * (tileWidth / 2)) -- The width on rows
          - (i * (tileWidth / 2)) -- The width on cols
        local y =
          mapY
          + (i * (tileHeight / 4)) -- The height on rows
          - (j * (tileHeight / 4)) -- The width on cols
        -- Draw the tiles
        love.graphics.draw(
          tilesheet, 
          tiles[map[i][j]],
          x, y,
        )
      end
    end
  end
end
```

[tileset]: /images/2021-isometric/tilesheet.png "Tileset"
[water]: /images/2021-isometric/water_with_bridge.png "Water bridge"
[illustration1]: /images/2021-isometric/illustration1.png "Isometric view"
[illustration2]: /images/2021-isometric/illustration2.png "Isometric view"
[illustration3]: /images/2021-isometric/illustration3.png "Isometric view"
