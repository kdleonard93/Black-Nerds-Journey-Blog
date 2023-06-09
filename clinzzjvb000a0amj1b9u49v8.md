---
title: "Day 21 - Building the Snake Game Pt 2"
seoTitle: "Day 21 - Building the Snake Game Pt 2"
seoDescription: "Discover advanced techniques and strategies for building the Snake Game in Part 2 of our tutorial series. Level up your game development skills."
datePublished: Fri Jun 09 2023 03:18:15 GMT+0000 (Coordinated Universal Time)
cuid: clinzzjvb000a0amj1b9u49v8
slug: day-21-building-the-snake-game-pt-2
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1686272442303/a4acfcea-ed37-4f23-b385-6b6d4d5304e7.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1686280541489/ccf0f4d9-c455-4ced-817a-6fc9a67067f1.png
tags: blogging, python, game-development, 100daysofcode, object-oriented-programming

---

## Today's Objective

As I mentioned yesterday today we learned about class inheritance and how we're going to use it to build out the other classes to keep score of the game and to detect collisions with the food, the wall, and the snake's tail.

#### Class Inheritance

To sum it up: Class Inheritance is the ability to inherit the properties of another class in a newly created one. Imagine you have a class called `Parent` that has special features and methods. Now, you can make another class, let's call it the `Child` class, that can utilize everything from the `Parent` class and can add its own unique methods. So, instead of starting from scratch every time, we can reuse and extend the features of existing classes to make our code more efficient and organized.

To get this initialized you would have to call `super().__init__()` within the 1 `__init__` function. I've added a code snippet to give a simple visual:

```python
class Parent:
    def __init__(self, parent_attribute):
        self.parent_attribute = parent_attribute

class Child(Parent):
    def __init__(self, parent_attribute, child_attribute):
        super().__init__(parent_attribute)
        self.child_attribute = child_attribute

confession = Child("I'm the Pappy!", "That's the truth!")


print(confession.parent_attribute)
print(confession.child_attribute)
```

The above code will print:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686278185393/b527df6e-df98-4f4a-b223-2470b16ff689.png align="center")

This is very useful for minimizing the need to rinse and repeat for class and method creation.

## The Project

So today we need to finalize the game by completing 4 objectives:

1. Detect food collision.
    
2. Create a scoreboard.
    
3. Detect collision with the wall.
    
4. Detect collision with the snake's tail.
    

This called for the creation of some new files and classes that can be found in the `day-20`'s folder (since I'm not starting today in a new folder). Detecting the food and re-assigning it to a random spot inherited methods from the `Turtle()` class. We used that to create a new turtle and customized it to represent food. We created `refresh` method as well that moves the food to a random X & Y coordinate once the head of the snake was `{number-value}` away from it depending on what you set. The same thing goes for the scoreboard in which we created a new `Turtle,` but, had to dive into the docs again to alter it to work as a scoreboard. Finally, added the work to detect wall and tail collision to wrap up!

You can find the final project here -&gt; [https://github.com/kdleonard93/100-Days-Of-Code\_Python/pull/12](https://github.com/kdleonard93/100-Days-Of-Code_Python/pull/12). If you want, clone the code from Day 20 and give the game a try yourself to see what high score your can get!

## **EOD**

There's the game in all its glory! Gonna go ahead and find a way to throw this up on the App Store and start raking in secondary income 😂. But all jokes aside, creating this game was pretty fun, and was actually able to apply a bit of what I learned at work earlier today 😁.

#### If you want to keep up with my progress or just want to connect as peers, check out my social links below and give me a follow!

* [**🐦 Twitter**](https://twitter.com/RingoMandingo93)
    
* [**💻 Github**](https://github.com/kdleonard93)
    
* [**👾 Discord**](https://discord.com/users/407639833146818570)
    
* [**👔 LinkedIn**](https://www.linkedin.com/in/kyle-leonard93/)