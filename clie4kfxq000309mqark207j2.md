---
title: "Day 19 - Instances, State, and Higher-Order Functions"
seoTitle: "Day19 - Unraveling Instances, State, and Higher-Order Functions"
seoDescription: "Explore Python's Instances, State, and Higher-Order Functions through engaging projects 'Etch-A-Sketch' and 'Turtle Race'."
datePublished: Fri Jun 02 2023 05:28:46 GMT+0000 (Coordinated Universal Time)
cuid: clie4kfxq000309mqark207j2
slug: day-19-instances-state-and-higher-order-functions
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1685680947267/9531836c-4607-45e0-ac7f-000529ea76e4.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1685683615734/8337896f-f06d-40c8-aba5-eb69b1c33a6d.png
tags: blogging, python, 100daysofcode, codenewbies, higher-order-functions

---

## Today's Objective

Today, we took a look into some concepts not touched on yet in this course: Instances, State, and Higher-Order Functions. I'll touch post a quick definition and example of each concept below:

1. **Instances**: An instance is a single and unique unit of a class. A class is a blueprint, and an instance is an individual object created from that blueprint. For example, if you have a class `Dog`, you can create an instance of `Dog` like `my_dog = Dog()` where `my_dog` is an instance of the class `Dog`.
    
2. **State**: In Python, state refers to the values of an object's attributes at a given time. For instance, if a `Dog` object has attributes like `name` and `age`, the combination of these attribute values at any moment constitutes the state of the `Dog` object. If `my_dog`'s name is "Fido" and its age is 3, that's the current state of `my_dog`.
    
3. **Higher-Order Functions**: In Python, higher-order functions are functions that can either accept other functions as arguments, return a function as a result, or both. This concept is a key part of functional programming. For example, Python's built-in `map()` function is a higher-order function because it takes a function and an iterable, applies the function to every item in the iterable, and returns a new iterable with the results.
    

Now these are definitions and examples pulled from the interweb. I will admit I'm not all that well-versed when it comes to state and higher-order functions so I felt that trying to explain them in my own words would not come across clear. With that being said, we can just dive into the two projects for today's lesson: "Etch-A-Sketch" and the "Turtle Race"

## Etch-A-Sketch

This project (or I should say challenge) was pretty easy. It mainly focused on incorporating event listeners, which are considered higher-order functions, to listen for the key input and then execute the action (or function) that is bound to that key.  
So this was a pretty straightforward challenge and I've added the code below (was only one file):

```python
from turtle import Turtle, Screen
import random

tim = Turtle()
screen = Screen()

def move_forward():
    tim.forward(10)
    
def move_backwards():
    tim.back(10)
    
def counter_clockwise():
    tim.left(10)
    
def clockwise():
    tim.right(10)
    
def clear():
    tim.clear()
    tim.penup()
    tim.home()
    tim.pendown()

screen.listen()
screen.onkey(key="d", fun=move_forward)
screen.onkey(key="a", fun=move_backwards)
screen.onkey(key="w", fun=counter_clockwise)
screen.onkey(key="s", fun=clockwise)
screen.onkey(key="c", fun=clear)

screen.exitonclick()
```

Nothing crazy here to note other than it was a decent re-introduction of the basics of Higher-Order Functions.

## The Turtle Race

This project on the other hand was a bit more complicated and took me a little bit of re-reading the Turtle docs and some previous lessons to get through it. The main focus of this project was to understand the use and importance of State and Instances. Since this one only needed one file as well, I'll post the full code but you can still check changes in [GitHub](https://github.com/kdleonard93/100-Days-Of-Code_Python/tree/main/day-19) as well

```python
from turtle import Turtle, Screen
import random

screen = Screen()
screen.setup(width=550, height=500)
user_bets = screen.textinput(title="Make your bet!", prompt="Who will win the race? Pick your color: ")
colors = ["red", "orange", "yellow", "green", "blue", "purple"]
y_pos = [100, 50, 0, -50, -100, -150]
all_turtles = []
    

for turtle_index in range(0, 6):
    new_turtle = Turtle(shape="turtle")
    new_turtle.color(colors[turtle_index])
    new_turtle.penup()
    new_turtle.goto(x=-250, y=y_pos[turtle_index])
    all_turtles.append(new_turtle)
    
if user_bets:
    race_on = True
    
while race_on:
    for turtle in all_turtles:
        if turtle.xcor() > 255:
            race_on = False
            winning_color = turtle.pencolor()
            if  winning_color == user_bets:
                print(f"You won the race with {winning_color}!")
            else:
                print(f"You lost the race with {winning_color}!")
                
        rand_distance = random.randint(0, 15)
        turtle.forward(rand_distance)
        
screen.exitonclick()
```

The second `for` loop is where I was tripped up the most because I didn't realize there were two methods for the color of the turtle before. I'm glad that it didn't frustrate me for too long though. For reference on what is considered a current "state", I've singled out which variables and objects are considered to hold a "state". Variables and Objects will be highlighted and state is what it holds:

* The `screen` object with its width and height attributes.
    
* The `user_bets` variable that holds the user's bet.
    
* The `colors` list and `y_pos` list.
    
* The `all_turtles` list which holds the turtle objects. Each turtle object also has a state, including attributes such as color and position (`xcor()` and `ycor()`).
    
* The `race_on` boolean variable that controls whether the race continues or not.
    
* The `winning_color` variable which holds the color of the winning turtle when a turtle crosses the specified x-coordinate.
    
* Each `turtle`'s x-coordinate in the `while` loop, as it determines whether the race should end.
    
* The random distance each turtle moves during each iteration of the `while` loop.
    

This should be a good reference point to loop back to in the future when it comes to pulling examples.

## EOD

And there goes day 19! Yeah, it's super late, but I'm chucking this up anyways - who cares about the 'perfect post time', amirite? lol.

#### If you want to keep up with my progress or just want to connect as peers, check out my social links below and give me a follow!

* [🐦 Twitter](https://twitter.com/RingoMandingo93)
    
* [💻 Github](https://github.com/kdleonard93)
    
* [👾 Discord](https://discord.com/users/407639833146818570)
    
* [👔 LinkedIn](https://www.linkedin.com/in/kyle-leonard93/)