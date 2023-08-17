---
title: "Automated Email Sender Project Check-In"
seoTitle: "Automated Email Sender with Python: Journey of Reps"
seoDescription: "Dive into the creation of a Python-based automated email sender. Explore the challenges, learn about email security practices, and get hands-on insight."
datePublished: Thu Aug 17 2023 02:34:14 GMT+0000 (Coordinated Universal Time)
cuid: cllejspyf000609mm1y8iew37
slug: automated-email-sender-project-check-in
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1692235826052/ed724522-9ad0-4ed0-8d61-88501921d825.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1692239391191/25548c0d-1d33-46ce-8d36-1f7338bd98a2.png
tags: blogging, python, backend, automation, emailsenderproject

---

## Automation Complication

I know, I know, I said "This Project should only take me a couple of weeks".....well, here I am 4 weeks later and only halfway through lol. Not that this project was just THAT difficult for me, it's more so a mix of learning new libraries and also having a very busy schedule in my personal life for the month of July and August as well.

The meat of the project is complete though! You can go over to my repo here -&gt; [https://github.com/kdleonard93/automated\_email\_sender](https://github.com/kdleonard93/automated_email_sender) and check in on the commits made since I started this project. Feel free to pull it down and give it a try yourself. Please note though, if you wanna try it out, you'll need to make a few adjustments:

1. Update the `sender_email` argument value in the `send_email` function to your own (you'll need to use gmail). Change the recipients email as well. (Dont you dare use mine lol)
    
2. Make sure you set your password in an environment variable since we are storing sensitive data (aka: password). You can do this in your terminal by running `export EMAIL_PASSWORD=your_password_here` .
    
3. Lastly, confirm all of the needed libraries are installed on your local.
    

Once you have the following checks and this repo pulled, run `python main.py` and you should be set!  
As I was writing this, I realized the amount of other sensitive info i had in the project (emails, env variables, etc.) So I made some code changes already to improve project 😄.

For those who wanna see a quick snippet of the `email_sender.py` file, you can take a peek below:

```python
import smtplib
import ssl
import csv
from email.mime.text import MIMEText
from email.mime.multipart import MIMEMultipart
import schedule
import time
from os import environ
from dotenv import load_dotenv

load_dotenv()  # This will load environment variables from a .env file.

PASSWORD = environ.get("EMAIL_PASSWORD")
SENDER_EMAIL = environ.get("SENDER_EMAIL")
SMTP_SERVER = environ.get("SMTP_SERVER")  # Set up the SMTP server and port
SMTP_PORT = int(environ.get("SMTP_PORT", 465))  # For SSL

# Check if necessary environment variables are set
if not (PASSWORD and SENDER_EMAIL and SMTP_SERVER):
    raise EnvironmentError("Required environment variables are missing!")


def read_email_data(filename="email_data.csv"):
    email_data = []
    with open(filename, "r") as file:
        reader = csv.DictReader(file)
        for row in reader:
            email_data.append(row)
    return email_data


def send_email(email_data, sender_email=SENDER_EMAIL):
    # Create email headers and body
    message = MIMEMultipart()
    message["From"] = sender_email
    message["To"] = email_data["recipient_email"]
    message["Subject"] = email_data["subject"]
    message.attach(MIMEText(email_data["body"], "plain"))

    # Create a secure SSL context
    context = ssl.create_default_context()

    # Try to log in to the server and send the email
    try:
        server = smtplib.SMTP_SSL(SMTP_SERVER, SMTP_PORT, context=context)
        server.login(sender_email, PASSWORD)
        server.sendmail(
            sender_email, email_data["recipient_email"], message.as_string())
    except Exception as e:
        print(f"An error occurred while sending the email: {e}")
    finally:
        server.quit()


def send_multi_emails(filename="email_data.csv"):
    email_data_list = read_email_data(filename)
    for data in email_data_list:
        send_email(email_data=data)


def job():
    """Define the job to be executed at a scheduled time."""
    send_multi_emails()


def email_schedule(interval):
    """Schedules the email sending job."""
    schedule.every(interval).minutes.do(job)
    while True:
        schedule.run_pending()
        time.sleep(1)
```

One thing I will admit to is that the automation for this had me stuck for a little. Learning a lot about security practices with this one as well and will need it for future projects so I've been appreciating the challenge.

## EOD

Wish I was able to get a check-in written sooner but, you know.....life. The last few things I need to do is create a log for the jobs, do some final testing after that, and then reflect and write my final thoughts on this project! See yall then!

#### **If you want to keep up with my progress or just want to connect as peers, check out my social links below and give me a follow!**

* [**🐦 Twitter**](https://twitter.com/RingoMandingo93) **(Not calling it X yet...doesn't roll of the tongue lol)**
    
* [**💻 Github**](https://github.com/kdleonard93)
    
* [**👾 Discord**](https://discord.com/users/407639833146818570)
    
* [**👔 LinkedIn**](https://www.linkedin.com/in/kyle-leonard93/)