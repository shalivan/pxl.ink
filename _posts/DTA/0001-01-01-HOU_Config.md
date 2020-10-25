---
title: configs Houdini

categories:
 - DTA
tags:
- CG
- Houdini
- Shortcuts
- Configs
description: .
permalink: /houdiniconfigs/
---

[Config folder](/src/configs)  

[Desktop](/src/configs/Hou/desktop/AB.desk)  

[Radial Menu](/src/configs/Hou/radialmenu/ABModeling.radialmenu)  

[qLibDarkFlatTheme](/src/configs/Hou/config/qLibDarkFlatTheme.hcs)  


```
I saw new polybevel state, that is what i was trying to say about modeling state.  What it lack is:
-  quick button for 'accept and enter selection'
- use same shortcuts in all modeling relateing nodes.

- better selection 9
- try to use transform instead of edit when group or all is selected


- what about a pivot ?
- what states. Modeling, moving full parts (copy to points)
- modeling state:
   - operacje jak loop straighten
   -
```

```
- acces to select by one key.
- redesign select mode to work always
- have acces to edit options like straighten
- T transform , prefer transform node
- S always for selection

-escape to edit again
-features from edit in other nodes
działaja snapy i handle na poziomie object   
inne toole mamy w topo build i inne w edit   
Hide not working all the time   
enter edit after merge / edit mode after chamfer

 packed ??    

```


```
BRAKUJE W KÓŁKU
- select groups '9'
- show others node geo
- hide geo/ show all/ invert
- select options



```




# CUSTOM
`Shift` + `W` - In all windows wireframe mode   
~~`Alt` + `W`~~ - close window  
~~`Ctrl` + `1`,`2`~~ ... - change   
~~`C` is visualize~~ should be: comment
`9` selection group        
`\` - manual update   `|` - auto update      
` ' ` - RESELECT FOR CURENT TOOL     
` ~ ` - SECURE SELECTION  


#### Match translate
> is icon on the right of transform params click, and select obj u want rotate to.



To set/change key klick on shelf or menu item while holding `Ctrl` + `Alt` + `Shift`

Options to change
- default Desktop
- default handle aligment: World
- standard tumblig wievport
- secure selection off
- add paths to 'Open file dialog'

----



# Viewport Manipulation

|||
|-|-|
`T` | Transform  
`R` | Rotate   
`E` | Scale    
`M` | World Coordinates    

### Pivot
For animation. Permanent pivot of object.

|||
|-|-|
`Insert` | pivot transform (take car e about pre transform for pivot after every viewport operation)  
`Shift` + `"` | pivot sth

### Handle
For modeling and placement. leave pivot unaffected.

|||
|-|-|
`'` | Deeatache Viewport handle temporary.  
`RMB>presistant` | To have 2second handles and pivot rotation   
`RMB>SnapTo..` | Pivot or centroid.  
`RMB>HandleParameters` | Options  
`RMB>Local/Global` | Local pivot points vs Global - centroid of all  
`RMB>TranslateGloballyInLocalControl` | Local transform of last selected


### Align  
Hover over geometry .. Y is up.
Check if you have object or world aligned handles it change behaviour

|||
|-|-|
`:` /  `:` + `Shift` | Align (`RMB>OrientationPeaking`).       
`selct placement` + `Shift` | only rotate    
`selct placement` + `Ctrl` | move dont rotate   
`selct placement` + `Ctrl` + `Shift` | lookat Y  (to change click handle with ctrl)   
`select axis` + `drag` | secondaty axies direction  

### Snap

### Grid plane

|||
|-|-|
`/` | Align Grid   
`?`  |


----



# Viewport Main

|||
|-|-|
`Alt`+`Space` |  wieport  
`B` | show uv layout !!!!!
`9` | select by group
`H` |  hide `H`+`ctrl`/`shift`   ??
||
`F2`-`F5` | Selection types box/lasso/paint/laser  


### Hide


----


# Viewport Selection

### Selection modes:  

|||
|-|-|
`Shift`+`V` | backmasking    
`Shift`+`C` | contained  

### Selection modify:  

|||
|-|-|
`N` | select all  
`Shift`+`N` | select none  
`Shift`+`B` | bounds   
`Shift`+`Ctrl`+`E` (on edges)| pgrowth oli age boundary  
`Shift`+`G` | Growth selection  
`Shift`+`S` | Shrink selection  
||
`A`+`ctrl`/`shift`+`[MMB]`/`[RMB]` | full selection / partial selection    
`Shift` + `P` | Set sellection pattern  
`Shift` + `🡰` `🡲` `🡱` `🡳` | Growth pattern  
`Shift` + `Ctrl` + `🡰` `🡲` `🡱` `🡳` | Growt pattern till the end  
`K` | Growth till paint under mouse  




## Edit

|||
|-|-|
`L` | Slide on Surface   
`H` | Peak  
`B` | Sculpt  
||
`Y` |  Edit  
`Shift`+`T`| Tweek mode   (no handles )


```

## PolyDraw

#### `Shift`+`1` Build

points:    
`[LMB]` - create / selsct  
`Shift`+`[LMB]` select  
`Ctrl` - angels  
`Alt` - wiewport  

`F` FILL  
`Shift`+`K`/`K` -  dziwnby bridge / BRIDGE  
`Shift`+`del` - remove unused points  

`Shift`+`C` - Circle  
`Shift`+`S` - Straighten  
`Shift`+`E` - Evenly space    

prims:  
`Shift`+`C` - Circle  
`Shift`+`X` - Collapse

#### `Shift`+`2` Slice  
#### `Shift`+`3` Split   
#### `Shift`+`4` Brush
#### `Shift`+`5` Smooth  

```



----

# Network View Graph


![](/src/hou/cfg/wheel1.png)



### Navigation

|||
|-|-|
`U` | Up  
`I` | Dive  
`Shift` + `/` | Find node by path   
`Ctrl` + `F` | Find node by name   
`PageUp` or `PageDown` | move through nodes `Shift`    
` ' ` | last view  
`F` or `G` | zoom selected   
`H` | zoom all

### Node customize

|||
|-|-|
`Z` | NODE shape  
`X` | NODE visualizer  
`C` | NODE color  

### Layaut


|||
|-|-|
`L` | layaut
`Shift`+`L` | layout Selected  
`Shift` + `A` + `🡰` `🡲` | (on selected nodes) - align horizontaly  
`Shift` + `A` +`🡱` `🡳`  | (on selected nodes) - align verticaly  
`Shift` + `S` | Change link type
`Ctrl`+`Shift`+`Alt`+ `LMB` | on a node will duplicate the node and automatically reference everything



----

# Parameter Fields

|||
|-|-|
`Alt` + `LLM`  | create key  
||
`Ctrl` + `LLM` | delete key    
`Ctrl`+ `Shift` + `LLM` | delete key whertever is     
`Ctrl` + `MMB` | zero   
||
`Shift` + `LLM` | OPEN CURVE EDITR   


.|.|.|
-|-|-|
<img src="/src/hou/parm_0.png" width="76"> |   Default value  | `Ctrl` + `MMB` - reverte to default
<img src="/src/hou/parm_1.png" width="76"> |   Modified value   | `Shift` + `RMB` - switch to previous value
<img src="/src/hou/parm_14.png" width="76"> |  Parameter being manipulated in wievport
<img src="/src/hou/parm_4.png" width="76"> |   Value changed waiting for kayframe
<img src="/src/hou/parm_2.png" width="76"> |   **Keyframe** / **fn** on current frame  |  `Alt` + `LMB` - add / `Ctrl` + `LMB` - remove key /  `Ctrl` + `Shift` + `LMB` - remove channel
<img src="/src/hou/parm_3.png" width="76"> |   **Keyframe** / **fn** on other frame
<img src="/src/hou/parm_6.png" width="76"> |   **Channel reference** on current frame
<img src="/src/hou/parm_7.png" width="76"> |   **Channel reference** on other frame  
<img src="/src/hou/parm_5.png" width="76"> |   **CHOP**
<img src="/src/hou/parm_11.png" width="76"> |  Non default language **fn**
<img src="/src/hou/parm_12.png" width="76"> |  Non default language **fn with channel reference**
<img src="/src/hou/parm_8.png" width="76"> |   Locked
<img src="/src/hou/parm_9.png" width="76"> |   **Take** - not changed  |
<img src="/src/hou/parm_10.png" width="76"> |  **Take** - not changed |  
<img src="/src/hou/parm_13.png" width="76"> |  Evaluated string (MMB on string param) | `Ctrl` or `Alt` + `E` - edit expression
<img src="/src/hou/parm_15.png" width="76"> |  Bound to viewport handler
<img src="/src/hou/parm_16.png" width="76"> |  Error
<img src="/src/hou/parm_18.png" width="76"> |  Error | wrong language used
<img src="/src/hou/parm_17.png" width="76"> |  After deleted all keys ?



--------------------------------------------




--------------------------------------------



# TOPs
Generate nodes  
`Shift` + `G` - revert cooked to graph and cook uncooked    // do it before delete from disc  
`Shift` + `V` - Dirty node and cook all  




--------------------------------------------