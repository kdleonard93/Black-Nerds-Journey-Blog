---
title: "Day 25 - US States Game + Movie List"
seoTitle: "Day 25 - US States Game + Movie List"
seoDescription: "Getting a better understanding of Pandas Library"
datePublished: Mon Jan 08 2024 04:17:47 GMT+0000 (Coordinated Universal Time)
cuid: clr4ewk6u00010ajk4jvhff2m
slug: day-25-us-states-game-movie-list
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1704686246528/563f51da-2228-4eb2-a321-ed765311dd76.png
tags: python, django, pandas, 100daysofcode, svelte, datamanipulation

---

## Let's start with the boring stuff

This past Sunday marked Day-25 of my 100 Days of Python journey. The challenge? To deepen my understanding of Pandas through a project that, honestly, wasn't the most thrilling – a U.S. States guessing game. Sure, it sounds mundane, but it's crucial stuff, especially since handling CSV files with Pandas is a fundamental skill in the world of finance apps. So, let's dive in and break down this project, tedious as it might have been!

#### 🎨 The Toolbox: turtle & pandas

For this project, we only needed two libraries: `turtle` and `pandas`. Turtle is like the old reliable of Python teaching tools. It's great for learning Python basics through small, graphical projects.

And then there's `pandas` – the data wizard of Python. Think of it as your go-to tool for manipulating structured data like CSV files. In this project, `pandas` was the key to managing the game's data, from importing state info to exporting our "to-learn" list. 📊📝

#### 🕹️ Setting the Scene: The Game Screen

The first order of business was setting up our game screen, creating a new window titled "U.S. States Game" and decking it out with a background image of a blank U.S. map. The image is a `.gif` file since the turtle library only works with those files for use within its methods. For example:

```
pythonCopy code    image = "blank_states_img.gif"  
    screen.addshape(image)
    turtle.shape(image)
```

With these lines, we're utilizing `turtle`'s `addshape()` and `shape()` functions to integrate our map into the game.

#### 📚 Crunching Data with Pandas

Next, we harnessed the power of `pandas` to read a CSV file named "50\_states.csv". This file was essentially the game's backbone, storing the names and coordinates of all U.S. states. We transformed this data into a list called `all_states`, setting us up for the game's logic. 🗺️

#### 🎮 The Gameplay: Guessing the States

This is where things got a tad more interesting. We started with an empty list, `guessed_states`, to track correct guesses. The game looped, prompting for state name guesses. Typing "Exit" would end the game and save a list of states still to be guessed into "states\_to\_learn.csv". A nice little feature to keep the challenge going! 🏁

#### ✍️ Marking the Map: Displaying Guessed States

Every correct guess brought a new turtle onto the scene to mark the state's name on the map. Simple, yet effective. You can find the project here if yu wanna check out the code.

So, that wraps up Day-25. While the project didn't exactly set my world on fire, it did reinforce some key skills. But let's be real, my mind kept drifting to a more exciting project...

### **Teasing FanFlix**

The working title? FanFlix. It's not set in stone, but the project itself is something I'm pretty pumped about. It's a CRUD app blending Svelte's sleekness with Django's robustness. I'm still chipping away at it, and I'll share more in a dedicated post once it's up and running. Stay tuned for a real-world example of Svelte and Django in harmony – something that's not too common out there.

#### 📢 Let's Connect!

Got any thoughts on Python, game coding, my main project, or just tech in general? Hit me up and lets chat!

* [**𝕏 Twitter**](https://twitter.com/RingoMandingo93)
    
* [**💻 Github**](https://github.com/kdleonard93)
    
* [**👾 Discord**](https://discord.com/users/407639833146818570)
    
* [**👔 LinkedIn**](https://www.linkedin.com/in/kyle-leonard93/)