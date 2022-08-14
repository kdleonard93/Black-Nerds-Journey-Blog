## Day 4: Randomization and Python Lists

## Today's Lesson
I feel like Day 4 was a much need breather from day 3. The assignments and video lectures seem to click a bit more. The main takeaway was the use of the Random Module and Lists. 
#### Random Module
The random module is a built-in module to help you generate random elements. It was pretty straight forward and the assignments were better explained as well, making them quicker to work through.
An example of that is the Heads or Tails assignment below:
```
#Remember to use the random module
#Hint: Remember to import the random module here at the top of the file. 🎲
import random
# 🚨 Don't change the code below 👇
test_seed = int(input("Create a seed number: "))
random.seed(test_seed)
 # 🚨 Don't change the code above 👆 It's only for testing your code.
	 
#Write the rest of your code below this line 👇

random_int = random.randint(0, 1)

if random_int == 1:
    print("Heads")
else:
    print("Tails")
```
#### Lists
Lists in Python are pretty much like Arrays in JS. We went over indexing, index errors, and nesting lists.
The same thing goes with the Lists assignments as in they were clearly explained. 
Example assignment below: 
```
# 🚨 Don't change the code below 👇
row1 = ["⬜️","⬜️","⬜️"]
row2 = ["⬜️","⬜️","⬜️"]
row3 = ["⬜️","⬜️","⬜️"]
map = [row1, row2, row3]
print(f"{row1}\n{row2}\n{row3}")
position = input("Where do you want to put the treasure?")
# 🚨 Don't change the code above 👆

#Write your code below this row 👇
horizontal = int(position[0])
vertical = int(position[1])


selected_row = (map[vertical - 1])
selected_row[horizontal - 1] = "X"

#Write your code above this row 👆

# 🚨 Don't change the code below 👇
print(f"{row1}\n{row2}\n{row3}")
```
## Day 4 Project - Rock Paper Scissors
The Rock Paper Scissors game I feel was pretty easy to get done once you figure out the logic. Basically you start off with the user input ranging from 0-2 and then you get the computer input by using the random generator. After the inputs are stored and changed to integers, you just go through a bunch of if/elif statements to compare the values and see who won. My code can be found below:
```
import random
rock = '''
    _______
---'   ____)
      (_____)
      (_____)
      (____)
---.__(___)
'''

paper = '''
    _______
---'   ____)____
          ______)
          _______)
         _______)
---.__________)
'''

scissors = '''
    _______
---'   ____)____
          ______)
       __________)
      (____)
---.__(___)
'''

# Write your code below this line 👇

user_choice = int(input(
    "What do you choose? Type 0 for Rock, 1 for Paper, 2 for Scissors:\n "))

computer_choice = random.randint(0, 2)
print(f"Computer chose {computer_choice}")

if user_choice == computer_choice:
    print("It's a tie!")
elif user_choice == 0 and computer_choice == 1:
    print("Computer wins!")
elif user_choice == 0 and computer_choice == 2:
    print("User wins!")
elif user_choice == 1 and computer_choice == 0:
    print("User wins!")
elif user_choice == 1 and computer_choice == 2:
    print("Computer wins!")
elif user_choice == 2 and computer_choice == 0:
    print("Computer wins!")
elif user_choice == 2 and computer_choice == 1:
    print("User wins!")
else:
    print("Invalid Input, loser")
```
##EOD
I feel today was needed after going through a rough day 3 😅. I also know I said I was going to do day 4 AND day 5 but I needed to do some dog sitting for a bit and let's be honest, day 5 is going to be about loops and that always tripped me up in JS and I still don't have quite the handle on it lol. So I'll double back on that tomorrow.

Goodnight folks ✌🏾

#### If you want to keep up with my progress or just want to connect as peers, check out my social links below and give me a follow!

<ul>
<li><a href="https://twitter.com/RingoMandingo93" target="_blank">🐦 Twitter</a></li>
<li><a href="https://github.com/kdleonard93" target="_blank">💻 Github</a></li>
<li><a href="https://discord.com/users/407639833146818570" target="_blank">👾 Discord</a></li>
<li><a href="https://www.linkedin.com/in/kyle-leonard93/" target="_blank">👔 LinkedIn</a></li>
</ul>