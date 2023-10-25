Purpose: The purpose of this project is to use Houdini to convert an input mesh into lego bricks. 

Implementation:

The first step was to use a pointsfromvolume node to find the points contained inside the mesh. 

These points were then sorted into groups based on the type of block that would be placed there. 
This involved first extracting the points that were at the very top of the mesh, which would be used to place the flat and slant blocks. To determine which points would be used to place flat blocks, I found the distance between the normal vector and the up vector (0, 1, 0). When this distance was below a certain user-specified threshold, I placed a slant block and changed the normal to orient the block in the right direction. When the distance was above the threshold, I placed a flat block with the user-specified probability. 

To place the other blocks that were not at the top of the mesh, I looped through the remaining points to first place 2x2 blocks. In the loop, I added the point to a list of points to place 2x2 blocks at, and removed the point and the 3 surrounding points contained in the current 2x2 block from the overall list of points so that they would not be considered as positions to place more 2x2 blocks at. After placing 2x2 blocks at each position in the computed list of points, I placed 1x1 blocks at each of the remaining points. 

Before placing any bricks, I used the matchsize node to scale them to the right sizes. I also translated the 2x2 block so that the center would be under a unit part of the block instead of the center of the entire block. 


![dino_render](https://github.com/RachelDLin/hw03-legos/assets/43388455/9c3df807-3f1a-4fe3-b0fa-0943c1bc90ad)
