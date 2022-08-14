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

/