## Day 7: Hangman Game

## The Project
Today's goal was to build out a hangman game and one thing I did really appreciate is how Angela broke down the build process into sections instead of having one intro video with just the objective. How she laid out the to-do's helped me get my mind around how certain things should work for generating the random name to where certain areas might need a loop to work properly. I think that helped reduce the time it would have taken to get this one done. 

## The Flow Chart
One thing that I am starting to appreciate is the flow charts and the need for them before starting the project. I would always dread having to make one and had the naive thought that it's not needed and I should be able to think through what needs to be done step by step without one. But let me tell ya, I was way wrong 😅. Once I got the hang of how to think through the build process with flow charts it became easier to actually start building the project.

I've added my flow chart below:

![Screen Shot 2022-08-19 at 2.05.26 PM.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1660932369182/YTGMlJ16Q.png align="left")


## Solution
This project really stretched my chops and as I mentioned in the intro, it was pretty satisfying. My solution is below:
`main.py`
```
from multiprocessing.spawn import import_main_path
import random
from hangman_words import word_list
from hangman_art import logo, stages

chosen_word = random.choice(word_list)
word_length = len(chosen_word)

end_of_game = False
lives = 6

print(logo)

# Testing code
print(f'Pssst, the solution is {chosen_word}.')

# Create blanks
display = []
for _ in range(word_length):
    display += "_"

while not end_of_game:
    guess = input("Guess a letter: ").lower()

    if guess in display:
        print(f"Youve already guessed {guess}.")

    # Check guessed letter
    for position in range(word_length):
        letter Al = chosen_word[position]
        print(
            f"Current position: {position}\n Current letter: {letter}\n Guessed letter: {guess}")
        if letter == guess:
            display[position] = letter

    # Check if user is wrong.
    if guess not in chosen_word:
        print(
            f"You guessed {guess}. That letter is not in the word. Life lossed.")
        lives -= 1
        if lives == 0:
            end_of_game = True
            print("You lose.")

    # Join all the elements in the list and turn it into a String.
    print(f"{' '.join(display)}")

    # Check if user has got all letters.
    if "_" not in display:
        end_of_game = True
        print("You win.")
    print(stages[lives])

```

If you check my [github repo](https://github.com/kdleonard93/100-Days-of-Code-Day-7), you'll notice the imported files used for the art and random names but I didn't think I needed to add that here to save the space. Everything I worked on was from this file only. 

## EOD
That wraps up today's work. I'm in ATL for the weekend so I'll most likely be splitting Day 8 up into 2 days. Luckily, that's something Angela mentioned in the summary video after the hangman project so I don't feel bad anymore for splitting up some longer days if needed 😁✌🏾


#### If you want to keep up with my progress or just want to connect as peers, check out my social links below and give me a follow!

<ul>
<li><a href="https://twitter.com/RingoMandingo93" target="_blank">🐦 Twitter</a></li>
<li><a href="https://github.com/kdleonard93" target="_blank">💻 Github</a></li>
<li><a href="https://discord.com/users/407639833146818570" target="_blank">👾 Discord</a></li>
<li><a href="https://www.linkedin.com/in/kyle-leonard93/" target="_blank">👔 LinkedIn</a></li>
</ul>
