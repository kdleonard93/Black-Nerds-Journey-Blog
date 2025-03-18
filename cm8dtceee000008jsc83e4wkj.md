---
title: "Creatures of Habit: Devlog Chronicles"
seoTitle: "Creatures of Habit: Devlog Chronicles - New Features & Code Wins"
seoDescription: "Jump into my latest dev progress adding XP systems, custom notifications, and analytics to my habit tracking RPG app built with Svelte 5 and TypeScript."
datePublished: Tue Mar 18 2025 01:26:56 GMT+0000 (Coordinated Universal Time)
cuid: cm8dtceee000008jsc83e4wkj
slug: creatures-of-habit-devlog-chronicles
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1741748950386/6c782483-593f-4ad5-aa96-e29ec2cb0818.png
tags: web-development, typescript, habits, svelte, drizzleorm, turso

---

## Checkpoint Reached +1

Hot damn, looking back at all the incremental work done on my project, can’t help but pat myself on the back because this is the first app I have that has a SOLID foundation from front to back. Now by solid foundation, I mean most of my core systems were built out and (most 😉) have tests to compliment them. Not only that, the tech stack used required me to create and manage my own schemas, authentication, and session handling. Compared to my last project [“Leo Ledger”](https://github.com/kdleonard93/Leo_Ledger), the scope itself has been completely different, in size and complexity. Trying to mesh a classic habit tracking app with RPG-like mechanics to gamify it has been my biggest challenge yet. A lot of this has been fun to learn and understand Svelte 5 and TypeScript a bit more, but I’m no expert now and have had my fair share of rage…..which feels like a right of passage with learning TypeScript lol.

Lo and behold, I’ve reached a major milestone, but am far from finished. In this article, I want to go over the new features added since my last entry:

* ### 🔮 Features:
    
    **\- Habit Completion**
    
    **\- XP Setup.**
    
    **\- Notifications System, Reminder, & Testing Route.**
    
    **\-** [**PostHog**](https://posthog.com/) **Implementation (Analytics Tracking).**
    
* ### 🪚 Fixes:
    
    **\-** `Edit Habit` **Functionality Fix.**
    
    **\-** `Logout` **Route POST action Fix for 1 of 2 CTAs.**
    
* ### 🦾 Enhancements:
    
    **\- New theme to give the app a bit of personality (NOT FINAL).**
    
    **\- Updated the** `Signup` **Route’s CTA with** `{isSubmitting}` **for a better UX.**
    
    **\- Implemented** `Toast` **in the app’s notification system.**
    
    **\- CodeRabbit** ***(Temporary; Experimenting with it.)***
    

Let’s get started with the **Features!**

## Small but Mighty Upgrades

Everything in my feature setup seems like it might be a small portion of the grand scope of the project but let me tell ya, that wasn’t the case.

### Habit Completion & XP Feature

This one was a bit of both a feature and an enhancement. The feature of adding a completed route and functionality enhanced the overall habit management system. Now there is a graveyard where all of your completed habits can go. On the `/completed` route, you can permanently delete those habits from the database. This ties into the XP feature since upon completing a habit, depending on the difficulty, you gain experience points!  
However…….those points are worthless at the moment 😂. The XP feature isn’t fully fleshed out yet, but there is activity in the console with proper fetch requests. Below, you can see an example of 1 completed and 1 deleted habit (Need to add an indicator for each to differentiate them in the graveyard….that’s what I’m calling the `/complete` route from now on). Once I permanently delete one, you can see all of the action in the console:

%[https://www.loom.com/share/fd92fb687cb143d0a89283d46bdc7566] 

* Once I click on “Delete Permanently” and confirm my choice, the application sends a DELETE request to the server.
    
* After the deletion is complete, it invalidates (refreshes) the relevant data with a GET request.
    
* Throughout this process, PostHog is tracking these events for analytics.
    

Fun stuff right?? As you can also see in the video, the theme is updated and has some color! There will probably be further adjustments there but that’ll be down the line.

### Notifications System, Reminder, & Testing Route

The notifications system was another BIG feature of the project. I wanted to create a flexible system that would support multiple notification types (in-app, email, SMS)so a plugin architecture was recommended as the best approach. This allows me to add new notification channels in the future without changing the core notification logic.

I implemented the system with three key components:

1. **NotificationManager**: The central hub that handles scheduling, displaying, and managing notifications
    
2. **NotificationStore**: A Svelte store that maintains the state of active notifications
    
3. **Notification Plugins**: Email and SMS plugins that demonstrate the extensibility of the system
    

Here's the code from the `NotificationManager.ts` file that shows the plugin architecture:

```typescript
// Notification Plugin Interface
export interface NotificationPlugin {
    send(notification: Notifications): void;
}

export class NotificationManager {
    private timeouts: Map<string, number> = new Map();
    private plugins: NotificationPlugin[] = [];
    private permission: NotificationPermission = 'default';

    constructor() {
        this.requestPermission();
    }

    public registerPlugin(plugin: NotificationPlugin): void {
        this.plugins.push(plugin);
    }

    // Other code...

    public showNotification(id: string, message: string, type: 'email' | 'sms' | 'in-app'): void {
        // Create notification record
        const notification: Notifications = {
            id,
            message,
            type,
            timestamp: new Date()
        };

        // Add to the notifications store
        notifications.update(n => [...n, notification]);

        // Send to plugins
        this.plugins.forEach(plugin => plugin.send(notification));
    }
}
```

Another difficult task was implementing the **Habit Reminder** feature, which allows users to set custom reminders for each habit. This uses the notification system but adds scheduled notifications based on time:

```typescript
function scheduleReminder() {
    if (!reminderTime) {
        toast.error('Please select a time for the reminder');
        return;
    }

    try {
        // Parse the time input (HH:MM)
        const [hours, minutes] = reminderTime.split(':').map(Number);
        
        // Calculate when the reminder should trigger
        const now = new Date();
        const reminderDate = new Date();
        reminderDate.setHours(hours, minutes, 0, 0);
        
        // If the time is earlier today, schedule for tomorrow
        if (reminderDate <= now) {
            reminderDate.setDate(reminderDate.getDate() + 1);
        }
        
        const delay = reminderDate.getTime() - now.getTime();
        
        // Schedule the notification
        notificationManager.scheduleNotification(
            `habit-reminder-${props.habitId}`,
            `Time to complete your habit: ${props.habitTitle}`,
            'in-app',
            delay
        );
        
        // Store reminder in localStorage for persistence
        if (hasLocalStorage) {
            localStorage.setItem(`reminder_${props.habitId}`, JSON.stringify({
                time: reminderTime,
                habitTitle: props.habitTitle
            }));
        }
        
        reminderEnabled = true;
        toast.success(`Reminder set for ${reminderTime}`);
    } catch (error) {
        console.error('Error scheduling reminder:', error);
        toast.error('Could not schedule reminder');
    }
}
```

The magic happens in how the system handles timing. When you select 8:00 AM for your "Morning Workout" habit, the system doesn't just blindly schedule it. It first checks if 8:00 AM has already passed today - if it has, it schedules the reminder for tomorrow instead. This prevents the annoying scenario where setting a reminder would trigger it immediately if that time has already passed.

I also made sure that reminders persist between sessions by storing them in localStorage. Each habit gets its own localStorage entry with a unique key: `reminder_${habitId}`.

The UI for reminders is clean and straightforward:

* If you haven't set a reminder yet, you see a time picker and a "Set Reminder" button
    
* Once a reminder is set, the UI changes to show the scheduled time and offers a "Remove Reminder" option
    

This kind of context-aware UI helps keep the interface clean while giving users exactly the controls they need.

I spent some time researching edge cases with reminder systems. What happens if a user sets a reminder for 11:59 PM? What if they set multiple reminders across different habits? Does the system handle timezone changes? These were all important considerations to ensure a robust user experience.

### Notification Testing Route

To help debug and demonstrate the notification system, I built a dedicated `/notifications` testing route. This special route lets me trigger different notification types, test delay timing, and verify that the UI components render correctly.

The testing page provides controls for:

* Sending immediate notifications
    
* Scheduling delayed notifications (with customizable delay)
    
* Testing different notification types (in-app, email, SMS)
    
* Clearing all pending notifications
    

This testing route has been invaluable during development. Rather than trying to debug notification issues in the middle of the main application flow, I can isolate and test notification functionality directly by just going to my created route.

The best part is that this testing route uses the exact same notification components and manager as the main application, so any fixes or improvements I make here automatically benefit the entire system.

As the application grows, I plan to expand this testing route to include more sophisticated scenarios, like simulating a day's worth of habit reminders compressed into a 1-minute demo, or testing how the system handles overlapping notifications. This dedicated testing environment will ensure that the notification system remains reliable even as new features are added. Before moving on to the PostHog implementation, I added a quick video below showing the notification testing route in action:

%[https://www.loom.com/share/e54a8b41b6174acb81b751a31acef302] 

### PostHog Implementation (Analytics Tracking)

Adding analytics to "Creatures of Habit" was a game-changer for understanding how users interact with the app. I chose PostHog because it's open-source, respects user privacy, and gives me powerful event tracking without complexity.

Implementing PostHog was surprisingly straightforward. I created a dedicated configuration file to centralize all PostHog settings:

```typescript
import type { PostHogConfig } from 'posthog-js';
import { PUBLIC_POSTHOG_KEY } from '$env/static/public';


console.log('🔍 PostHog: Config file loaded');

export const posthogConfig: Partial<PostHogConfig> = {
    api_host: 'https://us.i.posthog.com',
    capture_pageview: false,
    capture_pageleave: false,
    disable_session_recording: true,
};

export const getPostHogKey = () => {
    if (!PUBLIC_POSTHOG_KEY) {
        console.error('❌ PostHog: API key is not defined');
    }
    return PUBLIC_POSTHOG_KEY;
};
```

Notice how I've explicitly disabled session recording and automated `pageview/pageleave` tracking. I wanted complete control over what events get tracked, rather than having a flood of automatic events that might obscure what's truly important. Like I couldn't track a damn thing without movement events rapidly firing lol it was straight overkill.

The initialization happens in my layout file, ensuring PostHog is available throughout the application:

```typescript
// src/routes/+layout.ts
import posthog from 'posthog-js'
import { browser } from '$app/environment';
import { posthogConfig, getPostHogKey } from '$lib/plugins/PostHog';

export const load = async () => {
    if (browser) {
        posthog.init(getPostHogKey(), posthogConfig);
    }
    return {};
};
```

I'm using the `browser` check to ensure PostHog only initializes in client-side contexts, avoiding any server-side rendering issues.

For page navigation tracking, I implemented a custom solution using SvelteKit's `afterNavigate` hook:

```typescript
// src/routes/+layout.svelte
if (browser) {
    afterNavigate(() => {
        posthog.capture('$pageview');
    });
}
```

The real power comes from tracking specific user actions. Now I can see exactly which features users engage with most. For example, when a user completes a habit:

```typescript
async function completeHabit(habitId: string) {
    try {
        // API call to complete the habit
        const response = await fetch(`/api/habits/${habitId}/complete`, {
            method: 'POST'
        });

        // Process the response...

        // Track the habit completion event
        posthog.capture('habit_completed', {
            habitId,
            difficulty: habitData.difficulty,
            experienceEarned: data.experienceEarned
        });
        
        toast.success(`Gained ${data.experienceEarned} XP!`);
        // ...
    } catch (error) {
        console.error('Error completing habit:', error);
    }
}
```

Now I can answer questions like:

* Which habit difficulties do users prefer?
    
* How many habits do users typically track?
    
* What times of day do users engage most with the app?
    
* Which features lead to higher retention?
    

This data will be invaluable for prioritizing future features. If I see that 80% of users are setting reminders for their habits, I'll know to invest more in expanding the reminder functionality. Conversely, if a feature shows minimal engagement, I can either improve it or deprioritize further development in that area.

The best part is that all of this happens with minimal impact on performance and user privacy. PostHog is lightweight, and I'm only tracking the specific events that provide actionable insights.

## 🪚 Fixes: Small Changes, Big Impact

### Edit Habit Functionality Fix

This issue was racking my brain for a while. The edit functionality was almost working, but the form wasn't properly populated with the existing habit data. Users would click "Edit" on a habit, and the form would appear with blank or incorrect values.

After some debugging, I discovered the issue was in how I was handling the frequency data. The API was returning frequency information in a different structure than what my form component expected.

The fix required adjusting the data mapping in the edit page component:

```typescript
// src/routes/habits/[id]/edit/+page.svelte
const initialData: HabitData = {
    title: data.habit.title,
    categoryId: data.habit.categoryId ?? undefined,
    description: data.habit.description || '',
    frequency: data.habit.frequencyId ? 'custom' : 'daily',
    customFrequency: {
        days: []
    },
    difficulty: data.habit.difficulty,
    startDate: data.habit.startDate ?? new Date().toISOString()
};
```

The key insight was realizing that I needed to check for the existence of `frequencyId` to determine if this was a custom frequency habit. Previously, I was checking a property that sometimes didn't exist, causing the form to render incorrectly.

I also updated the submission handler to use the correct HTTP method and endpoint:

```typescript
async function handleSubmit(formData: HabitData) {
    const response = await fetch(`/api/habits/${data.habit.id}`, {
        method: 'PUT',
        headers: {
            'Content-Type': 'application/json'
        },
        body: JSON.stringify(formData)
    });

    if (!response.ok) {
        const errorData = await response.json();
        throw new Error(errorData.error);
    }

    await goto('/habits');
}
```

This might seem like a small change, but it had a massive impact on user experience. Now users can properly edit their habits instead of having to delete and recreate them. I’m still having some issues with the proper date and time showing on the “completed” tasks:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1742260233295/9474293f-350a-40f4-b737-fc88bfecd003.png align="center")

But it’s not breaking anything so that’s something I have noted to work on as a bug fix down the line.

### Logout Route POST Action Fix

I had two logout buttons in the app - one in the main navigation and another in the dashboard. Strangely, only one was working correctly. After investigating, I realized I wasn't using SvelteKit's `enhance` directive on the dashboard logout form.

The fix was simple but crucial:

```typescript
<form action="/logout" method="POST" use:enhance>
    <Button type="submit" variant="outline" size="sm" class="flex items-center gap-2">
        <LogOut class="h-4 w-4" />
        Logout
    </Button>
</form>
```

The `enhance` directive is crucial here - it tells SvelteKit to handle the form submission using client-side JavaScript when possible, rather than triggering a full page reload. Without it, the form was submitted traditionally, which disrupted the expected application flow.

I also removed the secondary Logout CTA cause it was redundant. This fix ensures that the logout button works consistently and provides a smooth user experience.

### Updated Signup Route's CTA with `isSubmitting` for Better UX

One of my pet peeves is form buttons that don't provide feedback. When you click "Sign Up" on most websites, you're left wondering if anything is happening, especially if there's network latency.

I solved this by adding a loading state to the signup form's button:

```typescript
<Button on:click={nextStep} disabled={isSubmitting}>
    {#if isSubmitting}
        <div class="mr-2 h-4 w-4 animate-spin rounded-full border-2 border-current border-t-transparent"></div>
        {currentStep === totalSteps ? 'Creating Account...' : 'Processing...'}
    {:else}
        {currentStep === totalSteps ? 'Create Account' : 'Next'}
    {/if}
</Button>
```

This provides two crucial UX improvements:

1. Visual feedback via the spinning loader
    
2. Text feedback that changes based on the current step
    

Additionally, the button gets disabled during submission, preventing accidental double-clicks that could lead to duplicate accounts or other errors.

It's a small enhancement that dramatically improves perceived performance and reduces user anxiety during the critical signup process.

### Implemented Toast in the App's Notification System

To provide non-intrusive feedback throughout the app, I integrated Svelte Sonner for toast notifications. These small, temporary messages appear at the top of the screen to confirm actions or display errors without disrupting the user experience.

### CodeRabbit (Temporary; Experimenting with it)

I don’t know about this one. Feels like a bit of overkill and has yet to point out anything that was a critical error. However, I’m going to give it some more time. I think this would be a slippery slope though if it DOES work. I can’t lean on AI too heavily or It’ll erode my basic debugging skills I’m already lacking a bit of lol. Nonetheless, I AM finding it helpful for catching small issues and suggesting improvements. One particularly helpful aspect has been its suggestions around TypeScript typing. It's helped me make my type definitions more precise and catch potential null reference errors.

All that said, I’ll continue treating it as an experiment for now and evaluate its usefulness as the project progresses.

## Looking Ahead

While I've made significant progress, there's still a lot to do:

1. **Stats & XP System Enhancement**: The stats need to actually affect things in the app and it also needs to be adjusted to have a `min` and `max` at character creation. Right now it’s just character lore at this point.
    
2. **Homepage Redesign**: I need a real homepage that demonstrates the unique RPG-habit connection with interactive elements and clear CTAs for engagement and sign-ups.
    
3. **Quests and Campaigns**: What’s an RPG app without quests?! This system has yet to be prototyped so I’d need to do some research.
    
4. **Dashboard and UI Improvements**: Enhance the user interfaces with character-updated status displays, streak indicators, and progress charts to improve the overall experience.
    
5. **Progressive Achievements**: Tiered achievement system with visual badges, titles, and an achievement gallery to provide additional motivation through accomplishments.
    

The journey of building this app has been pretty damn rewarding, even more so than the finance tracking app. Mainly based on the pure scope and how much I've learned thus far. It’s also shown me that there is still a shit ton to learn about these types of apps and how to properly build them. Trying to turn a habit-tracking app and transforming it into a dope RPG experience has stressed me out 😅 but also has pushed me in certain areas. Stay tuned for what’s next on deck 🤘🏾.

#### **If you want to keep up with my work or want to connect as peers, check out my social links below and give me a follow!**

* [**🦋 Bluesky**](https://bsky.app/profile/digitaldopamine.dev)
    
* [**💻 Github**](https://github.com/kdleonard93)
    
* [**👾 Discord**](https://discord.com/users/407639833146818570)
    
* [**👔 LinkedIn**](https://www.linkedin.com/in/kyle-leonard93/)