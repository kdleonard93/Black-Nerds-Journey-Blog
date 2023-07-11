---
title: "Practice?...We're Talking About Practice, Man."
seoTitle: "Automating Emails with Python: Coding Journey Detour"
seoDescription: "Building an Automated Email Sender using Python, improving my OOP skills, and delving into automation."
datePublished: Tue Jul 11 2023 14:35:24 GMT+0000 (Coordinated Universal Time)
cuid: cljye9n7o000909l0g0yrgmem
slug: practicewere-talking-about-practice-man
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1689083385806/fb9f0be3-4762-41e9-af8a-58f4cf7aa413.jpeg
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1689086025138/4f69a7fa-c5dc-4403-972d-c69b8f834628.jpeg
tags: pythonautomation, emailsenderproject, blacknerdsjourney, pythoncodewarrior, techdiyprojects

---

## Intro to the Switch Up

Hey folks, been a little over a couple of weeks since I posted but I had a big move out of the city that I finished up last week and we just got done unpacking and setting up most of our home. Lots of went into refurbishing, and my girlfriend and I enjoyed tackling these DIY projects sprinkled around the house. My workspace is shaping up well, and I didn't anticipate how personalizing my office could enhance focus while working remotely, reducing feelings of isolation or the desire to escape to coffee shops for a change of scenery (previously I had old roommates and lacked a dedicated home office, making do with my bedroom and living room.)

With being said, I had the urge to switch up my next couple of weeks to continue practicing what I've learned so far in Python, as mentioned in my last post. Also, I was getting kinda sick of working with the turtle module for EVRY SINGLE PROJECT 😅. While it's excellent for kickstarting the learning process, particularly with creating some classic games, it soon became monotonously familiar. So rather than merely tackling a handful of CodeWars challenges a few days a week and bouncing to the next course day, I intend to intersperse some standalone projects to further solidify these concepts. I genuinely need to master the nuances of OOP to enhance my skill in refining and updating existing code, all to progress in my present job. I'm banking on these projects to secure that knowledge. For me, repetition is key; short-term memory loss is a pain in the ass lol but I've been working on boosting my cognitive health for some time.

## The Project

The project that I'm going to work on over the next couple of weeks is an ***Automated Email Sender***. I researched beginner-friendly projects that involve automation, in an attempt to gradually advance towards more complex projects like chatbots and trading bots, and then eventually, NLP. I actually made one crypto trading bot not too long ago but so far, it carries out my orders with a "taker's fee" and does so at the prevailing market price instead of the limit price I've set with the "maker fee" only (maker fees are generally less than taker fees).  
I'll refrain from veering into a discourse about trading bots and the like, so back to the topic at hand 😄. After researching this project I noted some of the common libraries used as well as a game plan on how to tackle each day. Here's an outline of the project and resources required to hit the ground running:

**MVP (Minimum Viable Product)**:

1. **Send an Email**: The program should be able to send an email to any address.
    
2. **Customize the Subject and Body**: The user should be able to input the subject and body of the email.
    
3. **Send Multiple Emails**: The program should be able to send multiple emails, either to the same address or to different addresses.
    
4. **Schedule Emails**: The user should be able to schedule emails to be sent at specific times.
    
5. **Log Sent Emails**: The program should keep a log of all sent emails, including the date and time, recipient, subject, and body.
    

**Libraries Needed**:

* **smtplib**: This is the built-in Python library for sending emails using the Simple Mail Transfer Protocol (SMTP).
    
* **ssl**: Another built-in Python library. I'll use it to create a secure connection with your mail server.
    
* **getpass**: This built-in library is used for secure password handling.
    
* **schedule**: This is an external library that you can use to schedule emails to be sent at specific times.
    
* **pandas**: I will use this library to create and manage a DataFrame that will serve as your email log.
    

**Optional Libraries**:

* **os**: If you want to make your log persistent across runs (i.e., save it to a file), you'll need this library to interact with your operating system's file system.
    
* **datetime**: For working with dates and times, useful for scheduling and logging.
    

**Estimated Timeline**:

* **Days 1-2**: Research the needed libraries and setup the project. Draft the program by defining the main functions and how they'll interact.
    
* **Days 3-4**: Write the function to send a single email. Test this function to make sure it works correctly.
    
* **Day 5**: Write the function to send multiple emails. More tests.
    
* **Day 6**: Add scheduling capabilities to your program. You guessed it, +Testing.
    
* **Day 7**: Create the email log. "Testing testing, 1-2-3".
    
* **Day 8:** Do a final round of testing and debugging on the project as a whole to make sure all parts of the program work together correctly.
    
* **Day 9**: Polish project; Clean up code, add comments, write documentation, and anything else needed to wrap up the project.
    
* **Day 10**: Reflect on the project, and plan your next steps.
    

The project timeline is predicated on full-time work, so since this is a part-time endeavor, it'll take me roughly 2 weeks, as previously mentioned. I've initiated the repo and you can follow it on GitHub here -&gt; -&gt; [https://github.com/kdleonard93/automated\_email\_sender](https://github.com/kdleonard93/automated_email_sender)

## EOD

How I intend to document all of this is still under consideration. I might opt to write a midway and final report OR perhaps just a wrap-up post at the end. Likely the former, and maybe even a third if I stumble upon an exciting add-on to this project. But that brings today's post to a close, and I'm excited to get this one going!

#### **If you want to keep up with my progress or just want to connect as peers, check out my social links below and give me a follow!**

* [**🐦 Twitter**](https://twitter.com/RingoMandingo93)
    
* [**💻 Github**](https://github.com/kdleonard93)
    
* [**👾 Discord**](https://discord.com/users/407639833146818570)
    
* [**👔 LinkedIn**](https://www.linkedin.com/in/kyle-leonard93/)