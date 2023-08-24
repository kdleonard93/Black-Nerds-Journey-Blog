---
title: "Automated Email Sender - Finalized Project"
seoTitle: "Journey Through Building My Own Python Email Automation"
seoDescription: "Join me in my journey of building a Python-based automated email scheduler. Learn the coding hurdles and triumphs I experienced along the way."
datePublished: Thu Aug 24 2023 16:03:43 GMT+0000 (Coordinated Universal Time)
cuid: cllpcsp9r00040amldh5yf8br
slug: automated-email-sender-finalized-project
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1692892620784/072363d6-e949-4e70-89b1-d4c6482d52be.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1692892883081/8a77e33a-71d8-4c98-b2f3-0b60b1162b16.png
tags: python, security, backend, automation, object-oriented-programming

---

## It's all done!

What's up, folks! I wrapped up this project last night and early this AM and it's safe to say it was a pretty decent challenge along the way. When picking a "beginner" Python project to work on, I didn't expect it to last as long as this Email Sender did, and I definitely didn't expect the amount of work that actually had to go into getting this project to work successfully. Throughout the course, I did my best to follow the best practices when it comes to commits and PRs (Like I've been doing my `100 Days of Python Code` challenge \*still ongoing 😅\*) but will admit some commits were pushed directly through the master. I also created a proper README for anyone who wants to pull the project for themselves and use it! It's fully functional and you can modify it accordingly as you please 😁. The full project repo can be found here -&gt; [https://github.com/kdleonard93/automated\_email\_sender](https://github.com/kdleonard93/automated_email_sender).

## Reflection

What a ride this project has been! 🚀 Remember Day 1? Me neither because it was a blur of setting up Python environments and sorting out initial roadblocks like version control (yeah, Git, I'm looking at you 😅). But once the basics were nailed, the ball started rolling.

One of the big wins was getting scheduling right on Day 6. Man, figuring out how to automatically send emails based on a CSV file was very helpful and a challenge in itself. But now, If you've got a list of people to email and specific times to do it, just fire and forget! Gotta love automation.

I also took the security aspect seriously, keeping passwords and other sensitive stuff out of the GitHub repo by using `.env` and `.gitignore`. Can't trust the internet, ya know 😂?

```python
# .env example
EMAIL_PASSWORD=YourEmailPassword
SENDER_EMAIL=YourSenderEmail
SMTP_SERVER=YourSMTPServer
SMTP_PORT=YourSMTPPort
```

```python
# .gitignore example
.env
email_data.csv
email_log.csv 
venv/
```

Now, you might be wondering about stress testing. To be honest, I haven't dived into it yet, but it's on my radar for sure. I plan to tweak and refine this project over time, and that’s when I'll throw the stress tests into the mix.

All in all, it's been a whirlwind of code, tea, and a smidge of destressing 😄. Can't wait to see where this project takes me next, and what new skills I'll add to the ol' toolkit next. 🛠️

#### **If you want to keep up with my writing or just want to connect as peers, check out my social links below and give me a follow!**

* [𝗫 Twitter](https://twitter.com/RingoMandingo93)
    
* [**💻 Github**](https://github.com/kdleonard93)
    
* [**👾 Discord**](https://discord.com/users/407639833146818570)
    
* [**👔 LinkedIn**](https://www.linkedin.com/in/kyle-leonard93/)