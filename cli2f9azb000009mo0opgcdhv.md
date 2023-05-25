---
title: "Day 17: The "Quiz" Project and Benefits of OOP"
seoTitle: "Day 17: The "Quiz" Project and Benefits of OOP"
seoDescription: "Tackling custom Classes, Attributes, and Methods. Angela went over creating custom Classes, Attributes, and Methods when dealing with OOP."
datePublished: Thu May 25 2023 00:54:48 GMT+0000 (Coordinated Universal Time)
cuid: cli2f9azb000009mo0opgcdhv
slug: day-17-the-quiz-project-and-benefits-of-oop
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1684975959596/fcd94602-f8ed-454e-b4f0-1157a61b92eb.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1684976046583/66890421-bfa7-49da-b374-0211ebfb09e8.png
tags: python, web-development, backend, 100daysofcode, object-oriented-programming

---

## Today's Lesson

During day 17's lesson, Angela went over creating custom Classes, Attributes, and Methods when dealing with OOP. She touched back on examples from Day 16 and what I'll do is make quick note of the main takeaways.

### Unveiling Classes

A class is a blueprint used to create objects (specific instances of the class). Each instance of the class can have its own set of attributes and methods, and you can interact with the instance using these attributes and methods. This leads us to another important note for classes, and that is `Constructors`. A `Constructor` is a special method that's used to initialize new objects or instances of a class and is usually defined with the `__init__` method. (Note, I learned that `__init__` is technically an initializer. The real constructor in Python is `__new__` but is rarely used).

An example of creating a constructor method in a class is below.

```python
class Car:
    def __init__(self, make, model, color):
        self.make = make
        self.model = model
        self.color = color
```

Inside the `__init__` method, `self` refers to the instance of the class that's being initialized. By assigning to `self.make`, `self.model`, and `self.color`, you're setting attributes on the `Car` instance. Below are quick summaries of what Attributes and Methods are.

#### Attributes

An attribute is a variable associated with an instance of a class. It characterizes the object, is defined within the class using the self keyword, and is accessible or modifiable using the dot (.) operator. To put it simply, attributes are the unique details that define an object.

#### Methods

A method is essentially a function linked to a specific class. It outlines the behaviors or actions an instance of the class can perform. Generally operating on attributes or performing computations, methods are invoked on an instance using the dot (.) operator. In short, methods represent the actions an object can perform.

Angela explains these concepts well, enriching her explanation with ample examples. The day's project involved leveraging custom classes to develop a Quiz Game. From this point forward, I'll be committing the day's project code to their respective branches and then merge them into master. As the complexity of the projects grows, I'm considering providing a repository link with code snippets, rather than posting the entire solution. But for today, the entire solution will be provided :).

## Solution

##### `main.py`

```python
from question_model import Question
from data import question_data
from quiz_brain import QuizBrain

question_bank = []

for question in question_data:
    question_text = question["question"]
    question_answer = question["correct_answer"]
    new_question = Question(question_text, question_answer)
    question_bank.append(new_question)
    

quiz = QuizBrain(question_bank)

while quiz.still_has_questions():
    quiz.next_question()

print("You have finished the quiz")
print(f"Your final score is {quiz.score}/{quiz.question_number}")
```

`question_model.py`

```python
class Question:
    def __init__(self, text, answer):
        self.text = text
        self.answer = answer
```

`quiz_brain.py`

```python
class QuizBrain:
    def __init__(self, q_list):
        self.question_number = 0
        self.question_list = q_list
        self.score = 0
        
    def still_has_questions(self):
        return self.question_number < len(self.question_list)

        
    def next_question(self):
        current_question = self.question_list[self.question_number]
        self.question_number += 1
        user_answer = input(f"Q.{self.question_number}: {current_question.text} (True/False): ")
        self.check_answer(user_answer, current_question.answer)
        
    def check_answer(self, user_answer, correct_answer):
        if user_answer.lower() == correct_answer.lower():
            print("Correct!")
            self.score += 1
        else:
            print("Wrong!")
        print(f"The correct answer was: {correct_answer}.")
        print(f"{self.score}/{len(self.question_list)}")
        print("\n")
```

Here is a [link to the repo](https://github.com/kdleonard93/100-Days-Of-Code_Python/tree/day-17/day-17). There are a couple more files listed in the repo, `data.py` and `trial.py`. `data.py` is where the default data was held but I used [https://opentdb.com/](https://opentdb.com/) to generate a new random set of questions and answers. `trial.py` was just a file I used while doing a few examples from Angela's lecture videos.

These scripts demonstrate the efficacy of OOP in organizing and executing complex tasks. The `Question` class in `question_model.py` is used to create instances of questions, [`main.py`](http://main.py) assembles a `question_bank` list of `Question` objects, while `QuizBrain` class in `quiz_brain.py` handles the quiz flow, tracking the question number, score, and validating user answers.

## EOD

So that wraps up today! Felt good to understand this quicker than I think I would have a handful of months back. Having good co-workers to be semi-mentors for the mountain of questions I've asked has helped me learn PHP quicker and I feel like it's going to contribute to my Python learning more than I expected.

#### If you want to keep up with my progress or just want to connect as peers, check out my social links below and give me a follow!

* [🐦 Twitter](https://twitter.com/RingoMandingo93)
    
* [💻 Github](https://github.com/kdleonard93)
    
* [👾 Discord](https://discord.com/users/407639833146818570)
    
* [👔 LinkedIn](https://www.linkedin.com/in/kyle-leonard93/)