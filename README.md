# LEGO-ifying Meshes

## Result

https://github.com/horo-ursa/hw03-legos/assets/54868517/9d3fc084-b38a-4395-8e5d-760e35ca9f33

![rendered image](renderer/result.png)

## Mesh Pre-Processing
- The objective is to generate a set of points that are consistently distributed within the mesh itself.
- To accomplish this, I began by encasing the mesh within a bounding box and subsequently forming a matrix of points within this box. Utilizing the `vdbfrompolygons` node, I transformed the mesh into a point cloud, in which every point inside serves as a potential location for a LEGO brick.
- color and normal attributes for every point in our cloud are determined using the `attributefrommap` and `attributetransfer` nodes, which extract and assign the color and normal attributes based on the original mesh.


## Converting the points to LEGO bricks
- To characterize the points into different categories, I use `pcfind` 
