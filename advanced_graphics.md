# CSC8502 - Advanced Graphics for Games

---

This project included the tutorials and coursework submission for the CSC8502 - Advanced Graphics for Games module at Newcastle University.

A graphical planet scene was created using C++ and OpenGL. For this coursework I recieved a mark of 82%

Code for this project [can be found here.](https://github.com/AdSand/CSC8502/tree/master/Blank%20Project)

---

## Base Features
- Landscape from heightmap, with texturing
- Light source, with bump mapping
- Environment mapping with skybox and reflection on the water surface.
- Automatic camera that moves through the scene.
-  Scene graph to render nodes (moons and trees), with movement of the objects.
- Simple meshes and other textures to build up the scene.

<p align="center">
<img src="images/AdvancedGraphics1.png?raw=true"/>
</p>

---

## Advanced Features

#### Post processing effects

An underwater blurring and colour correction effect, when the camera moves below water level.

<p align="center">
<img src="images/AdvancedGraphics2.png?raw=true"/>
</p>

Added a film grain effect and grey scale. The grey scale ignores fragments that are close to purple.

<p align="center">
<img src="images/AdvancedGraphics3.png?raw=true"/>
</p>

The post processing effects were written using GLSL shaders.

---

#### Mutliple Viewpoints and Scenes

Three cameras are used in total
- Main Planet Camera – used for automatic and free camera movement.
- Space Camera –scene from space, rendering a different scene.
- Mini-map Camera – orthographic view, follows position of the character.

The main scene always shows in full screen. Seconds viewpoints are rendered in the bottom left of the screen, simultaneously. Different frustums are calculated for camera dependent culling.

<p align="center">
<img src="images/AdvancedGraphics4.png?raw=true"/>
</p>

---

#### Skeletal Animation
Skeletal animation is included, using the model matrix to allow the animated character to move across the planet.

<p align="center">
<img src="images/AdvancedGraphics6.png?raw=true"/>
</p>

---

#### Deferred Rendering
The scene can be viewed using deferred rendering, using the same camera. This uses 100 spotlights, with their colours changed to match the theme of the scene. This is also displayed in the bottom left simultaneously.

An improvement that could be made to the deferred rendering is allowing the animated character to use the light produced from this stage. Currently the shading of the animated character does not take into account the light calculations.

<p align="center">
<img src="images/AdvancedGraphics5.png?raw=true"/>
</p>

---

*Click the image below to view on YouTube.*


[![YouTube link to video](https://img.youtube.com/vi/a3bV8FHamDU/0.jpg)](https://www.youtube.com/watch?v=a3bV8FHamDU)

---
Texture credits

[Mossy Rock texutre](https://textures.pixel-furnace.com/texture?name=Mossy%20Rock)

[Rock texture](https://textures.pixel-furnace.com/texture?name=Rock%2004)

[Space cube map](https://tools.wwwtyro.net/space-3d/index.html#animationSpeed=1&fov=75.43504464834814&nebulae=true&pointStars=true&resolution=1024&seed=6rmkiduygiw0&stars=true&sun=true)

Mesh credits

[Tree mesh](https://assetstore.unity.com/packages/3d/vegetation/trees/dry-trees-86967)
