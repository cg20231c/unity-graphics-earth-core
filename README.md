# unity-graphics-earth-core

A particle system simulates and renders many small images or Meshes, called particles, to produce a visual effect. Each particle in a system represents an individual graphical element in the effect. The system simulates every particle collectively to create the impression of the complete effect.

![holoTable](img/holotable.png)

Particle systems are useful when you want to create dynamic objects like fire, smoke, or liquids because it is difficult to depict this kind of object with a Mesh (3D) or Sprite (2D). Meshes and Sprites are better at depicting solid objects such as a house or a car.

To provide flexibility when you author a particle system, Unity offers two solutions to choose from.The two particle system solutions are:

- The Built-in Particle System: A solution that gives you full read/write access to the system, and the particles it contains, from C# scripts. You can use the Particle System API to create custom behaviors for your particle system.
- The Visual Effect Graph: A solution that can run on the GPU to simulate millions of particles and create large-scale visual effects. The Visual Effect Graph also includes a visual graph editor to help you author highly customizable visual effects.

| Feature | Built-in Particle System | Visual Effect Graph |
| :--- | :--- | :--- |
| Render Pipeline Compatibility | Built-in Render Pipeline, Universal Render Pipeline, High Definition Render Pipeline | Universal Render Pipeline, High Definition Render Pipeline |
| Feasible number of particles  | Thousands | Millions |
| Particle system authoring | Simple modular authoring process that uses the Particle System component in the Inspector. Each module represents a predefined behavior for the particle. | Highly customizable authoring process that uses a graph view. |
| Physics | Particles can interact with Unity’s underlying physics system. | Particles can interact with specific elements that you define in the Visual Effect Graph. For example, particles can interact with the depth buffer |
| Script interaction | You can use C# scripts to fully customize the Particle System at runtime. You can read from and write to each particle in a system, and respond to collision events. The Particle System component also provides playback control API. This means that you can use scripts to play and pause the effect, and simulate the effect with custom step sizes. | You can expose graph properties and access them through C# scripts to customize instances of the effect. You can also use the Event Interface to send custom events with attached data that the graph can process. The Visual Effect component also provides playback control API. This means that you can use scripts to play and pause the effect, and simulate the effect with custom step sizes. |
| Frame buffers | No | In the High Definition Render Pipeline, provides access to the color and depth buffer. For example, you can sample the color buffer and use the result to set particle color, or you can use the depth buffer to simulate collisions. |

Unity’s Built-in Particle System allows you to create effects for every platform that Unity supports. The Built-in Particle System simulates particle behavior on the CPU which allows for the following main benefits:

- You can use C# scripts to interact with a system and the individual particles within it.
- Particle systems can use Unity’s underlying physics system and thus interact with Colliders in your Scene.

The Built-in Particle System uses a component, so placing a Particle System in a Scene is a matter of adding a pre-made GameObject (menu: **GameObject** > **Effects** > **Particle System**) or adding the component to an existing GameObject (menu: **Component > Effects > Particle System**). Because the component is quite complicated, the Inspector is divided into a number of collapsible sub-sections or **modules** that each contain a group of related properties.

When a GameObject with a Particle System is selected, the **Scene** view contains a small **Particle Effect** panel, with some simple controls that are useful for visualising changes you make to the system’s settings.


![SceneAndPanel](/img/SceneAndPanel.png)
![ParticleEffectPanel](/img/ParticleEffectPanel.png) 


| Part of the panel | Function |
| :---------------- | :--- |
| Playback Speed | To speed up or slow down the particle simulation. |
| Playback Time |  Indicates the time elapsed since the system was started; this may be faster or slower than real time depending on the playback speed.|
| Particle (Count) | Indicates how many particles are currently in the system. |
| Speed Range | Indicate the start speed of the particle, applied in the startin direction. |
| Simulate layers | Automatically preview all looping Particle Systems on the chosen layers, in addition to selected Game Objects. |
| Resimulate | If enabled, the Particle Systems will show changes made to the system immediately (including changes made to the Particle System Transform). |
| Show Bounds | Show world space bounding boxes |
| Show Only Selected | If disabled, all unselected Particle Systems in the current effect will be hidden. | 

The Particle System component has many properties, and for convenience, the Inspector organises them into collapsible sections called “modules”.


![InspectorAndMainModules](/img/InspectorAndMainModules.png)


The Particle System component has a powerful set of properties that are organized into modules for ease of use. This section of the manual covers each of the modules in detail. The list of modules is as follows:

List of Modules
- [Main Module](#main-module)
- [Emission Module](#emission-module)
- [Shape Module](#shape-module)
- [Velocity over Lifetime Module](#velocity-over-lifetime-module)
- [Noise Module](#noise-module)
- Lifetime Module
  - [Limit Velocity over Lifetime Module](#limit-velocity-over-lifetime-module)
  - [Force over Lifetime Module](#force-over-lifetime-module)
  - [Color over Lifetime Module](#color-over-lifetime-module)
  - [Size over Lifetime Module](#size-over-lifetime-module)
  - [Rotation over Lifetime Module](#rotation-over-lifetime-module)
- [Inherit Velocity Module](#inherit-velocity-module)
- Speed Module
  - [Lifetime by Emitter Speed Module](#lifetime-by-emitter-speed-module)
  - [Color by Speed Module](#color-by-speed-module)
  - [Size by Speed Module](#size-by-speed-module)
  - [Rotation by Speed Module](#rotation-by-speed-module)
- [Triggers Module](#triggers-module)
- [Renderer Module](#renderer-module)
- [Texture Sheet Animation Module](#texture-sheet-animation-module)
- [Lights Module](#lights-module)
- [Trails Module](#trails-module)
- [Custom Data Module](#custom-data-module)
- [Collision Module](#collision-module)
- [Sub Emitters Module](#sub-emitters-module)
- [External Forces Module](#external-forces-module)

## Main Module
The Particle System module contains global properties that affect the whole system. Most of these properties control the initial state of newly created particles. To expand and collapse the main module, click the Particle System bar in the Inspector window.


![MainModule](/img/MainModule.png)


| Property | Function |
| :--- | :--- |
| Duration | The length of time the system runs. |
| Looping | If enabled, the system starts again at the end of its duration time and continues to repeat the cycle. |
| Prewarm | If enabled, the system is initialized as though it had already completed a full cycle (only works if **Looping** is also enabled). |
| Start Delay | Delay in seconds before the system starts emitting once enabled. |
| Start Lifetime | The initial lifetime for particles. |
| Start Speed | The initial speed of each particle in the appropriate direction. |
| 3D Start Size	| Enable this if you want to control the size of each axis separately. |
| Start Size | The initial size of each particle. |
| 3D Start Rotation | Enable this if you want to control the rotation of each axis separately. |
| Start Rotation | The initial rotation angle of each particle. |
| Flip Rotation	| Causes some particles to spin in the opposite direction. |
| Start Color	| The initial color of each particle. |
| Gravity Modifier | Scales the gravity value set in the Physics window. A value of zero switches gravity off. |
| Simulation Space | Controls whether particles are animated in the parent object’s local space (therefore moving with the parent object), in the world space, or relative to a custom object (moving with a custom object of your choosing). |
| Simulation Speed | Adjust the speed at which the entire system updates. |
| Delta Time | Choose between **Scaled** and **Unscaled**, where **Scaled** uses the **Time Scale** value in the Time window, and **Unscaled** ignores it. This is useful for Particle Systems that appear on a Pause Menu, for example. |
| Scaling Mode | Choose how to use the scale from the transform. Set to **Hierarchy**, **Local** or **Shape**. Local applies only the Particle System transform scale, ignoring any parents. Shape mode applies the scale to the start positions of the particles, but does not affect their size. |
| Play on Awake | If enabled, the Particle System starts automatically when the object is created.
| Emitter Velocity | Choose how the Particle System calculates the velocity used by the Inherit Velocity and Emission modules. The system can calculate the velocity using a **Rigidbody** component, if one exists, or by tracking the movement of the **Transform** component. If no Rigidbody component exists, the system uses its Transform component by default.
| Max Particles | The maximum number of particles in the system at once. If the limit is reached, some particles are removed. |
| Auto Random Seed | If enabled, the Particle System looks different each time it is played. When set to false, the system is exactly the same every time it is played. |
| Random Seed | When disabling the automatic random seed, this value is used to create a unique repeatable effect. |
| Stop Action | When all the particles belonging to the system have finished, it is possible to make the system perform an action. A system is determined to have stopped when all its particles have died, and its age has exceeded its Duration. For looping systems, this only happens if the system is stopped via script. **Disable** means the GameObject is disabled, **Destroy** means the GameObject is destroyed, and **Callback** means the OnParticleSystemStopped callback is sent to any **scripts** attached to the GameObject. |
| Culling Mode | Choose whether to pause Particle System simulation when particles are offscreen. Culling when offscreen is most efficient, but you may want to continue simulation for off-one effects. **Automatic** means looping systems use **Pause**, and all other system use **Always Simulate.**, **Pause And Catch-up** means the system stops simulating while offscreen. When re-entering the view, the simulation performs a large step to reach the point where it would have been had it not paused. In complex systems, this option can cause performance spikes, **Pause** means the system stops simulating while offscreen, **Always Simulate** means The system processes its simulation on each frame, regardless of whether it is on screen or not. This can be useful for one-shot effects such as fireworks, where during the simulation would be obvious. |
| Ring Buffer Mode | Keeps particles alive until they reach the **Max Particles** count, at which point new particles recycle the oldest ones, instead of removing particles when their lifetimes elapse. **Disabled** means disabling the Ring Buffer Mode, so the system removes particles when their lifetime elapses, **Pause Until Replaced** means pauses old particles at the end of their lifetime until the **Max Particle** limit is reached, at which point the system recycles them, so they reappear as new particles, **Loop Until Replaced** means At the end of their lifetime, particles rewind back to the specified proportion of their lifetime until the **Max Particle** limit is reached, at which point the system recycles them, so they reappear as new particles. |

The system emits particles for a specific duration, and can be set to emit continuously using the **Looped** property. This allows you to set particles to be emitted intermittently or continuously; for example, an object may emit smoke in short puffs or in a steady stream.

The **Start** properties (**lifetime**, **speed**, **size**, **rotation** and **color**) specify the state of a particle on emission. You can specify a particle’s width, height and depth independently, using the **3D Start Size** property. The **3D Start Size** property allows you to specify a particle’s width, height and depth independently. In the Particle System **Main** module, check the **3D Start Size** checkbox, and enter the values for the initial x (width), y (height) and z (depth) of the particle.

## Emission Module
The properties in this module affect the rate and timing of Particle System emissions.


![EmissionModule](/img/EmissionModule.png)


| Property | Function |
| :--- | :--- |
| Rate over Time | The number of particles emitted per unit of time. |
| Rate over Distance | The number of particles emitted per unit of distance moved. |
| Bursts | A burst is an event which spawns particles. These settings allow particles to be emitted at specified times. **Time** is for setting the time (in seconds, after the Particle System begins playing) at which to emit the burst, **Count** is for setting a value for the number of particles that may be emitted, **Cycles** is for setting a value for how many times to play the burst, **Interval** is for setting a value for the time (in seconds) between when each cycle of the burst is triggered, **Probability** is for controlling how likely it is that each burst event spawns particles. A higher value makes the system produce more particles, and a value of 1 guarantees that the system produces particles. |

The rate of emission can be constant or can vary over the lifetime of the system according to a curve. If **Rate over Distance** mode is active, a certain number of particles are released per unit of distance moved by the parent object. This is very useful for simulating particles that are actually created by the motion of the object (for example, dust from a car’s wheels on a dirt track).

If **Rate over Time** is active, then the desired number of particles are emitted each second regardless of how the parent object moves. Additionally, you can add bursts of extra particles that appear at specific times (for example, a steam train chimney that produces puffs of smoke).

## Shape Module
This module defines the the volume or surface from which particles can be emitted, and the direction of the start velocity. The **Shape** property defines the shape of the emission volume, and the rest of the module properties vary depending on the Shape you choose.

All shapes (except Mesh) have properties that define their dimensions, such as the **Radius** property. To edit these, drag the handles on the wireframe emitter shape in the Scene view. The choice of shape affects the region from which particles can be launched, but also the initial direction of the particles. For example, a Sphere emits particles outward in all directions, a **Cone** emits a diverging stream of particles, and a **Mesh** emits particles in directions that are normal to the surface.


![ShapeModule](/img/ShapeModule.png)


Available shapes :
- Sphere
- Hemisphere
- Cone
- Donut
- Box
- Mesh
- Mesh Renderer
- Skinned Mesh Renderer
- Sprite
- Sprite Renderer
- Circle
- Edge
- Rectangle


![Shapes](/img/Shapes.png)

## Velocity Over Lifetime Module
Velocity Over Lifetime Module allows you to adjust the velocity of the particles over it's lifetime. Its is suitable for effects like smoke dissipating over time or sparks slowing down as they travel.

![VelocityOverLifetime](/img/Velocity-Over-Lifetime.png)

| Parameter | Function |
| -------- | -------- |
|Linear|Used to adjust the linear velocity of the particles to the intended|
|Orbital|Used to adjust the orbital velocity of the particles to the intended|
|Radial|Used to adjust the radial value|
|Speed|Used to adjust the speed value|

## Noise Module
Noise Module allows you to add variations to the movement of the particles.

![Noise](/img/Noise.png)

| Parameter | Function |
| -------- | -------- |
|Strength|Used to adjust the variations|
|Frequency|Used to adjust how often for the particles to change it's movement|
|Scroll Speed|Used to adjust the noise overtime|
|Octaves|Used to adjust how many layer of Noise it has|
|Position Amount|Used to adjust how the position affected by the Noise, if 0 then nothing happen|
|Rotation Amount|Used to adjust how the rotation affected by the Noise, if 0 then nothing happen|
|Size Amount|Used to adjust how the size affected by the Noise, if 0 then nothing happen|

## Renderer Module

  ![renderer](/img/renderer.png)

The Renderer module’s settings determine how a particle’s image or Mesh is transformed, shaded and overdrawn by other particles.

## Lifetime Module
  ### Velocity over Lifetime module
  
  ![velocity_over_lifetime](/img/velocity_over_lifetime.png)
  
  The Velocity over Lifetime module allows you to control the velocity of particles over their lifetime.
| **Property** | **Function** |
| -------- | -------- |
|Linear X, Y, Z  |  Linear velocity of particles in the X, Y and Z axes.|
|Space | Specifies whether the Linear X, Y, Z axes refer to local or world space.|
|Orbital X, Y, Z |  Orbital velocity of particles around the X, Y and Z axes.|
|Offset X, Y, Z |  The position of the center of orbit, for orbiting particles.|
|Radial |  Radial velocity of particles away from/towards the center position.|
|Speed Modifier |  Applies a multiplier to the speed of particles, along/around their current direction of travel.|

  ### Limit Velocity over Lifetime Module
  
  ![limit_velocity_over_lifetime](/img/limit_velocity_over_lifetime.png)
  
  This module controls how the speed of particles is reduced over their lifetime.
| **Property** | **Function** |
| -------- | -------- |
|Separate Axes  |  Splits the axes up into separate X, Y and Z components.|
|Speed | Sets the speed limit of the particles.|
|Space |  Selects whether the speed limitation refers to local or world space. This option is only available when **Separate Axes** is enabled.|
|Dampen |  The fraction by which a particle’s speed is reduced when it exceeds the speed limit.|
|Drag |  	Applies linear drag to the particle velocities.|
|Multiply by Size |  	When enabled, larger particles are affected more by the drag coefficient.|
|Multiply by Velocity |  When enabled, faster particles are affected more by the drag coefficient.|

  ### Lifetime by Emitter Speed module

 ![lifetime_by_emitter_speed](/img/lifetime_by_emitter_speed.png)
  
  This module controls the initial lifetime of each particle based on the speed of the emitter when the particle spawns. It multiplies the start lifetime of particles by a value that depends on the speed of the object that spawned them. For most Particle Systems, this is the GameObject velocity, but for sub-emitters, the velocity comes from the parent particle that the sub-emitter particle originated from.
<table>
    <thead>
        <tr>
            <th><b>Property<b></th>
            <th><b>Function<b></th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td rowspan=4>Multiplier</td>
            <td rowspan=4>The multiplier to apply to the particle’s initial lifetime. The module uses this value differently depending on the curve mode you set. The curve modes are: 
             <ul>
               <li> Constant: Uses the constant multiplier value you set for this property. Using this curve mode ignores the Speed Range property.</li>
               <li> Curve: Takes the emitter’s speed, maps it to a value between 0 and 1 based on the Speed Range, then uses the normalized value to sample the curve.</li>
               <li> Random Between Two Constants: Sets a random multiplier for each particle between the two values you set for this property. Using this curve mode ignores the Speed Range property.</li>
               <li> Random Between Two Curves: Takes the emitter’s speed, maps it to a value between 0 and 1 based on the Speed Range, then uses the normalized value to sample each curve. For each particle, the module sets the multiplier to a random value between the two samples.</ul>
            </td>
        </tr>
    </tbody>
    <tbody>
        <tr>
            <td rowspan=4>Speed Range</td>
            <td rowspan=4>The multiplier to apply to the particle’s initial lifetime. The module uses this value differently depending on the curve mode you set. The curve modes are: 
              The minimum and maximum emitter speeds the Particle System maps to a value along the Multiplier curve. If the emitter’s speed is equal to the first value, the multiplier is the value at the start of the curve. If the emitter’s speed is equal to the second value, the multiplier is the value at the end of the curve. This property is only relevant if the curve mode for Multiplier is set to Curve or Random Between Two Curves.
            </td>
        </tr>
    </tbody>
</table>

  ### Force over Lifetime module

  ![force_over_lifetime](/img/force_over_lifetime.png)
  
  Particles can be accelerated by forces (such as wind or attraction) that are specified in this module.
| **Property** | **Function** |
| -------- | -------- |
|X, Y, Z |  Force applied to each particle in the X, Y and Z axes.|
|Space | 	Selects whether the force is applied in local or world space.|
|Randomize | 	When using the Two Constants or Two Curves modes, this causes a new force direction to be chosen on each frame within the defined ranges. This causes more turbulent, erratic movement.|

  ### Color over Lifetime module

 ![color_over_lifetime](/img/color_over_lifetime.png)
  
  This module specifies how a particle’s color and transparency changes over its lifetime.
| **Property** | **Function** |
| -------- | -------- |
|Color  |  The color gradient of a particle over its lifetime. The very left-hand point of the gradient bar indicates the beginning of the particle’s life, and the very right-hand side of the gradient bar indicates the end of the particle’s life. In the image above, the particle starts off orange, fades in opacity over time, and is invisible by the time its life ends.|

  ### Size over Lifetime module

 ![size_over_lifetime](/img/size_over_lifetime.png)
  
  Many effects involve a particle changing size according to a curve, which can be set in this module.
| **Property** | **Function** |
| -------- | -------- |
|Separate Axes  |  	Control the particle size independently on each axis.|
|Size | A curve which defines how the particle’s size changes over its lifetime.|

  ### Rotation over Lifetime Module

 ![rotation_over_lifetime](/img/rotation_over_lifetime.png)
  
  Here, you can configure particles to rotate as they move.
| **Property** | **Function** |
| -------- | -------- |
|Separate Axes  |  Control rotation independently for each axis of rotation.|
|Angular Velocity | Sets the speed limit of the particles.|

## Inherit Velocity module

 ![inherit_velocity](/img/inherit_velocity.png)

This module is part of the Particle System component. When you create a new Particle System GameObject, or add a Particle System component to an exiting GameObject, Unity adds the Inherit Velocity module to the Particle System. By default, Unity disables this module.
| **Property** | **Function** |
| -------- | -------- |
|**Mode**  |  Specifies how the emitter velocity is applied to particles.|
|  Current |  The emitter’s current velocity will be applied to all particles on every frame. For example, if the emitter slows down, all particles will also slow down.|
|  Initial |  The emitter’s velocity will be applied once, when each particle is born. Any changes to the emitter’s velocity made after a particle is born will not affect that particle.|
|**Multiplier** |  The proportion of the emitter’s velocity that the particle should inherit.|

## Speed Module
  ### Color By Speed Module
Color By Speed Module allows you to adjusts the color of the particles based on their speed. It is suitable for effects where particle color indicates speed, such as a flame changing from yellow to red as it accelerates.

![ColorBySpeed](/img/Color-By-Speed.png)

| Parameter | Function |
| -------- | -------- |
|Color|Used to adjust the color you want to change with speed|
|Speed Range|Used to adjust the range of the speed for the color changes|

  ### Size By Speed Module
Size By Speed Module allows you to adjusts the size of the particles based on their speed. It is suitable to make the particles grow or shrink as they move.

![SizeBySpeed](/img/Size-By-Speed.png)

| Parameter | Function |
| -------- | -------- |
|Size|Used to adjust the size you want to change with speed|
|Speed Range|Used to adjust the range of the speed for the size changes|

  ### Rotation By Speed Module
Rotation By Speed Module allows you to adjusts the rotation of the particles based on their speed. It is suitable for creating swirling effects.

![RotationBySpeed](/img/Rotation-By-Speed.png)

| Parameter | Function |
| -------- | -------- |
|Angular Velocity|Used to adjust the angular velocity|
|Speed Range|Used to adjust the range of the speed|

## Triggers Module

![trigger](/img/trigger.png)

The Built-in Particle System’s Triggers module allows you to access and modify particles based on their interaction with one or more Colliders in the Scene.

## Renderer Module
Renderer Module allows you to add sprites to the particle system.

To make a Material for renderer, you can use this step:
1. Download from the github the file named **Meledak.png**.
2. Import the picture with right click at assets in view project.
3. Click **import new assets** and pick Meledak.png and then click "Create" and "Material"
4. If you check the material you have made, you can see the inspector view .

![Renderer1](/img/Renderer1.png)

5. In **Shader** click **Standard** and change it with **Particles** then **Standard Unlit**.

![Renderer2](/img/Renderer2.png)

6. In **Rendering Mode** change **Opaque** to **Fade**.
7. Drag the **Meledak.png** to the box on the left side of **Albedo**
8. Open the **Inspectore** of the **Particle System** and then click **Renderer** and the box to enable it.

![Renderer3](/img/Renderer3.png)

9. Drag the **Material** Asset that have been made to the **Material** like in the picture.

## Texture Sheet Animation Module
Texture Sheet Animation Module allow you to animate sprites sheet. This is how to use it:
1. Open the **Particle System**'s inspector, search for **Texture Sheet Animation** and click it with the box next to it.
2. It will open this inspector:

![Texture-Sheet-Animation](/img/Texture-Sheet-Animation.png)

3. Change the **X** with 5 and the **Y** with 2. This score is based on the sum of **X** and **Y** pictures in the Meledak.png which is 5 for the **X** and 2 for the **Y**.
4. Particles now have animation.

The result is like this:

![Texture-Sheet-Animation-Hasil](/img/Texture-Sheet-Animation-Hasil.png)

## Lights Module
Lights Module allow the particles to cast light. This is how to use it:
1. Make a **light** in the **Hierarchy** with a right click and click **Light** and then **Point Light**.
2. It will open this inspector:

![Light1](/img/Light1.png)

3. Choose the color that you like to be made a light for the **Particles** at the **Color** section.
4. Open the **Particle System** and click **Lights** with the box next to it.

![Light2](/img/Light2.png)

5. Drag the **Light** that has been made to the **Light** section.
6. Adjust the parameter with what you want or you can follow the picture above. 

The result will be like this:

![Light-Hasil](/img/Light-Hasil.png)

NOTE: If the light from the particle doesn't show up, it means there are not any place to be illuminated. This problem can be solved with adding a new object in the hierarchy. You can make a terrain from right-clicking in the **hierarchy** and the choose **3D Object** then **Terrain**.

## Trails Module
Trails Module allows you to add effects like a tail of long line. There are 2 kind of Trails in unity that you can use, **Particles** and **Ribbon**.

The Configuration of the **Particles** is like this:

![Trails-Particles](/img/Trails-Particles.png)

The result for the **Particles** is like this:

![Trails-Particles-Hasil](/img/Trails-Particles-Hasil.png)

The Configuration of the **Ribbon** is like this:

![Trails-Ribbon](/img/Trails-Ribbon.png)

The result for the **Ribbon** is like this:

![Trails-Ribbon-Hasil](/img/Trails-Ribbon-Hasil.png)

## Custom Data Module

![custom data](/img/custom data.png)

The Custom Data module allows you to define custom data formats in the Editor to be attached to particles.

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

## External Forces Module
External forces module make the particle affected by windzone in your scene
| Property | Function |
| -------- | -------- |
|Multiplier|Scale value applied to wind zone forces.|
|Influence Filter	|Choose whether to include Force Fields based on a Layer Mask, or via an explicit List.|
|List|Define an explicit list of Force Fields that can affect this Particle System. This appears when the Influence Filter is set to List.|
|Influence Mask	|Use a Layer Mask to determine which Force Fields affect this Particle System. This appears when the Influence Filter is set to Layer Mask.This is set to Everything by default, but you can enable or disable the following options individually: Nothing (automatically unticks all other options, turning them off); Everything (automatically ticks all other options, turning them on); Default; TransparentFX; Ignore Raycast; Water; UI; PostProcessing |

## Scripting Particle System
Script interface for the Built-in Particle System.  
[Scripting Documentation](https://docs.unity3d.com/ScriptReference/ParticleSystem.html)

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


ASSET = https://assetstore.unity.com/packages/vfx/particles/particle-pack-127325 
