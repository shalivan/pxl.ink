---
title: Game Mechanics Movement
description: Systems, Progression, Economy, Balance
categories:
  - PSY
tags:
  - Design
  - Gameplay
  - GameDev
  - Narration
permalink: /gamemechanicsmulti/
aliases:
  - gamemechanicsmulti
---
Related notes: [Ludology](/ludology/)  [Game Design](/gamedesign/)    [Game Mechanics](/gamemechanics/)    [Game Theory](/gametheory/)   [Level Design](/leveldesign/)  [Taxonomy](/puzzle/)

 
 {% comment %}  [[08-01-01-GameDesign]]  [[10-01-01-GameTheory]]   [[Classic_Mechanics]]  [[05-01-01-MechanicsSingle]] [[09-01-01-Ludology]] [[10-01-01-GameTheory]]  [[12-01-01-Lore]]  {% endcomment %}




```




# Controls


- where is locus of controll... play character directly or just give direction or control one character at a time in team
[Cognition (choices)](/cognition/)
## Movement

>Mirrors Edge, Spiderman, Tony Hawk, Mario

https://www.youtube.com/watch?v=tAE2H5qJ8A8



movement: feadback to inputs

1. `acceleration` , `max`, `deceleration`
- short acc,decc - character stiff
- long line supre meat boy or uncontrolable or hard to stop , runing on ice
6 frames to full speed - start - 3 frames stop
6x 4 - meat boy have longet
stop 3 frames is x9 times faster than mario.


2. - jump
jump height to body size
mario - x4
meatboy 6x

`climb` `hang`, `fall`

3. air friction. if you stop stic it will fall



4. dash -
- can controll in air or static
- dash canceling CELESTE
 - dash cancel in last sek turned to massive jump with momentum of dash
 - do with crouch
 - separate dash and jump to modify
 - second dash


5. climb

Build tools not features

systemic stories - can be wider (as biproduct of system) or just complicated narratives (cannot return to town after robbing bank)
risk of crappy uunsatisfaing story - foreshadow , justification , character ark, redemption, pase -


mastery -

retreat to safty - shift tempo between atack and deense -



### Movement

controlls ? // move to mechancs ???

mario, movements, and combos
other approach, use enviro  - repeal yourself from projectiles or enemiies
timeing  - bust speed by shooting  - rythmic action whtn delease  -  (pathless)
keep momentu by chaining  -  / hook, slide hop, (titabfall)  / quake - bunny hopping  / mirrots efge


horizontal gameplay vs vertical


##### Accessibility , easy of use
   Degree of representation vs abstracion


--------------------
- fixed angle thrid person
- dynamic angle  - colision on distance problems / many design constraints at a time. need to organize  
    - never pivot in space (orbit around avatar)
    - level design and camera must cooperate
    - global coords or quaternions to persist state  (players think in eulers)
    - `yaw`, `pitch`, (optionally `roll`) `distance`, `latteral` and `vertical offset` for framing, `fov`
    - prevent  break line of site  (all cam cuts should be more than 30 angle )
      - can swing (rotate, detect by raycast)
      - pushing away from an obstacle while player is trying to swing toward it. (then must push cam toward)
    - organize constrain in way of degree of freeedom u need. and prioretixe
      -  
    -
- fps
https://youtu.be/C7307qRmlMI
--------------------



## Camera (Gamatography)
(user think in euler look up down or on sides)

- Yaw, Pitch and roll
- distance from pivor
- laterral and vertical offset for framing
- fov

##### FOV
- FOV values can be different. 60 vertical FOV equaled 75 HOR+ FOV which is based in 4:3 aspect ratio, equals to 90 HOR- FOV which is based 16:9 aspect ratio or higher.
- 85 HOR+ FOV and not 90 is the maximum FOV that gives you peripheral vision without making a fisheye effect on 16:9 aspect ratio which is the standard now.
- **competitive gamers** that need the most FOV so they can see everything
- For **simracers**, 1:1 world accurate FOV is vitally important, and what a 1:1 FOV with no distortion is is completely dependent on how big your monitor is and how far away it is from your eyes. Think of your monitor like
- [https://dinex86.github.io/FOV-Calculator/](https://dinex86.github.io/FOV-Calculator/)

https://www.theastronauts.com/2019/04/the-secrets-of-fov/

####  FPS
simple


####  TPS fixed:
2d scroller   
camera locked  (rails)    
top wiev: rts-top   
slajdy   

####  TPS dynamic:
thgird person - hardest to design  (fixed angels are easier to make)
- automatic gudience to not controll cam and character by player
   - cam and level work toghether
   - line of sight must be small enough to fit throuhgh level
   - swing away from obstacles (detected earlier)
   - camera must satisfy lot of constraints
   - you can change distance to player depend on angle
   - see player and enviroment
   - depth perception and distance judgeing is preaty week


```