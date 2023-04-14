---
title: retroPy Movement (Part I)
date: 2022-04-23 12:00:00 -500
categories: [retroPy,Tutorials]
tags: []
---

## Introduction

Welcome to the retroPy Movement tutorial. For this tutorial, we will go learn to move and control sprites in your retroPy game. 

## Installing Asset
Before we begin, I recommend downloading the asset below as we will be using it in this tutorial.

Asset:
[playerT.rs4][1]

[1]:{{ site.url }}/download/file.pdf

Once you have downloaded the asset, place it in the assets directory of your retroPy.

## Loading Player into Screen

Let's start by creating the character for our player by adding these 3 lines.

`p_player = LoadSprite("playerT.rs4")` will call the asset we have into an instance.<br>
`player = actor(p_player, 112, 112, 0, 0, 0)` will create our player at the center of our screen.<br>
`player.currNdx(0)` will be the direction our player is facing (currently it faces to the right).

Your code should resemble the code shown below:

```python
from retroPy import rpy, actor, LoadSprite

p_player = LoadSprite("playerT.rs4")
player = actor(p_player, 112, 112, 0, 0, 0)
player.currNdx(0)

def update(dt):
    player.update(dt)

def draw():
    rpy.clear()
    player.draw()
    
#=========================================================================
rpy.run(update, draw)
```

If everything is working as intended, you should see your player at the center of your screen. As we are trying to focus on simplifying the lesson, we will not be adding animations to our player.

## Input Moving Left & Right

Now let's input movement into our player. We'll start by making him move left and right based on our controls.

```python
def update(dt):
    if rpy.btnLeftDown():
        player.speed_x = -20        
    if rpy.btnRightDown():
        player.speed_x = 20        

    player.update(dt)
```

Great, we can now move around. However, it looks slight off as our player does not face the direction that he is moving in. In order to make the player face the left, we need to flip the sprite horizontally using `player.currNdx(0, 1)`.

Our new code for `update()` should look like this:
```python
def update(dt):
    if rpy.btnLeftDown():
        player.currNdx(0, 1)
        player.speed_x = -20        
    if rpy.btnRightDown():
        player.currNdx(0, 0)
        player.speed_x = 20         

    player.update(dt)
```

We'll finish up the movement by adding code to make our player stop moving when the left or right button is released. This will allow us to control our player effectively.
```python
    if rpy.btnLeftUp():
        player.speed_x = 0
    if rpy.btnRightUp():
        player.speed_x = 0
```

Finally, we have a player that we can move with. 

## Creating Gravity and Ground

Now that we have completed the player movement, let’s add in gravity so that the player will fall until he hits the ground.

We'll start with creating the ground first as we do not want the player to fall off the screen. 

`rpy.hline(0, 238, 240, 7)` will draw a line starting from the y-coordinate at 238 to represent the ground.

Next, let's implement code that allows our player to not fall below the line.

```python
if player.bot_y > 238:
    player.bot_y = 237
```

This `if` statement restricts the position of our player from going above the 238 y-coordinate and to position our player on the 237 y-coordinate (which is above the ground).

Finally, we'll create the gravity by adding acceleration to the player in the y-direction with `player.acc_y = 300`

This is what the final code looks like:

```python
def update(dt):
    if rpy.btnLeftDown():
        player.currNdx(0, 1)
        player.speed_x = -20        
    if rpy.btnRightDown():
        player.currNdx(0, 0)
        player.speed_x = 20   

    if rpy.btnLeftUp():
        player.speed_x = 0
    if rpy.btnRightUp():
        player.speed_x = 0      

    player.acc_y = 300

    player.update(dt)
    
    if player.bot_y > 238:
       player.bot_y = 237
        
def draw():
    rpy.clear()
    player.draw()
    rpy.hline(0,238,240,7)
```

Our player should now be falling to the ground when running this script.

## Improving and Cleaning Code

Its generally not a good idea to hardcode values in our script as it tends to create errors. Examples of hardcoding values in our script are as follows:

`player.speed_x = 20`<br>
`player.bot_y = 237`

A good practice would be to assign global variables for these values instead:

`player_walkSpeed = 20` <br>
`gAcc = 300` <br>
`groundLevel = 238` <br>

We'll go back to our `update()` and `draw()`  methods to implement the global variables.

The finalized code:
```python
from retroPy import rpy, actor, LoadSprite

p_player = LoadSprite("playerT.rs4")
player = actor(p_player, 112, 112, 0, 0, 0)
player.currNdx(0)

player_walkSpeed = 20
gAcc = 300
groundLevel = 238

def update(dt):
    global player_walkSpeed, gAcc, groundLevel   

    if rpy.btnLeftDown():
        player.currNdx(0, 1)
        player.speed_x = -player_walkSpeed        
    if rpy.btnRightDown():
        player.currNdx(0, 0)
        player.speed_x = player_walkSpeed     

    if rpy.btnLeftUp():
        player.speed_x = 0
    if rpy.btnRightUp():
        player.speed_x = 0    

    player.acc_y = gAcc

    player.update(dt)
    
    if player.bot_y > groundLevel:
       player.bot_y = groundLevel-1
        
def draw():
    global player_walkSpeed, gAcc, groundLevel     
    rpy.clear()
    player.draw()
    rpy.hline(0, groundLevel, 240, 7)
    
#=========================================================================
rpy.run(update, draw)  
```

Congratulations! You have a controllable player that walks on a solid ground and abides by the laws of gravity.

We'll cover more elements of movement such as jumping in our next turorial [Movement Part II][2].

[2]:{{ site.baseurl }}{% link _posts/2023-03-25-retropy-movement-tutorial-part-2.md %}