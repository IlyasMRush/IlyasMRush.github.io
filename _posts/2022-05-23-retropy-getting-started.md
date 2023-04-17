---
title: Getting Started
date: 2022-05-23 12:00:00 -500
categories: [retroPy APIs]
tags: []
---

## Introduction

retroPy is a game console for retro gaming using the Raspberry Pi Pico and programmed in Python.
Most concepts of the retroPy mimic small game engines such as PyGame Zero, Pyxel and Pico-8.
The main idea of retroPy is to be able to create retro games using a “modern” programming language (e.g. Python).
One of retroPy's great qualities is that it runs on a small gaming console, making it super mobile.
retroPy is definitely a fun way to learn Python and a simple way to get into game programming.

![img-description](/assets/img/console1.png)
![img-description](/assets/img/console2.png)

## Installation

If you have one of the following consoles, there is nothing to install.
However, you will need to install Thonny to code in Python.


## Update

> RetroPy is fresh out of the oven and currently just got of beta. Do keep a look out for updates.
{: .prompt-info }



## Example

Below is an example of using retroPy as a graphic tool.

```python
from retroPy import rpy

rpy.clear()
rpy.filled_circle(120, 120, 100, 8)
rpy.text("hello!", 95, 115, 7)

rpy.show()
```
Next is an example of using retroPy as a simple game engine.


```python
from retroPy import rpy, Rect

def update(dt):
    pass

def draw():
    rpy.clear()
    rpy.filled_circle(120, 120, 100, 8)
    rpy.text("hello!", 95, 115, 7)

def on_key_down(key):
    pass
def on_key_up(key):
    pass

rpy.run(update, draw, on_key_down, on_key_up)
```

## retroPy Color Palette

retroPy uses a 16 color palette system.
_(retroPy uses the same color palette system as Pico-8)._

![img-description](/assets/img/color_pallet.png)

Color values:

> 0x0000, 0x194A, 0x792A, 0x042A, 0xAA86, 0x5AA9, 0xC618, 0xFF9D,

> 0xF809, 0xFD00, 0xFF64, 0x0726, 0x2D7F, 0x83B3, 0xFBB5, 0xFE75

## API Reference
```
orientation(setting)
set the orientation of the display
setting values:
0 – normal
1 – rotation 90 degrees
2 – rotation 180 degrees
3 – rotation 270 degrees
```


## Graphics


## Example of sprites
### Actors

| Asteroid 4x14x14 | 
|-|
| ![img-description](/assets/img/asteroid.png) |


| Bomb1 2x8x8 | Bomb2 2x8x8 |
|-|-|
| ![img-description](/assets/img/bomb_1.png) | ![img-description](/assets/img/bomb_2.png) |

| boosters 2x16x7 |
|-|
| ![img-description](/assets/img/boosters.png)

| boy_idle <br> 2x16x16 | boy_idle_r <br> 2x16x16 | boy_idle_l <br> 2x16x16 | boy_idle_u <br> 2x16x16 |
|-|-|-|-|
| ![img-description](/assets/img/boy_idle.png) | ![img-description](/assets/img/boy_idle_l.png)| ![img-description](/assets/img/boy_idle_r.png) | ![img-description](/assets/img/boy_idle_u.png) |

| boy_walk_d <br> 4x16x16 | boy_walk_l <br> 4x16x16 | boy_walk_r <br> 4x16x16 | boy_walk_u <br> 4x16x16 |
|-|-|-|-|
| ![img-description](/assets/img/boy_walk_d.png) | ![img-description](/assets/img/boy_walk_l.png) | ![img-description](/assets/img/boy_walk_r.png) | ![img-description](/assets/img/boy_walk_u.png) |

| enemy2 2x16x16x |
|-|
| ![img-description](/assets/img/enemy2.png) |

| explosion <br> 3x16x16 | explosion1 <br> 6x16x16 | Explosion2 <br> 5x16x16 |
|-|-|-|
| ![img-description](/assets/img/explosion.png) | ![img-description](/assets/img/explosion1.png) | ![img-description](/assets/img/explosion2.png) |

| heart 3x16x16 | Heart_red 3x16x16 |
|-|-|
| ![img-description](/assets/img/heart.png) | ![img-description](/assets/img/heart_red.png) |

| lips 5x16x16 |
|-|
| ![img-description](/assets/img/lips.png) |

| projectile 4x8x16 | Projectile1 2x14x6 |
|-|-|
| ![img-description](/assets/img/projectile.png) | ![img-description](/assets/img/projectile1.png) |

| ship 3x16x16 | Ship1 1x26x12 | Ship2 1x16x16 |
|-|-|-|
| ![img-description](/assets/img/ship.png) | ![img-description](/assets/img/ship1.png) | ![img-description](/assets/img/ship2.png) |

| projectile 4x8x16 | Projectile1 2x14x6 |
|-|-|
| ![img-description](/assets/img/Wall1.png) | ![img-description](/assets/img/Wall2.png) |

| Test1.py 1x16x16 |
|-|
| ![img-description](/assets/img/Test1.png) |


## Setup
### Rect
A built in class.
(x,  y,  width,  length)

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



## Getting Started
### Minimal Code

```python
from retroPy import rpy

def update(dt):
    pass

def draw():
    pass

def on_key_down(key):
    pass
def on_key_up(key):
    pass

rpy.run(update, draw, on_key_down, on_key_up)
```

### Drawing primitives
```python
from retroPy import rpy, Rect

def update(dt):
pass

def draw():
    rpy.clear(1)
    rpy.filled_rect(Rect(0, 0, 24, 24), 5)
    rpy.filled_circle(50, 50, 12, 8)
    rpy.text("Hello World", 75, 100, 7)
    pass

def on_key_down(key):
    pass
def on_key_up(key):
    pass

rpy.run(update, draw, on_key_down, on_key_up)
```

### Sprite
Using a sprite
```python
from retroPy import rpy, Rect, actor, LoadSpriteStr
from Assets import boy

player = actor(LoadSpriteStr(boy.boy_idle), 20, 20, 0, 0, 0)
player.flipDuration(300)
player.speed_x = 80
player.bound_x(0,224)

def update(dt):
    player.update(dt)

def draw():
    rpy.clear()
    player.draw()
def on_key_down(key):
    pass

def on_key_up(key):
    pass

rpy.run(update, draw, on_key_down, on_key_up)
```