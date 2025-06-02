---
title: SOP

categories:
 - HOU
tags:
- Houdini
- SOP

description: Curves
permalink: /sopcurves/
---


To preserve curve direction u must preserve vertex order.

---


# SOP

- `curve` node

----



#### Cut on point
- `Poly Cut` | can cuts only on points (destroy point groups but retain primitive)
- `Convert Line`  |   Redraw primitive  (destructive for groups & attributes)   - can use `Poly Cut` with: `*` in `Cut Points`, and `Cut` in `Strategy` .
- `Poly Path` |   Redraw primitive (destructive for groups & attributes) - can use `Poly Cut` with: `*` in `Cut Points`, and `Cut` in `Strategy` . Then: 'Clean' with: [v] 'Consolidate Points' and 'Fix Overlaps'

#### Redraw
- `Refine`
- `Resample` | Redistribute point and attribs alobg the spine (blend attribs)
- `Carve` | (will disconect points ! )
- `Fuse` |

#### Inject edge where is no point  
- `Boolean`
- `Poly Split`
- `Clip`
- `Knife`
- `Intersection analysis`
- `Incrementersection stitch`

#### Labs tool
-  `Poly Slice` make points on curve or prim > slice / preserve edge group & curve dir. snap.   
  Based on:
   - poly split  
   - boolean (faster)
- `Merge Splines` - with specific conditioons.
- `direction ???`
- `Poly Wire UV` !!!! - <<<

# NURBS & B splines

[Be More Moog: Tool Design That Empowers Users | Richard C Thomas | Games Workshop](https://youtu.be/6BAtzdMGnwA)    
[Advanced Road Generation | Erwin Heyms | Games Workshop](https://youtu.be/G5Iq-jxgZn0)  
