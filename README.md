# LEGO-ifying Meshes

### Used Late Day - 10/23 4:25 pm

## Project Overview
This is a Houdini project that can "LEGO-ify" 3D models! Using procedural modeling techniques and VEX, the project converts any faceted mesh into a collection of LEGO pieces.

## Process
### Converting the Mesh to Points
- The first step is to convert the mesh into a group of uniformly distributed points, where each point will eventually be converted to a LEGO brick.
- I create a bounding box surrounding the mesh and use a `pointsfromvolume` node to generate points in 3D space.
- In a separate node chain, I use a `vdbfrompolygons` and `convertvdb` node to compute the closed volume of the mesh, creating a point cloud.
- I combine the VDB volume and 3D points using a `groupcreate` node to find all points within the mesh's volume. Then, I remove all the points outside the mesh group using a `blast` node.
- Using an `attributetransfer` node, I get the color and surface normal information for each particle based on the original mesh.
    
### Converting the Points to LEGO Bricks
This project supports three overall categories of LEGO bricks:
| Block bricks        | Slope bricks         | Flat bricks|
| -----------         | -----------          |------              |
| ![](block_brick.png)| ![](slope_brick.png) | ![](flat_brick.png)|

- 
### Preventing LEGO Bricks from Intersecting



In order to correctly place each type, you will need to categorize your mesh points.
- Slope bricks should be placed at any particle whose transferred surface normal is sufficiently dissimilar to the vector <0, 1, 0>.
You will ultimately allow the user to specify the exact threshold of dissimiliarity, so you may set it to whatever value you wish for now.
- Flat bricks should only be placed on particles that do not have another particle above them.
You can use an Attribute Wrangle node to search the immediate area of each particle using VEX code.
For example, you could find the number of points above each point using `pcfind`: `int ptsAbove[] = pcfind(0, "P", location_to_search, search_radius, 1);`
If `location_to_search` is `@P` plus some vertical offset, you can effectively search only the area above each particle.
- Block bricks (e.g. 2x2, 2x1, and 1x1 bricks) can be placed anywhere else.

Consider assigning particles to different groups based on the criteria above, then placing bricks based on each particle's group.
For example, you could set a particle to be in a "top of mesh" group like so using VEX:
```
if (len(ptsAbove) == 0 && len(ptsBelow) == 1) {
    @group_top = 1;
}
```

## Preventing LEGO bricks from intersecting
Since we ask you to create your LEGO-ified model from bricks that are not simply 1x1 in size, you will need to make sure that
the bricks you place are not intersecting other bricks. To do so, you will need to perform a bounding box test for each brick:
- Using a pair of Block Begin and Block End nodes, iterate over every particle in your mesh volume
  - To examine each particle individually, you can compare its `@ptnum` to the iteration number (`detail(1, "iteration")`).
- For the particle you're examining, use a Copy to Points node to place a Box at its location,
where the Box's size is the size of the LEGO brick you're trying to place. Thsi will act as your potential brick's bounding box.
- Using a Group Create node with your bounding box and particle field as inputs,
assign the particles that fall within the bounding box to a group (its name is up to you).
  - This node should feed into a Wrangle Attribute node that uses VEX to remove all particles
(except the current loop iteration particle) that fall within the bounding box
from the particle field, effectively tagging them as "used up" in the placement of the brick
  - If the number of particles within your bounding box equal the number of particles it
would overlap if it were the first brick placed (e.g. 4 particles for a 2x2 block brick),
then the current particle is a valid location at which to place a brick.
  - If the number of particles within your bounding box is less than the number it would normally overlap,
then a brick __should not__ be placed there (i.e. the loop should just continue to the next particle)
- The two "if" statement branches in the above bullet points can be implemented using a Switch-If node,
 which can be followed by a Split node to create two "outputs" from this logic: particles in a group tagging them as
"places to put a brick on" and "places that did not have a brick placed at them".

## User Controls
The project allows users to interact with the geometry by exposing certain parameters:
- Brick Scale: adjust the scale of the bricks by altering the point separation parameter.
- Slope Threshold: change the threshold at which a particle is determined to be a sloped brick instead of a block brick.
- Top Brick Coverage: adjust the percentage of flat bricks covering the surface instead of exposed bricks.
