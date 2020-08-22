
---
layout: default
title: Syntax
parent: VEX
---


### Read Attribute
`@foo = v@P[0]` - Fetch 'x' position   (Can also use .x, .y, and .z  [0], [1], and [2] index)  
`@foo = v@opinput1_P` - Fetch attribute from second input  
`@foo = point(1, "Cd", @ptnum)`; - read point attribute from second input (older than wrangles, those don't use @'s)  
`@foo = prim(0, "string_attribute_name", @primnum)` - read primitive attribute from point wrangle     
`@foo = details(0, attribute)` -  Fetch from detail string    
`@foo = detail("../repeat_begin1_metadata1/","iteration", 0)` - get iteration number      

##### in expressions:   
`detail(-1,"iteration", 0)` - get iteration number from spare parameter fn for   


### Attribute from Group (0/1)
`i@foo = @group_bar;` - store group 'bar' in attribute 'foo'  
`i@foo = (@group_bar==1) ? 1:0;` - using if statement  
`i@foo = inpointgroup(0, "bar", @ptnum);` -  in Point group     
`i@foo = invertexgroup(0, "bar", int vertexnum)  ` - in Vertex group          
`i@foo = inprimgroup(0, string groupname, int primnum) `- in Prim group    

```glsl
if (@group_bar==1)
  @foo=1;
else
  @foo=0;
```
```glsl
int ingroup = inpointgroup(0,"bar",@ptnum);
if (ingroup == 1)
   @foo=1;
else
   @foo=0;
```

```glsl
if(inprimgroup(0,"barA", @id) == 1 && inprimgorup(0,"barB", @id)){
  @foo=1;
 }
 else if(inprimgroup(0,"barA", @id)){
  @foo=0;
 }
```



###  Group by Attribute value
`Partition SOP` - can create grups by rule  
`if (@P.x>0) i@group_bar = 1;` - Add to group by attribute treshold     
`if (match("*box1", s@objname) == 1) @group_bar = 1;` - Add to group if strings mach   
`setpointgroup(0, sprintf("points_%g", (@ptnum + int(rand(@ptnum)) % ch("num_groups") ), @ptnum, 1, "set");` -   




### Create Group
##### by normal
```
vector up = set(0,1,0);
vector N = v@N;
float angle = acos( dot(normalize(up), normalize(N)));
angle = angle/(3.14/180);
if(angle<chf("threshold")){
        @group_bar = 1;
}
```

### Group Operations

`expandpointgroup(int opinput, string groupname)`   





### Casting

#### Class
`(float)foo` - cast to float  
`float(foo)`  - cast to float  
`vector(foo)` -  `v@foo = dot(v@N,normalize(vector(rand(@ptnum)))) * 0.5 + 0.5;`    

`s@foo =  itoa(i@number)` - Int > String   
`f@foo =  atof(f@number)` - String > Float (0.0 if the string does not contain a number)    
`i@foo =  int(rint(f@float))` - Float > Int        

`hsctorgb()`  
`rgbtohsv()`  
`rgbtoxyz()`  
`zyztorgb()`  

`serialize ()`  
`unserialize()`  

#### Conversion
`Cd = Cd.zzy;` - swizzle  

### Transfer
#### Detail > Points (point wrangle)
Import `detailarray` as a local point array.
(If any array element modulo of 2  is equal to zero,
point with the same number is colored.)
```cpp
int importarray[] = detail(0, 'detailarray');
foreach(int i; importarray)
   {
   if(i%2 == 0)
      {
      setpointattrib(0, 'Cd', i, {1,0,0});
      }
   }
```
#### Points > Detail (detail wrangle)
Iterates over the geometry points, reads their positions  and puts each value into a detail array   
```cpp
v[]@myarray;

for(int i=0; i<@numpt; i++){
   vector item = point(0, 'P', i);
   insert(@myarray, 0, item);
   }
```
```cpp
int npt = npoints(0);
vector importarray[];

resize(importarray, npt);
for(int i = 0; i < npt; i++) {
    importarray[i] = point(0, "P", i);
    }
```
#### (point wrangle)
Export every point to one detail array
```cpp
int point[] = array(@ptnum);
setdetailattrib(0, "points", point, "append");
```
https://andreasbabo93.wixsite.com/sbabovfx/useful-vex-and-expressions             
http://mrkunz.com/blog/08_22_2018_VEX_Wrangle_Cheat_Sheet.html






### Accumulate
<img align="left" width="100" height="100" src="">

```cpp
f@accusum = 0;

for(int i=0; i<@numpt; i++){
    @accusum = @accusum + point(0, 'mattemp', i);
    @testloopcount += 1;
    }

for(int j=0; j<@numpt; j++){
    setpointattrib(0, 'accu', j, @accusum);
    }
```

Collect in detail attrib:
```cpp
vector p[];
p[0] = v@P;
setdetailattrib(0, "pArray", p, "append");
```