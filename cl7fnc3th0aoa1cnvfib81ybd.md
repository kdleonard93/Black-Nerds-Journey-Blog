## Day 9: Dictionaries, Nesting, & the Secret Auction

## Today's Lesson
Hey folks, today we learned about Dictionaries and Nesting dictionaries and lists within one another. Everything covered with dictionaries ranged from creating, emptying, and updating the dictionaries. After learning about that, we covered nesting dictionaries within an array or another dictionary.

For example, one of the exercises asked us to write the function allowing new countries to be added to the travel_log list, which was a list of 2 dictionaries. Each of those dictionaries had a `cities` key value that contained a list of cities.
Figuring out the `def` structure was straightforward enough but it took me a bit to figure out that I needed to create a new empty dictionary to hold the values passed when calling the function. My solution to the exercise is below:

```
travel_log = [
    {
        "country": "France",
        "visits": 12,
        "cities": ["Paris", "Lille", "Dijon"]
    },
    {
        "country": "Germany",
        "visits": 5,
        "cities": ["Berlin", "Hamburg", "Stuttgart"]
    },
]
# 🚨 Do NOT change the code above

# TODO: Write the function that will allow new countries
# to be added to the travel_log. 👇

# new_visits = int
# new_city = ""


def add_new_country(country_visited, times_visited, cities_visited):
    new_country = {}
    new_country["country"] = country_visited
    new_country["visits"] = times_visited
    new_country["cities"] = cities_visited
    travel_log.append(new_country)


# 🚨 Do not change the code below
add_new_country("Russia", 2, ["Moscow", "Saint Petersburg"])
print(travel_log)

```

## Project
As for the project of the day. We were to create a secret auction program that takes in the input name as the key and the input price as the value. After getting the first user's name, a prompt then asks "if there are other auctioneers. If yes, then the console is cleared and it loops over the same questions. Once the user answers no for "additional auctioneers", then we loop through the current bids and whichever one is the highest, the results are printed with a message that they won.

##### Solution:
```
from art import logo
import os


def clear():  # Cross-platform clear screen
    os.system('cls' if os.name == 'nt' else 'clear')


print(logo)

bid = {}
bidding_finished = False


def find_highest_bidder(bidding_record):
    highest_bid = 0
    winner = ""
# bidding_record = {"Kyle": 342, "Ky": 123}
    for bidder in bidding_record:
        bid_amount = bidding_record[bidder]
        if bid_amount > highest_bid:
            highest_bid = bid_amount
            winner = bidder
    print(f"The Winner is {winner} with a bid of ${highest_bid}")


while not bidding_finished:
    name = input("What Is you Name: ")
    price = int(input("What is your bid price: $"))
    bid[name] = price
    continue_bidding = input(
        "Are there any other bidders? Yes or No?\n")
    if continue_bidding == "no":
        bidding_finished = True
        find_highest_bidder(bid)
    elif continue_bidding == "yes":
        clear()

```

#### Note:
Since I didn't use Replit as angela did, and used my own IDE/text Editor, I had to use a different method of clearing the console. Unlike the method she used, which was importing `clear()` from the Replit package, I instead imported `os` and built out my `clear()` function that way.

## EOD
That wraps up Day 9 and while it was a challenge, it was a bit less time-consuming than day 8. See you folks for day 10 ✌🏾

#### If you want to keep up with my progress or just want to connect as peers, check out my social links below and give me a follow!

<ul>
<li><a href="https://twitter.com/RingoMandingo93" target="_blank">🐦 Twitter</a></li>
<li><a href="https://github.com/kdleonard93" target="_blank">💻 Github</a></li>
<li><a href="https://discord.com/users/407639833146818570" target="_blank">👾 Discord</a></li>
<li><a href="https://www.linkedin.com/in/kyle-leonard93/" target="_blank">👔 LinkedIn</a></li>
</ul>
