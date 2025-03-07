---
title: VEX expressions
description: Patterns, Expressions, Op()
categories:
 - VEX
tags:
- VEX
- Houdini
- Code
permalink: /vexpressions/
---
> Obsidian:  [[09-01-01-V_Attribs]] [[10-01-01-V_Syntax]] [[07-01-01-V_Strings]] [[05-01-01-V_Orientation]] [[03-01-01-V_Measure]] [[03-_V_Curves]]



https://vfxbrain.wordpress.com/


[SOP Vexpression.hiplc](/src/hip/SOP_Vexpression.hiplc)  


<!-- more -->

Hide UI element in HDA https://youtu.be/g5E4GYKlY18?t=589
Hide When : `{ input != 1 }`
-

checking if  @group_name == 1.



# Attirb


Visualize n-gons with VEX
```
if (primvertexcount(0, @primnum) > 4)
{@Cd = set(1, 0, 0);}
```
---

@ptnum == `npoints(0)-1`
or alternatively:

@ptnum == @numpt-1
If you happen to want 1st AND last point at the same time, you can use this expression:

@ptnum%(@numpt-1)==0


## Read



#### Read from other class

- `attrib` / `detail`/`prim`/`point`/`vertex`
- `point(0, 'foo', int pointnumber)` - Without existence check - These functions return the attribute value if the given detail/primitive/point/vertex exists and has the given attribute, or a zero/empty value otherwise.
- `pointattrib(0, 'foo', int pointnumber, int &success)` -
With existence check - distinguish between the attribute value actually being zero/empty vs. the function returning zero/empty value
- `attrib`
- `getattribute()` - more complex


#### Read form other input
```
vector value = point(1,"foo",@ptnum);
setpointattrib(0,"foo",@ptnum, value. "set");
```

```
f@attrib = f@input1_attrib;
```


## Write

- `setpointattrib(0,"foo",@ptnum, point(1,"foo",@ptnum), "set")`


# Expressions

- Backticks ``` ` ``` are for use in a string field: group input, name sop. (when fn inside ??) ``` `@ptnum` ``` - to get string name form nueric output.

- `Ctrl` + `C` - copying of node can be passed in parameters: `/obj/geo_foo/OUT_foo`. You can drag and drop nodes to param fields.



## Group field
Group field in every SOP


By points number pattern:
- `0 1 2 35-55` - by point / prim
- `npoints(0)-1` - last
- ``` 0-`npoints(0)-10` ``` - Leave last 9 points   
- ``` 0 `npoints(0)-1` ``` - First and last  


By attribute value:
 - `@shop_materialpath="/obj*"` - by material name attribute
 - `@name=NameAttrib*` - by name attribute
  - `@name="" ` - all without names
 - `@copynum==2` - delete copies after copie node
 - `@foo>=0.5`  - by Attribute

By pattern:
  - `group1` / `GroupName` - by group name -  work only on group  
  - `!GroupName` - work only on inverted group   
  - `!{group1 group2 group3}`
  - `!group1 !group2 !group3` - not group1 or not group2 or not group3 which would be everything except for elements that are in all groups
  -  `15 ^!first_half ^!first_ten` will exclude the 15, rather than acting like 15 ^!{first_half first_ten}
  - `@step_iter=2 ^!@happen_t=1` - "remove things from the previous statement (^) that are not (!) part of the following group".




## Float field


#### [Add] / [Transform]  SOP

- `detail(0,'P',1)` - get y component of position from detail attribute (which node, which attrib, which channel(z,y,z))
- `ch('sizey')/2` - reference to channel from same node (i.e: copy size from x to y)
- `ch('../xx')` ?? - ref to channel from node above (HDA interface/menu)
- `rand(3.3)`

## Int field
- `detail(-1,'iteration',0)%4` - loop 4 (spare)






#### [Switch] SOP
- `if (f@burned>0)`
- `if(strcmp(details(0, "foo"), "shit")==0, 1, 0)` - if value of detail attribute 'foo' is string of 'shit'.  [Use Switch-if]
- `npoints(-1)!=0` - switch if there is any geometry
- `if (npoints("../intersectionanalysis2/")>0,1,0)` - switch if intersected
- `if (detail(-1,'iteration',0)%2==0,1,0)` - switch even and odds

## String field


#### [Name] SOP
- ``` `detail(-1,"iteration",0)` ``` - name by iteration - get iteration number from spare parameter fn. for  [ForLoop] Meta Import



## Delete


#### [Blast] SOP

Group: 
`@primN.y=1` - add box, add normals, add blast with expression: `@primN.y=1`

#### [Delete] SOP

Delete by Pattern   

  - ``` 0-`npoints(0)-10` ``` - Leave last 9 points   
  - ``` 0 `npoints(0)-1` ``` - First and last   

Delete by Expression  
  - point delete: `@ptnum==@numpt-1` / `@ptnum==npoints(0)-1` / `$PT==$NPT-1` - Last     
  - point delete: `@ptnum%(@numpt-1)==0`  - First and last   
  - primitives: `prim(0, $PR, "intrinsic:closed", 0) == 1` -  Delete polygonal curves which could be translated into NURBS, and cause crash. (dlelet non selected on prims)   
  - `@copynum==2` - delete copies after copie node

Other delete check how it works:   
 - `if(@primnum==-1)` - points which are not a part of prim.

## Expression Field

#### [Partition] SOP
Rule
  - ```group_`@shop_materialpath` ``` - Make groups from materials  
  - ``` `@attrib_to_break` ```



#### [Group Expression] SOP
VExpression  
- `dot(@N,chv("XYZ")) > chf("Amount")``
- `neighbourcount(0, @ptnum)<=3` - By edges count from point    
- `rand(@elemnum) > chf("amount")` - Random Amount   
- `@Cd.r * chf("Amount")` - Color Amount   
- `@elemnum % chi("pattern")` - Modulo Pattern   
- `fit01(@ptnum % chi("modulo"),0,1)` - Modulo Pattern     
- `dot(@N,chv("direction")) > chf("amount")` - Vector Normal    
- `rand(float(i@piece)*.89461)<.5?1:0` - Group random conected pieces  (prims)    
- `@Cd.x > 0.5 && @Cd.x < 0.8`    
- ``` @ptnum == `npoints(0)-1` ``` - z bloga jakiegos  (last pt on curve )  
- `v@N.y<0` - add to group primitives with normal down.


#### [Attribute expresion] SOP

Vexpression:  
- `self` - pass Trough    
- `value` - set Value    
- `self * value `  
.
- `lerp(self, @opinput1_P, ch('amount'))` - morph with 2 input   
- `set(self.x, 0, self.z)` - flatten to z (vector)  
.
- `set(self.x, max(self.y, ch('level') + getbbox_min(0).y), self.z)` - Flatten P    
- `set(self.x, max(self.y, ch('level') + getbbox_min(0).y), self.z)` - Roatet Up N     
- `lerp(self, normalize(self-getbbox_center(0)) * ch('radius') + getbbox_center(0), ch('amount'))` - Spheryphy P  
.
- `@P - getbbox_center(0)` - Spheryphy N  
- `rand(@elemnum)`  
- `@opinput1_P` - second input position  


---


## Wrangle

- `if(@primnum == -1) @group_disconnected = 1;` - Separate points and geometry   (prims)
- `if ( rand(@ptnum) >0.2 ) { removepoint(0,@ptnum); }` - remove points
- `if (@Cd.r < 0.1) { i@group_mygroup=1; }` - change group on color
- `if ( rand(@ptnum) > ch('threshold') ) { removepoint(0,@ptnum); }`
- `i@index = (int)fit01(rand(detail(1,"iteration",0)*1234),0,11);` - randomise int in range. in prim wrangle
- ``` @manifoldnumber=`opdigits(".")` ``` - will delete group by digits in node name !!! (from Polydoctor SOP)  

---



# Operators


`geoself()`, `0`, `@OpInput1`- Returns a handle to the current geometry

- `opname(".")` - node name `'$OS'`   
- `opname("..")` - name of node Container   
- `opinput(".", 0)` -  name of the node connected to input 0  
- `opinputpath(".", 0)` - path of the node connected to input 0 (`/obj/geo/lastNodeName`)  
- `opinputpath("/obj/geo/null1", 0)` - path to the node conected to first input of null1              
- `opfullpath(".")` - returns the full path of a node   
- `oprelativepath("../sourcePath","../targetPath")` - Returns the relative path from one node to another      

##### Get param from node inputs
- `@P = point(1,'P',i@ptnum)` - ?? a gdzie channel jajk vektor ? << sprawdzic
- `@P = v@OpInput1_P` - get Pos from 2op.
- `point('opinput:1', 'P', i@ptnum)`  
- `point(@OpInput2, 'P', i@ptnum)` - is not 0 based !!  
- `v@Cd = vertex(1,"Cd",@primnum, vertexprimindex(0,@vtxnum));`
- `v@Cd = vertex(1,"Cd", @vtxnum);`

##### Get param from spare
- `point(-1,0,"P",0)`, `point(-1,0,"P",1)` `point(-1,0,"P",2)`- x,y,z point position from geometry referenced in spare field.
- `detail(-1,'iteration',0)` -

##### Get param from other node
- `point('op:/obj/geo1/OUT', 'P', i@ptnum)` - get position from OUT node   
- `point('op:../../OUT', 'P', i@ptnum)`- get position from OUT node   



### op:
`op:` operator is that it allows you to grab live data from another node elsewhere in your scene.
op: syntax is what you use when you're trying to use inline geo as a file-like object
basically if you need to dynamically cook something and return the result in place of something asking for a file, you use the op: prefix can also be done in texture-related VOPs to look up COPs in supported render engines
This will work as long as the data being fed in is the type of data the parameter the path to the node must be an absolute path starting from the root path:  
- `op:/img/img1/gamma1` - get texture in COPs/Imp. Put as image name  
- `op:/obj/cop2net1/OUT` - get texture from COP  
- `op:/obj/geo/MyNode` = ``` op: `opfullpath(“../../MyNode”)` ``` - For relative path use opfullpath    
- ``` point("op:`opfullpath("../../null1")`","Cd",@ptnum) ``` - Copy color from points of other node  
- ``` s@instancepath = sprintf(op:../../var_%s, VariantEnding); ```-


---





# Patterns
 Pattern may be a numeric pattern, attribute pattern, or group name pattern.
 - `?` -  Match any character  
 - `*` - Match any substring  
 - `^` - Exclude from match  
 - `[list]` - Match any of the characters specified in the list.  
 - `!*` - ????????????  
 - `a*`,`^aardvark` - Match any string beginning with a except for aardvark.    
 - `[abc]*z` - Match any string beginning with a, b or c and ending with z.    
 - `g*`,`^geo*` - Match any string beginning with g, but not any string beginning with geo.    
 - `^pattern` - Remove matching, `0-100:2 ^10-20` every other number 1 to 100 except the 10 to 20.  
 - `!pattern` - Every except the ones matching the pattern. `!1-10` means every except the numbers 1 to 10.   

### Points/primitives numbered
 - `n` - number n.   
 - `n-m` - from n to m (inclusive).   
 - `n-m:step` - from n to m (inclusive) skipping every step. Eg; `1-100:2` every other number from 1 to 100.    
 - `n-m:keep,step` - from n to m (inclusive). Use the first keep numbers and then skip every step after that.    
 .
 - `0-5000:2 ^ 40-200`  - range with wxceptions
 - `!50-200`   
 - `@P.y>0` - all points whose Y component is greater than   
 `0*/ $BBY>.9999`     
 - `@id=5-10`  
 - `@id="5 8 10 15"` - the attribute syntax //space separated list of integer values, need to enclose the list in quotes.
 - `@myattr=fooBar` - by name  
 - `@myattr="foo bar"` - quotation marks if it contains spaces   
 - `=`, `==`, and `!=`  - on string attr  
 - `(* and ?)` -  wildcards value when using   
 - `{arm* ^arm3*}`  - in the pattern. includes all groups whose names start with arm, but not arm3.   

---


### Channels/Parameters

`ch()` -  channel reference
`chf()` - float  
`chs()` - string  
`chi()` - int  
`ch3()` - matrix3  
`chramp()` - rampo  f@Cd = chramp('Cd',rand(@ptnum));   - noise ramp
`chop("../chops/OUT/chan1")` - get chop channel    

#### Rampkeys:  
```glsl
int rampkeys = chramp("ramp");

for( int i=i; i<=rampkeys; i++){
    float pos = ch(sprintf("ramp%gpos", i));
    float val = ch(sprintf("ramp%gvalue", i));
}
```

 you can interact with ramp keys just like a multiparm block. The ramp parameter itself has the value of how many keys there are:
```
c int rampkeys = chramp(“ramp”);
for( int i=i; i<=rampkeys; i++){ float pos = ch(sprintf("ramp%gpos", i));
float val = ch(sprintf("ramp%gvalue", i)); // Do stuff }
```
@flight404 (I normally don’t condone 1-based loop indices but the keys do start at 1 and not 0. I supposed you could switch to doing `i+1` in the `sprintf` calls though if you wanted)  


---





``` $HIP/`opname("..")`/cache/sim_`opinput(".", 0)`/`opinput(".", 0)`.`$F+1`.bgeo ```  -  name from upstream node input0 with previous frame  




---

# H script

- `$F3` - int frame with `padzero(5, $F)`- pad0    
- `$FF` - float frame   
- `${F}` - The current frame, (as set with the Playbar controls)   
- ``` `$F+1` ``` - Next frame   
.
- `$N` - Old number of points `npoints(0)`  
- `$OS` - `opname("..")`- for container name    
.
- `$FSTART` - start frame, `$FEND` - end frame  
.
- `$T` - Current time, in seconds `f@Time`  
- `$ST` - only present in DOP contexts `f@SimTime` - Float simulation time   
- `$SF`- only present in DOP contexts `f@SimFrame` - Float simulation frame    
- `1/$FPS` - `f@TimeInc` - Float time step   





### Textport
HScript Textport

- `exhelp` - and fn.  
- `help`
