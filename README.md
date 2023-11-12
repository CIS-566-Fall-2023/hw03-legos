# LEGO-ifying Meshes

## Project Overview
In this assignment, I made a Houdini project that can convert any faceted mesh to a collection of LEGO pieces.

![render](https://github.com/kyraSclark/hw03-legos/assets/60115638/21ba9fd9-d85d-4729-811e-8bc401a2d2d1)
---

## Creating your node
I created a custom node in the nodes window that you will enter and add nodes within; this will be your LEGO-ifying node.
![image](https://github.com/kyraSclark/hw03-legos/assets/60115638/afc90988-735e-47a6-8b38-8f82ada3f3ea)
![image](https://github.com/kyraSclark/hw03-legos/assets/60115638/526969e1-7911-4077-ab81-b28424524e3b)

## LEGO bricks
For this assignment, I to support three overall categories of LEGO brick:

2x2 Block bricks  
![image](https://github.com/kyraSclark/hw03-legos/assets/60115638/888d4344-2495-4196-94f1-83462cec056f)

2x1 Block bricks
![image](https://github.com/kyraSclark/hw03-legos/assets/60115638/fefa6e2c-38a3-4119-85c8-42652eca8eea)

1x1 Block bricks
![image](https://github.com/kyraSclark/hw03-legos/assets/60115638/2154482b-8715-41b1-851d-81178bc0cb26)

2x1 Flat bricks
![image](https://github.com/kyraSclark/hw03-legos/assets/60115638/6af32108-8aee-4667-b565-274d8a59d431)

Slope bricks
![image](https://github.com/kyraSclark/hw03-legos/assets/60115638/43dd7958-8e76-41ec-900b-23eec4955e67)

And all exposed tops have round tops
![image](https://github.com/kyraSclark/hw03-legos/assets/60115638/09240227-70b0-48b4-8c6a-56d7559d8af6)

## Customizable Parameters
My Lego-ifier has the following options available to the user: 

![image](https://github.com/kyraSclark/hw03-legos/assets/60115638/a359ddca-5b55-4e86-bc9a-a9a8afe4c486)

Slope controls the slope of the slope bricks. 0 Means there is no slope as you can see here: 
![image](https://github.com/kyraSclark/hw03-legos/assets/60115638/ee95cc0d-d647-4591-a2d5-7a62304574f6)

Whereas, -1 makes it a very sharply sloped brick:
![image](https://github.com/kyraSclark/hw03-legos/assets/60115638/2cc5f2e2-7e44-4b95-974c-0234b18955ee)

I recommend a value of around -.24 to get the optimal LEGO shape: 
![image](https://github.com/kyraSclark/hw03-legos/assets/60115638/cd64c056-703b-46f6-9d15-be18396d9346)

We also have the Scale value which controls the scale of all the bricks. The default is 1. But we can change the overall LEGO piece like so: 
![image](https://github.com/kyraSclark/hw03-legos/assets/60115638/d3c8e2bf-e521-404f-8fdc-00534225804b)
![image](https://github.com/kyraSclark/hw03-legos/assets/60115638/f3112206-f321-4471-87b6-cf467bdbb9bf)

## Color the bricks
Next, I got the texture file of the model and used the attribute transfer to add color to the mesh. 
![image](https://github.com/kyraSclark/hw03-legos/assets/60115638/523a8462-ca1a-4fe6-8840-980f61adf147)

Now, the color of the model is transferred to the points, and the following lego brick!
![image](https://github.com/kyraSclark/hw03-legos/assets/60115638/20ed24b4-3b4a-4e25-8ae3-e43018b26557)



