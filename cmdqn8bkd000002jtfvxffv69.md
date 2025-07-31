---
title: "Creatures of Habit: Devlog Chronicles - Part 3"
seoTitle: "Creatures of Habit: Tauri, LLC & What's Next"
seoDescription: "Follow my journey building Creatures of Habit. This update covers Tauri integration for desktop & mobile, UI improvements, forming an LLC, and future plans."
datePublished: Thu Jul 31 2025 00:15:20 GMT+0000 (Coordinated Universal Time)
cuid: cmdqn8bkd000002jtfvxffv69
slug: creatures-of-habit-devlog-chronicles-part-3
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1753405630912/269c805d-9931-42cd-a3e3-1c82c3f6c5e8.png
tags: app-development, typescript, sqlite, habits, svelte, drizzleorm, turso

---

## Check-in time, A LOT has been worked on.

Sup folks, it's been nearly two months since my last post, and a ton of work has been done on “Creatures of Habit”. It’s so much that by the time I went through every little thing, I’d lose the attention of 5 people still keeping up with my articles.

![](https://media2.giphy.com/media/v1.Y2lkPTc5MGI3NjExM2Rub25zd2ppaHA5eHhuejB4NXk5bnY0ZjJmOGkybGJ0dTI4MnZkZCZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9cw/rnHMRKkJ7EYc2RBLrH/giphy.gif align="center")

But bad jokes aside, I’ve worked on numerous fixes and improvements to the UI, set up the base work for staging deploys, implemented Tauri for mobile and desktop app capabilities, dedicated local db setup (in progress), and Auth0 implementation (research, no code yet). I’ve also been doing things to situate myself in the proper position if I ever want to ship this app. It’s growing into something I never imagined I’d be able to make, but I’ve been loving the journey. So I’ve officially registered my business “Digital Dopamine LLC” and trademarked it ✊🏾. I’ve been having discussions with some peers of mine, and it seems we are all clear that we want to be able to work for ourselves at some point. They all have different professions, and when combining our heads and skills, we see a lot of opportunity to be had, even during these troubling times here in the States.

With that said, I’m going to cover the following in this article:

* An overview of the code that has been committed.
    
* Background around the LLC and Trademark decision
    
* Other project ideas that sprouted from the conversations I’ve had. None of which I’ll be starting before getting this app to a good spot.
    

So let’s get into it.

## Code Updates Galore

Most of the code updates related to UI fixes, theme changes, big improvements to data integrity, improved performance, with some maintenance & debugging updates to top it off. Like always, you can check out the pull requests merged in since my last post (May 27th) → [https://github.com/kdleonard93/creatures-of-habit/pulls?q=is%3Apr+is%3Aclosed](https://github.com/kdleonard93/creatures-of-habit/pulls?q=is%3Apr+is%3Aclosed). Below is a quick screenshot for the folks who don’t know their way around GitHub.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1753410759919/6fd164c2-b906-41f1-a2e6-a7a15960146f.png align="center")

I follow the same flow of putting every update behind a PR, even if it’s just me working on this project. My current automated testing suite does a great job of helping me catch issues before successfully committing and pushing. This helped me prevent a few breaking changes when updating packages and Svelte versions, amongst other things like lint errors.

### Changes to the Theme

There have been many changes to the theme. Mostly visually, but there are a few things updated with the logic on some components. The main one being the Progress bar. In my last article, I mentioned I added the progress bar along with some other UX improvements for the Dashboard. But I discovered a handful of bugs with the Progress bar, like issues with habit completions, how the state is updated when new habits are added after already completing a few or all habits, and resetting that state each day. It was tricky as hell. I had an issue with what I was retrieving from the DB as a completed VS active habit. The math didn’t account for new habits being added, so I pretty much had an update for it to take: `(number of rows where completed = true / total number of rows) * 100`. This way, once new habits were added, the total changed, fixing my calculation. Then I was able to pass the function’s return down as a prop and assign the value to the Progress Bar UI that’s on the user’s Dashboard.

Outside of that, most changes were just a bunch of CSS and Tailwind config updates. Below is a quick video of me touring the “New and Improved Design!!!!!!”:

%[https://www.loom.com/share/1e88db6da12643d4b562db0f9409cd44?sid=89d48ab7-8d49-47ee-b940-64ab77490f4a] 

### Taurica, Taurida, and Tauri(s)

If the section title doesn’t make sense, check out the [wiki](https://en.wikipedia.org/wiki/Tauri). When trying to make a unique title, I learned that the Tauri were ancient people who settled in the Crimea peninsula. Not sure if the Tauri framework was inspired by the Tauri people, but it made for a good title 😄.

Anyway, to get back on track, I wanted to discuss Tauri and why I’ve integrated this framework into my app. Better yet, I’ll just post their sales pitch below:

> Tauri is a framework for building tiny, fast binaries for all major desktop and mobile platforms. Developers can integrate any frontend framework that compiles to HTML, JavaScript, and CSS for building their user experience while leveraging languages such as Rust, Swift, and Kotlin for backend logic when needed.

Basically, this framework will allow me to launch this app on Mobile and Desktop as well as Web. The only additional headache is to at least learn to understand Rust. So far, I have not needed to write anything extensive in Rust that wasn’t a part of their [SvelteKit setup docs](https://tauri.app/start/frontend/sveltekit/). It was pretty smooth to get it implemented as well. Just an add of the cli with `pnpm add -D @tauri-apps/cli@latest` a quick `pnpm tauri init` did about 85% of what’s needed to make this app cross-platform. The remaining 15% was updated by me, but very minimally, and there is a dope repo I found from this [post in the sveltejs subreddit](https://www.reddit.com/r/sveltejs/comments/1kqtmdl/announcing_v20_of_tauri_svelte_5_shadcnsvelte/?share_id=NW2Nbxy6bLhw_WsYNcvER&utm_content=2&utm_medium=android_app&utm_name=androidcss&utm_source=share&utm_term=3): [https://github.com/alysonhower/tauri2-svelte5-shadcn](https://github.com/alysonhower/tauri2-svelte5-shadcn). Which was perfect for my project since I’m using Svelte v5 as well. So referencing his config files helped a lot in getting mine set. That’s it! I’d say I’m 95% cross-platform ready, with the remaining 5% saved for figuring out how to push this to production once I get to that point.

### Small But Impactful

The rest of the code changes were pretty small in terms of functionality, but there were heavy visual upgrades, Product & Support pages built out, and dummy content added to them. There was also some research done on tools I wanted to add, like Auth0, as well as get a local DB setup, so I’m not constantly manipulating the real DB. A local DB is even more important to have before this app launches, so I can test properly after it’s live. I won’t get into the details of the code added for this part since it seems unnecessary, but you can see me go through the pages in the video above.

## LLC Me, Baby

Not too long ago, at my place of work, which currently pays my bills, there was an available company with Rocket Lawyer. During that meeting, I learned that as a Cars.com employee, I get a few free benefits with their services, one being setting up an LLC. It just felt like the right move to do, considering how rapidly things are changing in the industry now and in our society in general. There’s no telling when Rocket Lawyer’s partnership might be replaced with a different one.

So I pulled the trigger, and while I should have planned a big spend like this a bit better 😅, it was relatively affordable in terms of securing the name of your business and trademark. So the plan is to release any products/projects moving forward under `Digital Dopamine`. I’ve had the name for a while, as my portfolio website’s URL is [digitaldopamine.dev](https://digitaldopamine.dev/), and it hits home for me. Today’s digital age is all about quick and fast dopamine hits from social media, gaming, or any form of visual entertainment, and I saw no better name for my company that will be building apps and tools for the geeks around the web. Which leads me to the next project I started discussing with some close friends of mine.

## New App…..For Next Year

One of my good friends loves to cook and wanted to start a smash burger business in the burbs of Chicago, since there are no good smash burger locations once you leave the metropolitan area. I initially offered just to make his landing page, but after talking through the idea for an hr or so, I asked if there was any app that he would love that isn’t out at the moment. We found an app called RecipeMe, and while that app does a lot of good things, it was missing one big feature. Not that they will be reading my article, but I don’t want to say exactly what feature we were talking about, but it would require an LLM implementation, and I have a few ideas to branch off of that as well, that’s catered to our culture of cooking. One thing I need to do is start researching the OG recipes from our parents and grandparents and get that data stored in a Notion doc or something. That way, once I’m ready to start building it, I’ll be prepped with unique homemade recipes (hopefully) not found anywhere else on the internet.

## Looking Ahead

That’s about it for this write-up. Please check out the repo if you want a deeper dive into what code has been implemented since Part 2. Creatures of Habit is coming together nicely, but I still have a lot of work left to do. A quick look at what’s ahead:

1. **Push Notifications**: I need to figure out how to get push notifications working on mainly the Desktop and Mobile apps, and then follow that up with web.
    
2. **User Management Enhancement**: I need to implement a “Forgot Your Password” feature as well as a “Delete Your Profile” feature, along with other user management improvements.
    
3. **Offline Support Research (cont.)**: While we have Tauri set up, we still need to get an “Offline First” implementation in.
    

Until next time, folks. Be easy and keep pushin’ 🤘🏾.

#### **If you want to keep up with my work or want to connect as peers, check out my social links below and give me a follow!**

* [**🦋 Bluesky**](https://bsky.app/profile/digitaldopamine.dev)
    
* [**💻 Github**](https://github.com/kdleonard93)
    
* [**👾 Discord**](https://discord.com/users/407639833146818570)
    
* [**👔 LinkedIn**](https://www.linkedin.com/in/kyle-leonard93/)