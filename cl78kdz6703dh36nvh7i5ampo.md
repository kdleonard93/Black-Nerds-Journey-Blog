## Day 8: Function Parameters & Ceasar Cipher

## Day 8's Lesson
Starting in this section, we touch on using function parameters with inputs. Angela discusses the difference between positional vs. keyword arguments. The lesson itself was straightforward. One thing I questioned was the use of the keyword arguments. Angela only explained assigning the arguments within the parameters. However, I found it much easier to read and understand by assigning the variables outside of the parameters and just adding the stored variable within.

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

#### If you want to keep up with my progress or just want to connect as peers, check out my social links below and give me a follow!

<ul>
<li><a href="https://twitter.com/RingoMandingo93" target="_blank">🐦 Twitter</a></li>
<li><a href="https://github.com/kdleonard93" target="_blank">💻 Github</a></li>
<li><a href="https://discord.com/users/407639833146818570" target="_blank">👾 Discord</a></li>
<li><a href="https://www.linkedin.com/in/kyle-leonard93/" target="_blank">👔 LinkedIn</a></li>
</ul>