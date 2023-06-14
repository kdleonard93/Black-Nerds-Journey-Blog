---
title: "Day 22 - Building Pong: The Famous Arcade Game"
seoTitle: "Python Coding: Journey Through Pong Game Creation"
seoDescription: "Experience the journey of creating the Pong Arcade Game with Python. Learn about the challenges and successes of coding game logic."
datePublished: Wed Jun 14 2023 05:20:44 GMT+0000 (Coordinated Universal Time)
cuid: cliv9kbkd00080ai69jev3nqa
slug: day-22-building-pong-the-famous-arcade-game
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1686715708767/a808f69d-68fa-4c25-a56a-a05c32323bec.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1686719924175/b53254c2-44b2-4638-978b-7f34dae41b85.png
tags: python, 100daysofcode, pythongamedevelopment, pongarcadegame, programmingchallenges

---

## **Agenda for the Day**

Hey folks! My task for today was to conjure up the classic "Pong Arcade Game", utilizing all the knowledge and skills I've garnered thus far. Angela didn't introduce any fresh concepts and today was all concentrated on the game development. So, I'll dive into some of the riveting and tricky bits of this venture, with examples and my thoughts on why it was a pain in the ass at certain points 😄.

## **Dissecting the Project**

Oddly enough, this might have been the least technical segment of the task, yet for some reason, my initial estimations on how to segment this project were off a bit, enough to make me double back to some of my previous notes and older lectures. The project was ultimately sectioned into the following stages:

* Create the game screen
    
* Create the first paddle and add movement controls
    
* Create another paddle
    
* Create the ball and make it start moving left or right
    
* Detect collision with the wall and bounce from that position
    
* Detect collision with a paddle and bounce from that position
    
* Detect when the paddle misses
    
* Keep the score
    

As you can see, this project is a bit more challenging than the snake game but once I finally completed it, I was happy with the end result and the skills I was able to practice!

## **It Either Made Sense, Or It Didn't**

Parts of this project came together quite effortlessly. We've been tinkering with the turtle module for a while now and recent projects have been a breeze to kickstart. Setting up the file structure, basic imports, variables, and event handlers was a piece of cake. But, when it came to detecting the collision with the top and bottom walls as well as collision with the paddles, it was quite the mental task. I found myself either over-analyzing or underthinking and needed a bit of a helping hand. For instance, devising the logic for when the ball strikes the paddle proved to be the most challenging segment of this project for me. I had to take into account the dimensions of both the ball and the paddle while devising the logic. Another obstacle was resetting the ball's position once a score was made, while simultaneously making it move in the opposite direction to give the other player a fair start on the next round. Here's a glimpse at how the ball and bounce logic was constructed:

```python
from turtle import Turtle


class Ball(Turtle):
    def __init__(self):
        super().__init__()
        self.shape("circle")
        self.penup()
        self.color("white")
        self.x_move = 10
        self.y_move = 10
        self.movement = 0.1
        
    def move(self):
        new_x = self.xcor() + self.x_move
        new_y = self.ycor() + self.y_move
        self.goto(new_x, new_y)
    
    def bounce(self):
        self.y_move *= -1
        
    def paddle_bounce(self):
        self.x_move *= -1
        self.movement *= 0.7
        
    def reset_position(self):
        self.goto(0, 0)
        self.movement = 0.1
        self.paddle_bounce()
```

Additionally, in the code snippet above, you can see that I have a movement attribute that sets the ball's initial speed, and, each time it hits a paddle, the speed is ramped up. The speed, along with the position, is reset when someone scores. There were a few more areas that required a fair amount of thought, but overall, this was an engaging project. You can check out the final product here -&gt; [**https://github.com/kdleonard93/100-Days-Of-Code\_Python/tree/main/day-22**](https://github.com/kdleonard93/100-Days-Of-Code_Python/tree/main/day-22) and here's a short gif of me playing a round of pong solo.

![Screen Recording 2023-06-13 at 11.57.00 PM](https://p21.f4.n0.cdn.getcloudapp.com/items/qGu6DKlx/080eaab1-18e5-41b2-8a71-2049e3a17185.gif?source=viewer&v=f1f041bbdb24f12ac5c45c82bd6a93dd align="left")

Due to limitations of the free version of Zight, the gif only spans 15 seconds and I didn't want to use my work account for personal stuff so you only get to witness one point being scored lol. Here's hoping that Loom introduces gif-making capabilities soon.

## **EOD**

Cheers to another Python game accomplished! It was indeed tough, but it was a significant step in consolidating recent knowledge and realizing that there is still more to learn. I've been spending some time on [codewars.com](http://codewars.com) to improve my skills and I'm contemplating devoting one or two of my weekly sessions to working on more practice problems rather than rushing into new concepts. This way, I'll be able to thoroughly grasp every aspect of this journey. Peace out! ✌🏾

#### If you want to keep up with my progress or just want to connect as peers, check out my social links below and give me a follow!

* [**🐦 Twitter**](https://twitter.com/RingoMandingo93)
    
* [**💻 Github**](https://github.com/kdleonard93)
    
* [**👾 Discord**](https://discord.com/users/407639833146818570)
    
* [**👔 LinkedIn**](https://www.linkedin.com/in/kyle-leonard93/)