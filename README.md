# LEGO-ifying Meshes

## Project Overview
This is a Houdini project that can convert any faceted mesh to a collection of LEGO pieces.

## Result
<p align="center">
 <img src="https://github.com/LichengCAO/hw03-legos/assets/81556019/aeada1a8-e807-45a7-8590-1cddd3157ad2"/>
</p>

## Implementation
|figure|step |
|:----:|:---:|
|<img src="https://github.com/LichengCAO/hw03-legos/assets/81556019/9b65f622-78d4-45a7-bbe7-87bfdc16e9b0" width="300"/>|This set of nodes help me convert geometry into a group of points. I used a `bound` node and a `pointsfromvolume` node to generate a set of points within the bounding box of the input mesh and used `vdbfrompolygons` and `convertvdb` to prepare the input mesh so that it could be used as the input of `group` node which gave me a group of points within the mesh. And I utilized the `blast` node to knocked out points that weren't in the mesh.|
| <img src="https://github.com/LichengCAO/hw03-legos/assets/81556019/89cebae7-ebd4-4ef3-89d4-cc59a4a2fff9" width="300"/>|I used these nodes to read UV from the mesh and transfer the desired values(N, d) to points for following operations. First, I used the attribfrommap node to apply a texture map to the input mesh. And then I used `attribtransfer` to transfer both color and normal information onto the points for next steps. I also incorporated an `attribwrangle` node to establish the scale of the points, ensuring they matched the point separation value of the `pointsfromvolume` node. This adjustment facilitates the alignment of the scale with the density of the point group in subsequent stages.|
|![avoidcollide](https://github.com/LichengCAO/hw03-legos/assets/81556019/0e3eaeab-089d-4d2e-80e6-c3a65155922c)|This block reads points from the group and splits the points into 2 groups. I employed a `group` node to identify points within the 2x1x2 bounding box, and I used a `switchif` node to determine points that have three other adjacent points, designating them as suitable locations for placing 2x1x2 bricks.|
|![findtop](https://github.com/LichengCAO/hw03-legos/assets/81556019/8119b735-61b4-46d3-bf43-445cac2b2150)|For the points that weren't in 2x1x2 bricks, I didn't use blocks to further split them based on the bounding box. Instead, I used `pcfind` to find points that have certain normal or don't have points above them, splited the points with `split` node and placed different bricks based on that information. Finally, I used `merge` node to merge all kinds of bricks into one output.|
|![controller](https://github.com/LichengCAO/hw03-legos/assets/81556019/95318b12-b825-45c3-ba4d-e55bb3ed9eea)|Furthermore, I added a null node to make certain parameters accessible for users. "Normal tolerance" is used to decide whether a slop brick should be placed. Since I used the dot product of the desired normal and the normal of the point to check if the point can be considered as a slop point, I can simply use the value of "Normal tolerance" as the threshold. I also provided "Portion of flat" to allow users to set the percentage of "top" particles displayed as flat bricks. I simply added a random number in the `attribwrangle` node which was used to find the flat bricks, and said that only when the random number is below the "portion of flat" could the point be considered as a point that the flat bricks can be placed on.
