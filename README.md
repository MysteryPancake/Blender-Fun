# Blender Fun
Blender projects and node experiments.

## [Caustics](caustics.blend)
[Inspired by Evan Wallace](https://medium.com/@evanwallace/rendering-realtime-caustics-in-webgl-2a99a29a0b2c), I used Geometry Nodes to create caustics by distorting a mesh.

[<img src="images/causticanim.gif?raw=true" width="480" alt="Caustics demo">](caustics.blend)

First it uses a Raycast node to find where the light surface collides with the water surface ([thanks Erindale!](https://www.youtube.com/watch?v=ZCCQXoJoIK4))

Then it uses Refract from Vector Math:

> For a given incident vector A, surface normal B and ratio of indices of refraction (IOR), Refract outputs the refraction vector R.

- The incident vector is the direction light is going. Here it's the normal vector of the light surface.
- The surface normal is the vector pointing up from the water. Here it's the Hit Normal returned by Raycast.
- The ratio of indices of refraction depends what materials it goes through. Here it's `IOR of air / IOR of water`.

Because different materials have different IOR values, I created a custom IOR attribute on the water.

When Raycast collides with the water surface, it reads the water's custom IOR attribute when performing the division above.

<img src="images/causticnodes.png?raw=true" alt="Caustics nodes">
