---
title: Modeling - Vegetation
categories:
  - ART
tags:
  - Art
  - 3D
  - CG
description: Vegetation, foliage
permalink: /foliage/
aliases:
  - foliage
---
> [Color](/color/)  [Modeling](/modeling/)  [Sculpting](/sculpting/) [SpeedTree](speedtree)

{% comment %}
 >Obsidian: [[21-01-01-Art]]   [[17-01-01-SpeedTree]]  [[17-01-01-Modeling]], [[17-01-01-Modeling_Foliage]]  [[18-01-01-Color]] [[16-01-01-Sculpting]] [[14-01-01-Procedural]] [[08-01-01-Material]]  [[20-01-01-VisualDesign]] [[17-01-01-Paint]]  [[14-01-01-Procedural]]  [[12-01-01-LevelDesign]] 
{% endcomment %}

# Vegetation modeling

## Technical pipeline

We need `parts` which we will combine into `objects`. then objects will be used in `composition`.

### Complexity Level
By complexity
- Grass - Simplest
- Weeds - Blossoms, seeds
- Bushes - Complex leafy canopy, hierarchical branch structure
- Trees - Defines silhouettes
- Hero Assets - Sculpted, complex canopy

By Quality
- Stylized
- Natural Real

# References
## References

- Characteristic
    - References:
        - [Foliage Library](https://treelib.ca/)
        - [Plantnet.org app for identification](http://www.plantnet.org/)
        - For trees, use references without leaves to see branch structure
    - Silhouettes
        - Various sizes and shapes (grass, plants, bush, tree)
        - Negative spaces
        - Slightly noisy
        - Organic and interesting from any angle
    - Clustering - clusters of leaves
    - Characteristic Elements: 
	    - Ecosystem-biomes, Leaf band, Beginning, Gravity, Grouping (higher leaf implies more vertical shape change) Age decay processes which might alter their appearance
    - Characteristic Behavior:
        - Reproduction method (seeds, spores, cuttings) that influence growth patterns and distribution in different environments.
        - New tree growth requires light, leading to competition in young and middle-aged forests, potentially leaving no space for new trees
        - Non-vascular plants grow in shadows to retain moisture
        - Moss predominantly faces north in the Northern Hemisphere
        - Growth towards the sun
        - Stress or disease which can alter the visual characteristics of plants, like leaf discoloration or unusual growth patterns.
    - Biome-specific plant adaptations:
        - In gardens, plants are clean
        - Standalone plants are wide; forest plants make space for others, influenced by surrounding flora
        - drought resistance or tolerance to different soil types.
        - interact with other species (both plant and animal) in an ecosystem, like symbiotic relationships or as habitats.
        - weather climate
    - Natural Shapes: 
	    - Thickness follows Leonardo DaVinci's constrain
	    - Size of leaves should be natural. 

## Concepting

- Planning
    - Biomes come first (big picture)
    - Define biome identity > determine necessary plants > identify use cases
    - Silhouette readability is crucial but should be generic for repetition
    - Environmental factors like wind or wet soil define biome identity; roots can help ground assets
    - Leaf scale and texel density - avoid scaling to maintain weight and density

- Foliage Structure
    - Leaf Morphology
        - Conifer
        - Broadleaf
            - Venation types on leaves (parallel on grass)
            - shapes (e.g., oval, lanceolate, palmate) and margins (e.g., smooth, serrated).

    - How leaves connect to branches
    - Frond references for replicating branch structure
    - Trees' appearance can vary, and bark structure may change over time

# Modeling

Methods for Foliage Production:
- Past: Direct modeling, L-Systems, self-organizing models
- Present: Skeletonization, Photogrammetry, Simulation
- Future: LiDAR, AI, Single View reconstruction, L-Systems

  
## Atlas

### Leaf Atlas 
Texture atlas with elements for creating clusters, not used in-game:
- Scanning:
    - Leaf on a lighting table (lit from below for translucency), use 15mm prime lens; flatten with a book to avoid self-shadowing.
    - Take 6 pictures with light at different angles, clockwise, keep alignment perfect.
- Sculpting
- Node Material (similar to Substance Designer)

### Leaf Cluster Atlas 
For combining and attaching elements, crucial for the creation process; can be made in tools like SpeedTree:
- Components from leaf atlas:    - Main bare branch    - Bare branch extender    - Main leafy branch    - Filler branch x2    - Extender branch x2    - Single leaf    - Fruits    - Bark strip
- Cutout leaves

## Branches

Leonardo da Vinci's Constraint:
- The combined cross-sectional area of branches at any point should approximate the area of the trunk or parent branch. This aids in maintaining structural integrity and balance.

Branch Structure:
- Figure out branch structure: Understanding where to switch from branch geometry to card geometry.
- [YT Eric Wiley Substance atlas](https://youtu.be/5uqVlDlg3yo)


## Modeling 
Speedtree
- branch transition - additional band with alpha


## Variants



# Material 

#### Bakes 
 - Derive thickened and subdivided model from low poly.
  - Material id's for parts

**Painting**
  - Spots with color variations (some blurry)
  - Use also sharp lines
  - Paint masks: sss,
  - Veins and celular patterns
  - Vines to subsurface mask!

- color
    - fuzzy shading
    - blend with landscape layer or use landscape layers as a mask
- normal
    - to camera ? bottom up ?  
    - rotating normals towards camera instead of pointing them up, is a good supplement to unify grass shading, while not causing uniform ugly white sheen
    - if tangent space normals are enabled in material, your normal will be flipped for backface. While it is desired behavior for grass cards with default normals,
    - if you are using foliage with edited normals, the backfaces will have incorrect normals. Using foliage with edited normals implies disabling disabling tangent space normals and handling normals yourself in the material using two-sided sign.
    - You’d want every grass blade to have some sort of distinct specular highlights, preferably corresponding to grass blade orientation, supported by normal map. (not pointing grass normals straight up)
    - normal map is in use, it also helps if its intensity is high enough to shift surface-subsurface balance from card level to grass blade level.
- vertex anim **movement**  
    - rotate on slopes to have grass pointing up all the time !!!
    - wind and interaction, bend grass near player
    - wygiac przy playerze cardsy troche do kamery  
    - scale anim and size on distance to betere disappear LOD
    - scale grass down on last lod
    - how fast move depend on scale `smooth ramp =x*(in+1))/(x-in)`
- sss  (Subdermal maps)
    - SSS color should not differ considerably from albedo.
    -  SSS is obtained by sampling environment cubemap in the direction, opposite of the normal. If your grass cluster normals are pointing upwards, they will sample the skylight from bottom part. Needless to say, that if skylight is set to use black for lower hemisphere, you won’t get any subsurface from indirect light.
	- Rendering: SSS for foliage is using gausian method: vec3 sss = exp(-3 * abs(NdotL) / (radious + 0.001)); while skin is using exponential method. There are other methods like: ray tracing / screen space 
	- https://youtu.be/wfPoVnBFv-0
- - off specular on bottom 
- shadows ... ?


# Animation 


# Composition and Placement 
  - Cluster foliage, procedural placement system



**Lighting**
  -  balance between skylight and directional light intensity. In case, when latter is overly strong, there will be distinct separation between zones of dominant subsurface and surface It feels that tweaking subsurface intensity separately for direct and indirect light we pretty good thing to have, but this one would be only tweakable per light, not per material.

- use shadow, ? without can be smoother.



# Optimization

  - 2 sided foliage option
  - Early z pass 
 - LODs

----------------------




# Foliage


#### Grass
#### Fungi

#### Roots 

#### Trees

#### Moss

'Lot more porous, with amassive amount of self-shadowing, ambient occlusion, and transmitted light. The moss itself tends to have a lighter color at the tips than deeper towards the base. And there’s a strong viewing angle dependency – when viewed straight on, you can see down into the shadows between the fibers, and while viewed from an angle, only the tips are visible.'




---

# Tools

Available tools for foliage creation: 2023
- SpeedTree https://www.youtube.com/c/SpeedTreeMiddleware
- H GrowInfinite 1.2.19  https://fxmode.gumroad.com/l/GrowInfinite  
- H Simple Tree Tools 2.6    https://www.youtube.com/watch?v=0VqA99bpGHc
- H Labs https://www.youtube.com/watch?v=IZ5uJYg0ELM&list=PLXNFA1EysfYkiIWvM3CBXO-TsYE1H42dK   https://www.sidefx.com/tutorials/tree-generator/
- B The Grove3d  https://www.thegrove3d.com/releases/the-grove-release-6/ Blender  https://www.thegrove3d.com/
[houdini tree HDA](https://youtu.be/abQtNpUUdGw)
- Houdini pegasus tools - procedural sim 


-----------------


# Houdini Pegasus foliage 


4 types of nodes: 
- control
- component 
- switch 
- solver 


---


Bruno Moulia

> Book history : natural design of nature - computer generated plants and organics Oliver Deussen, Bernd Lintermann


# Links

[YT Foliage workflow](https://youtu.be/wGvCy-Yai9A)
Houdini rocks
https://youtu.be/2kDSsbrFEKw
Water Single Layer 
https://www.artstation.com/blogs/rovana_c/poGo/water-shader-single-layer-material
Map 
https://www.youtube.com/watch?v=sZWD9bud-gk
https://www.youtube.com/watch?v=uQNND6ShfqQ
https://www.youtube.com/watch?v=eueGP4SIgGo
https://youtu.be/onTfg05yeyw                                   

Modeling
- [Modeling high plands](https://www.exp-points.com/sven-mren-foliage-study)
- [TexturesCom tut](https://www.textures.com/tutorials/double-sided-leaves-modelling)
- [YT Houdini # Speedier Trees in Houdini: Botanically inspired production ](https://www.youtube.com/watch?v=e8ITnlrcvcQ&t=1709s)
- https://www.youtube.com/watch?v=P7lZ-D-Fkus&list=PL-169OEn7ZLXkprHiKwS6rOW_UrJCAvxO
-  https://www.artstation.com/artwork/qQVZqR
Wind
- [Ghinish technique playlist 1 wind & 2 grass](https://www.youtube.com/watch?v=P7lZ-D-Fkus&list=PL-169OEn7ZLXkprHiKwS6rOW_UrJCAvxO)
- [pt 3 using blender](https://youtu.be/BFnwkBv19TA)
- [RT flowmap dynamic grass](https://www.raywenderlich.com/6314-creating-interactive-grass-in-unreal-engine-4)
- https://youtu.be/MKX45_riWQA  Interactive Wind and Vegetation in 'God of War'

FOLIAGE: 
Set custom foliage data 
repleace with skeletal
https://youtu.be/JvX-BRmqlr8?t=921
https://www.youtube.com/watch?v=vXalfRAnXak&list=PLVCUepYV6TvPYbofpEf_ghznfihM-yt-B


