# LEGO-ifying Meshes

## Project Overview
This Houdini project allows one to convert any faceted mesh to a collection of LEGO pieces. 

Allowing us to go from something like this:
![Mesh](https://github.com/hansen-yi/hw03-legos/assets/97490525/69223336-86f0-44f1-b041-3ca7e7a1828f)

to something like this:
![All](https://github.com/hansen-yi/hw03-legos/assets/97490525/68829953-079a-4f91-9e43-735429e08959)

In general, each lego-ified mesh is made up of 5 parts (2x2, 2x1, 1x1, sloped, and flat bricks) :
<p>
  <img src = "https://github.com/hansen-yi/hw03-legos/assets/97490525/cc2b7894-160b-4213-bfbe-2f0e8c3bb792" width = "30%" hspace = "5">
  <img src = "https://github.com/hansen-yi/hw03-legos/assets/97490525/9bc0c8fe-b3c6-4c77-8e1b-6ac3c54dde6c" width = "30%" hspace = "5">
  <img src = "https://github.com/hansen-yi/hw03-legos/assets/97490525/b93217bd-28ad-4aad-8300-fc216c9161d2" width = "30%" hspace = "5">
</p>
<p>
  <img src = "https://github.com/hansen-yi/hw03-legos/assets/97490525/8b073848-0ffc-4e07-8e13-7eccafbc55fb" width = "30%" hspace = "5">
  <img src = "https://github.com/hansen-yi/hw03-legos/assets/97490525/36c23e1b-5b96-46be-9b46-813d2554e820" width = "30%" hspace = "5">
</p>

(In addition, the flat bricks are made up of three different types of 2x1 bricks, and four different types of 1x1 bricks - each is chosen at random to be placed in the model)

## Exposed node parameters
![Controller](https://github.com/hansen-yi/hw03-legos/assets/97490525/3914518d-004d-476b-8261-2afaf303b965)

There also exists a controller that allows the user to adjust:
  - the scale of the bricks that compose the model, which also at the same time changes how many bricks are being used for the model
  - the threshold at which a particle is determined to be a sloped brick instead of a block brick
  - the percentage of "top" particles that display as flat bricks

The following illustrates changing the scale from 0.08 to 0.04 to 0.025:
<p>
  <img src = "https://github.com/hansen-yi/hw03-legos/assets/97490525/08ccdcc0-8893-446a-8168-a96588b01443" width = "33%">
  <img src = "https://github.com/hansen-yi/hw03-legos/assets/97490525/2a83c16d-2e34-4bd8-9c09-78ed37f145c8" width = "33%">
  <img src = "https://github.com/hansen-yi/hw03-legos/assets/97490525/d4756a92-04b3-4cdf-8ed7-4b2564429d1c" width = "33%">
</p>

The following illustrates changing the sloped brick threshold from 0 to 0.5 to 0.95:
<p>
  <img src = "https://github.com/hansen-yi/hw03-legos/assets/97490525/aa59547a-9980-4c7e-a893-e33a2f0b1724" width = "33%">
  <img src = "https://github.com/hansen-yi/hw03-legos/assets/97490525/272b0f79-1dd1-4fda-8c56-c9d83fef958a" width = "33%">
  <img src = "https://github.com/hansen-yi/hw03-legos/assets/97490525/f7b879fa-53f1-4745-9eca-5c4b568bba91" width = "33%">
</p>  
  
The following illustrates changing the percentage of "top" particles from 100% to 50% to 0%:
<p>
  <img src = "https://github.com/hansen-yi/hw03-legos/assets/97490525/f9c9c3c1-1048-4798-a8cf-018f0a5b482e" width = "33%">
  <img src = "https://github.com/hansen-yi/hw03-legos/assets/97490525/be85ff19-7028-42aa-918d-fff7d5198215" width = "33%">
  <img src = "https://github.com/hansen-yi/hw03-legos/assets/97490525/6d3488a7-436d-4b2d-8bcc-ca5bd5c2df47" width = "33%">
</p>

## Renders
![finalLegoRender](https://github.com/hansen-yi/hw03-legos/assets/97490525/1df80be2-0308-4295-8678-fff4055059b2)
![legoRenderSmall1](https://github.com/hansen-yi/hw03-legos/assets/97490525/62d80071-327a-42da-8444-bcfe63e71eb0)

