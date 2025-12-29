---
title: GLSL
description: Syntax
categories:
  - VEX
tags:
  - GLSL
  - Shaders
  - Rendering
  - Code
  - RealTime
  - GameDev
---
> PxlInk:
> Obsidian:  [[11-01-01-HLSL]] [[09-01-01-U_Shaders]] [[15-01-01-Shading]]


[Junichiro Horikawa](https://www.youtube.com/watch?v=tksYIBRcylU "https://www.youtube.com/watch?v=tksYIBRcylU")
[Ultimate Copernicus Guide](https://youtu.be/ZPL215vfNwg?t=13209)


#### Signature
Source and destination (src, dst) like input and output 
if not optional context error becausre it need input 


Code run by kernel

- layer - input 
- pararmeter - param 
```c
#bind layer src? val=0 // if no input use val 
#bind layer !&dst // only outputs 

// coding
@KERNEL 
{
	{@dist.set(@src)} 
}
```


```
@KERNEL 
{
// gradient on screen
float xgrad = (float)@ix/xres; // cast to float
float xgrad = 1.0f*@ix/xres; 
}
```


```c
@KERNEL 
{
// gradient on screen
float xgrad = (float)@ix/xres;
float ygrad = (float)@iy/yres;
float zgrad = max(xgrad/ygrad);
value = sin((value+Time)*45)   // need to include time in block
@dist.set(value);
}
```


```c
#bind layer src // source is mandatory 
#bind layer !&dst // only outputs 

// coding
@KERNEL 
{
	{@dist.set(@src)} 
}
```

 when you bind an attribute like P, it passes it as a fixed size array it can be changed size outside the kernel but not within it

```c
// Shared in global workgroups 
global int x = 0; 
// Shared in local workgroups 
local int x = 0; 
// Only in this kernel 
int x = 0;
```
2. opencl and C follow the same general design for the most part
    though there are some extra stuff in opencl like vector types (float3, float4, float16 etc)
    for multidimensional stuff one example is mat3 (edited)
    they are represented as an array of float3 (edited)
    
    
Noise in OCl
```c
// Bind writable position:
#bind point &P float3
#include <mtlx_noise.h>

@KERNEL
{
    float3 pos = @P;
    pos += mtlx_noise3d_3((float3)(1.0f), (float3)(0.0f), pos*(float3)(3), (int3)(10)) * (float3)(.2);
    @P.set(pos);

}
```
http://www.dmi.unict.it/~bilotta/gpgpu/notes/11-opencl.html