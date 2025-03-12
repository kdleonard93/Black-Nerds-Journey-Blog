---
title: "Creatures of Habit: Devlog Chronicals"
seoTitle: "Creatures of Habit: Coding Challenges & Progress Check"
seoDescription: "Building 'Creatures of Habit', a habit-tracking RPG app. Tackling coding challenges, TypeScript vs PHP, and a 24-day streak. Follow my journey and progress."
datePublished: Fri Jan 24 2025 14:14:33 GMT+0000 (Coordinated Universal Time)
cuid: cm6auff8a00000alaclgl2qpy
slug: creatures-of-habit-coding-challenges-progress-check
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1737723304938/9d658be5-130a-4bb7-b753-29cded84aa8c.png
tags: app-development, web-development, typescript, hashnode, svelte, drizzleorm, turso

---

## Biggest Challenge Yet

Boy, has this been a busy year so far, and it’s not even a month old. Since [my last article](https://blacknerd.dev/how-to-build-custom-authentication-in-sveltekit-a-session-and-cookie-overview), I’ve been putting in a ton of time on this project. As soon as the new year hit, I made it a goal to work on this or a different project every day to see how long I could keep my coding streak. I’m 24 days in now, and there is no sign of breaking, but then again, it’s been less than a month 😅.

The main accomplishment with this is to build up my consistency. I recently got a new promotion working on a different team (which also started this year) so I’ve been trying to skill up on my day-to-day consistency. Like many others, I assume the wild nature of how life in the US has been unfolding has been…..distracting, to say the least. But with that aside, I’m aiming for 2025 to be my year of consistency. I’m talking like BIG CONSISTENT energy, where my entire GitHub contribution graph for this year is fully green and I have at least one solid project in production, that project being [Creatures of Habit](https://github.com/kdleonard93/creatures-of-habit).

## State of the App and Roadmap

After writing up my authentication, I made a roadmap and plan on what I needed to accomplish for an MVP. Below is the rough plan and I’m only going to post the sub-tasks of Phases 1 and 2. Phases 3-5 will just show the feature/goal for that sprint since it’ll be a while until I start them and didn’t want to bloat this article:

### Phase 1: Foundation & Authentication (4-6 weeks)

1. User System Setup
    
    * <s>Implement secure user registration and login using Lucia authentication library</s>
        
        * <s>Integrate with database for user data storage</s>
            
        * <s>Implement password hashing and security measures</s>
            
    * <s>Design and implement intuitive profile creation flow</s>
        
        * <s>Multi-step wizard for gathering user information</s>
            
        * <s>Profile completeness indicator</s>
            
    * <s>Develop basic settings page with account management options</s>
        
        * <s>Password change functionality</s>
            
        * Notification preferences
            
        * Privacy settings
            
    * Implement optional email verification system
        
        * Automated verification email sending
            
        * Secure verification link generation and processing
            
2. Character Creation
    
    * <s>Design and implement fantasy race selection system</s>
        
        * <s>Create detailed descriptions and visual representations for each race</s>
            
        * <s>Implement unique stat bonuses and abilities for each race</s>
            
        * <s>Develop race-specific storylines and background options</s>
            
    * Develop custom avatar creation system
        
        * Design modular character parts (hair, eyes, body types, etc.)
            
        * Implement color customization for various features
            
        * Create randomization option for quick character generation
            
    * <s>Design and implement initial class or path choice system</s>
        
        * <s>Create detailed class descriptions and abilities</s>
            
        * <s>Implement class-specific starting equipment and skills</s>
            
        * <s>Develop class change or multi-class options for future progression</s>
            
    * <s>Develop starting stats allocation system</s>
        
        * <s>Create balanced stat distribution options</s>
            
        * <s>Implement stat impact explanations and tooltips</s>
            
        * Develop reallocation or respec options for future use
            
    * Implement character naming system
        
        * Create name generation options (random, themed, custom)
            
        * Implement name uniqueness checks
            
        * Develop naming conventions and filters
            

### Phase 2: Core Habit System (6-8 weeks)

1. Habit Management
    
    * <s>Implement CRUD operations for habits</s>
        
        * <s>Design intuitive habit creation interface</s>
            
        * <s>Develop habit editing and updating functionality</s>
            
        * <s>Implement soft and hard deletion options</s>
            
        * <s>Add a visual when selecting a custom frequency so the user can see the days on the task</s>
            
    * Design and implement habit categories and types
        
        * Create pre-defined categories (health, productivity, etc.)
            
        * Implement custom category creation
            
        * Develop habit type system (daily, weekly, one-time)
            
    * Develop frequency settings for habits
        
        * <s>Implement daily, weekly, and custom recurrence options</s>
            
        * Develop reminder system integrated with frequency settings
            
    * Implement difficulty levels for habits
        
        * ***Create balanced difficulty scale (easy, medium, hard, etc.)***
            
        * Develop adaptive difficulty system based on user performance
            
        * Implement difficulty-based rewards and experience points
            
    * Design and implement reward calculations
        
        * Create algorithm for calculating rewards based on difficulty and consistency
            
        * Implement bonus rewards for streaks and milestones
            
        * Develop penalty system for missed habits
            
2. Daily System
    
    * Design and implement daily quests and tasks view
        
        * Create visually appealing and intuitive daily dashboard
            
        * Implement task prioritization and sorting options
            
        * Develop quick-add functionality for impromptu tasks
            
    * Implement check-in system
        
        * Design user-friendly check-in interface
            
        * Develop partial completion options for habits
            
        * Implement undo or correction functionality for accidental check-ins
            
    * Develop streak tracking system
        
        * Implement streak calculation algorithm
            
        * Create visual representations of streaks (flames, chains, etc.)
            
        * Develop streak recovery options (grace periods, streak freezes)
            
    * Implement daily reset logic
        
        * Develop time zone aware reset system
            
        * Implement rollover options for uncompleted tasks
            
        * Create daily summary and reflection prompts
            
    * Design and implement progress indicators
        
        * Create visual progress bars for habits and overall daily goals
            
        * Implement milestone celebrations and achievements
            
        * Develop long-term progress tracking and visualization
            

### Phase 3: RPG Elements (6-8 weeks)

### Phase 4: UI/UX Implementation (4-6 weeks)

### Phase 5: Enhanced Features (6-8 weeks)

As you can see, I still have PLENTY to get done before this app is considered a working alpha. Anything crossed out has been finished so you can see my current state for this app. But I’m already very proud of the work I've put in thus far. This is the most consistent I’ve been with coding since my Lambda School days, and my current streak surpassed all streaks set when I was enrolled in 2019.

Some of the biggest challenges with what I’ve finished though would have to relate to the user system and character creation setup. I leaned **HEAVILY** on online resources and examples from other apps but got the job done. One thing that’s constantly tripping me up is the type system. Working with types in Typescript vs types in PHP throws me for a loop every time. They are pretty different in terms of how types are implemented and while Typescript is more strict and unforgiving, PHP is a bit looser, has type juggling, and is written differently for the most part (EX: Typescript uses type interfaces and PHP only uses them in certain contexts).

This brings me back to a hurdle I’ve mentioned in my past posts: the annoying action of context-switching. I’d love to focus on Typescript and Svelte for work and my personal projects, but the world isn’t my oyster, so I gotta do what I gotta do to pay the bills 💸.

For example, here is how I have the CreatureStats type interface set up in TS:

```typescript
export interface CreatureStats {
	strength: number;
	dexterity: number;
	constitution: number;
	intelligence: number;
	wisdom: number;
	charisma: number;
}

export interface RegistrationData {
	email: string;
	username: string;
	password: string;
	confirmPassword: string;
	age: number;
	creature: {
		name: string;
		class: CreatureClassType;
		race: CreatureRaceType;
		stats: CreatureStats;
		background?: string;
	};
	general: string;
}
```

You can see the stats being created in its own interface and being referenced in the RegistrationData interface. Below, it’s being set in my RegistrationWizard.svelte component with it’s default values:

```svelte
	let formData = $state<RegistrationData>({
		email: '',
		username: '',
		password: '',
		confirmPassword: '',
		age: 0,
		creature: {
			name: '',
			class: CreatureClass.WARRIOR,
			race: CreatureRace.HUMAN,
			stats: {
				strength: 10,
				dexterity: 10,
				constitution: 10,
				intelligence: 10,
				wisdom: 10,
				charisma: 10
			},
			background: undefined
		},
		general: ''
	});
```

Whereas, this is how it would look in PHP:

```php
<?php

interface CreatureStats {
    public function getStrength(): int;
    public function getDexterity(): int;
    public function getConstitution(): int;
    public function getIntelligence(): int;
    public function getWisdom(): int;
    public function getCharisma(): int;
}
```

```php
<?php

$creatureStats = [
    'strength' => 10,
    'dexterity' => 8,
    'constitution' => 12,
    'intelligence' => 14,
    'wisdom' => 10,
    'charisma' => 6
];

$registrationData = new RegistrationData();
$registrationData->email = "{enter email}";
$registrationData->creature = [
    'name' => '{Creature Name}',
    'class' => CreatureClass::ARCHER,
    'race' => CreatureRace::ELF,
    'stats' => $creatureStats
];
```

The key differences between TS and PHP when it comes to types:

* **Type Safety**: TypeScript provides compile-time type checking, while PHP relies on runtime checks and optional type hints.
    
* **Advanced Types**: TypeScript supports generics, unions, intersections, and more, which PHP does not natively support.
    
* **Interfaces**: TypeScript interfaces are purely structural, while PHP interfaces are more rigid and require explicit implementation.
    

However, the daily work and consistency are helping alleviate the struggle with context switching, so I just have to keep up the hustle.

## Oh, You Want a Lil Preview???

Instead of showing every little thing I’ve done via code snippets, I implore you to check out the Github repo and clone/fork it to try it out locally. It’s nothing pretty as of yet but a lot of the main features are ready to use/test out. In the video below, I’ll go through creating a new user, character, and habit. This should show the persistence of the user log-in and state, basic CRUD, and a look at the user dashboard and creature dashboard.

%[https://www.loom.com/share/09ed1fcb61d84c66bc77cbc789f8dde2] 

I tend to ramble so I used all 5 min of the loom video limit for free accounts lol. But I do touch on everything I said I would. Some other features work like, “Change Password” and" “Edit Habit” but I was running out of time so they aren’t shown in the demo

## EOD

✌🏾 that wraps up my check-in. Hopefully, some interested people out there want to check out the app locally and play around. I’m always open to feedback so if you have any suggestions or critiques, submit an issue or contribute and make a pull request! I’m planning on doing another check-in within the next month or 2 so be on the lookout for my next update!

#### **If you want to keep up with my work or want to connect as peers, check out my social links below and give me a follow!**

* [**🦋 Bluesky**](https://bsky.app/profile/digitaldopamine.dev)
    
* [**💻 Github**](https://github.com/kdleonard93)
    
* [**👾 Discord**](https://discord.com/users/407639833146818570)
    
* [**👔 LinkedIn**](https://www.linkedin.com/in/kyle-leonard93/)