---
title: "Day 23: Python Turtle Crossing Game - OOP and Creativity"
seoTitle: "Day 23: Python Turtle Crossing Game - OOP and Creativity"
seoDescription: "Day 23 Python journey: Create a fun Turtle Crossing game using Classes, Class Inheritance, and Python's Turtle module."
datePublished: Thu Jun 22 2023 01:19:32 GMT+0000 (Coordinated Universal Time)
cuid: clj6ggyv0000809mj9tbs21hu
slug: day-23-python-turtle-crossing-game-oop-and-creativity
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1687203709265/84371033-331a-4f7d-812e-4e95eb893d61.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1687396643067/75a77509-16ec-4a40-8e19-281948fce0df.png
tags: python, game-development, 100daysofcode, blackintech, turtlecrossinggame

---

Hey folks! We're on to Day 23 and it's time to delve into our 2nd capstone project. If you've been following along, you'll remember our work with Classes, Class Inheritance, and creating methods within those classes. Today, we're adding a new element to our programming toolkit: the Python turtle game engine. This project will give us an opportunity to apply what we've learned in a practical and engaging way. In my experience, building these games has been a great method for reinforcing newly learned concepts. So, let's dive in and see if we can get these turtles across the street. Here's to another day of coding 🤘🏾😄!

## Breaking down the Problem

So we need to figure out how to exactly get the game set up and below is how we broke down the project:

* Move the turtle up with a specified keypress
    
* Create and move cars
    
* Detect collisions with cars and display a "GAME OVER"
    
* Detect completion of the game and start a new level
    
* Create a scoreboard.
    

## The Project

Since this is a capstone project, I'm going to go into more detail about what exactly we did in each file, but I'll still only post a snippet or two, leaving the whole repo to be viewed on GitHub -&gt; [https://github.com/kdleonard93/100-Days-Of-Code\_Python/tree/day-23/day-23](https://github.com/kdleonard93/100-Days-Of-Code_Python/tree/day-23/day-23).

With the final lines of code in place, our Turtle Crossing Game has taken shape, showcasing the capabilities of Python's Turtle module and the OOP principles I've been practicing. Let's take a closer look at what we've accomplished.

We start off with our [`main.py`](http://main.py) file, which serves as the core of our game. Here, we set up our game screen, initialize our player, car manager, and scoreboard, and keep the game running as long as our turtle dodges traffic. Below is a snippet of the code from `main.py`:

```python
import time
from turtle import Screen
from player import Player
from car_manager import CarManager
from scoreboard import Scoreboard

screen = Screen()
screen.setup(width=600, height=600)
screen.tracer(0)

player = Player()
car_manager = CarManager()
scoreboard = Scoreboard()

screen.listen()
screen.onkey(player.go_up, "Up")

game_is_on = True
while game_is_on:
    time.sleep(0.1)
    screen.update()
    
    car_manager.create_car()
    car_manager.move_cars()
    
    for car in car_manager.all_cars:
        if car.distance(player) < 20:
            game_is_on = False
            scoreboard.game_over()
            
    if player.is_at_finish_line():
        player.go_to_start()
        car_manager.level_up()
        scoreboard.increase_level()
            
screen.exitonclick()
```

As you can see from the code above, I import the necessary modules and initialize the game screen, player, car manager, and scoreboard. The script then starts listening for an 'Up' key press to make the turtle move. The game loop begins, controlled by the `game_is_on` flag, where the screen gets updated, cars are created and moved, and collision between cars and the player is checked. If a collision occurs, the game ends. If the player reaches the finish line, the player is moved back to the start, and the level of difficulty is increased. The game loop runs until a collision happens, and the game can be exited anytime by clicking on the screen.

Next, we delve into `car_manager.py`. We create new car objects at random intervals, color them randomly for a little excitement, and handle the movement of the cars. As the player progresses, the cars get faster, increasing the difficulty with each level. This was a bit of a challenge and you can see a snippet of this code below:

```python
from turtle import Turtle
import random

COLORS = ["red", "orange", "yellow", "green", "blue", "purple"]
STARTING_MOVE_DISTANCE = 5
MOVE_INCREMENT = 10


class CarManager:
    def __init__(self):
        self.all_cars = []
        self.car_speed = STARTING_MOVE_DISTANCE
        
    def create_car(self):
        random_chance = random.randint(1,6)
        if random_chance == 1:
            new_car = Turtle("square")
            new_car.shapesize(stretch_wid=1, stretch_len=2)
            new_car.penup()
            new_car.color(random.choice(COLORS))
            random_y = random.randint(-280, 260)
            new_car.goto(300, random_y)
            self.all_cars.append(new_car)
        
    def move_cars(self):
        for car in self.all_cars:
            car.backward(self.car_speed)
            
    def level_up(self):
        self.car_speed += MOVE_INCREMENT
        
```

Then, there's the [`player.py`](http://player.py) file or, the turtle itself. Our turtle begins at the starting position and moves towards the finish line when the "Up" key is pressed. Upon reaching the finish line, our turtle resets to the starting position, signaling a successful level completion and displaying the current level for the player.

Which leads to the [`scoreboard.py`](http://scoreboard.py) file, which keeps track of the player's progress. It shows the current level and if the player is smashed by a careless driver, `GAME OVER` will appear in the middle of the screen.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1687395777239/41616fd3-739f-4c4f-8b7c-c42f3ac52aee.gif align="center")

Creating this game not only puts into practice what we've learned about Classes, Class Inheritance, and creating methods within those classes, but also tests our understanding of the Python turtle game engine.

But the beauty of coding is in its limitless possibilities, right? Angela challenged the audience to remix this game to show off some creativity and skill. I'm admittedly not going to do this extra challenge but for anyone that finds the turtle game fun should give it a shot! The turtle module is a large playground for creativity, and I've come to find there's always something new to learn and explore.

## EOD

With that, I conclude Day 23 of our 100-day Python journey. Stay tuned for more fun projects and keep those coding gears grinding. Happy coding! 🤘🏾😄!

#### **If you want to keep up with my progress or just want to connect as peers, check out my social links below and give me a follow!**

* [**🐦 Twitter**](https://twitter.com/RingoMandingo93)
    
* [**💻 Github**](https://github.com/kdleonard93)
    
* [**👾 Discord**](https://discord.com/users/407639833146818570)
    
* [**👔 LinkedIn**](https://www.linkedin.com/in/kyle-leonard93/)