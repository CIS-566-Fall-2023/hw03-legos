Completed capybara:

<img width="860" alt="image" src="https://github.com/sherryli02/hw03-legos/assets/97941858/cfbb1153-0ccc-424f-af9f-8362abbeb9b3">


Unfortunately my renders are taking longer than anticipated, and I'll update with them as soon as they're done.

# LEGO-ifying Meshes

## Project Overview

This Houdini project enables the user to convert any faceted mesh to a collection of LEGO pieces.

## Converting the mesh to points

First, the input mesh was converted into a series of uniformly distributed points. I used a VDB From Polygons node followed by a Convert VDB node to compute the closed volume of the mesh. In another node chain, I computed the bounding box of the mesh and then used a Points from Volume node to generate points in 3D space. I then combined both chains with a Group Create node to find all points that fell within the mesh's volume, and removed them with a blast node.

## Converting the points to Lego bricks

Five different Lego brick types are supported: 2x2, 1x2, 1x1, slope, and flat. I used VEX and `pcfind` to isolate the points that had no point above them as well as a point below them, representing the topmost bricks which consist of either slope or flat bricks. I allowed the user to specify the threshold of dissimilarity to the vector <0, 1, 0> of the point's normal at which a slope brick should be placed by using an Attribute Transfer node from the original mesh, calculating the dot product between the original normal and <0, 1, 0>, and only placing a slope brick if the dot product is under the threshold. I used more VEX to find which cardinal direction the normal was closest to (+x, -x, +z, or -z), and rotating the block correspondingly.

On all other topmost points where slope bricks are not placed, either flat bricks or no bricks are placed; this ratio is controlled by the user.

Block bricks are placed on all the remaining points. I used a pair of Block Begin and Block End nodes to perform bounding box tests over every remaining point in order to ensure that no intersection occured. To examine each particle individually, I compared its `@ptnum` to the iteration number (`detail(1, "iteration")`). For the current point, I used a Copy to Points node to place a Box to act as a bounding box at its location, where the Box's size matched the size of the brick to place. I then used a Group Create node with your bounding box and particle field as inputs to assign the particles that fell within the bounding box to a group. I then used VEX to remove all particles
except the current loop iteration particle that fell within the bounding box from the particle field, effectively tagging them as "used up" in the placement of the brick. If and only if the number of particles within the bounding box equalled the number of particles it would overlap if it were the first brick placed (e.g. 4 particles for a 2x2 block brick), then the current particle was a valid location at which to place a brick, and I added the point to a group. I used Switch-If and Split nodes to create two "outputs" from this logic: point groups tagged as either "places to put a brick on" and "places that did not have a brick placed at them".

In order to have the bricks be placed from largest to smallest, I repeated the for loop process in order of 2x2, 2x1, 1x2, and 1x1 bricks.

## Exposing node parameters

The user can interact with the output through a singular controller node with certain parameters:

- The scale of the bricks that compose the model.
- The threshold at which a point is determined to be a sloped brick instead of a block brick.
- The percentage of "top" points that display as flat bricks versus placing no brick there at all.


## Extra Credit
Rigid body simulation.
