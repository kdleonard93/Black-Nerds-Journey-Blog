## Day 12: Global / Local Scope & Number Guessing Game

## Today's Lesson
After another good break (took a trip to South Dakota for a BachlorX party) and a couple days using my free time to get familiar with PHP, I'm back from day 12, and today's lesson was pretty digestible. In the past projects and lessons, we technically used global and local scope within our code but this Angela dug a little deeper into the concepts.

### Local Scope

Local scope is just a variable or definition that can only be called inside of the `def` that it's nested in. For example, in this code below, I created a `def` named `high_five` and just gave it some simple logic. The `clean_high_five = True` inside the `high_five` definition is the local scope and when I call the `def` it returns "Nice One". Even though I tried to change the value to "False", the call was outside of the scope so it did not take effect.

```
def high_five():
    clean_high_five = True
    if clean_high_five == True:
        print("Nice one!")
    else:
        print("Oof, swing and a miss")

clean_high_five = False
high_five()
```

Now If I were to change the code around a bit, like below, the print statement would now be "Oof, swing and a miss" since I changed the value inside the scope of the definition.

```
def high_five():
    clean_high_five = True
    clean_high_five = False
    if clean_high_five == True:
        print("Nice one!")
    else:
        print("Oof, swing and a miss")


high_five()
```

### Global Scope

Global Scope is a def that you really don't plan on changing. Within CSS, global scope is really keyed in for me since there are certain styles and colors you want to be consistent throughout the entire design. I've tried to put this as simple as possible below.
```
globe = "Yes"


def is_it_global():
    print(f"{globe}")


is_it_global()
```

Here I'm able to reference the variable "globe" within the `def is_it_global()`. That's about as simple as I can explain global scope right now 😅. There are ways to get around modifying global scope within a `def`. For example, instead of printing, I can use a return statement and just save it to the global scope like so:
```
globe = "Yes"


def is_it_global():
    return "Modified"


globe = is_it_global()
print(f"{globe}")
```
Not really recommended in most cases though.

## Project
We made a guessing game today and mine is named "Leo's Guessing Game" (I know, really creative 😂). It was the first project she didn't give any hints or a starter guide for so it was a bit of an uphill battle for a bit but utilizing resources and previous projects as references helped a good amount and I only got stuck on the `while` loop logic a bit. Below is my solution code.
```
from random import randint
from art import logo

easy_mode = 10
hard_mode = 5

# Function to check answer
def check_answer(guess, answer, turns):
    """User checks guess against the answer. If 'Too High' or 'Too Low', return remaining # of turns."""
    if guess > answer:
        print("Too High")
        return turns - 1
    elif guess < answer:
        print("Too Low")
        return turns - 1
    else:
        print(f"You Win! The answer was {answer}")


# Function to set dificulty
def set_dificulty():
    level = input("Choose your dificulty. 'Easy' or 'Hard'").lower()
    if level == "easy":
        return easy_mode
    else:
        return hard_mode


# Function to choose a random number 1 - 100
def leos_game():
    print(logo)
    print("Welcome to your boi's guessing game! Super straight forward 😁")
    print("Try to guess the right number between 1 - 100")
    answer = randint(1, 100)

    turns = set_dificulty()
    # Repeat the guessing functionality if they get it wrong.
    guess = 0
    while guess != answer:
        print(f"You have {turns} turns left to guess the number.")

        guess = int(input("Make a guess: "))

        # Track the number of turns and reduce by 1 if they get it wrong.
        turns = check_answer(guess, answer, turns)
        if turns == 0:
            print("You ran out of turns, loser.")
            return
        elif guess != answer:
            print("Guess again")


leos_game()

```
## EOD
That wraps up my day and tomorrow it looks like we are working on debugging only, so there wont be a project but I still plan to write up my day for reference.

#### If you want to keep up with my progress or just want to connect as peers, check out my social links below and give me a follow!
﻿
<ul>
<li><a href="https://twitter.com/RingoMandingo93" target="_blank">🐦 Twitter</a></li>
<li><a href="https://github.com/kdleonard93" target="_blank">💻 Github</a></li>
<li><a href="https://discord.com/users/407639833146818570" target="_blank">👾 Discord</a></li>
<li><a href="https://www.linkedin.com/in/kyle-leonard93/" target="_blank">👔 LinkedIn</a></li>
</ul>


