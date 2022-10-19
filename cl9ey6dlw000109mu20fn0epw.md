# Day 15: Local Dev Setup + Coffee Machine Project

## Today's Objective & News Update
Holla to my future self and anyone that's still reading along. Between day 14 and Day 15, a lot of changes happened within my personal life and career. I'm happy to say, I LANDED THE JOB AS A SOFTWARE ENGINEER I AT MY CURRENT COMPANY!! 
&nbsp;
<iframe src="https://giphy.com/embed/br43v11JLIm9fUlVwX" width="480" height="270" frameBorder="0" class="giphy-embed" allowFullScreen></iframe><p><a href="https://giphy.com/gifs/mlb-chicago-white-sox-tim-anderson-br43v11JLIm9fUlVwX">via GIPHY</a></p>
&nbsp;
So lately, I've just been going over some dev tools I will be using for the job as well as watching some PHP videos since that's the main language used for that team. Hoping that trying to learn both PHP as well won't hinder my grasp of more complicated Python concepts in the future but difficult challenges are usually how I grow.

## Coffee Machine Project
We didn't learn anything new for day 15 and the main focus was to get the students set with their local environment. Since I was using my own local environment for the first 14 days, I pretty much speed through those sections.

#### Solution
```
import os


def clear():  # Cross-platform clear screen
    os.system('cls' if os.name == 'nt' else 'clear')
    
MENU = {
    "espresso": {
        "ingredients": {
            "water": 50,
            "coffee": 18,
        },
        "cost": 1.5,
    },
    "latte": {
        "ingredients": {
            "water": 200,
            "milk": 150,
            "coffee": 24,
        },
        "cost": 2.5,
    },
    "cappuccino": {
        "ingredients": {
            "water": 250,
            "milk": 100,
            "coffee": 24,
        },
        "cost": 3.0,
    }
}

profit = 0
resources = {
    "water": 300,
    "milk": 200,
    "coffee": 100,
}


def is_resource_sufficient(order_ingredients):
    """Returns True when order can be made, False if ingredients are insufficient."""
    for item in order_ingredients:
        if order_ingredients[item] > resources[item]:
            print(f"​Sorry there is not enough {item}.")
            return False
    return True


def process_coins():
    """Returns the total calculated from coins inserted."""
    print("Please insert coins.")
    total = int(input("how many quarters?: ")) * 0.25
    total += int(input("how many dimes?: ")) * 0.1
    total += int(input("how many nickles?: ")) * 0.05
    total += int(input("how many pennies?: ")) * 0.01
    return total


def is_transaction_successful(money_received, drink_cost):
    """Return True when the payment is accepted, or False if money is insufficient."""
    if money_received >= drink_cost:
        change = round(money_received - drink_cost, 2)
        print(f"Here is ${change} in change.")
        global profit
        profit += drink_cost
        return True
    else:
        print("Sorry that's not enough money. Money refunded.")
        return False


def make_coffee(drink_name, order_ingredients):
    """Deduct the required ingredients from the resources."""
    for item in order_ingredients:
        resources[item] -= order_ingredients[item]
    print(f"Here is your {drink_name} ☕️. Enjoy!")


is_on = True

while is_on:
    choice = input("​What would you like? (espresso/latte/cappuccino): ")
    if choice == "off":
        is_on = False
    elif choice == "report":
        print(f"Water: {resources['water']}ml")
        print(f"Milk: {resources['milk']}ml")
        print(f"Coffee: {resources['coffee']}g")
        print(f"Money: ${profit}")
    else:
        drink = MENU[choice]
        if is_resource_sufficient(drink["ingredients"]):
            payment = process_coins()
            if is_transaction_successful(payment, drink["cost"]):
                make_coffee(choice, drink["ingredients"])
```
### EOD
I'm hoping to get back into my daily or at least every other day grind for this course but once I start my new position on 11/1, who knows exactly how taxing my days will be trying to learn a whole new working environment with my new team. Only time will tell 😁 

#### If you want to keep up with my progress or just want to connect as peers, check out my social links below and give me a follow!
﻿
<ul>
<li><a href="https://twitter.com/RingoMandingo93" target="_blank">🐦 Twitter</a></li>
<li><a href="https://github.com/kdleonard93" target="_blank">💻 Github</a></li>
<li><a href="https://discord.com/users/407639833146818570" target="_blank">👾 Discord</a></li>
<li><a href="https://www.linkedin.com/in/kyle-leonard93/" target="_blank">👔 LinkedIn</a></li>
</ul>