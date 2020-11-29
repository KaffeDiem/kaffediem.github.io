---
layout: post
title: Recreating Flappy Bird in Löve2D
---

*Notice* that this blog post has not been finished

In this post, which will be updated as I make progress, I will try to walk trough the creation of a *Flappy Bird Clone* written in Lua with Löve2D.

### Physics

One of the things I wondered the most about was the physics of the jumping
bird. I remembered it to be quite simple and went for a quick Google search. As
it turns out, the bird is just constantly accelerating downwards, and some user
input makes it jump by a set amount. Take a look at the Stack Overflow answer
below. 

![Flappy Bird physics](/images/2020-FlappyBird/birdphys.png)

### Things to be solved

* How is the collision-box, which the bird may pass trough, going to be
  implemented?
* Are the obstacles generated in a constant time interval? That is to say, can
  two obstacles occur shortly after each other?
* How is the state system going to be implemented, and do I want to go trough
  the struggle of implementing a menu?


### Tools to be used

I am going to do the animations with [Anim8](https://github.com/kikito/anim8),
which may seem like an overkill, but I want to learn it. I want to do OOP, and a very simple way to do this in Lua, which does not support it out of the box is with [Classic](https://github.com/rxi/classic). This simply allows for an abstraction of objects to be created within Lua. I want to create an object for the player and objects for the obstacles that the player should avoid. The obstacle objects are therefore easy to delete afterwards, once they have done their duty. 

The last library which I will be using is [Windfield](https://github.com/SSYGEN/windfield). Windfield is a wrapper for Box2D, which is quite an advanced physics engine and most defiantly too much in this project, however I want to get used to it. 

### Getting started

So now to the actual coding. We import the modules and write the three main functions of any Löve2D project. 
```lua
wf = require "windfield"
anim8 = require "anim8"
object = require "classic"

function love.load()
    -- Set window size to the size of the desktop (or phone screen)
    sw, sh = love.window.getDesktopDimensions() 
    love.window.setMode(sw, sh, {resizable = false, fullscreen = false})
end

function love.update(dt)
end

function love.draw()
end
```
Then we will be creating two new *classes* with the Classic module. This is done before anything else, as we are just telling our program that these are going to be classes. This is done with 
```lua
Player = Object:extend()
Obstacle = Object:extend()
```
That is all for setting up the barebones structure. 

### Making a controllable player

Next up is implementing a basic player. I already drew an owl for this purpose. It is going to be animated, and there are 3 pictures in total, this is one of them.

![Owl](/images/2020-FlappyBird/owl_1.png)

It is simply a 32x32 picture that I drew in a few minutes. The goal is to have the three pictures in total run as an animation during one second, but we will be waiting with the animation till later.

The player is going to be initialised with `p = Player()` in the `love.load` function. To initialise a player it is also necessary to create some constructor for it. For now, this is going to be the constructor for my player. 
```lua
-- Initial loading of player
function Player:new()
   self.x = 0.1 * sw
   self.y = 0.4 * sh
   self.w = 0.05 * sw
   self.h = 0.1 * sh
   self.speed = 20
   self.jump = 20
   self.image = love.graphics.newImage("sprites/owl_1.png")
   self.box = world:newCircleCollider(self.x, self.y, 0.05*sw)
end
```
The first thing you may ask is; why do we use `0.1 * sw` for the positions? This is because we want to support all desktop dimensions. It means `10% into the screen from the left side` when `sw` is the screen width and `40%` down from the top of the screen on the y-axis. 