## Day 3: Conditional Statements, Logical Operators, Code Block and Scope

## My realization
Okay folks, my ambition of doing two courses at the same time is just beyond exhausting. The issue that I have is that the 100 days of code course is much denser than the ZTM (Zero to Mastery) course; 100 days of code has 66 hours of material while the ZTM course only has 22 hours. So I see myself spending too much time thinking the ZTM course will have more concepts and explain things a bit more clearer but I've gained equal knowledge from both courses and they both have quality material. With that being said, this blog will now be focused on just the 100 days of code course. I still plan to go through the other course but now, at my own leisure. There is no point of me burning myself out after my workday of coding as well. 

Another thing that I will say is a bit frustrating is that the 100 days of code course claims that each day you shouldn't have to spend more than an hr - hr 1/2. Today's workload proved that to be inaccurate 😅. Here is a quick screenshot of the assignments that are sprinkled through the day's material before the "Project of the Day" -> https://www.loom.com/i/70128563ae324f808339210518276bc4. As you can see, there were two assingmets that took me a few attempts to get though. These assignments both had the "This is a Difficult Challenge" message before the instructions. There's no way someone new to Python will be able to get through the course material (which is literally an hr of video, already debunking the claim "Only 1 hour per day needed" ) + the assignments and then finally the project all in an hr - hr 1/2. However, the course material is still really good and I'm learning a lot, just a little salty that I planned my journey on only needing to spend a max of an hr and a half to 2 hours per day on these which is not the case for me (yet). But I digress 😏.

## Learning how Control Flow and Logical Operators work in Python.
Today was chalked full of lessons that I either have forgotten from JS or something I probably never fully grasped 😅. But to sum it up, today was a good amount of work with `if`/`elif`/`else` statements and how we go about nesting if/elif statements and how to list multiple separate if/elif statements. The assignments really tested my mental after a rough work day and there were definitely a few step away from the desk just because I'm exhausted. 
<iframe src="https://giphy.com/embed/l3V0p1WFoSIrzPLW0" width="480" height="480" frameBorder="0" class="giphy-embed" allowFullScreen></iframe><p><a href="https://giphy.com/gifs/l3V0p1WFoSIrzPLW0">via GIPHY</a></p>

Below are a few assignment examples:

#### BMI 2.0
##### Goal: Write a program that interprets the Body Mass Index (BMI) based on a user's weight and height. It should tell them the interpretation of their BMI based on the BMI value:
- Under 18.5 they are underweight
- Over 18.5 but below 25 they have a normal weight
- Over 25 but below 30 they are slightly overweight
- Over 30 but below 35 they are obese
- Above 35 they are clinically obese.

My Solution:
```
height = float(input("enter your height in m: "))
weight = float(input("enter your weight in kg: "))

bmi = round(weight / (height ** 2))

if bmi < 18.5:
    print(f"Your BMI is {bmi}, you are underweight.")
elif bmi > 18.5 and bmi < 25:
    print(f"Your BMI is {bmi}, you have a normal weight.")
elif bmi > 25 and bmi < 30:
    print(f"Your BMI is {bmi}, you are slightly overweight.")
elif bmi > 30 and bmi <= 35:
    print(f"Your BMI is {bmi}, you are obese.")
else:
    print(f"Your BMI is {bmi}, you are clinically obese.")
```

### Leap Year
#### Goal: Write a program that works out whether a given year is a leap year. A normal year has 365 days, leap years have 366, with an extra day in February. 

This is how you work out whether if a particular year is a leap year.

- on every year that is evenly divisible by 4 

- **except** every year that is evenly divisible by 100 

- **unless** the year is also evenly divisible by 400

My Solution:
```
year = int(input("Which year do you want to check? "))

if year % 4 != 0:
    print("Not Leap Year.")
elif year % 4 == 0:
    if year % 100 != 0:
        print("Leap Year.")
    elif year % 100 == 0:
        if year % 400 == 0:
            print("Leap Year.")
        else:
            print("Not Leap Year.")
```
I learned a good amount from these assignments and will def be saving these for future reference.

## 100 Days of Code Project: Day 3 - Treasure Island Pick Your Own Adventure
I was really excited to give this project a go when it was introduced at the beginning of the days material but after going through the day and spending more time that I thought I would, I ran out of time where I think it would be effective for me to work on this. I wouldn't retain as much knowledge as I would when fully alert.

So I plan to knock out this project before work tomorrow and will update this blog with the project and my thoughts! I at least wanted to get keep the blog post itself on schedule but will NOT be up until 12am CST trying to finish this project. If you're reading this tonight, check back tomorrow for the solution but if you happen to catch this article tomorrow 8/12, then the solution and my thought should be listed as an **Update:**
Got an update here for ya! Finished the Day 3 project and you can see the solution I had below 😁.

```
 print('''
*******************************************************************************
          |                   |                  |                     |
 _________|________________.=""_;=.______________|_____________________|_______
|                   |  ,-"_,=""     `"=.|                  |
|___________________|__"=._o`"-._        `"=.______________|___________________
          |                `"=._o`"=._      _`"=._                     |
 _________|_____________________:=._o "=._."_.-="'"=.__________________|_______
|                   |    __.--" , ; `"=._o." ,-"""-._ ".   |
|___________________|_._"  ,. .` ` `` ,  `"-._"-._   ". '__|___________________
          |           |o`"=._` , "` `; .". ,  "-._"-._; ;              |
 _________|___________| ;`-.o`"=._; ." ` '`."\` . "-._ /_______________|_______
|                   | |o;    `"-.o`"=._``  '` " ,__.--o;   |
|___________________|_| ;     (#) `-.o `"=.`_.--"_o.-; ;___|___________________
____/______/______/___|o;._    "      `".o|o_.--"    ;o;____/______/______/____
/______/______/______/_"=._o--._        ; | ;        ; ;/______/______/______/_
____/______/______/______/__"=._o--._   ;o|o;     _._;o;____/______/______/____
/______/______/______/______/____"=._o._; | ;_.--"o.--"_/______/______/______/_
____/______/______/______/______/_____"=.o|o_.--""___/______/______/______/____
/______/______/______/______/______/______/______/______/______/______/_____ /
*******************************************************************************
''')
print("Welcome to Treasure Island.")
print("Your mission is to find the treasure.")

# Write your code below this line 👇

choice1 = input(
    'You\'re at a cross road. Where do you want to go? Type "left" or "right" \n').lower()
if choice1 == "left":
    choice2 = input(
        'You\'ve come to a lake. There is an island in the middle of the lake. Type "wait" to wait for a boat. Type "swim" to swim across. \n').lower()
    if choice2 == "wait":
        choice3 = input(
            "You made it to Bountiful Booty Island, where the treasures run deep as your cheeks. There is a Trap house with 3 doors. One red, one yellow and one blue. Which colour do you choose? \n").lower()
        if choice3 == "red":
            print("It's a room full of fire. Game Over.")
        elif choice3 == "yellow":
            print("You secured the bag! You Win!")
        elif choice3 == "blue":
            print("You enter a room of thirst traps. Game Over.")
        else:
            print("You chose a door that leads into a black hole. Game Over.")
    else:
        print("You get attacked by an angry goblin. Game Over.")
else:
    print("You Became depressed because you didnt find the gem. Game Over.")
```

Goodnight folks! ✌🏾

#### If you want to keep up with my progress or just want to connect as peers, check out my social links below and give me a follow!

<ul>
<li><a href="https://twitter.com/RingoMandingo93" target="_blank">🐦 Twitter</a></li>
<li><a href="https://github.com/kdleonard93" target="_blank">💻 Github</a></li>
<li><a href="https://discord.com/users/407639833146818570" target="_blank">👾 Discord</a></li>
<li><a href="https://www.linkedin.com/in/kyle-leonard93/" target="_blank">👔 LinkedIn</a></li>
</ul>