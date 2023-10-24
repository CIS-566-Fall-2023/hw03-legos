# LEGO-ifying Meshes
(using a late day) 

## Project Overview
In this assignment, I used procedural modeling in Houdini to convert any faceted mesh to a collection of LEGO pieces, including slope bricks, flat bricks, and block bricks (2x2, 2x1, 1x1).

I used one of Houdini's Test Geometry node to visualize my LEGO-ification. 

## Renders and Parameters 
<img width="800" alt="front4" src="/lego-renders/front-4.jpg">
<img width="800" alt="side4" src="/lego-renders/side-4.jpg">

### Examples of different parameter settings 
<img width="500" alt="param1" src="/lego-renders/param-1.jpg">
<img width="500" alt="front3" src="/lego-renders/front-3.jpg"> 
<img width="500" alt="side3" src="/lego-renders/side-3.jpg">

<img width="500" alt="param2" src="/lego-renders/param-2.png">
<img width="500" alt="front1" src="/lego-renders/front-1.jpg">
<img width="500" alt="side1" src="/lego-renders/side-1.jpg">

<img width="500" alt="param3" src="/lego-renders/param-3.png">
<img width="500" alt="front2" src="/lego-renders/front-2.jpg">
<img width="500" alt="side2" src="/lego-renders/side-2.jpg">

## Creating a custom LEGO-ifying node
- I converted my mesh into points and got the color and surface normal information of each particle using an Attribute Transfer node 
- I converted my points to LEGO bricks:
  - First I collected the "top" particles of my mesh using an Attriubte Wrangle VEX function that checked if a point had a particle above it (if no particles were above, then it was placed in the "top" point group)
  - From the "top" group, I checked for points to place slope bricks versus flat bricks
    - If a top group point had a surface normal that was different enough from <0, 1, 0> then it would be placed in the "slope" point group, else it was a normal "top" group point
      - Based on the normal's x/y/z values, I determined if a slope brick would be facing left/right/forward/backward
    - Slope bricks were placed at slope points, whereas Flat bricks were placed at non-slope group top points
  - Block bricks (2x2, 2x1, 1x1) were placed at every point not already filled with a slope or flat brick
    - I used a greedy approach, first populating 2x2 bricks, then 2x1, then lastly 1x1
    - I prevented bricks from intersecting by using bounding boxes and Block Begin/Block End nodes
      - If the number of particles within a bounding box equaled the number of particles that would overlap with a brick (e.g. 4 particles for a 2x2 block brick, 2 particles for 2x1), then a brick would be placed there
- I exposed node paramters to the node including:
  - adjusting the scale of the bricks using the 'bricksize' parameter
  - changing the threshold that particles would be determined to be a sloped brick using the 'slopethreshold' parameter
  - adjusting the percentage of "top" particles that use flat bricks versus no brick at all using the 'toppercentage' parameter

