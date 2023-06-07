---
title: "Day 20 - Building the Snake Game: Part 1"
seoTitle: "Day 20: Launching the First Phase of Snake Game Development"
seoDescription: "Day 20 of '100 Days of Python': Dive into Snake Game creation. Learn class creation techniques and avoid coding pitfalls."
datePublished: Wed Jun 07 2023 13:25:08 GMT+0000 (Coordinated Universal Time)
cuid: clilqsb86000p09jkhhcg8cvl
slug: day-20-building-the-snake-game-part-1
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1686141688240/52bd385b-80d9-46d2-ab21-448d1442df0b.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1686143794509/1c39411d-cae4-4d0b-a421-d429f2605057.png
tags: python, backend, game-development, 100daysofcode, codenewbies

---

## The Objective

For the following days (Day 20 and Day 21), the objective is the build the classic Snake game. Angela breaks down the goals for the and part one will consist of:

1. Creating the snake body by creating 3 squares on the screen last a given starting point.
    
2. Moving the snake forward without breaking.
    
3. Finally, add the ability to turn the snake.
    

There weren't any new concepts discussed in today's lesson, but, looking at Day 21, we touch base on `Class Inheritance`.

## Making the Snake

This project has to be one of the hardest I've tried yet. More so on all the connected parts than the lack of understanding of certain concepts. We built the snake in our main.py file initially but then migrated the snake build into its own file and `Class`.

#### Snake Class:

```python
class Snake:
    def __init__(self):
        self.full_snake = []
        self.create_snake()
        self.head = self.full_snake[0]
        
    def create_snake(self):
        for position in STARTING_POSITION:
            new_snake = Turtle(shape="square")
            new_snake.penup()
            new_snake.goto(position)
            self.full_snake.append(new_snake)
```

After getting it created, we worked on the movement. This part is where I struggled a bit due to needing to work with `X` and `Y` coordinates. Trying to get the 3 squares to align like a snake and then move smoothly took some more diving into the [Python Turtle Graphics doc](https://docs.python.org/3/library/turtle.html). After the snake got moving, we worked on adding the ability to turn it, which was a little bit easier to grasp and code up. After a couple of hours of early AM work, finished part 1! The snake moves forward and can turn without turning on itself.  
  
Video: [Snake Game Part 1 Example](https://www.loom.com/share/5f624e84854649e7be0201261efec7f4)  
  
Since I'm working on more than one file for this project, I won't be posting everything I wrote today but you can find it in the `Day-19` folder on GitHub -&gt; [https://github.com/kdleonard93/100-Days-Of-Code\_Python/tree/day-20/day-20](https://github.com/kdleonard93/100-Days-Of-Code_Python/tree/day-20/day-20)

## EOD

That wraps up Part 1 of the Snake Project. Since I worked on this before my normal work hours, there's a chance I'll be posting Part 2 (Day 21) later this evening. There I will make note of the new concept `Class Inheritance` and wrap up my first full Python game!

#### If you want to keep up with my progress or just want to connect as peers, check out my social links below and give me a follow!

* [🐦 Twitter](https://twitter.com/RingoMandingo93)
    
* [💻 Github](https://github.com/kdleonard93)
    
* [👾 Discord](https://discord.com/users/407639833146818570)
    
* [👔 LinkedIn](https://www.linkedin.com/in/kyle-leonard93/)