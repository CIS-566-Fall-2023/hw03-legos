# Lego-fication

[see the HIP file here!] (https://drive.google.com/file/d/1OJE3G5J6TwUa0AFRf9qrRIE1JXpcrs3Z/view?usp=sharing)
[Video Demo](https://drive.google.com/file/d/1HzRkZeabLmmwkA_GAhiIFzLpTP8KAu1-/view?usp=sharing)

## Objective
- More advanced Houdini exploration; learn how to voxellize meshes into LEGO bricks!

## Inspiration
I was inspired by the LEGO movie to lego-ify meshes as well as more advanced environments, like ocean waves

## What's customizable:
- Size/resolution of bricks
- Angle threshold at which to place angled bricks

## Implementation details
- Used and then voxellized ocean tutorial from [Houdini's Ocean Tools Tutorial](https://www.sidefx.com/tutorials/houdini-16-ocean-tools/)
- Checked mesh intersection with grid of points
- Categorized mesh points into 4 types of blocks: Angled, Flat, 2x2 bricks, and 1x1 bricks.
  - Angled bricks for point normals that surpass a certain threshold
  - Implementation of greedy algorithm that tries to put larger blocks first

