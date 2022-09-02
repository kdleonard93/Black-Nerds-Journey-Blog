## Day 10: Functions With Outputs and Calculator Project

## Today's Lesson
More function fun today as we touched on functions with outputs. The main takeaway with the concept of functions with outputs was that you would utilize a `return` statement instead of using `print`. This way, the output of the function's instructions would then be able to be passed into another function as an argument. Below is an example from our leap year exercise from a previous lesson refactored:

```
def is_leap(year):
  if year % 4 == 0:
    if year % 100 == 0:
      if year % 400 == 0:
        return True
      else:
        return False
    else:
      return True
  else:
    return False

def days_in_month(year, month):
  month_days = [31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31]
  if is_leap(year) and month == 2:
    return 29
  return month_days[month - 1]

year = int(input("Enter a year: "))
month = int(input("Enter a month: "))
days = days_in_month(year, month)
print(days)
```

Here you can see that we are looking to find the days in a month but we also check if it is a leap year or not since on leap years the month of Feb has 29 days instead of 28. Before, the `return` statements in the ` def is_leap(year)` function were just parent statements stating if it was a leap year or not. Understanding this is getting a bit clearer when thinking in a bigger scope but still can be a bit tricky for me.

## The Project
Today we worked on creating a calculator and it was for sure challenging. In order to achieve our goal, we had to start by defining the operations, which was easy enough. Example: `def add(n1, n2): return n1 + n2` and so on. After that, we needed to create a dictionary for the operations and so far things were looking pretty smooth. But that's where it ended lol. The hints and explanation videos started off by having us create the first part of the calculation request, asking the user to give a number, then pick an operation, then give a second number. After the second number is given we define another value, `calculation_function` which holds the operation entered by the user. That gave us the basic calculation set up but the next steps were to have the user decide if they wanted to press 'y' to keep going and use the last answer to make more calculations or press 'n' to start a new calculation. This is where I was dead stuck and after spending some time trying to figure it out. I new we had to use a while loop but couldn't figure out how exactly. After some time working on it and looking into the hints, we needed to use recursion after the else statement so that there is not an infinite loop as well as make another variable `should_continue`, or something along those lines, and set it to initially be True. Below you can find my solution on how I put the above together:

```
from art import logo

# add


def add(n1, n2):
    return n1 + n2

# subtract


def subtract(n1, n2):
    return n1 - n2

# multiply


def multiply(n1, n2):
    return n1 * n2


# divide
def divide(n1, n2):
    return n1 / n2


operations = {
    "+": add,
    "-": subtract,
    "*": multiply,
    "/": divide
}


def calculator():
    print(logo)
    num1 = float(input("What's the first number?: "))
    for symbol in operations:
        print(symbol)

    should_continue = True

    while should_continue:
        operation_symbol = input("Pick an operation: ")
        num2 = float(input("What's the next number?: "))
        calculation_function = operations[operation_symbol]
        answer = (calculation_function(num1, num2))

        print(f"{num1} {operation_symbol} {num2} = {answer}")

        if input(f"Type 'y' to continue calculating with {answer}, or type 'n' to start a new calculation: ") == "y":
            num1 = answer
        else:
            should_continue = False
            calculator()


calculator()

```

## EOD
Today was fun but Angela's closing video has me a bit worried about tomorrow 😅. It's the first capstone project and it's to create a BlackJack game 😬. See you, folks, for day 11 ✌🏾

#### If you want to keep up with my progress or just want to connect as peers, check out my social links below and give me a follow!

<ul>
<li><a href="https://twitter.com/RingoMandingo93" target="_blank">🐦 Twitter</a></li>
<li><a href="https://github.com/kdleonard93" target="_blank">💻 Github</a></li>
<li><a href="https://discord.com/users/407639833146818570" target="_blank">👾 Discord</a></li>
<li><a href="https://www.linkedin.com/in/kyle-leonard93/" target="_blank">👔 LinkedIn</a></li>
</ul>