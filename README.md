# LEGO-ifying Meshes

## Overview
In this Houdini project, I've created a Houdini node that can convert input mesh to collection of LEGO pieces.

### PBR render result:
![](/real_render.jpg)
(Three-point lighting technique is used.)

### Physics Simulation:
![](/lego_sim.gif)

## LEGO-ify Procedure
First, based on pointsfromvolume node, the input mesh is divided into particles. And the color of each point is decided with attribfrommap and attribtransfer node.
Then, with a for-loop, particles are divided according to the block size, with intersection test. And then for the actual type of both 1x1 and 2x2 block are decided, according to if there is other blocks above, and their previous normal direction.

## Parameters

![](/parameters.png)
These parameters are exposed to outside of the node. Block size is the unit size of each block. Slope threhold is the threshold value of normal.y to decide whether a top 1x1 block is slop block. Top flat brick % decided how many of the top flat brick will show up. The brick vacancy decide the size of gap between each block, to make it looks more realistic. The texture path decided the texture used in the lego.

## Physics simulation

Physics simulation is based on DOP network. Inside the DOP network, the lego model is imported with RBD packed object, with previous pack nodes for each lego brick in lego-ify geometry node. Then a rigidbody solver node is added for it. Also, a static plane is added, with static solver. In the end, don't forget to add gravity.