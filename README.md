# Cube Engine

![Cube Engine](http://i.imgur.com/m9jjG.png)

Cube Engine is an HTML5 3D engine based on canvas, absolutely no OpenGL and thus no 3D acceleration. This is a proof of concept and learning project, but it can be fun to some extent... as long as you have a ludicrously powerful computer.

## Demo
Check out the [live demo](http://nurgak.github.com/Cube-engine).

## World
The world resembles that of [Minecraft](http://www.minecraft.net/), a popular voxel-type 3D game based on boxes. You can add and remove everything and anything, different types of nodes are available. The borders are only limited by the size of an integer in Javascript, that means the world is generated dynamically as the player visits new areas. There is no vertical limit, but rendering distance is somewhat limited.

The topography of the world is generated by a pseudo-random function. The underlying system imitates that of Minecraft: the world is made of 16 by 16 by infinity node "chuncks". The pseudo-random function generates a single height value for each chunk and the height values in between are interpolated. Everything under the height value is filled with nodes and everything above is left empty. Depending on the height different types of soil can be found (grass, dirt, sand...).

Contrary to Minecraft the world renderer uses a 2D perlin-noise generator rather than 3D, there are no ores or tunnels underground, no enemies or mobs, no trees or physics. Since the renderer takes all the processing power the features must be limited.

A height map and a frames per second graph can be enabled in the menu.

## Rendering

![Cube Engine rendering with textures](http://i.imgur.com/Iz9IA.png)

The rendering is a simple painter's algorithm, everything is drawn from back to front, so nodes close to the camera are drawn over the nodes further away. As canvas doesn't have any 3D rendering capabilities the engine uses very basic 3D rendering techniques. Some optimisation techniques like back-face culling, occlusion culling and frustum culling have been implemented. Octrees aren't adapted to this game and scale, chunks are better suited.

To make things go faster a lower rendering distance can be selected.

Canvas doesn't support textures, so texture implementation must be made from ground up: an affine texture mapping system is used. Rendering with textures makes the game noticeably slower so a simple renderer, that uses plain colors, is also available.

Textures are stored in a _png_ file, the texture placement is exactly the same as Minecraft's, so one could use any current Minecraft texture pack with this game.

## Saving
One can locally save a game, this stores all nodes in a 3 by 3 chunk (with the player in the middle chunk) in the browsers local memory or in a file. The data can be loaded locally, but not from a file (for security reasons). To load a world from file the program must be run from a server.

## Problems
Corner clipping isn't supported, so being too close to a node will lead to its removal and one will be able to see what's on the other side.

The way Javascript handles floating point numbers makes it difficult to have exact integers, something that the collision system relies on. This was solved by "rounding" the numbers when close to an integer, but it's not a very elegant solution.

Chrome has some trouble rendering in plain color, specifically it's the `context.fill()` function that doesn't work when called too much it seems.

Firefox doesn't let the browser lock the pointer unless it's in full screen mode, this program should never run in full screen, unless on a super computer.

## Licence
Released under the [WTFPL](http://sam.zoy.org/wtfpl/COPYING).