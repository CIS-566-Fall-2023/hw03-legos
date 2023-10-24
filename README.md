# LEGO-ifying Meshes

## Project Overview- Kisha Yan

![FinalRender](https://github.com/kishayan02/hw03-legos/assets/97934823/7da18e49-59fd-44da-851a-b56edf8ca3fb)

## Converting a mesh to points
To convert the mesh to points, I followed the tutorial in class and used bound, pointsfromvolume, vbdfrompolygons, and convertvbd nodes. Then, I grouped the points and blasted the points that I didn't want. Finally, I used an attribtransfer as well as an attribfrommap to obtain the colors of the toy.

## Converting the points to LEGO bricks
First, I separated the points from the previous step into 3 groups: top, slope, and brick.

For the **top** group, I found all the points with no points above them and 1 point below them and put these points in a group called surface. Then, I chose a point to be a top block with a probability controlled by the controller node. To prevent the blocks from intersecting, I created a loop that iterated through all these points and chose the ones with a bounding box of size 2 for the 2x1x1 flat block. The rest of the points were assigned a 1x1x1 flat block.

![Top](https://github.com/kishayan02/hw03-legos/assets/97934823/78dc7def-5b0e-406a-8b98-455d28abba34)
 
For the **slope** group, I use a formula to determine the angle between the normal of a point and <0, 1, 0>. If the angle difference is greater than a certain threshold (which correlates with an angle) controlled by the controller, and it is also in the surface group, it becomes a slope block.

![Slope](https://github.com/kishayan02/hw03-legos/assets/97934823/f994c1ca-d166-4758-8c2f-51fcf0d9560c)

Finally, for the **brick** group, I first placed 2x1x2 blocks using the same logic of iterating through all the points of a group, but with a bounding box of size 4. I did the same process with 2x1x1 blocks, and I filled the rest of the points as 1x1x1 bricks. Finally, I merged all groups together to create the final iamge.

![Bricks](https://github.com/kishayan02/hw03-legos/assets/97934823/e629fc48-0e1b-41dd-8fa7-83468be9466a)

## Exposing node parameters
There is a blue control node that controls the following

Block Scale (default: 0.05)
- The smaller the value, the smaller the point separation, and thus the smaller the Lego blocks
  
Slope Threshold (default: 0.6)
- Scale from 0 to 1
- The smaller the value, the more slope blocks there are, there is a lower threshold for the minimum angular difference
  
Top Percentage (default: 1)
- Scale from 0 to 1
- The smaller the value, the fewer top blocks are placed (randomly decided). This does not affect the number of slope blocks placed

## Rendering
A plastic-like material was applied, along with three lights and a camera to create this render.

Thanks :)


