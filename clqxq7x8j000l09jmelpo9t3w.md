---
title: "Personal Finance Tracker Project and 2024 Plans"
seoTitle: "Project Planning to Reality: Personal Finance App | Digital Dopamine"
seoDescription: "Join me on my journey from project planning to developing a Personal Finance app. Discover insights on SvelteKit, Django, CockroachDB, and more tech choices"
datePublished: Wed Jan 03 2024 12:00:10 GMT+0000 (Coordinated Universal Time)
cuid: clqxq7x8j000l09jmelpo9t3w
slug: personal-finance-tracker-project-and-2024-plans
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1704262361339/2fb0dc0b-ac9d-4411-9f66-3903c75270cd.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1704262392564/bd8d813a-dc57-4fe6-b157-19369ae573db.png
tags: postgresql, docker, python, django, typescript, cockroachdb, svelte

---

## Project Planning

Hey folks, after a bunch of quick trials with a bunch of different stacks, I finally settled on what I'm going to focus on with this project. The projection of a project of this size is about 6 months but knowing how I work and what I have going on in my personal life, I'm hoping to have a working app within a year. The new tech coming out these days has sent me down many rabbit holes, resulting in me wanting to use all of it in my day-to-day activity 😄. With that urge aside, I needed to make a decision on what I was going to use for the Personal Finance app mentioned in my [last post](https://blacknerd.dev/twitter-bot-roadblock). I have a hard time making decisions as is on tech stacks and the idea of needing to learn new technologies when I'm still perfecting languages I use in my salaried job is exhausting and pretty daunting at times. But I know the pain and constraints with tried and true technologies and at my point in my career, I feel these new technologies are going to become more relevant and needed in this evergrowing industry where exponential growth is imminent. My main goal is still a career working with Python but to also try and pinpoint the finance industry, whether it's big tech or freelancing, hence this project. The tech I've worked with for deciding my stack (New to Old) includes [SvelteKit](https://kit.svelte.dev/), [Python](https://www.python.org/) ([Django](https://www.djangoproject.com/) + [Flask](https://flask.palletsprojects.com/en/3.0.x/)), [Bun](https://bun.sh/) (for frontend package management), [Docker](https://www.docker.com/), [CockroachDB](https://www.cockroachlabs.com/), [FaunaDB](https://fauna.com/), Cloudflare, and [Redner.](https://render.com/) While all of these tools had their use cases, I ended with SvelteKit + Typescript for my front-end, Python w/ Django for my back-end, and CockroachDB for my database. I plan to deploy on Render (That's still to be determined though.) Was fun and frustrating during this trial but my reasoning behind my choice is pretty sound in my opinion.

## Sticky Stacking

When I first started this project, I went in with the idea of 100% using a serverless database, whether it was Relational or Non-Relational. So out of the available options, I tried out CockroachDB and Fauna DB.

#### Svelte Sorcerer

Out of all of the frontend frameworks out there these days, Svelte was won me over for its easy learning curve and simplicity. I compared mainly Vue and Svelte, but Solid.js and Qwik were also considered. I didn't even consider Recact cause i have personal issues with that framework and is just a "me" problem 😂. The winner though, was Svelete for many reasons:

1. **Performance**: Svelte's compiler approach ensures that the final bundle size is smaller and the runtime performance is faster. For an expense-tracking app, which likely involves numerous interactive elements and frequent updates, Svelte’s efficient update mechanism can make the UX much smoother for the customers, aka myself and my lady.
    
2. **Ease of Development**: Svelte's syntax is simple and intuitive, and has less boilerplate code (especially related to react). This should make the development process faster and more straightforward, especially since this project shouldn't call for highly complex functionalities.
    
3. **State Management**: Ahh yes, state management. Svelte’s reactive state management is straightforward and built-in, eliminating the need for additional state management libraries. This is a godsend for me since managing state was always difficult (\*cough\* ***react*** \*cough\*). This simplifies handling user inputs, server responses, and UI updates, which are core aspects of an expense-tracking application.
    
4. **Learning Curve and Productivity**: I've been reading into Svelete for some time now but just recently using it in a project (\**new portfolio below\**), and its learning curve isn't as steep as other frameworks. I was scaffolded and going pretty quickly with a skeleton project. The clear and concise codebase can also be easier to maintain and scale.
    
5. **SvelteKit for Full-Stack Development**: If the expense tracking app requires both frontend and backend development, SvelteKit offers an all-in-one solution, streamlining the development process. It provides features like server-side rendering, static site generation, and file-based routing, which can be very beneficial.
    

#### Django Dogg

Regarding the backend framework, Django won the battle here against Flask and Fa. I experimented a bit with both and my decision was pretty back and forth, but all in all, Django fits this project's needs the most. Some of the key features for choosing Django:

1. **Structured and Feature-Rich**: Django's "batteries-included" approach provides a lot of built-in functionalities that I learned are beneficial for this app. The admin interface (best feature in my opinion), user authentication, and ORM are particularly useful. The admin interface can be quickly customized to manage expenses, categories, and user accounts, which would be a significant part of an expense-tracking app.
    
2. **ORM and Database Management**: Django's ORM is powerful and simplifies interactions with the database. For an expense tracking app, where you'll be dealing with a lot of CRUD operations, Django's ORM can make these tasks more manageable and efficient.
    
3. **Security**: Django totes its robust security and helps avoid common mistakes like SQL injection, cross-site scripting, cross-site request forgery, etc. For an app dealing with personal financial data, security is essential.
    
4. **Scalability**: While Flask is also scalable, Django's structure and components make it easier to scale for larger applications. If the expense tracking app grows in complexity or user base, Django can handle this growth more readily.
    
5. **Community and Ecosystem**: Django has a large community and extensive documentation, which makes finding solutions to problems easier. There are also a bunch of dope packages to extend Django, adding functionality and/or simplifying development.
    

#### Durable like a Cockroach

Choosing between these two was my biggest decision and ultimately came down to which would be easier to set up and what worked better with my backend choice. After playing with Fauna first, I chose CockroachDB because I was planning on using Django as my backend framework and I was familiar with SQL. On the other hand, I am very familiar with JSON and work with it a lot for work so Fauna's JSON-like document model was pretty attractive. The issue I found with Fauna though, is that there's not a lot of support out there in terms of resources and community, making using this for a large project a difficult task. When trying out CockroachDB, the learning curve, to me, seems to be a bit steeper but they have ***much*** more learning material. They also have more organized and richer documentation with a load of resources in what they call "Cockroach University". These resources include quick projects, webinars, and free courses that offer certificates upon completion. This makes CockroachDB an easy winner for this particular project, but I still plan to build something with Fauna at some point this year. Here are the main reasons for CockraochDB summed up

1. **Strong Consistency**: For a financial application, data consistency is crucial. CockroachDB's strong consistency model ensures that all transactions are accurate and reliable, which is paramount in handling financial data where errors or inconsistencies can have serious consequences.
    
2. **Distributed SQL Database**: CockroachDB's architecture is inherently distributed, making it highly resilient and suitable for applications that require high availability and fault tolerance. It's said to be especially beneficial if the app needs to scale or maintain high uptime. FaunaDB offers a distributed serverless platform as well so this was kind of a tie.
    
3. **Transactional Data Integrity**: CockroachDB supports full ACID transactions, which is important for an application dealing with financial records. Ensuring the integrity of each transaction (like adding or modifying expense entries) is essential, and CockroachDB's focus on transactional integrity aligns well with this requirement.
    
4. **SQL Interface**: The use of standard SQL in CockroachDB can be a significant advantage. SQL is an OG in the database game, making it easier to find developers familiar with it or to work within a team that already has SQL knowledge. This could lead to a smoother development process and easier maintenance. I know we use MySQL at my company so having access to public AND company resources are nice to haves for learning and troubleshooting.
    
5. **Scalability and Geo-Distribution**: CockroachDB's scalability and support for geo-distributed clusters can be advantageous if the app grows in user base or if there's a need to provide low-latency access to users in different geographical locations.
    

#### Diving in off the Dock(er), no `Bun` intended...😏

I started out wanting to containerize this application while using Bun to serve up my app. I was put in my place immediately 😅. The complexity of getting Bun set up with Docker is not well documented whatsoever and the few example projects I saw were a bit too basic for me to apply what they were showing to this project. So my idea is to just stick with using node and (possibly) implement bun after launching the project as an enhancement. I understand Docker enough to get around some troubleshooting for my work at Cars Commerce, but I'm no expert whatsoever. So I'm banking on this project to bring along some good lessons (and plenty of challenges).

## **Project Concept**

**Objective**: My journey with the "Personal Finance Tracker" is not just about developing a project; it's about crafting a personal financial assistant. This tool, grounded in advanced analytics, aims to provide precise financial health forecasts. My goal is to empower not only myself but potentially others as well, enabling more informed decisions about finances.

**Project Significance**: More than a mere technical endeavor, this project is a deeply personal endeavor aimed at demystifying financial management for a broader audience, ranging from lower-income communities to students, and working professionals. Through predictive analytics, my ambition is to boost financial literacy, guiding users to navigate through financial challenges and plan proactively for their future.

### **Understanding the Scope**

**Key Features – From Concepts to Reality**

1. **Tracking Income and Expenses**: A core feature where users can log and monitor their finances for a crystal-clear view of their financial status.
    
2. **Categorizing Financial Transactions**: An automatic system to categorize transactions – making it simpler to understand spending habits and pinpoint areas for improvement.
    
3. **Predictive Analysis (*extra credit*)**: Using historical data to forecast future expenses and savings, aiding in strategic budget planning and financial decision-making.
    

**Intended Users**: From budget-conscious individuals and students to long-term investment planning professionals – this tool is designed for anyone looking to upgrade their financial management skills.

**Use Cases**: Whether it's regular budget tracking, setting financial goals, forecasting expenses, or identifying savings opportunities, this tool aims to cover it all.

### **Technical Journey and Choices**

**Technology Stack Decisions**

1. **Frontend**: After exploring various options, I've landed on SvelteKit with TypeScript and Vite. Their modern architecture and fast rendering capabilities promise a seamless user experience.
    
2. **Backend**: I chose Python with Django over Flask for its flexibility and simplicity – crucial for potential future customizations.
    
3. **Database**: CockroachDB won over Fauna for its strong consistency, transactional data integrity, and rich documentation for newcomers.
    

**Extra Tools**: I plan to Dockerize my app. Bun was considered, but it's currently on the "extra credit" list, possibly integrated at the project's end as an enhancement.

**Rationale Behind Choices**: Each piece of the tech stack was selected for its strength and industry relevance. SvelteKit for frontend efficiency, Python and Flask for a flexible backend, and FaunaDB for robust serverless data management – a combination that I believe will address the needs of this project effectively.

### **Project Timeline and Milestones**

**Rough Timeline**

* **Phase 1**: Conceptualization and Planning (Month 1)
    
* **Phase 2**: Development of Core Features (Months 2-4)
    
* **Phase 3**: Integration and Testing (Month 5)
    
* **Phase 4**: Launch and Feedback Incorporation (Month 6)
    
* **Note**: Aiming for completion within a year, considering personal and professional commitments. Timeline adjustments are possible.
    

**Key Milestones**

* **M1**: Project Blueprint and Requirement Analysis (End of Month 1)
    
* **M2**: Alpha Version with Basic Features (End of Month 3)
    
* **M3**: Beta Version *+Predictive Analysis* (End of Month 5)
    
* **M4**: App Launch (End of Month 6)
    

**New Dev Portfolio & Anticipating the Journey Ahead**

I'm pumped again as I venture deeper into this project, eager to immerse myself in the technologies I've chosen and tackle the challenges they present. Over the last couple of weeks, I took a long and much-needed vacation. During that time I built a new dev portfolio and added it to a domain I picked up last year with a vision of what I'm trying to offer and contribute to the space of development: [Digital Dopamine](https://digitaldopamine.dev/).

This blog post marks the beginning of a new series dedicated to this project, where I'll be sharing detailed plans and technical insights as the project unfolds. Alongside, I'll continue my journey with the 100-days-of-python challenge. While it might seem monotonous at times, I told myself I was going to complete it and I'm committed to seeing it through (don't know why I did that to myself though lol "Life Been Lifing" 😅).

For those interested in following the project's progress, feel free to ⭐️ and 👀 the repository here: [Leo\_Ledger on GitHub](https://github.com/kdleonard93/Leo_Ledger). Let's get to work!

#### **If you want to keep up with my writing or want to connect as peers, check out my social links below and give me a follow!**

* [**𝕏 Twitter**](https://twitter.com/RingoMandingo93)
    
* [**💻 Github**](https://github.com/kdleonard93)
    
* [**👾 Discord**](https://discord.com/users/407639833146818570)
    
* [**👔 LinkedIn**](https://www.linkedin.com/in/kyle-leonard93/)