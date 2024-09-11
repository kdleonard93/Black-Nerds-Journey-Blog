---
title: "Day 28 & 29 - Pomodoro GUI  & Password Manager with Tkinter"
datePublished: Wed Sep 11 2024 13:35:40 GMT+0000 (Coordinated Universal Time)
cuid: cm0xwletr000709le0mo4fkfr
slug: day-28-29-pomodoro-gui-password-manager-with-tkinter
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1726023349914/b951a6e1-afd9-4ab4-b434-a14bb7886c56.png
tags: app-development, python, web-development, backend, codenewbies

---

### Tomato Tomàto

I’m combining these 2 days (and will probably group these up moving forward) and the Day 28 project was interesting but pretty boring 🥱. The objective was to create a Pomodoro app, which is essentially a focus time/break stopwatch. The app itself is very useful but there are of course a ton of apps similar to this that would be more beneficial and are built completely differently, but nonetheless, it was good practice.  
The code can be found here → [https://github.com/kdleonard93/100-Days-Of-Code\_Python/tree/main/day-28](https://github.com/kdleonard93/100-Days-Of-Code_Python/tree/main/day-28) and give the program a try yourself. There weren’t any new and noteworthy concepts covered on this day so I won’t bore you with rambling about it.

### Peak Tkinter

Day 29 however, was a very interesting project. The password manager we created was supposed to have 3 main functions:

* Clean UI and alined entry fields
    
* The “Generate Password” button generated a strong random password and added it into the corresponding field + copied it to your clipboard.
    
* The “Add” button adds it to a text file and starts a new line after.
    

Pretty straightforward goals but I also wanted to add another button to clean up file when I didn’t want it anymore. So I decided to add 1 additional function to this project that isn't in the module:

* I added a “Delete” button that deletes the file.
    

One thing she notes here is that people are more inclined to store passwords on their local machine since that is the safer option and for the most part, I agree. However, she just tosses the password into a textfile. Now, I’m sure there are better methods to store passwords locally, but the one thing I added to her implementation was to make text file hidden to at least give me the illusion of storing passwords safely on my machine 😂. I enjoyed the password manager project and picked up a few tips along the way.

#### Some Things I Learned

There were two new functions from Tkinter that I hadn’t used before and picked up here. The `tk.insert()` and `tk.delete()` functions were used for my “Generate Password” and “Delete Text File” buttons, respectively. Nothing super unique about how they work but here is a quick overview and let’s say our entry in question is `email`:

* `email.insert(index, "Text")`: Takes 2 arguments, the first is the index of entry you choose and the second argument is the text you’d like to insert. Pretty damn simple
    
* `email.delete(start_index, end_index)`: Takes 2 arguments, being the start and the end indexes of what you want to delete. 9/10, you’d write something like: `email.delete(0, END)` to delete the entire entry field.
    

The second main takeaway from this project was the use cases for the paperclip library. Now I didn’t actually use that library for this project since Tkinter has its own clipboard functions, but, I do see myself using this library on future projects that need some sort of auto copy to clipboard. Bookmarked 🤘🏾.

If you wanna give this little project a spin, you can clone/fork it here → [https://github.com/kdleonard93/100-Days-Of-Code\_Python/tree/main/day-29](https://github.com/kdleonard93/100-Days-Of-Code_Python/tree/main/day-29)

Here’s a lil’ demo:

%[https://www.loom.com/share/62f424523b1f41efa48e1749133e86ce?sid=9b767fde-e585-412e-9967-fe9e6f96bfea] 

### EOD

That pretty much sums up these 2 days. I mentioned this in a previous post but I’ve been trying to figure out the best and most affordable way to gain some Kubernetes skills. Was informed by my company that they “didn’t have the budget” for the certificate training. Which to me is pretty shocking as the certificate is only $400. I’d understand not being able to reimburse tuition or anything else at a similar scale but $400??

But enough of my ranting, I still plan to make moves in the DevOps field and gain a deeper knowledge of Kubernetes and Docker. I’m finding that I like DevOps more and more as time passes. Either that or I’m starting to hate designing pages more and more as the day goes on lol. I’m garbage at styling and would truly be happier if I never have to do it again.

#### **If you want to keep up with my writing or want to connect as peers, check out my social links below and give me a follow!**

* [**𝕏 Twitter**](https://twitter.com/RingoMandingo93)
    
* [**�**](https://twitter.com/RingoMandingo93)[**� Github**](https://github.com/kdleonard93)
    
* [**👾 Discor**](https://discord.com/users/407639833146818570)[**d**](https://www.linkedin.com/in/kyle-leonard93/)
    
* [**👔 LinkedIn**](https://www.linkedin.com/in/kyle-leonard93/)