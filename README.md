# Blender Fun
Blender projects and node experiments.

## [Caustics](caustics.blend)
[Inspired by Evan Wallace](https://medium.com/@evanwallace/rendering-realtime-caustics-in-webgl-2a99a29a0b2c), I made caustics by distorting a mesh based on refraction.

[<img src="images/causticanim.gif?raw=true" width="480" alt="Caustics demo">](caustics.blend)

Firstly it uses a `Raycast` node to find where the light surface collides with the water surface ([thanks Erindale!](https://www.youtube.com/watch?v=ZCCQXoJoIK4))
<br>
The animation shows how `Raycast` moves depending on the ray length. It travels along the normal vector.

Next it uses `Refract` from `Vector Math`:

> For a given incident vector A, surface normal B and ratio of indices of refraction (IOR), Refract outputs the refraction vector R.

- The incident vector is the direction light is going. Here it's the normal vector of the light surface.
- The surface normal is the vector pointing up from the water. Here it's the `Hit Normal` returned by `Raycast`.
- The IOR ratio depends which two materials light travels through. Here it's `IOR of air / IOR of water`.

Because different materials have different IOR values, I added a custom IOR attribute to the water.
<br>
When `Raycast` collides with the water surface, it reads the water's custom IOR attribute when performing the division above.

<img src="images/causticnodes.png?raw=true" alt="Caustics nodes">

## [Mirror](mirror.blend)

Another example of using `Raycast` to distort a mesh.

[<img src="images/mirroranim.gif?raw=true" width="480" alt="Mirror demo">](mirror.blend)

Requires `Capture Attribute` due to [reasons described by Garek](https://developer.blender.org/T94218).

<img src="images/mirrornodes.png?raw=true" alt="Mirror nodes">

## [Explosion](explosion.blend)

Blender version of an effect originally made in Houdini.
<br>
Uses `Split Edges` to separate each face, then travels along the normal to move each face outwards.

[<img src="images/explosionanim.gif?raw=true" width="480" alt="Explosion demo">](explosion.blend)

## [Forest](forest.blend)

**WARNING:** This is slow because `Realise Instances` was needed to apply the materials correctly.
<br>
Requires Blender 3.1 or above due to `Vertex Neighbours` controlling the leaves shader.

[<img src="images/forestanim.gif?raw=true" width="720" alt="Forest demo">](forest.blend)
