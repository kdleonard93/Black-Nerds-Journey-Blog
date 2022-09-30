## Day 14: Rick and Morty Battle Royal Project

## Today's Lesson
For Day 14 I wanted to remix the project to challenge myself. I've completed 90% of the project in terms of my remix but to have the project work just like Angela has it in the course, I have that complete and ready to showcase. 

## Angela's Project
Just to clarify the objective of Angela's game: The game compares the follower count of 2 random users and the player guesses which user has a higher follower_count. The data set was something new for this project because while we learned about `dictionaries` and `lists`, we haven't used them in tandem with these capstone projects. But that's the gist of the game and there is a bunch of logic you have to think through in order to have this set up correctly. Some of which I needed some assistance with and others I tackled on my own. Note: The data was pre-set with a follower count and we didn't connect with any APIs to get the count.

## Rick and Morty Battle Royal
My spin on the game was to not only create data that fits the Rick and Morty universe but to also change the game's objective to be more of a fighting-style guessing game instead of just a guessing game. 

#### Change One
The first thing I changed was the key values:

***OG Data***
```
    {
        'name': 'Instagram',
        'follower_count': 346,
        'description': 'Social media platform',
        'country': 'United States'
    }
```

***Remix***
```
    {
        'name': 'Rick Sasnchez',
        'power': random.randint(1, 500),
        'skill': 'Intelligence',
        'country': 'United States'
    }
```

I updated`follow_count` to `power` and gave `power` a randomly generated number between 1-500. Next, I changed the `description` with `skill`. So far both still function the same, as in they are used as a description for the name of the person/fighter. The plan though was to associate skills with a function that give boons or disadvantages against other skills (kind of like elements in pokemon). That part of the project is not yet finished but since it's just fun addition and not needed. I was waiting to figure that out last.

#### Change Two
The second change was for one of the rules for the game. In Angela's version regardless of who has the higher user count, she instructed to make user B the new user A. The issue with my game is, I want the winner of the game to be assigned as fighter A on each new round, regardless if the winner is fighter A or fighter B. That logic is kicking my ass 😂. I've been looking into creating actual fighting games with Python to assist with getting this done but haven't cracked it just yet.

So besides the Winner carryover and skill stat addition, everything is working properly! I wrapped this up. I will add the code here but i will note that with the use of more files, I'm more likely going to start just linking my git repo. We will see though.

### Solution

Main.py
```
from game_data import data
import random
from art import logo, vs, defeat
import os


def clear():  # Cross-platform clear screen
    os.system('cls' if os.name == 'nt' else 'clear')


def format_data(account):
    """Format the account data into printable text."""
    account_name = account["name"]
    account_skill = account["skill"]
    return f"{account_name}, with the skill of {account_skill}"


def check_answer(fighter, a_power, b_power):
    """Take The User figter and power and return if they won the fight"""
    if a_power > b_power:
        return fighter == "a"
    else:
        return fighter == "b"


# Display Art
print(logo)
winning_streak = 0
game_should_continue = True
account_b = random.choice(data)


while game_should_continue:
    # Generat random account from game data
    account_a = account_b
    account_b = random.choice(data)
    while account_a == account_b:
        account_b = random.choice(data)

    print(f"{format_data(account_a)}.")
    print(vs)
    print(f"{format_data(account_b)}.")

    # Ask user to pick fighter.
    fighter = input(
        "Who will be your warrior? Type 'A' for the first fighter. Type `B` for the second fighter.").lower()

    # Check power level
    # Get the power level of each fighter
    a_power_lvl = account_a["power"]
    b_power_lvl = account_b["power"]
    is_correct = check_answer(fighter, a_power_lvl, b_power_lvl)

    # Clear Console
    clear()
    # Give feedback
    if is_correct:
        winning_streak += 1
        print(f"Your Fighter Wins!!!")
    else:
        game_should_continue = False
        print(defeat)
        print(f"Your streak was {winning_streak}")


# Use dice rolls to determin skill buffers
```
game_data.py
```
import random

data = [
    {
        'name': 'Rick Sasnchez',
        'power': random.randint(1, 500),
        'skill': 'Intelligence',
        'country': 'United States'
    },
    {
        'name': 'Morty Smith',
        'power': random.randint(1, 500),
        'skill': 'Wit',
        'country': 'Portugal'
    },
    {
        'name': 'Summer Smith',
        'power': random.randint(1, 500),
        'skill': 'Intelligence',
        'country': 'United States'
    },
    {
        'name': 'Beth Smith',
        'power': random.randint(1, 500),
        'skill': 'Intelligence',
        'country': 'United States'
    },
    {
        'name': 'Jerry Smith',
        'power': random.randint(1, 500),
        'skill': 'Sympathy',
        'country': 'United States'
    },
    {
        'name': 'A Piece Of Toast',
        'power': random.randint(1, 500),
        'skill': 'Luck',
        'country': 'United States'
    },
    {
        'name': 'Evil Morty',
        'power': random.randint(1, 500),
        'skill': 'Intelligence',
        'country': 'United States'
    },
    {
        'name': 'Mr. Poopy Butthole',
        'power': random.randint(1, 500),
        'skill': 'Power',
        'country': 'Argentina'
    },
    {
        'name': 'Mr. Goldenfold',
        'power': random.randint(1, 500),
        'skill': 'Agility',
        'country': 'United States'
    },
    {
        'name': 'Jessica',
        'power': random.randint(1, 500),
        'skill': 'Charm',
        'country': 'Brasil'
    },
    {
        'name': 'Space Beth',
        'power': random.randint(1, 500),
        'skill': 'Intelligence',
        'country': 'United States'
    },
    {
        'name': 'Tammy Gueterman',
        'power': random.randint(1, 500),
        'skill': 'Power',
        'country': 'Canada'
    },
    {
        'name': 'Squanchy',
        'power': random.randint(1, 500),
        'skill': 'Power',
        'country': 'United States'
    },
    {
        'name': 'Mr Meeseeks',
        'power': random.randint(1, 500),
        'skill': 'Agility',
        'country': 'United States'
    },
    {
        'name': 'Bird Person',
        'power': random.randint(1, 500),
        'skill': 'Intelligence',
        'country': 'Trinidad and Tobago'
    },
    {
        'name': 'Naruto Smith',
        'power': random.randint(1, 500),
        'skill': 'Luck',
        'country': 'United States'
    },
    {
        'name': 'Tricia Lang',
        'power': random.randint(1, 500),
        'skill': 'Charm',
        'country': 'United States'
    },
    {
        'name': 'Jacob',
        'power': random.randint(1, 500),
        'skill': 'Dexterity',
        'country': 'United States'
    },
    {
        'name': 'Joyce Smith',
        'power': random.randint(1, 500),
        'skill': 'Empathy',
        'country': 'United States'
    },
    {
        'name': 'Leonard Smith',
        'power': random.randint(1, 500),
        'skill': 'Empathy',
        'country': 'United States'
    },
    {
        'name': 'Mortimer Smith Jr.',
        'power': random.randint(1, 500),
        'skill': 'Power',
        'country': 'United States'
    },
    {
        'name': 'Bruce Chutback',
        'power': random.randint(1, 500),
        'skill': 'Wit',
        'country': 'United States'
    },
    {
        'name': 'Pencilvester',
        'power': random.randint(1, 500),
        'skill': 'Wit',
        'country': 'Spain'
    },
    {
        'name': 'Scary Terry',
        'power': random.randint(1, 500),
        'skill': 'Agility',
        'country': 'Spain'
    },
    {
        'name': 'Dr. Xenon Bloom',
        'power': random.randint(1, 500),
        'skill': 'Support',
        'country': 'Barbados'
    },
    {
        'name': 'Abradolf Lincler',
        'power': random.randint(1, 500),
        'skill': 'Tank',
        'country': 'United States'
    },
    {
        'name': "Mr. Nimbus",
        'power': random.randint(1, 500),
        'skill': 'Agility',
        'country': 'United States'
    },
    {
        'name': 'Noob Noob',
        'power': random.randint(1, 500),
        'skill': 'Wit',
        'country': 'United States'
    },
    {
        'name': 'Planetina',
        'power': random.randint(1, 500),
        'skill': 'Tank',
        'country': 'Colombia'
    },
    {
        'name': 'King Flippy Nips',
        'power': random.randint(1, 500),
        'skill': 'Wit',
        'country': 'Canada'
    },
    {
        'name': 'Hamurai',
        'power': random.randint(1, 500),
        'skill': 'Defense',
        'country': 'United States'
    },
    {
        'name': 'Sleepy Gary',
        'power': random.randint(1, 500),
        'skill': 'Support',
        'country': 'United States'
    },
    {
        'name': 'Ms. Pancakes',
        'power': random.randint(1, 500),
        'skill': 'Charm',
        'country': 'United States'
    },
    {
        'name': 'Taddy Mason',
        'power': random.randint(1, 500),
        'skill': 'Charm',
        'country': 'United States'
    },
    {
        'name': 'Two Brothers',
        'power': random.randint(1, 500),
        'skill': 'Power',
        'country': 'United Kingdom'
    },
    {
        'name': 'Jan Michale Jensen',
        'power': random.randint(1, 500),
        'skill': 'Power',
        'country': 'United States'
    },
    {
        'name': 'Shrimply Pibbles',
        'power': random.randint(1, 500),
        'skill': 'Agility',
        'country': 'United States'
    },
    {
        'name': 'Zeep Xanflorp',
        'power': random.randint(1, 500),
        'skill': 'Intelligence',
        'country': 'United States'
    },
    {
        'name': 'Elon Tusk',
        'power': random.randint(1, 500),
        'skill': 'Intelligence',
        'country': 'United Kingdom'
    },
    {
        'name': 'The President',
        'power': random.randint(1, 500),
        'skill': 'Intelligence',
        'country': 'Canada'
    },
    {
        'name': 'Davin',
        'power': random.randint(1, 500),
        'skill': 'Support',
        'country': 'India'
    },
    {
        'name': 'Glootie',
        'power': random.randint(1, 500),
        'skill': 'Wit',
        'country': 'United States'
    },
    {
        'name': 'Ants-In-My-Eyes Johnson',
        'power': random.randint(1, 500),
        'skill': 'Support',
        'country': 'India'
    },
    {
        'name': 'Michael and Pichael Thompson',
        'power': random.randint(1, 500),
        'skill': 'Support',
        'country': 'China'
    },
    {
        'name': 'The Vindicators',
        'power': random.randint(1, 500),
        'skill': 'Defense',
        'country': 'Brasil'
    },
    {
        'name': 'Unity',
        'power': random.randint(1, 500),
        'skill': 'Power',
        'country': 'Colombia'
    },
    {
        'name': 'Cop Rick and Cop Morty',
        'power': random.randint(1, 500),
        'skill': 'Agility',
        'country': 'Cuba'
    },
    {
        'name': 'Mr. Goldmanbachmajorian',
        'power': random.randint(1, 500),
        'skill': 'Wit',
        'country': 'United States'
    }
]

```
art.py
```
logo = """
 ▄▄▄▄▄▄▄▄▄▄▄  ▄▄▄▄▄▄▄▄▄▄▄  ▄▄▄▄▄▄▄▄▄▄▄  ▄    ▄       ▄▄▄▄▄▄▄▄▄▄▄  ▄▄        ▄  ▄▄▄▄▄▄▄▄▄▄        ▄▄       ▄▄  ▄▄▄▄▄▄▄▄▄▄▄  ▄▄▄▄▄▄▄▄▄▄▄  ▄▄▄▄▄▄▄▄▄▄▄  ▄         ▄ 
▐░░░░░░░░░░░▌▐░░░░░░░░░░░▌▐░░░░░░░░░░░▌▐░▌  ▐░▌     ▐░░░░░░░░░░░▌▐░░▌      ▐░▌▐░░░░░░░░░░▌      ▐░░▌     ▐░░▌▐░░░░░░░░░░░▌▐░░░░░░░░░░░▌▐░░░░░░░░░░░▌▐░▌       ▐░▌
▐░█▀▀▀▀▀▀▀█░▌ ▀▀▀▀█░█▀▀▀▀ ▐░█▀▀▀▀▀▀▀▀▀ ▐░▌ ▐░▌      ▐░█▀▀▀▀▀▀▀█░▌▐░▌░▌     ▐░▌▐░█▀▀▀▀▀▀▀█░▌     ▐░▌░▌   ▐░▐░▌▐░█▀▀▀▀▀▀▀█░▌▐░█▀▀▀▀▀▀▀█░▌ ▀▀▀▀█░█▀▀▀▀ ▐░▌       ▐░▌
▐░▌       ▐░▌     ▐░▌     ▐░▌          ▐░▌▐░▌       ▐░▌       ▐░▌▐░▌▐░▌    ▐░▌▐░▌       ▐░▌     ▐░▌▐░▌ ▐░▌▐░▌▐░▌       ▐░▌▐░▌       ▐░▌     ▐░▌     ▐░▌       ▐░▌
▐░█▄▄▄▄▄▄▄█░▌     ▐░▌     ▐░▌          ▐░▌░▌        ▐░█▄▄▄▄▄▄▄█░▌▐░▌ ▐░▌   ▐░▌▐░▌       ▐░▌     ▐░▌ ▐░▐░▌ ▐░▌▐░▌       ▐░▌▐░█▄▄▄▄▄▄▄█░▌     ▐░▌     ▐░█▄▄▄▄▄▄▄█░▌
▐░░░░░░░░░░░▌     ▐░▌     ▐░▌          ▐░░▌         ▐░░░░░░░░░░░▌▐░▌  ▐░▌  ▐░▌▐░▌       ▐░▌     ▐░▌  ▐░▌  ▐░▌▐░▌       ▐░▌▐░░░░░░░░░░░▌     ▐░▌     ▐░░░░░░░░░░░▌
▐░█▀▀▀▀█░█▀▀      ▐░▌     ▐░▌          ▐░▌░▌        ▐░█▀▀▀▀▀▀▀█░▌▐░▌   ▐░▌ ▐░▌▐░▌       ▐░▌     ▐░▌   ▀   ▐░▌▐░▌       ▐░▌▐░█▀▀▀▀█░█▀▀      ▐░▌      ▀▀▀▀█░█▀▀▀▀ 
▐░▌     ▐░▌       ▐░▌     ▐░▌          ▐░▌▐░▌       ▐░▌       ▐░▌▐░▌    ▐░▌▐░▌▐░▌       ▐░▌     ▐░▌       ▐░▌▐░▌       ▐░▌▐░▌     ▐░▌       ▐░▌          ▐░▌     
▐░▌      ▐░▌  ▄▄▄▄█░█▄▄▄▄ ▐░█▄▄▄▄▄▄▄▄▄ ▐░▌ ▐░▌      ▐░▌       ▐░▌▐░▌     ▐░▐░▌▐░█▄▄▄▄▄▄▄█░▌     ▐░▌       ▐░▌▐░█▄▄▄▄▄▄▄█░▌▐░▌      ▐░▌      ▐░▌          ▐░▌     
▐░▌       ▐░▌▐░░░░░░░░░░░▌▐░░░░░░░░░░░▌▐░▌  ▐░▌     ▐░▌       ▐░▌▐░▌      ▐░░▌▐░░░░░░░░░░▌      ▐░▌       ▐░▌▐░░░░░░░░░░░▌▐░▌       ▐░▌     ▐░▌          ▐░▌     
 ▀         ▀  ▀▀▀▀▀▀▀▀▀▀▀  ▀▀▀▀▀▀▀▀▀▀▀  ▀    ▀       ▀         ▀  ▀        ▀▀  ▀▀▀▀▀▀▀▀▀▀        ▀         ▀  ▀▀▀▀▀▀▀▀▀▀▀  ▀         ▀       ▀            ▀      
                                                                                                                                                                 
 ▄▄▄▄▄▄▄▄▄▄   ▄▄▄▄▄▄▄▄▄▄▄  ▄▄▄▄▄▄▄▄▄▄▄  ▄▄▄▄▄▄▄▄▄▄▄  ▄            ▄▄▄▄▄▄▄▄▄▄▄       ▄▄▄▄▄▄▄▄▄▄▄  ▄▄▄▄▄▄▄▄▄▄▄  ▄         ▄  ▄▄▄▄▄▄▄▄▄▄▄  ▄                        
▐░░░░░░░░░░▌ ▐░░░░░░░░░░░▌▐░░░░░░░░░░░▌▐░░░░░░░░░░░▌▐░▌          ▐░░░░░░░░░░░▌     ▐░░░░░░░░░░░▌▐░░░░░░░░░░░▌▐░▌       ▐░▌▐░░░░░░░░░░░▌▐░▌                       
▐░█▀▀▀▀▀▀▀█░▌▐░█▀▀▀▀▀▀▀█░▌ ▀▀▀▀█░█▀▀▀▀  ▀▀▀▀█░█▀▀▀▀ ▐░▌          ▐░█▀▀▀▀▀▀▀▀▀      ▐░█▀▀▀▀▀▀▀█░▌▐░█▀▀▀▀▀▀▀█░▌▐░▌       ▐░▌▐░█▀▀▀▀▀▀▀█░▌▐░▌                       
▐░▌       ▐░▌▐░▌       ▐░▌     ▐░▌          ▐░▌     ▐░▌          ▐░▌               ▐░▌       ▐░▌▐░▌       ▐░▌▐░▌       ▐░▌▐░▌       ▐░▌▐░▌                       
▐░█▄▄▄▄▄▄▄█░▌▐░█▄▄▄▄▄▄▄█░▌     ▐░▌          ▐░▌     ▐░▌          ▐░█▄▄▄▄▄▄▄▄▄      ▐░█▄▄▄▄▄▄▄█░▌▐░▌       ▐░▌▐░█▄▄▄▄▄▄▄█░▌▐░█▄▄▄▄▄▄▄█░▌▐░▌                       
▐░░░░░░░░░░▌ ▐░░░░░░░░░░░▌     ▐░▌          ▐░▌     ▐░▌          ▐░░░░░░░░░░░▌     ▐░░░░░░░░░░░▌▐░▌       ▐░▌▐░░░░░░░░░░░▌▐░░░░░░░░░░░▌▐░▌                       
▐░█▀▀▀▀▀▀▀█░▌▐░█▀▀▀▀▀▀▀█░▌     ▐░▌          ▐░▌     ▐░▌          ▐░█▀▀▀▀▀▀▀▀▀      ▐░█▀▀▀▀█░█▀▀ ▐░▌       ▐░▌ ▀▀▀▀█░█▀▀▀▀ ▐░█▀▀▀▀▀▀▀█░▌▐░▌                       
▐░▌       ▐░▌▐░▌       ▐░▌     ▐░▌          ▐░▌     ▐░▌          ▐░▌               ▐░▌     ▐░▌  ▐░▌       ▐░▌     ▐░▌     ▐░▌       ▐░▌▐░▌                       
▐░█▄▄▄▄▄▄▄█░▌▐░▌       ▐░▌     ▐░▌          ▐░▌     ▐░█▄▄▄▄▄▄▄▄▄ ▐░█▄▄▄▄▄▄▄▄▄      ▐░▌      ▐░▌ ▐░█▄▄▄▄▄▄▄█░▌     ▐░▌     ▐░▌       ▐░▌▐░█▄▄▄▄▄▄▄▄▄              
▐░░░░░░░░░░▌ ▐░▌       ▐░▌     ▐░▌          ▐░▌     ▐░░░░░░░░░░░▌▐░░░░░░░░░░░▌     ▐░▌       ▐░▌▐░░░░░░░░░░░▌     ▐░▌     ▐░▌       ▐░▌▐░░░░░░░░░░░▌             
 ▀▀▀▀▀▀▀▀▀▀   ▀         ▀       ▀            ▀       ▀▀▀▀▀▀▀▀▀▀▀  ▀▀▀▀▀▀▀▀▀▀▀       ▀         ▀  ▀▀▀▀▀▀▀▀▀▀▀       ▀       ▀         ▀  ▀▀▀▀▀▀▀▀▀▀▀              
                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  
"""

vs = """
 ██▒   █▓  ██████ 
▓██░   █▒▒██    ▒ 
 ▓██  █▒░░ ▓██▄   
  ▒██ █░░  ▒   ██▒
   ▒▀█░  ▒██████▒▒
   ░ ▐░  ▒ ▒▓▒ ▒ ░
   ░ ░░  ░ ░▒  ░ ░
     ░░  ░  ░  ░  
      ░        ░  
     ░            
"""

defeat = """
██▄   ▄███▄   ▄████  ▄███▄   ██     ▄▄▄▄▀ 
█  █  █▀   ▀  █▀   ▀ █▀   ▀  █ █ ▀▀▀ █    
█   █ ██▄▄    █▀▀    ██▄▄    █▄▄█    █    
█  █  █▄   ▄▀ █      █▄   ▄▀ █  █   █     
███▀  ▀███▀    █     ▀███▀      █  ▀      
                ▀              █          
                              ▀           
"""

```
## EOD
So I will plan to update this article with the new code once i figure out the last 2 additional features I wanted to add. If it ends up being a whole different beast than I think it is, I might make a Part 2 of this and add all of that code there.

#### If you want to keep up with my progress or just want to connect as peers, check out my social links below and give me a follow!
﻿
<ul>
<li><a href="https://twitter.com/RingoMandingo93" target="_blank">🐦 Twitter</a></li>
<li><a href="https://github.com/kdleonard93" target="_blank">💻 Github</a></li>
<li><a href="https://discord.com/users/407639833146818570" target="_blank">👾 Discord</a></li>
<li><a href="https://www.linkedin.com/in/kyle-leonard93/" target="_blank">👔 LinkedIn</a></li>
</ul>
