## Day 8: Function Parameters & Ceasar Cipher

## Day 8's Lesson
Starting in this section, we touch on using function parameters with inputs. Angela discusses the difference between positional vs. keyword arguments. The lesson itself was straightforward. One thing I questioned was the use of keyword arguments. Angela only explained assigning the arguments within the parameters. However, I found it much easier to read and understand by assigning the variables outside of the parameters and just adding the stored variable within.

For example:

Angela's way
```
def grett_with(name, location):
  print(f"Hello {name}")
  print(f"What is it like in {location}?")

greet_with(name="Kyle", location="Illinois")
```

How I did it (can go 2 ways):
```
name = input("What is your name: ")
location = input("Where do you live: ")

def grett_with(name, location):
  print(f"Hello {name}")
  print(f"What is it like in {location}?")

greet_with(name, location)

# or

name = "Kyle"
location = "Illinois"

def grett_with(name, location):
  print(f"Hello {name}")
  print(f"What is it like in {location}?")

greet_with(name, location)
```

I guess for me since I'm coming from JS, the way I have it seems to click more with me but if there is some reason why I shouldn't be doing it that way, hopefully, someone can enlighten me, or maybe I will enlighten myself at some point.

## The tough part: Caesar Cypher Project
Alright, so the goal is to create a game/tool that can encode and decode messages by following a set of prompts. It starts off by asking the user if they want to decode or encode a message. When encoding, the user is asked to type a message, then type the shift number which is how many times the user wasn't in the position of the letter to shift (Angela mentioned something about Caesar doing this to send encoded messages during the war but this is not a history journal so I won't explain any of that 😂).
After the number is chosen, the terminal gives you the encoded result. It'll then ask you if you want to go again and if you choose yes, you can decode your message by following the same set of prompts. For the decode to work, you have to match the same shift number as well.

I haven't gotten through all of this project because it's a bit tricky for me but, I plan to have an update and solution by tomorrow!

####**Update 8/26/22**
Okay, so this project kind of kicked my ass 😅. I had to go through some of the "To-dos" using some of her walkthroughs because I just couldn't figure out how to shift the letters initially. After figuring out how to shift them forward, shifting them backward wasn't too hard but then the last bit, where we had to account for bugs or irregular inputs (Examples: if the shift number is over the total number of letters in the alphabet and of the users enter anything other than letters like symbols, numbers, and spaces) It was all mentally exhausting and is something I will need to practice on more. Nothing new, just practice more problems similar to this but with different logic needs. My solution can be found below.

```
from art import logo

alphabet = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l', 'm', 'n', 'o', 'p', 'q', 'r', 's', 't', 'u', 'v', 'w', 'x', 'y',
            'z', 'a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l', 'm', 'n', 'o', 'p', 'q', 'r', 's', 't', 'u', 'v', 'w', 'x', 'y', 'z']


def caesar(text, shift, direction):
    end_text = ""
    if direction == "decode":
        shift *= -1
    for char in text:
        if char in alphabet:
            position = alphabet.index(char)
            new_position = position + shift
            end_text += alphabet[new_position]
        else:
            end_text += char
    print(f"The {direction}d text is {end_text}")


print(logo)

should_continue = True
while should_continue:
    direction = input("Type 'encode' to encrypt, type 'decode' to decrypt:\n")
    text = input("Type your message:\n").lower()
    shift = int(input("Type the shift number:\n"))

    shift = shift % 26
    caesar(text, shift, direction)
    result = input(
        "Type 'yes' if you want to go again. Otherwise, type 'no'.\n")
    if result == "no":
        should_continue = False
        print("Peace")
```

#### If you want to keep up with my progress or just want to connect as peers, check out my social links below and give me a follow!

<ul>
<li><a href="https://twitter.com/RingoMandingo93" target="_blank">🐦 Twitter</a></li>
<li><a href="https://github.com/kdleonard93" target="_blank">💻 Github</a></li>
<li><a href="https://discord.com/users/407639833146818570" target="_blank">👾 Discord</a></li>
<li><a href="https://www.linkedin.com/in/kyle-leonard93/" target="_blank">👔 LinkedIn</a></li>
</ul>