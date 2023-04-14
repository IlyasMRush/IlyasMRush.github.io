---
title: retroPy Movement (Part II)
date: 2022-04-23 12:00:00 -500
categories: [retroPy,Tutorials]
tags: []
---

## Introduction

In this tutorial we will be continuing our code from the [previous tutorial][1] by adding a jumping mechanic for our player.

[1]:{{ site.baseurl }}{% link _posts/2023-03-25-retropy-movement-tutorial-part-1.md %}

We will assign Button A for jumping.  In order to sump, we need to give relatively large value to player.speed_y eg -190.  The value is negative since we need the player to move up the screen. We will use a player_jumpSpeed 

player_jumpSpeed = -190
if rpy.btnADown():
player.speed_y = player_jumpSpeed


This works but if you continuously press the A Button, the player will so go out of the top screen.  It seems that our player can fly.
To avoid this, we will have to keep track of the player position.  Jump only if the player is no the ground.
We’ll start with 
player_isGrounded = False
when is reach the ground we will set it to True
    if player.bot_y > groundLevel:
       player.bot_y = groundLevel-1
       player_isGrounded = True
(Don’t forget we also need to include the global for our new variables)
```python
player_walkSpeed = 50
player_jumpSpeed = -190
player_isGrounded = False
gAcc = 300
groundLevel = 238

def update(dt):
    global player_isGrounded, player_walkSpeed, player_jumpSpeed, gAcc, groundLevel     
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

    if rpy.btnADown() and player_isGrounded:
        player.speed_y = player_jumpSpeed
        player_isGrounded = False

    player.acc_y = gAcc

    player.update(dt)
    
    if player.bot_y > groundLevel:
       player.bot_y = groundLevel-1
       player_isGrounded = True
```
(move-04)

Double Jump / Multiple Jumps

To achieve multiple jumps, we need to keep track of a few more states.
```python
player_isJumping = False
player_jumpCount = 0
player_jumpMax = 2
```
We need to check if player is Jumping with player_isJumping
We need to track how many multiple jump has been made and make sure that it doesn’t exceed the maximum player_jumpMax.
```python
    if player_isGrounded:
        player.acc_y = 0
        player.speed_y = 0
        player_jumpCount = 0
        player_isJumping = False
        if rpy.btnADown():
            player.speed_y = player_jumpSpeed
            player_jumpCount += 1
            player_isGrounded = False
            player_isJumping = True
    else: # in the air
        player.acc_y = gAcc
        if rpy.btnADown():
            if player_jumpCount < player_jumpMax and player_isJumping:
                player.speed_y = player_jumpSpeed
                player_jumpCount += 1
```
Again, don’t forget to add the globals:
    `global player_isJumping, player_jumpCount, player_jumpMax`

At this point you will be able to do a double jump to increase the number of multiple jumps, just change the value of player_jumpMax

Full code:
```python
from retroPy import rpy, actor, LoadSprite

p_player = LoadSprite("playerT.rs4")
player = actor(p_player, 112, 112, 0, 0, 0)
player.currNdx(0)

player_walkSpeed = 50
player_jumpSpeed = -190
player_isGrounded = False
player_isJumping = False
player_jumpCount = 0
player_jumpMax = 2

gAcc = 300
groundLevel = 238

def update(dt):
    global player_isGrounded, player_walkSpeed, player_jumpSpeed, gAcc, groundLevel
    global player_isJumping, player_jumpCount, player_jumpMax
    
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

    if player_isGrounded:
        player.acc_y = 0
        player.speed_y = 0
        player_jumpCount = 0
        player_isJumping = False
        if rpy.btnADown():
            player.speed_y = player_jumpSpeed
            player_jumpCount += 1
            player_isGrounded = False
            player_isJumping = True
    else: # in the air
        player.acc_y = gAcc
        if rpy.btnADown():
            if player_jumpCount < player_jumpMax and player_isJumping:
                player.speed_y = player_jumpSpeed
                player_jumpCount += 1
    
    player.update(dt)
    
    if player.bot_y > groundLevel:
       player.bot_y = groundLevel-1
       player_isGrounded = True
        
def draw():
    global player_walkSpeed, gAcc, groundLevel     
    rpy.clear()
    player.draw()
    rpy.hline(0, groundLevel, 240, 7)
    
#=========================================================================
rpy.run(update, draw)
```
(move-05)























