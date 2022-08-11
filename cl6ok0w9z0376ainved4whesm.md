## Day 2: Python Object and Data Structure Basics (Part 2)

## Today's Task
So today is kind of a continuation of yesterday in terms of the information learned. I'm not sure how this will play out as I get along in both courses (Details on both courses are <a href="https://blacknerd.dev/the-second-start-of-my-journey-to-become-a-fullstack-dev">noted in my 1st article</a>) but it seems like the 0-100 course will move a bit faster than the 100 days of code (aka 100-DOC) course. With that being said, there might be days where I just discuss the project of the day from the 100-DOC course since I want to stay pretty concurrent with both courses. I'm also going to try and get up a bit earlier to do some of the pre-work or watch some of the course material before the evening so I',m not up late trying to stay true to my promise to myself of daily projects and blog posts.

## 100 Days of Code Project: Day 2 - Tip Calculator
Today's project was a tip calculator. I thought the process of getting an accurate split amount was a pretty cool concept and could see myself applying that logic to other things down the line. This project required the use of `f("strings)`, mathematical operations, value conversion (Strings -> Integers or Integers -> Float or Float/Int -> String), the `round()` function, and everything we learned previously. I'd say the conversions tripped me up ever so slightly since it's typed a little differently than JS but once I did a few, it started to click. Below is the final result of my project:
```
print("Welcome to the band name generator")
bill = int(input("What is the total bill?"))
tip = int(input("What is the tip percentage? 10, 12, 0r 15?"))
people = int(input("How many people are splitting the bill?"))

total = round(bill * (1 + tip/100))
share = round(total / people, 2)

print(f"Each person should pay: {share}")
```
Note: I don't plan on always adding just the solution to the article. In the beginning, while the projects are not that heavy with code, I will just throw a quick snippet. Once the projects get bigger, I'll still throw snippets but the full project will live on GitHub. I have my first 2 days pushed and plan to push a repo for each day.

## EOD

Today was fun and pretty interesting but all In all, I'm still at the very basic stages so things are pretty understandable and semi-relatable to JS.

Note #2: I wanted to reiterate that this blog's main purpose is for me to notate my journey for notes and helpful feedback. If anyone else finds these articles helpful or just entertaining, that'll be a bonus. I also want to warn you that once I get further into the projects, I will most likely get less formal with my writing. I don't want to sound like a robot or have my articles feel like cookie-cutter opinion pieces/blogs. (Your boi, aka me, has a pretty silly personality when I get comfortable 😄).

#### If you want to keep up with my progress or just want to connect as peers, check out my social links below and give me a follow!

<ul>
<li><a href="https://twitter.com/RingoMandingo93" target="_blank">🐦 Twitter</a></li>
<li><a href="https://github.com/kdleonard93" target="_blank">💻 Github</a></li>
<li><a href="https://discord.com/users/407639833146818570" target="_blank">👾 Discord</a></li>
<li><a href="https://www.linkedin.com/in/kyle-leonard93/" target="_blank">👔 LinkedIn</a></li>
</ul>