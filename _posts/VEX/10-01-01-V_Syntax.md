---
title: VEX
description: Syntax
categories:
  - VEX
tags:
  - VEX
  - Code
  - Houdini
permalink: /vex/
---
> Obsidian:  [[08-01-01-V_Expressions]]  [[09-01-01-V_Attribs]]  [[07-01-01-V_Strings]] [[05-01-01-V_Orientation]] [[03-01-01-V_Measure]] [[03-_V_Curves]]



<!-- more -->


**VEX** - is not indented language, and is written for a specific context.  
**CVEX** - VEX code that runs outside a context. CVEX doesn’t have predefined variables, since it is just a program that Houdini calls with certain arguments (usually corresponding to points or data on points).

Geometry editing by speed: `Houdini node` > `VOP` > `compiled blocks` > `VEX` > `python`

# Wrangler

**Attrib Wrangle** - CVEX-context  more generic and the trend seems to be steering away from sop/pop specific nodes. wrapper around the more generic "attribvop" sop.   Attrib Wrangle/VOP and other CVEX nodes like Geo Wrangle DOP, POP Wrangle DOP, Volume Wrangle...) and their VOP equivalents node set to run over Detail (only once) addprim() addpoint() addvertex() removeprim() removepoint() (There is no removevertex() functiononly Attribwrangle you can add geometry (points, prims etC), which you can't in a point wrangle.  Also the functions to access geometry are different

**Point Wrangle** - wraps around a vopsop which provides a bit more data to vex in order to qualify it as "vop" context (still some functions  unique to Point Wrangle)

## Data types

|variable | | ||
|--|--|--|--|
|`float` |`f@` |  float  |**Default data type**|
|`vector2` |`u@` | 2 floats  ||
|`vector` |`v@`  | 3 floats   ||
|`vector4` |`p@` |  4 floats  ||
|` int` |`i@` | integer ||
|`matrix2`  |`2@`  |2×2 floats||
|`matrix3` |`3@`  |   3×3 floats||
|`matrix` | `4@`  |  4×4 floats| `4@transform = matrix(ident());`|
|`string` | `s@`   | string |`s@myString = "abc";`|

### Reserved Keywords

`break`, `bsdf`, `char`, `color`, `const`, `continue`, `do`, `else`, `export`, `false`, `float`, `for`, `forpoints`, `foreach`, `gather`, `hpoint`, `if`, `illuminance`, `import`, `int`, `integer`, `matrix`, `matrix2`, `matrix3`, `normal`, `point`, `return`, `string`, `struct`, `true`, `typedef`, `union`, `vector`, `vector2`, `vector4`, `void`, `while`  

# Precedence

### Arithmetic
`=`, `==` (same as), `!=`, `>`,` <`, `>=`, `<=` , `+=`, `++` - add one , `%` - modulus  

### Conditionals

`==` - equal,`!=` - is not equal    
`a ~~= b` - equivalent to `match(a, b)` strings      
`!` - Logic negation  
`||`- Logic OR  
`&&` - Logic AND  


# Functions
```cpp
int fnName(int a, b; string c)
{
    int c=0;
    c = a*b;
    return c;
}
```

```
// call fn:
int foo = 1;
@bar = fnName(foo, @ptnum);
```
Function that return array:  
```cpp
function int[] poo(){
    return {5};
}
```

```
/ call fn:
i[]@t = poo();
```

# Conditioning


Standard conditioning
```cpp
if(b<a) {
    s@foo = "true";
}
else if(b=a){
    s@foo = "equl";
}
else {
    s@foo = "false";
}
```

Standard conditioning, but no brackets
```cpp
if(b < a)
    s@foo = "true";
else if(b=a)
    s@foo = "equl";   
else
    s@foo = "false";
```

One liner  
```cpp
if(b<a) s@foo = "true";
else if(b=a) s@foo = "equal";
else s@foo = "false";
```

Ternary conditional (short version):  `(condition) ? true : false`. use logical operators: `&&` (AND), `||` (OR).

```cpp
@P.y *= (v@P.y > 0) ? ch("ValueAbove") : ch("ValueBelow");
```
```cpp
@foo = (@ptnum <= 0 || @ptnum >= (@numpt-1)) ? 1 : 0; // Color first and last point
```


# Loops

`i@numiterations` - The expected total number of iterations
`i@iteration` - The current iteration number, always starting at 0 and increasing by 1 each loop.
`f@value` - In piece-wise loops, this is the current value of the attribute
`i@ivalue` - In simple repetition, this is an integer version of value.

### For
Do for x times

```cpp
int a = 5;
for (int i=0; i<13; i++) {
    a *= 5;
    if (a > 10000000) break;
}
i@a = a;
```



### ForEach
Iterate over array elements

```cpp
v[]@colors = { { 1,0,0} , {0,1,0} , {0,0,1} };

foreach(vector x; @colors)
{
   if (x == {1,0,0})
    {
       @colors[0] = set(rand(@ptnum+123),rand(@ptnum-1),rand(@ptnum+42));
    }
}
```



### While
Until condition

change colors of nearby points from 2 op.
```cpp
float rad=ch('radius');
int  maxpt=10;
int handle;
vector foo;

// cloud open
handle= pcopen(@OpInput2,"P",@P,rad,maxpt);

while(pciterate(handle)) //return one until point is valid
{
   pcimport(handle,"Cd",foo);
   @Cd = foo;
}

```


`break` keyword - can stop the loop at any point  

`continue` keyword to jump to the next loop iteration. in this example we average point position with positions of neighbours which are above it in world space (their Y coordinate is larger)  

# Arrays

`array()` - Efficiently creates an array from its arguments.  
`int fooArray[] = {};` - Array variable    
`int fooArray[] = array(1,2,3,4); ` - Array variable      
`i[]@fooArray = {-1,0,1};` - Array attribute    
`i[]@connected_pts = neighbours(0, @ptnum);` - Array attribute   



`i@firstItem = numbers[0];` - Reading from arrays    
`vector fooArray[] = v[]@fooArray; ` - Load array attributes into local var      

`numbers[0] += 1;` - Add value to [0]   
`i@fooArray[1] = @primnum;` - Set primnum in array[1]       

`getcomp()` - Gets the value of an array component, the same as array[num].    
`setcomp()` - Sets the value of an array component, the same as array[num] = value.    

##### Slice
`i[]@firstHalf = numbers[:2];` - Slicing   
`i[]@secondHalf = numbers[2:];` - Slicing   
`i@secondLastItem = numbers[-2];` - Indexing can also go backwards   
##### Add Remove   
`push(numbers, i@returnedPopVal);` - Appends element to the array   
`removevalue(i[]@fooArray, ValueToRemove); `   

`pop(i[]@MyArray, IndexToRemove)` - -last item from the array (decreasing the size of the array by 1) and returns it.    
`push(@MyArray, ValueToAdd)` - Adds an item to the end of an array (increasing the size of the array by 1).   
`resize()` - Sets the length of the array. If the array is enlarged, intermediate values will be 0 or "".      

##### Search
`i@lenghtOfArray = len(numbers);`  `len()` - -length of an array.    
`find(i[]@MyArray, ValueToFind)`      



##### Serialize
`serialize()` - Flattens an array of vectors or matrices into an array of floats.    
`unserialize()` - Reverses the effect of serialize: assembles a flat array of floats into an array of vectors or matrices.



Other fns works with arrays:  
`min()`
`avg()`
`spline()`
`import()`
`addattribute()`
`metaimport()`



#### random item using ptnum  

```cpp
string array[] = ['A','B','C'];
s@letter = array[fit(random(@ptnum,0,1,0,21)];
```

in specific frames


```cpp
int frames[] = {2,4,10,11};
if( find( frames, @Frame) >= 0){
}
```



#### Flattening an array of vectors and reverting it

```cpp
vector vectors[] = { {1,2,3}, {4,5,6}, {7,8,9} };
f[]@serializedVectors = serialize(vectors);
v[]@unserializedFloats = unserialize(f[]@serializedVectors);
```

#### lerp arrays

```cpp
function float[] array_lerp(float array1[]; float array2[]; float amount)
{
    int count = len(array1);
    float result[];

    for (int i=0; i<count; i++)
    {
        float cur_result = lerp(array1[i],array2[i],amount);
        append(result,cur_result);
    }
    return result;
}
```

`neighbours()` - An array-based replacement for the neighbourcount/neighbour combo. Returns an array of the point numbers of the neighbors of a given point.  


# Matrices
Array of arrays  
intilize a vector  

```cpp
float   f = 0;
vector  v = set(f,f,f);
matrix3 m = set(f,f,f,f,f,f,f,f,f);
        m = set(v,v,v);

```
```cpp
float f = getcomp(m,0,0); // read the value
```


# Structs


# Include
```cpp
#include "math.h"
```
Import files from:  
`$HIP/vex/include`   
`$HOME/houdiniXX.X/vex/include`    
`$HH/vex/include`    


-----
https://www.pragmatic-vfx.com/
