---
title: "My AI Time Machine (or my code for turning videos into video games)"
date: 2023-11-24
---

I clicked on the video link in my inbox, and there was our childhood home. 
It had been sold over a decade ago, and was subsequently hit by a tree during Hurricane Sandy.
My dad had been converting his old 8mm camcorder tapes into MP4 video, and this was one of the relics 
that had emerged from the time capsule.

As I watched the shaky video, I wanted to linger in the hallway, and the hidden corner where my sister 
and I would hide out as children just to pop out and startle each other on the way to our bedrooms (we 
were easily entertained).
Thankfully, there was a [paper that might allow me to construct such a time machine](https://repo-sam.inria.fr/fungraph/3d-gaussian-splatting/).

My time machine would be a virtual one. In step one, I would use the approach in the paper to train 3D models of scenes.
In step two, I would navigate the 3D scene via a video game rendering engine. In particular, the paper explains how to model the scene 
as a collection of 3-dimensional Gaussians; the final scene is rendered by projecting these Gaussians into a 2D view and then alpha compositing. 
It turns out that this rendering process is differentiable, so the same ML frameworks and hardware used to train AI models work here. 

And with that, I was off. After some pre-processing of the video and training the model, I was able to linger in the hallway.
<video src="https://github.com/krisheswaran/krisheswaran.github.io/assets/22381514/a04e7da0-040b-4a7a-9c2e-0e52d2d22e92" type="video/mp4" controls>
</video>

Pretty soon, I found my way back to my grad school studio apartment, and even flew through the bookshelf of our own home in San Francisco.
<video src="https://github.com/krisheswaran/krisheswaran.github.io/assets/22381514/b8a93487-255f-4e88-a5d2-70e493a50722" type="video/mp4" controls>
</video>

As a manager of managers, my day job no longer offers the opportunity to train models or write code. So I feel like I've gone 
back in time just by working on this project. But it sure does feel like the future.
