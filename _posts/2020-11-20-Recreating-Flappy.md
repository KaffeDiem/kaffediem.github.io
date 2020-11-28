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
which may seem like an overkill, but I want to learn it. 

I want to do OOP, and a very simple way to do this in Lua, which does not
support it out of the box is with 
