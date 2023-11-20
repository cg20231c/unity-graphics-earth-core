# unity-graphics-earth-core

A particle system simulates and renders many small images or Meshes, called particles, to produce a visual effect. Each particle in a system represents an individual graphical element in the effect. The system simulates every particle collectively to create the impression of the complete effect.

![holoTable](img/holotable.png)

Particle systems are useful when you want to create dynamic objects like fire, smoke, or liquids because it is difficult to depict this kind of object with a Mesh (3D) or Sprite (2D). Meshes and Sprites are better at depicting solid objects such as a house or a car.

To provide flexibility when you author a particle system, Unity offers two solutions to choose from.The two particle system solutions are:

- The Built-in Particle System: A solution that gives you full read/write access to the system, and the particles it contains, from C# scripts. You can use the Particle System API to create custom behaviors for your particle system.
- The Visual Effect Graph: A solution that can run on the GPU to simulate millions of particles and create large-scale visual effects. The Visual Effect Graph also includes a visual graph editor to help you author highly customizable visual effects.

| Feature                       | Built-in Particle System                                                                                                                                                                                                                                                                                                                                 | Visual Effect Graph                                                                                                                                                                                                                                                                                                                                                                                  |
| :---------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Render Pipeline Compatibility | Built-in Render Pipeline, Universal Render Pipeline, High Definition Render Pipeline                                                                                                                                                                                                                                                                     | Universal Render Pipeline, High Definition Render Pipeline                                                                                                                                                                                                                                                                                                                                           |
| Feasible number of particles  | Thousands                                                                                                                                                                                                                                                                                                                                                | Millions                                                                                                                                                                                                                                                                                                                                                                                             |
| Particle system authoring     | Simple modular authoring process that uses the Particle System component in the Inspector. Each module represents a predefined behavior for the particle.                                                                                                                                                                                                | Highly customizable authoring process that uses a graph view.                                                                                                                                                                                                                                                                                                                                        |
| Physics                       | Particles can interact with Unity’s underlying physics system.                                                                                                                                                                                                                                                                                           | Particles can interact with specific elements that you define in the Visual Effect Graph. For example, particles can interact with the depth buffer                                                                                                                                                                                                                                                  |
| Script interaction            | You can use C# scripts to fully customize the Particle System at runtime. You can read from and write to each particle in a system, and respond to collision events. The Particle System component also provides playback control API. This means that you can use scripts to play and pause the effect, and simulate the effect with custom step sizes. | You can expose graph properties and access them through C# scripts to customize instances of the effect. You can also use the Event Interface to send custom events with attached data that the graph can process. The Visual Effect component also provides playback control API. This means that you can use scripts to play and pause the effect, and simulate the effect with custom step sizes. |
| Frame buffers | No | In the High Definition Render Pipeline, provides access to the color and depth buffer. For example, you can sample the color buffer and use the result to set particle color, or you can use the depth buffer to simulate collisions.|


## Collision Module
Collision module allows your particles to collides with other game object in your scene.
This thing decides how particles bump into stuff in your scene. Pick Planes or World in the first menu to say if your collision rules are for flat surfaces or everything in the world.  
### Plane module properties
![collision module planes](img/planemodule.png)
| Property | Function |
| -------- | -------- |
|Planes popup|Select Planes mode.|
|Planes|An expandable list of Transforms that define collision planes.|
|Visualization|Selects whether the collision plane Gizmos will be shown in the Scene view as wireframe grids or solid planes.|
|Scale Plane|Size of planes used for visualization.|
|Dampen|The fraction of a particle’s speed that it loses after a collision.|
|Bounce|The fraction of a particle’s speed that rebounds from a surface after a collision.|
|Lifetime Loss|The fraction of a particle’s total lifetime that it loses if it collides.|
|Min Kill Speed|Particles travelling below this speed after a collision will be removed from the system.|
|Max Kill Speed|Particles travelling above this speed after a collision will be removed from the system.|
|Radius Scale|Allows you to adjust the radius of the particle collision spheres so it more closely fits the visual edges of the particle graphic.|
|Send Collision Messages|If enabled, particle collisions can be detected from scripts by the OnParticleCollision function.|
|Visualize Bounds|Renders the collision bounds of each particle as a wireframe shape in the Scene view.|
### World module properties
![world module](img/worldmodule.png)
| Property | Function |
| -------- | -------- |
|World popup	|Select World mode.|
|Collision Mode	|3D or 2D.|
|Dampen|The fraction of a particle’s speed that it loses after a collision.|
|Bounce|The fraction of a particle’s speed that rebounds from a surface after a collision.|
|Lifetime Loss	|The fraction of a particle’s total lifetime that it loses if it collides.|
|Min Kill Speed	|Particles travelling below this speed after a collision will be removed from the system.|
|Max Kill Speed	|Particles travelling above this speed after a collision will be removed from the system.|
|Radius Scale	|Setting for 2D or 3D.|
|Collision Quality	|Use the drop-down to set the quality of particle collisions. This affects how many particles can pass through a collider. At lower quality levels, particles can sometimes pass through colliders, but are less resource-intensive to calculate.|
|Collides With	|Particles will only collide with objects on the selected layers.|
|Max Collision Shapes	|How many collision shapes can be considered for particle collisions. Excess shapes are ignored, and terrains take priority.|
|Enable Dynamic Colliders	|Dynamic colliders are any collider not configured as Kinematic|
|Voxel Size	|A voxel represents a value on a regular grid in three-dimensional space.|
|Collider Force	|Apply a force to Physics Colliders after a Particle collision. This is useful for pushing colliders with particles.|
|Multiply by Collision Angle	|When applying forces to Colliders, scale the strength of the force based on the collision angle between the particle and the collider. Grazing angles will generate less force than a head-on collision.|
|Multiply by Particle Speed	|When applying forces to Colliders, scale the strength of the force based on the speed of the particle. Fast-moving particles will generate more force than slower ones.|
|Multiply by Particle Size	|When applying forces to Colliders, scale the strength of the force based on the size of the particle. Larger particles will generate more force than smaller ones.|
|Send Collision Messages	|Check this to be able to detect particle collisions from scripts by the OnParticleCollision function.|
|Visualize Bounds	|Preview the collision spheres for each particle in the Scene view.|

![Alt text](img/collisionex.png)

When using collisions, particle size can cause graphic clipping issues. The Radius Scale property helps by defining an approximate circular radius as a percentage of the actual size, preventing sinking effects.  

Dampen and Bounce properties are handy for solid objects—like gravel bouncing off surfaces, while snowball particles lose speed. Lifetime Loss and Min Kill Speed reduce residual particles after collisions, ideal for dissipating effects quickly, such as a fireball's particles after impact.

## Sub Emitters Module
Particle Systems allow for diverse effects at different lifetimes using sub-emitters. These are ordinary Particle System objects, creating nested effects.  
![Alt text](img/subemmiter.png)
To trigger a sub-emitter, you can use these are the conditions:

- Birth: When the particles are created.  
- Collision: When the particles collide with an object.  
- Death: When the particles are destroyed.
- Trigger: When the particles interact with a Trigger collider.
- Manual: Only triggered when requested via script. See ParticleSystem TriggerSubEmitter.
![  ](img/subemmiterex.png)

Burst emission is exclusive to Collision, Trigger, Death, and Manual events. Properties like size, rotation, color, and lifetime can be inherited from the parent particle to the sub-emitter.  

Velocity inheritance is controlled through the Inherit Velocity module.  

Emit Probability property adjusts the likelihood of sub-emitter events, with a value of 1 guaranteeing trigger and lower values reducing probability.

## Creating Simple Rain
1. Create a Particle System rename it into rain and reset the transform, make the position y value to 15  
![Alt text](img/step1.png)
2. Set the shape in the shape module to box and set the scale x and z to 20 (you can make it bigger)  
![Alt text](img/step2.png)  
3. Check the velocity over lifetime module and set the linear to random between two constants and set the y value to -25 and -35 (you can change the x value to add direction to the rain)  
![Alt text](img/step3.png)  
4. In the renderer Module chang the render mode to streched billboard  
![Alt text](img/step4.png)  
5. In the main module check the 3d start size and set it to random between two constants and set the x value to 0.1 and 0.1, y value to 1 and 2, z value to 0.1 and 0.1, and set the start speed to 0, max particle to 10000  
![Alt text](img/step5.png)  
6. In the same module set the start color transparency to around 70%  
![Alt text](img/step6.png)    
7. In the Emmision module, change the rate over time to 500  
![Alt text](img/step7.png)  
8. Check the collision module and set  
type > world
Dampen > 1
Bounce > 0
lifetime loss > 0.4  
![Alt text](img/step8.png)  
Result:  
![Alt text](img/result.gif) 
