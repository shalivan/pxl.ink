---
title: Niagara
description: Paradigm
categories:
  - PXL
tags:
  - Unreal
  - VFX
  - Rendering
  - HLSL
  - Niagara
  - RealTime
  - GameDev
  - NodesGraph
permalink: /niagara/
aliases:
  - niagara
---
> Obsidian: [[16-01-01-VFX|VFX]] [[04-01-01-U_Niagara|Niagara]]

# Project Setup

https://drive.google.com/file/d/1I4dglPjeXLcNkSGxGok8sQCy59qgYcF9/edit

- /Edit /Project Settings /Collisions /Trace Channels Name = `FluidTrace`, Default Response = `Ignore`
- enable "UV from Hit" engine feature

### Project Basics
- Ninja folows points, socets, bones - not shapes 
- can corelate materials with tags


---


# Effect Types




## Aera FX
Embed component to `ninjaLive Actor`
- give you **interaction volumes** that help with sim activation > registering overlapping obj > component is capturing pivot bone or point. 
- simulation plane is trace mesh itself > to painter > to sim 
## Character FX
Add to movable actor like pawn. Cannot relay on interaction volume. We have user defined list instead.  And continuous interaction. 
- user defined component > projecting to trace mesh 
- texture offset automate (but default is ok)

## Traces types
`Camera` to `Camera facing plane` > behave like a billboard
`Camera` to `Fixed Pland` > Project form cam
`Fixed Point` to `Fixed Pland` > Project from top 

## Global Sim 
- active / deactivate 
- attach to player 



# Buffers
Temporary storage of data 

- Render buffer > render targets 
- Velocity  > foliage
- Density > bump 
- Pressure >  can derive normal
### Buffer Method
- **Render targets expose** > external render targets  assets (created manualy) < easy acces and can read rt like textures 
- **Direct Drive** - Primary / Secondary material that is applayed with tags  (internal RT) 
 



---
- `Generate overlap events ` Set in Mesh :  Colision

# FluidNinja Actors/Components 



##  NinjaLive Component
- all params there 

	- Live Activation 
	- Live Interaction 
		- Continous interaction component name - z czym interaktwac 
		- Overlap obj inclusive type > list  
		- Track actor primitive component with tag ! 
		- [ ] Camera Facing 
		-  single target mode - to interpolate  points nicely
	- Live Brush Settings 
		-
		


### Activation / Interaction Volume 
- optimise 









### Trace mesh Component 

----


Setups: 
- Simulation should be always World (level main axies)/Screen Align (Not rotating !!!)
- ![[Pasted image 20241108171941.png | 300]]
- texture offset   (world space offsset - help build large scale ) essential for implementing small local sim limit to map into infinite surface 
- ![[Pasted image 20241108172856.png | 300]]



---
v

# Preset manager BP  

- can add to scene to test 
