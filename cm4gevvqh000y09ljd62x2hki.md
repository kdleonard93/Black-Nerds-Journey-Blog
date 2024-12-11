---
title: "Building Custom Authentication: A Session and Cookie Overview"
seoTitle: "Custom Authentication in SvelteKit: Session & Cookie Overview"
seoDescription: "Explore building custom authentication in SvelteKit without auth libraries. Learn about session management, cookie handling, and secure token storage."
datePublished: Mon Dec 09 2024 02:26:40 GMT+0000 (Coordinated Universal Time)
cuid: cm4gevvqh000y09ljd62x2hki
slug: how-to-build-custom-authentication-in-sveltekit-a-session-and-cookie-overview
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1733710869894/deacc8a0-5edc-4c44-8f41-77e6af05767c.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1733710985075/169ef829-a933-40d7-a4f2-f2b8d7e5405c.png
tags: software-development, authentication, python, typescript, svelte, drizzleorm

---

### Intro

What’s up folks, been a minute since my last post. As everyone and their mother knows the last couple of months have been pretty hectic in terms of things going on in the world. All the while, I’ve been head down on making moves within my company and the efforts have paid off. My last project ([https://leo-ledger.onrender.com/](https://leo-ledger.onrender.com/)) seems to still be living, due to Render changing its free tier limits (although, it still takes about 60 seconds for the server to boot back up 🫠). No additional work has been put into it and I’m now thinking that I will most likely leave the project as is. This is due to the fact that I don’t plan on using HTMX in many of my future projects. I enjoyed seeing its capability when it comes to working closely with Python, but 9/10, I’m opting for Svelte w/Typescript to handle my front end.

I’ve become comfortable with the pair and depending on the type of project I’m doing, I will either choose Django to handle my backend or stick with Typescript, an ORM, and DB tool. I recently started a new project with a scope bigger than I’ve handled before 😅, but I wanted to challenge myself with one main objective, to strengthen my understanding of the scope of different types of applications. I work for a company that builds and maintains websites for car dealerships and I’ve gotten a great sense of the workflow of a company this size and our client’s needs/expectations for their customers. As mentioned earlier, My last project was a Finance tracker and the scope of that project is much different than what I do for a paycheck. That leads me to my new project and the theme of this article.

#### 🥁🥁🥁*Drum Roll*🥁🥁🥁

My next project is a RPG Habit Tracker App! Nothing super original about this idea but the scope of this type of app is much different than my finance tracker and what I do at my job. This forces me to reach for new tools that will better suit the project’s functionality which for me, is what keeps me excited about building things. I’ve probably mentioned it in a previous article but my tendency to be a “Jack of All Languages” sometimes hinders me from really understanding a specific language if I don’t do enough work with it. It’s come to bite me in the ass a couple of times as well but I’m learning to manage my context switching a bit better. One thing I need to do is practice more on code wars and get OOP fundamentals down to a T as well as just thinking a bit more pragmatically. But enough rambling, we’re here to talk about some pretty dope things I learned when I started to work on authentication for my new app. My repo is pubic for the moment but i might move it back to private. Get a gander while you still can → [https://github.com/kdleonard93/creatures-of-habit](https://github.com/kdleonard93/creatures-of-habit).

### So Long Lucia

When deciding on the tech stack I was going to use for this project, the Sveltekit scaffolding process showed Lucia and I’ve heard of the tool in the past as a great choice for setting up Auth within a Sveltekit app. But when I got my project all set. I noticed there were no Lucia references in the auth.ts file. After some searching on the net, I discovered that the maintainer was no longer working or using Lucia himself and explained that it just wasn’t working in its current state. They made an [announcement](https://github.com/lucia-auth/lucia/discussions/1714) stating that it would be deprecated in March 2025. But what they are doing to circumvent the hole it’s leaving in the community, is turning that repo into a learning source on implementing auth from scratch on your own. Now I'm sure that sounds cumbersome and I thought the same exact thing, but it really wasn’t that bad and I ended up learning a bit about general guidelines related to implementing auth on web applications.

### Okay Cool, You Learned About Sessions……Want a Cookie?!?!

Hopefully, the section title wasn’t too corny 😏, but this is where I yap about how I appreciate what that maintainer did. If they never made documentation on how to convert from Lucia and build auth from scratch on my own, I might have switched up my stack a bit and used Drizzle with Supabase instead of Drizzle with Turso. The Lucia docs are straightforward and concise when it comes to examples of setting up `sessions` and `cookies`, providing documentation links for related references like, encoding schemes, the Crypto: randomUUID() method, and the SHA-256 hash function to name a few.

Without getting into much of the nitty gritty (much of which i’m still wrapping my head around), the main advantage with digging deep and writing these from scratch is I can apply this knowledge to other projects that don’t necessarily use the same stack. It also helps me understand the nuances of authentication under the hood so I’m better equipped to be a helping hand to folks that aren’t privy to building auth.

Let's dive into the nuts and bolts of implementing authentication from scratch. I'll break down my `auth.ts` file to show you how surprisingly manageable this process can be (even though some concepts are still a. bit fuzzy to me).

#### The Building Blocks

First up, we have some core functionality for handling sessions:

1. **Session Token Generation**: We create a secure random token using `crypto.getRandomValues()` and encode it in `base32`. This gives us a unique identifier for each user session.
    

```typescript
export function generateSessionToken() {
    const bytes = crypto.getRandomValues(new Uint8Array(20));
    return encodeBase32LowerCase(bytes);
}
```

2. **Session Creation**: When a user logs in, we create a new session by:
    
    * Hashing the token using SHA-256 (for secure storage)
        
    * Setting an expiration date (30 days from creation)
        
    * Storing it in our database with the user's ID
        

```typescript
export async function createSession(token: string, userId: string) {
	const sessionId = encodeHexLowerCase(sha256(new TextEncoder().encode(token)));
	const session: table.Session = {
		id: sessionId,
		userId,
		expiresAt: new Date(Date.now() + DAY_IN_MS * 30)
	};
	await db.insert(table.session).values(session);
	return session;
}
```

The cool thing about this approach is that we never store the raw session token in our database, just the hashed version. This adds an extra layer of security in case our database ever gets compromised.

#### Session Management & Validation

The real magic happens in the `validateSessionToken` function. Here's what it does:

* Checks if the session exists
    
* Verifies it hasn't expired
    
* Automatically renews sessions that are close to expiring (15 days out)
    
* Returns the user's data if everything checks out
    

```typescript
export async function validateSessionToken(token: string) {
	const sessionId = encodeHexLowerCase(sha256(new TextEncoder().encode(token)));
	const [result] = await db
		.select({
			// Adjust user table here to tweak returned data
			user: { id: table.user.id, username: table.user.username },
			session: table.session
		})
		.from(table.session)
		.innerJoin(table.user, eq(table.session.userId, table.user.id))
		.where(eq(table.session.id, sessionId));

	if (!result) {
		return { session: null, user: null };
	}
	const { session, user } = result;

	// Check if session is expired
	const sessionExpired = Date.now() >= session.expiresAt.getTime();
	if (sessionExpired) {
		await db.delete(table.session).where(eq(table.session.id, session.id));
		return { session: null, user: null };
	}
	// Renew session if close to expiration
	const renewSession = Date.now() >= session.expiresAt.getTime() - DAY_IN_MS * 15;
	if (renewSession) {
		session.expiresAt = new Date(Date.now() + DAY_IN_MS * 15);
		await db
			.update(table.session)
			.set({ expiresAt: session.expiresAt })
			.where(eq(table.session.id, session.id));
	}

	return { session, user };
}
```

I also implemented automatic session renewal. If a user's session is within 15 days of expiring, it gets extended in the background. This creates a smoother user experience to prevent kicking users off the app when their current session ends 🤘🏾.

#### Cookie Management

The final piece of the puzzle is cookie handling. We set two main functions:

```typescript
setSessionTokenCookie(event, token, expiresAt)
deleteSessionTokenCookie(event)
```

These handle the grits of cookie management with some important security settings:

* `httpOnly: true` prevents JavaScript access to the cookie
    
* `sameSite: "lax"` provides a good balance between security and usability
    
* Proper expiration handling ensures cookies clean up after themselves
    

#### Why This Matters

Building this from scratch instead of using a library like Lucia taught me a ton about web security. It's not just about storing a user's login state – it's about:

* Secure token generation and storage
    
* Protection against session hijacking
    
* Proper cookie security settings
    
* Graceful session expiration handling
    

While it might seem daunting at first, breaking down authentication into these components makes it much more approachable. Plus, as I previously mentioned, I can now adapt this knowledge to any framework or project I work on in the future.

The full file is below for reference:

```typescript
import type { RequestEvent } from '@sveltejs/kit';
import { eq } from 'drizzle-orm';
import { sha256 } from '@oslojs/crypto/sha2';
import { encodeBase32LowerCase, encodeHexLowerCase } from '@oslojs/encoding';
import { db } from '$lib/server/db';
import * as table from '$lib/server/db/schema';

const DAY_IN_MS = 1000 * 60 * 60 * 24;

export const sessionCookieName = 'auth-session';

export function generateSessionToken() {
	const bytes = crypto.getRandomValues(new Uint8Array(20));
	const token = encodeBase32LowerCase(bytes);
	return token;
}

export async function createSession(token: string, userId: string) {
	const sessionId = encodeHexLowerCase(sha256(new TextEncoder().encode(token)));
	const session: table.Session = {
		id: sessionId,
		userId,
		expiresAt: new Date(Date.now() + DAY_IN_MS * 30)
	};
	await db.insert(table.session).values(session);
	return session;
}

export async function validateSessionToken(token: string) {
	const sessionId = encodeHexLowerCase(sha256(new TextEncoder().encode(token)));
	const [result] = await db
		.select({
			// Adjust user table here to tweak returned data
			user: { id: table.user.id, username: table.user.username },
			session: table.session
		})
		.from(table.session)
		.innerJoin(table.user, eq(table.session.userId, table.user.id))
		.where(eq(table.session.id, sessionId));

	if (!result) {
		return { session: null, user: null };
	}
	const { session, user } = result;

	// Check if session is expired
	const sessionExpired = Date.now() >= session.expiresAt.getTime();
	if (sessionExpired) {
		await db.delete(table.session).where(eq(table.session.id, session.id));
		return { session: null, user: null };
	}
	// Renew session if close to expiration
	const renewSession = Date.now() >= session.expiresAt.getTime() - DAY_IN_MS * 15;
	if (renewSession) {
		session.expiresAt = new Date(Date.now() - DAY_IN_MS * 15);
		await db
			.update(table.session)
			.set({ expiresAt: session.expiresAt })
			.where(eq(table.session.id, session.id));
	}

	return { session, user };
}

export type SessionValidationResult = Awaited<ReturnType<typeof validateSessionToken>>;

export async function invalidateSession(sessionId: string): Promise<void> {
	await db.delete(table.session).where(eq(table.session.id, sessionId));
}

export function setSessionTokenCookie(event: RequestEvent, token: string, expiresAt: Date): void {
	event.cookies.set(sessionCookieName, token, {
		httpOnly: true,
		sameSite: "lax",
		expires: expiresAt,
		path: '/'
	});
}

export function deleteSessionTokenCookie(event: RequestEvent): void {
	event.cookies.delete(sessionCookieName, {
		httpOnly: true,
		sameSite: "lax",
		maxAge: 0,
		path: '/'
	});
}
```

If anyone is looking for a deeper dive into the docs, I’ve added a couple of references below:

* [https://lucia-auth.com/](https://lucia-auth.com/) (resources on implementing authentication with JavaScript and TypeScript)
    
* [https://thecopenhagenbook.com/](https://thecopenhagenbook.com/) (a general guideline on implementing auth in web applications)
    

### “Creatures of Habit” Status

My newest project, Creatures of Habit, is underway and off to a good start. The reason behind waiting to create an RPG-specific habit-tracking app is:

1. I love RPGs….plain and simple 😂.
    
2. There are a few habit trackers out there that gamifies the tasks but none of them seemed to work exactly how I pictured it would work.
    

My stack for this project is Sveltekit w/Typescript, Shadcn Svelte + Tailwind CSS, Drizzle ORM, and authentication based on [this guide](https://lucia-next.pages.dev/) from the Lucia maintainer. My goal, while hefty, is to create the perfect habit-tracking app for me and me only…if other people like it then so be it lol. But in all seriousness, my MVP (Minimum Viable Product) for this project is to get a working web app that actually functions like a storyboard/tabletop RPG. None of the other apps focus on the hero (or creature in my app’s case) enough. There are always a few stats given but none really felt like an RPG, just these shell RPGs that feel like grind fests or they turned into more of a subscription model for extra features and I totally get the latter if it’s a small team and they want to actually make money from the work they did. Habitica is a great example of an app that I want to make an improved version of. It’s got most of the features I’d want in an RPG-style habit tracker but there are also a few things I think it’s missing. Here is a little screenshot of the Dailies tab:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1733707561746/cd682bec-a241-4663-93e0-ffe6fb4922c0.png align="center")

One main feature I’d like to change is the quest system. It seems more akin to chores than actual quests. The main reason is because there is no story behind each quest. My idea is to treat them as recurring quests that get harder and harder each run-through, kind of like a roguelike progression with dungeons. Each dungeon has a boss but before you get to that boss level, you have to complete the objectives on each preceding level. Once the dungeon is cleared, there is a new tier you can do that will offer more exp and loot. That’s just one thing I’d change amongst a few others but overall, this will be an interesting journey to completion (or at least a working alpha). I made a roadmap in Notion and you can find that here → [https://www.notion.so/Creatures-of-Habit-Roadmap-135ab7433e8e80d6a175c7de10bdb631?pvs=4](https://www.notion.so/Creatures-of-Habit-Roadmap-135ab7433e8e80d6a175c7de10bdb631?pvs=4)

### Day 30-33 of “100 Days of Python”

Moving like molasses with this course 😅, but still moving nonetheless. The 4 days that were completed covered:

1. Errors, Exception, & JSON data
    
2. Flash Card Project
    
3. Email Sending with the `smtplib` & `datetime` modules.
    
4. Learning about API Endpoints w/ ISS Overhead Notifier project
    

The only new(ish) things covered within these 4 days were Errors, Exceptions, and using API Endpoints + Parameters. I won’t go into detail on these areas since this article is focused on Auth and my new project but you can find the completed code for each day on my [100-Days-Of-Python repo](https://github.com/kdleonard93/100-Days-Of-Code_Python).

### Conclusion

So that’s a wrap on this joint. There are lots of intriguing milestones to hit over the next year and I’m starting to settle in with what works for me in terms of my productivity. Tons of things learned in 2024 and I’m excited to get 2025 started on the right foot. I plan to continue posting article updates for the project but will also start smaller Python-based projects as well to not tire myself out on building Creature of Habit. The Python-specific projects are going to revolve around scripting and making things to automate my daily life + scripts for autonomous investing, specifically using the various APIs in the blockchain space. Until next time, folks ✌🏾.

#### **If you want to keep up with my work or want to connect as peers, check out my social links below and give me a follow!**

* [🦋 Bluesky](https://bsky.app/profile/digitaldopamine.dev)
    
* [**💻 Github**](https://github.com/kdleonard93)
    
* [**👾 Discord**](https://discord.com/users/407639833146818570)
    
* [**👔 LinkedIn**](https://www.linkedin.com/in/kyle-leonard93/)