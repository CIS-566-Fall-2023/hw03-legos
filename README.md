# LEGO-ifying Meshes - Claire Lu
In order to lego-ify a mesh, we can take one of Houdini's Test Geometry nodes and implement a network that "blockifies" it - making it composed of a variety of lego blocks.

![dino-render](https://github.com/ClaireL21/hw03-legos/assets/102630261/e9dbabb6-c465-4191-a9d1-daad9648bf6e)

| ![dino-render3](https://github.com/ClaireL21/hw03-legos/assets/102630261/4056a4b2-0315-46d3-a39c-74412b39b9f1)| ![dino-render2](https://github.com/ClaireL21/hw03-legos/assets/102630261/f7a892b8-34d5-4197-8d42-18a9760c7eb5) |
| -----------         | -----------          |
| ![dino-render5](https://github.com/ClaireL21/hw03-legos/assets/102630261/d69769b1-0e64-44c0-8daa-b89088ea03ab) | ![dino-render4](https://github.com/ClaireL21/hw03-legos/assets/102630261/63cae8ba-c5f5-42ef-9740-6941f9aa73b9) |

## Convert Mesh to Points
The first step was to convert the given mesh to a volume of points. I did this by using a VDB node and a Convert VDB node to compute the volume of the mesh and then using a Points from Volume node to generate the points in 3D space from the mesh. Next, I set the scale of all the particles so that the particle separation (how far points are from each other) can be customized by the user. This impacts how "blocky" the end output is. Larger particle separation results in larger lego bricks and a "blockier" feel to the output.

Below are two outputs obtained from blockifying - the first one is a result of smaller particle separation between points and the second one uses a larger scale.
![dino-render5](https://github.com/ClaireL21/hw03-legos/assets/102630261/d69769b1-0e64-44c0-8daa-b89088ea03ab)
![dino-render4](https://github.com/ClaireL21/hw03-legos/assets/102630261/63cae8ba-c5f5-42ef-9740-6941f9aa73b9)

## Convert Points to LEGO bricks
The lego output uses a variety of bricks: Block bricks (2x2, 2x1, 1x1), slope bricks (1x1) and grill bricks (2x1).
| Block bricks        | Slope bricks         | Flat bricks|
| -----------         | -----------          |------              |
| ![](block_brick.png)| ![](slope_brick.png) | ![](flat_brick.png)|

The logic for categorizing points is done inside an `Attribute Wrangle` node. I essentially create three groups, one for sloped bricks, grill bricks, and block bricks, and assign each point to one of the three groups.

Slope bricks are placed on particles where the normal is sufficiently dissimilar to the up vector. Grill bricks are placed on particles where there are no particles above the current one. This can be determined by using the `pcfind` function, and offsetting the current y position by a small amount as the location to search. Then, when `pcfind` returns a group of nearby points, we can check to see if they are points above the current particle. Lastly, we place block points on all other particles.

## Preventing Intersecting Lego Blocks
We can place blocks at points by looping through each particle and placing a LEGO brick at particle if there isn't one already there. We can then remove any particles that are covered by the current LEGO brick to ensure that we don't place multiple bricks on the same particle. 

However, because the LEGO blocks used are different sizes and shapes, we use a greedy method to first place as many large blocks as possible and then fill the space with smaller blocks. This is done by iterating through each point and keeping track of which points remain unused by a brick after assigning bricks to particles as described above. Once we have finished our for loop, we will have split the original input group of points into "points occupied by LEGO bricks" and "points unoccupied by LEGO bricks". Since we cannot place any more of the current size of LEGO bricks onto our points, then we must occupy the remaining unused points with a smaller brick type. We can do this repeatedly with decreasing brick sizes until we have occupied all points with a brick.

## Exposing Node Parameters
In order to make the LEGO-ifying usable as a tool, I exposed certain parameters to be customizable for the user. These included 1) the point separation of the particles (which controls the size of the LEGO bricks and in turn makes the end output more or less "blocky"), 2) the threshold of block slope (which controls the number of slope blocks), 3) the percentage of grill bricks (which controls the number of grill bricks), and 4) the color of the blocks (which applies a tint to the brick color).

![dino_par_interface](https://github.com/ClaireL21/hw03-legos/assets/102630261/188195e2-256a-4bd0-9d86-89bfaf7b918e)

## Rendering
Lastly, I rendered the LEGO-ified mesh using the three-point lighting technique and made the material for the bricks plastic-like. 

Below are some outputs of the LEGO-ified mesh!

| ![dino-render3](https://github.com/ClaireL21/hw03-legos/assets/102630261/4056a4b2-0315-46d3-a39c-74412b39b9f1)| ![dino-render2](https://github.com/ClaireL21/hw03-legos/assets/102630261/f7a892b8-34d5-4197-8d42-18a9760c7eb5) |
| -----------         | -----------          |
| ![dino-render5](https://github.com/ClaireL21/hw03-legos/assets/102630261/d69769b1-0e64-44c0-8daa-b89088ea03ab) | ![dino-render4](https://github.com/ClaireL21/hw03-legos/assets/102630261/63cae8ba-c5f5-42ef-9740-6941f9aa73b9) |

