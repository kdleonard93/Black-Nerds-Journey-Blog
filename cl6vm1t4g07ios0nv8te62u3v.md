## Day 5: Python Loops

## Today's Lesson
So today was all about loops and the use of what we learned in the previous lessons. I found it to be a bit easier than I thought it was going to be. Maybe because I banged my head on my desk so much when learning for/forEach loop and its variations in JS, it just clicked this time around after coming back to it. The way you implement it in python is a bit more straightforward as well.

#### Example of a `for()` loop in JS:
```
for (let i = 0; i < 9; i++) {
  console.log(i);
}
```
Output: 
```
012345678
```

##### My hardships with learning this in JS
The conditions in JS vs Python are what I believe were the key differences with me getting the python way of doing for loops. I will say it's a bit more condensed in JS but that's where I start to trip up once the logic and for loop gets more complicated; How you write the loop iteration was confusing for me at the start. Then once you get to situations where the initialization block and the conditional block are not added or needed, my brain starts to melt trying to figure out how to move forward. Usually results in me stuck with an infinite loop cause I never remembered how to properly break the loop in the body.

#### Example of a `for()` loop in Python:
```
numbers = [1, 2, 3]

for x in numbers:
  print(x)
```
Output: 
```
1
2
3
```
##### Python's straightforward approach
As you can see, Python's (simple) version of a `for` loop is somewhat different but all in all similar. The main difference is the loops syntax itself where you don't have to classify the variable (Python doesn't use the var/let/const syntax or anything similar). You also don't need to tell it how many times to run through the loops since indentation is key for the loops in Python. Any condition or statement within the for loop itself will be run in succession. When it comes to looping through a range of elements, its as simple as using the `range(start, finish)` method.

## Day 5: Password Generator
This project was actually pretty cool considering the need for ***VERY*** strong passwords these days.
Not much to explain about the function of the project (pretty obvious from the name 😄) and you can see my solution code below:
```
import random
letters = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l', 'm', 'n', 'o', 'p', 'q', 'r', 's', 't', 'u', 'v', 'w', 'x', 'y',
           'z', 'A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z']
numbers = ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9']
symbols = ['!', '#', '$', '%', '&', '(', ')', '*', '+']

print("Welcome to the PyPassword Generator!")
nr_letters = int(input("How many letters would you like in your password?\n"))
nr_symbols = int(input(f"How many symbols would you like?\n"))
nr_numbers = int(input(f"How many numbers would you like?\n"))

password = ""

for letter in range(1, nr_letters + 1):
    password += random.choice(letters)

for number in range(1, nr_numbers + 1):
    password += random.choice(numbers)

for symbol in range(1, nr_symbols + 1):
    password += random.choice(symbols)

strong_password = ''.join(random.sample(password, len(password)))

print(f"Your password is: {strong_password}")

```

My final solution was a bit different from the instructors' solution but the way I have it implemented is a bit cleaner and uses some methods that haven't been discussed yet (I didn't know them prior; Learned these methods as I was looking for ways to break the password up, shuffle it, and add it back together in a string.)

If you are curious on the instructors solutions, I've added it below:
```
import random
letters = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l', 'm', 'n', 'o', 'p', 'q', 'r', 's', 't', 'u', 'v', 'w', 'x', 'y', 'z', 'A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z']
numbers = ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9']
symbols = ['!', '#', '$', '%', '&', '(', ')', '*', '+']

print("Welcome to the PyPassword Generator!")
nr_letters = int(input("How many letters would you like in your password?\n")) 
nr_symbols = int(input(f"How many symbols would you like?\n"))
nr_numbers = int(input(f"How many numbers would you like?\n"))

password_list = []

for char in range(1, nr_letters + 1):
  password_list.append(random.choice(letters))

for char in range(1, nr_symbols + 1):
  password_list += random.choice(symbols)

for char in range(1, nr_numbers + 1):
  password_list += random.choice(numbers)

print(password_list)
random.shuffle(password_list)
print(password_list)

password = ""
for char in password_list:
  password += char

print(f"Your password is: {password}")
```
As you can see, the instructor's solution had a few more steps but everything is still pretty clear with her version.

## EOD
That concludes day 5. All in all, I enjoyed today's lesson and feel like I was able to grasp loops a bit better in Python my first time around. For day 6, looks like we are getting into While Loos, Code Blocks, and Functions.

#### If you want to keep up with my progress or just want to connect as peers, check out my social links below and give me a follow!

<ul>
<li><a href="https://twitter.com/RingoMandingo93" target="_blank">🐦 Twitter</a></li>
<li><a href="https://github.com/kdleonard93" target="_blank">💻 Github</a></li>
<li><a href="https://discord.com/users/407639833146818570" target="_blank">👾 Discord</a></li>
<li><a href="https://www.linkedin.com/in/kyle-leonard93/" target="_blank">👔 LinkedIn</a></li>
</ul>
