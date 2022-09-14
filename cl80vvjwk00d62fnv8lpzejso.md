## Day 11: The Balckjack Capstone Project - Solution

## Day 11 Continuation
As I noted on my 1st day 1 post, my plan was to break down this project into multiple parts. I worked on it throughout the weekend and finally finished it up. I will say, while I was able to get through a bit of the project without the hints, I still needed to utilize them when I got stuck which happened a decent amount of times 😅. Nonetheless, I know where I need to practice and will be doing so before moving on to Day 12. 

##Solution
```
############### Our Blackjack House Rules #####################

# The deck is unlimited in size.
# There are no jokers.
# The Jack/Queen/King all count as 10.
# The the Ace can count as 11 or 1.
# Use the following list as the deck of cards:
## cards = [11, 2, 3, 4, 5, 6, 7, 8, 9, 10, 10, 10, 10]
# The cards in the list have equal probability of being drawn.
# Cards are not removed from the deck as they are drawn.
# The computer is the dealer.

import random
from art import logo
import os


def clear():  # Cross-platform clear screen
    os.system('cls' if os.name == 'nt' else 'clear')


def deal_card():
    """Getting a random card from the list of available cards and returning the value"""
    cards = [11, 2, 3, 4, 5, 6, 7, 8, 9, 10, 10, 10, 10]
    return random.choice(cards)


def calculate_score(cards):
    """Calcuate the total sum of the list of dealt cards"""
    if sum(cards) == 21 and len(cards) == 2:
        return 0
    if 11 in cards and sum(cards) > 21:
        cards.remove(11)
        cards.append(1)

    return sum(cards)


def compare(user_score, computer_score):
    if user_score == computer_score:
        return "Draw"
    elif computer_score == 0:
        return "Lose, Opponent has Blackjack"
    elif user_score == 0:
        return "Win with a Blackjack"
    elif user_score > 21:
        return "Bust. You Lose"
    elif computer_score > 21:
        return "Computer went over 21. You win."
    elif computer_score < user_score:
        return "You have the higher score. You win!"
    else:
        return "You Lose."


def play_game():
    print(logo)
    # Deal User and Comp 2 cards each
    user_cards = []
    computer_cards = []
    is_game_over = False
    for _ in range(2):
        user_cards.append(deal_card())
        computer_cards.append(deal_card())

    while not is_game_over:
        user_score = calculate_score(user_cards)
        computer_score = calculate_score(computer_cards)
        print(f"User Cards: {user_cards}. Your Score: {user_score}")
        print(f"Computer's First card: {computer_cards[0]}")

        if user_score == 0 or computer_score == 0 or user_score > 21:
            is_game_over = True
        else:
            user_should_deal = input(
                "Do you want to draw another card? Type Y for Yes or N for No: ").lower()
            if user_should_deal == "y":
                user_cards.append(deal_card())
            else:
                is_game_over = True

    while computer_score != 0 and computer_score < 17:
        computer_cards.append(deal_card())
        computer_score = calculate_score(computer_cards)

    print(f"  Your final hand: {user_cards}. Your final score: {user_score}")
    print(
        f"  Computer's final hand: {computer_cards}. Comnputer's final score: {computer_score}")
    print(compare(user_score, computer_score))


while input("Would you like deal again? Y for yes and N for no: ") == "y":
    clear()
    play_game()

```

#### If you want to keep up with my progress or just want to connect as peers, check out my social links below and give me a follow!
﻿
<ul>
<li><a href="https://twitter.com/RingoMandingo93" target="_blank">🐦 Twitter</a></li>
<li><a href="https://github.com/kdleonard93" target="_blank">💻 Github</a></li>
<li><a href="https://discord.com/users/407639833146818570" target="_blank">👾 Discord</a></li>
<li><a href="https://www.linkedin.com/in/kyle-leonard93/" target="_blank">👔 LinkedIn</a></li>
</ul>
