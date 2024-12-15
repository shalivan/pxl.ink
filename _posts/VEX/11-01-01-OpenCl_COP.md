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