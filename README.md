# LEGO-ifying Meshes

## Project Overview

Procedural Houdini LEGO-ifier to convert any mesh into a model of LEGO pieces with a variety of shapes and sizes as well as accurate color. The LEGO pieces included are as follows:
- 2x2 brick
- 2x1 brick
- 1x1 brick
- sloped brick
- flat 1x1 brick
- flat 2x1 grill brick

The Houdini file includes controls for a user to customize brick size, frequency of "top" (flat) bricks being placed, and angular threshold for placing sloped bricks.

![image](https://github.com/wc41/hw03-legos/assets/97757188/e3061156-1070-4800-bacf-28d3011095a6)
![image](https://github.com/wc41/hw03-legos/assets/97757188/5d100270-9e4f-4eea-888f-28c57c3d3980)
![image](https://github.com/wc41/hw03-legos/assets/97757188/f1bf7503-ffce-4814-9c6a-4ea2c5148bff)

https://github.com/wc41/hw03-legos/assets/97757188/7e301bd2-b72f-4c0f-aa43-e60682f67eaa

## Process
- The group of points encompassing the mesh are determined as follows:
  - (1) VDBfrompolygons node -> ConvertVDB node to compute closed volume
  - (2) Pointsfromvolume node on bounding box of mesh
  - Create group of points by taking all points in (2) that are inside (1)
  - Blast all points outside of group
  - Attribute transfer Color and Normal point data from the mesh to the points
    - This requires using attribfrommap node and texture file to convert primitive material attribute to point Cd attribute
    - The normal data is corrected with VEX code (explained further)
- After getting the group of points, they are partitioned based on their location

![image](https://github.com/wc41/hw03-legos/assets/97757188/159a8d43-8d9f-4551-9ac2-30ec09a462d8)

  - Partitioning "angled" points involves a VEX function determining the difference between the transferred normal data and {0, 1, 0}.
    - ![image](https://github.com/wc41/hw03-legos/assets/97757188/0edd7b0c-c578-40a7-89d3-9f857b8226a0)
    - These angled points are then partitioned into 4 directions, based on their X and Z normal values
    - Their normals are adjusted so that the slope brick faces the correct direction
    - All un-angled points are corrected so their normals are {1, 0, 0}.
  - Partitioning "top" points involves a VEX function querying every point and whether a point was above it or below it
  - Prioritizing larger bricks over smaller bricks requires a for-loop
    - Iterates over each point, adds a single point for each desired block-shape bounding box that fits
    - For example: iterate over points, if point fits a 2x2 brick along with 3 others, it is added to the final group & the other 3 are removed
    - The desired brick is then copied to this group with copytopoints node
- Node parameters:
  - Brick Size is a parameter for particle separation from Pointsfromvolume node
    - Range: 0-0.3
  - Slope Threshold is a parameter for how far the normal separation from {0, 1, 0} has to be for the slope brick to appear
    - Range: 0-1
  - Top-Brick Percentage is a parameter for how many of the "top" bricks appear as opposed to an empty space
    - Range: 0-1



## Source Files
https://drive.google.com/file/d/1Coxo1xLHG-ALQGJ5SC2TZj1ZmM-i4lcl/view?usp=drive_link 
