---
title: "Twitter....I Mean X Bot Roadblock"
seoTitle: "Twitter Bot Challenges & Day 24 Python Journey"
seoDescription: "Exploring the hurdles of creating a Twitter bot using Tweepy and diving into Day 24 of the 100-Days-Of-Python challenge."
datePublished: Wed Oct 11 2023 02:52:30 GMT+0000 (Coordinated Universal Time)
cuid: clnl5o2kz00030ak12raaba49
slug: twitter-bot-roadblock
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1696457499406/c3e7e219-0d27-47a2-9607-527084394c9b.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1696992583789/85c25c9e-3484-4504-9dd6-dbef74779a20.png
tags: python, 100daysofcode, twitterapi, pythonbots, tweepy

---

## Getting this started

After the `Email Sender` project, I scouted again to see what would be an excellent project but a bit more challenging and more practical for day-to-day use (I don't plan to actually use the auto email sender....at least not yet 😁). So after discussing things I could do that would benefit both of us, we figured that a Twitter bot would help us both. She'd have a tool to automate her Twitter posts of her plants and I'd get some practice building out Python bots. It seemed easy enough to get all of the details:  
**\- Set up a Twitter Developer Account**  
**\- Code the Bot**  
**\- Spice up the bot**  
**\- Deploy the Bot**

Tweepy is the popular library of choice for working with Twitter's API and their documentation is understandable. For the sake of clarity, I'm going to reference X as Twitter (like the good lord intended 😂)

## API Permissions are the battle

The main issue I'm having with this bot creation is with API Permissions. Tweepy's docs help a good amount but I'm not sure what I'm missing between their doc ([https://docs.tweepy.org/en/stable/authentication.html#twitter-api-v2](https://docs.tweepy.org/en/stable/authentication.html#twitter-api-v2)) and Twitter's ([https://developer.twitter.com/en/docs/twitter-api/tweets/manage-tweets/api-reference/post-tweets](https://developer.twitter.com/en/docs/twitter-api/tweets/manage-tweets/api-reference/post-tweets)). My permissions for the Twitter account are for API V2 and restricted V1 access. However, no matter what I did to change the code to get a post to work, I kept getting an error about API permissions.

![SpongeBob gif. While it rains outside, SpongeBob sits alone at a booth in the Krusty Krab, staring blankly at a steaming mug.](https://media2.giphy.com/media/ISOckXUybVfQ4/giphy.gif?cid=ecf05e47gdg0iqx3gkzh6lbkqed7wisr043ef8e4t0monzw8&ep=v1_gifs_search&rid=giphy.gif&ct=g align="center")

I tried to see if I could access the few API v1 endpoints I had access to but that didn't work either. My working repo is here -&gt; [https://github.com/kdleonard93/Twitter\_bot](https://github.com/kdleonard93/Twitter_bot) and you can see how I currently have it set up (if anyone knows what I'm doing wrong let me know 🙏🏾). Most attempts were to the POST endpoint but I tried to GET a list of recent tweets as well as read my follower count but no luck there either. The closest I got was where I had a setup that prompted me to navigate to the URL provided to get a code to authenticate, but once I go to that URL (Which has my ID, redirect URL, and Username data in it) I get an error. [https://loom.com/i/96fe0e1cb1b740ccbe5c4f9437c60cc5](https://loom.com/i/96fe0e1cb1b740ccbe5c4f9437c60cc5)

After coming back to this a handful of times with a "fresh mind" but no progress with this issue, I've decided to pause it and see if any of my peers might know what I'm missing, instead of frustrating myself day in and day out. Considering that my lady still needs to create the content that I'd be posting (listing images, deals, etc.) I can take a breather and work on something else while I try to source some guidance. That led me to move on to Day 24 in my 100-Days-Of-Python course (yes....I'm still planning on finishing all 100 days 😄) as well as pick a new project that is more useful for now while I figure out the Twitter bot and wait for content to post. The new project is a "Personal Finance Tracker with Predictive Analysis". The predictive analysis portion of the project is extra credit since it will involve ML which I have never dove into. This might also sound more difficult than the last project, and I'm sure it is 😅, but it's something fresh that I need.

## Day 24 - Files, Directories, and Paths

This day came pretty easy. It's pretty much just an overview of directories and how to access the files within through relative and absolute paths. Reading and Writing files are easy peasy as well utilizing one main method, `open()`. `open()` returns a file object, and is most commonly used with two positional arguments and one keyword argument: `open(filename, mode, encoding=None).` The first argument is a string that will be the file name or the path to the file you're trying to read. The `mode` argument is to determine which way the file is to be used. You can read `mode="r"`, write `mode="w"`, and append `mode="a"` for most people's needs. There are a couple more, like `r+` for reading and writing and `b` for opening the file in binary mode.

A quick example of this would be:

```python
open('letter.txt', 'r')
or
open('letter.txt', mode='r')
```

Personally, I prefer `open('letter.txt', mode='r')` so whoever reads the code, is provided more clarity on what that is doing, but to each their own. This leads us to a nice lil' trick for Python to ensure the file closes after the update is made. We do this by using `with` and `as` like so:

```python
# Example 1
with open('letter.txt', mode='w') as new_letter:
    """The text below will update whatever text is on letter.txt"""
    new_letter.write("New letter, who dis?")

# Example 2
with open('letter.txt', mode='r') as new_letter:
    """The call below will read letter.txt and store the data in `contents`."""
    contents = read_letter.read()
    print(contents)

# Example 3
with open('letter.txt', mode='a') as new_letter:
    """The call below will append the added text to letter.txt at the end of the file."""
    new_letter.write("It's ya boi, that's who?")
```

There's more to learn about "Input and Output" though and I recommend taking a peek at the docs -&gt; [https://docs.python.org/3/tutorial/inputoutput.html#reading-and-writing-files](https://docs.python.org/3/tutorial/inputoutput.html#reading-and-writing-files).

## The Project - Mail Merger Project

The project for day 24 was not as hefty as some of the more recent days, which I appreciate very much ( ͡⏿ ͜ʖ ͡⏿). The goal was to take a list of names from a given doc and create email drafts for each person. The content was the same but the names needed to be swapped out for each new file and labeled as such in the file name and body copy. Outside of using a for loop, this project consisted of only what we learned on day 24 and the code is brief:

```python
PLACEHOLDER = "[name]"
        
with open("/Users/kyleleonard/100-Days-Of-Code_Python/day-24/Input/Names/invited_names.txt") as names_file:
   names = names_file.readlines()
   print(names)
   
with open("/Users/kyleleonard/100-Days-Of-Code_Python/day-24/Input/Letters/starting_letter.txt") as letter_file:
    letter_content = letter_file.read()
    for name in names:
        stripped_name = name.strip()
        new_letter = letter_content.replace(PLACEHOLDER, stripped_name)
        with open(f"/Users/kyleleonard/100-Days-Of-Code_Python/day-24/Output/ReadyToSend/letter_for_{stripped_name}", mode="w") as completed_letter:
            completed_letter.write(new_letter)
```

That's it! Now the files created from running this are listed in the repo and you can check it all out here -&gt; [https://github.com/kdleonard93/100-Days-Of-Code\_Python/tree/main/day-24](https://github.com/kdleonard93/100-Days-Of-Code_Python/tree/main/day-24).

## EOD

My main goal now is to get started on that other project I mentioned while also tackling days 25-30. I'm starting to wind down with all the weddings vacations, birthdays, and everything in between, and am VERY happy about it. I never realized how exhausting travel could be when you're doing it in succession for a few months. Nonetheless, there are a couple of new things out in the dev world that have been released over the last month:

* [Bun - A JS runtime & toolkit](https://bun.sh/blog/bun-v1.0.4) (Stable version)
    
* [Mojo - A superset of Python built for AI](https://www.modular.com/mojo) (No stable version yet but an SDK is available)
    

These 2 intrigue me the most and I plan to use Bun as my runtime for my new project. I know this will inevitably cause me a headache with the impending wall of errors I plan to face. It should be good for me though, forcing me to get acquainted with Bun and maybe even trying to contribute to it or other open-source tools I use. Fingers crossed 🤞🏾 and until next time, ✌🏾.

#### **If you want to keep up with my writing or just want to connect as peers, check out my social links below and give me a follow!**

* [𝕏 Twitter](https://twitter.com/RingoMandingo93)
    
* [**💻 Github**](https://github.com/kdleonard93)
    
* [**👾 Discord**](https://discord.com/users/407639833146818570)
    
* [**👔 LinkedIn**](https://www.linkedin.com/in/kyle-leonard93/)