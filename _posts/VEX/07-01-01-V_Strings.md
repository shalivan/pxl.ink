---
title: VEX Strings
description: RAW
categories:
  - VEX
tags:
  - VEX
  - Code
  - Houdini
permalink: /strings/
---
> Obsidian:  [[08-01-01-V_Expressions]] [[09-01-01-V_Attribs]] [[10-01-01-V_Syntax]] [[05-01-01-V_Orientation]] [[03-01-01-V_Measure]] [[03-_V_Curves]]

### Strings


- `atof()` - converts a string to float
- `atoi()` - string to int
- `itoa()` - int to string



i@xxx222 = rint(opdigits(s@shop_materialpath));


```
### to String
##### Float

` ; ` - name from class nad string    
`sprintf("%s %d", "piece", @ptnum)` - from string and ptnum  
`sprintf("_%03d", @ptnum)` - set ptnum as a 3 digits number (001, 002)    
`sprintf("%08.3f", value)`- padding and number of decimal points it will round to

`printf("P = %g, dot(N, P) = %g, %d = %x\n", P, dot(N, P), ptnum, ptnum);`  
`printf("RGB = { %g,%g,%g }\n", clr.r, clr.g, clr.b);`  
`printf("P = %20s\n", "20 chars");`  
`printf("%-+20s\n", "Left justified and quoted");`  
`printf("%+08.3g\n", velocity);`  
`printf("%*.*g\n", width, precision, value);`  
`Cf = texture(sprintf("/maps/map%d.rat", i));`   
`Cf = texture(sprintf("/maps/map%04d.rat", i));`  

##### Int to string

`s@name = "piece"+itoa(i@class);` - Name from class attrib. (Connectivity sop)   
`s@name = "packed_prim"+itoa(@primnum);` - Name from packed primitive number   
`s@name = "say_my_name"+itoa(nearpoint(1,@P));` - Closest point to this primitive   


### from String

opdigits("oriev548.hip") << return 548...





##### -
`s@name = point(1,"name",nearpoint(1,@P));` - Get point attrib from the closest point   
`@i = match("name", s@group);` - check if string match attrib  >> `match(a, b)`  - short: `a ~~= b`    
`if (match("/obj/.../texture_material", s@shop_materialpath)) @group_mygroup = 1;` - if material

###  Strings Operations
`s@[]pathsplith = split(path, "/")` - splits the string in pieces based on the "/"  
`@newpath = join(pathsplit, "_")` - merges the elements of an array with "_"   
`@filename = pop(pathsplit)` - removes the last element from the array and addign to new var  

`@name = string[0:1];` - H
`@name = string[0:1];` - Hello worl
```
