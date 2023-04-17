---
title: retroPy API
date: 2022-05-23 12:00:00 -500
categories: [retroPy APIs]
tags: []
---

## retroPy Color Palette

retroPy uses a 16 color palette system.
_(retroPy uses the same color palette system as Pico-8)._

![img-description](/assets/img/color_pallet.png)

Color values:

> 0x0000, 0x194A, 0x792A, 0x042A, 0xAA86, 0x5AA9, 0xC618, 0xFF9D,

> 0xF809, 0xFD00, 0xFF64, 0x0726, 0x2D7F, 0x83B3, 0xFBB5, 0xFE75

## API References

### rpy

`quitRun()`
- 

`pauseRun()`
- clear the screen with color 

`resumeRun()`
- set the pixel at x, y with color

`pauseTimer()`
- draw a line starting at x1, y1 and ending at x2, y2

`resumeTimer()`
- draw a horizontal line at x, y with length and color

`color_p()`
- draw a verticle line at x, y with length and color

`color_palette()`
- draw a circle center x, y with radius and color 

`color_reset()`
- draw a filled circle center x, y with radius and color 

```
orientation(setting)
set the orientation of the display
setting values:
0 – normal
1 – rotation 90 degrees
2 – rotation 180 degrees
3 – rotation 270 degrees
```


### Graphics

Setup

`Rect(x,  y,  width,  length)`
- A built in class.


`clear()`
- clear the screen black

`clear(color)`
- clear the screen with color 

`pixel(x, y, color)`
- set the pixel at x, y with color

`line(x1, y1, x2, y2, color)`
- draw a line starting at x1, y1 and ending at x2, y2

`hline(x, y, length, color)`
- draw a horizontal line at x, y with length and color

`vline(x, y, height, color)`
- draw a verticle line at x, y with length and color

`circle(x, y, radius, color)`
- draw a circle center x, y with radius and color 

`filled_circle(center, radius, color)`
- draw a filled circle center x, y with radius and color 

`rect(Rect, color)`
- draw a rectangle at Rect with color 

`filled_rect(Rect, color)`
- draw a filled rectangle at Rect with color 

`text(string, x, y, color)`
- write a string at x, y with color


## Actors

`actor(ptr2spriteTable, x, y, flipDuration, speed_x, speed_y, mode)`
- create an actor with spriteTable at x, y with flipDuration and speed_x and speed_y
- speed is in pixel per second (float)

`speed(speed_x, speed_y)`
- actor speed x direction and y direction

`speed_x (property)`
- get actor speed x direction

`speed_x(speed)`
- set actor speed in the x direction

`speed_y (property)`
- get actor speed y direction

`speed_y(speed)`
- set actor speed in the y direction

`pos(pos_x, pos_y)`
- set actor positions

`pos_x (property)`
- get actor x poaition

`pos_x(position)`
- set actor x position

`pos_y (property)`
- get actor y poaition

`pos_y(position)`
- set actor y position

`bound(xmin, xmax, ymin, ymax)`
- set the maximum and minimum x and y positions

`bound_x(xmin, xmax)`
- set the maximum and minimum x  positions

`bound_y(ymin, ymax)`
- set the maximum and minimum y positions

`dist(actor)`
- get distance between 2 actors

`sprite()`
- change the spriteTable

`currNdx(ndx)`
- get the current sprite index

`moveTowards(x, y, speed, dt)`

`draw()`
- draw the actor in the draw

`collider()`
- 

`colliderEx()`
- 

`colliderPt()`
- 

`resizeCollider()`
- set actor speed in the x direction

`drawCollider()`
- get actor speed y direction

`collider_xy()`
- set actor speed in the y direction

`pos_cx()`
- set actor positions

`pos_cy()`
- get actor x poaition

`bot_cx(position)`
- set actor x position

`id()`
- get actor y poaition

`type()`
- set actor y position

`val()`
- set the maximum and minimum x and y positions

`mid_x()`
- set the maximum and minimum x  positions

`mid_y()`
- set the maximum and minimum y positions

`bot_x()`
- 

`bot_y()`
- 
