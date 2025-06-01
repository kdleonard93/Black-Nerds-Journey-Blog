---
title: "Creatures of Habit: Devlog Chronicles - Part 2"
seoTitle: "Creatures of Habit: Devlog Chronicles - Part 2"
seoDescription: "Embracing TDD, Elevating the UX & Developing CI Workflow Systems"
datePublished: Wed May 28 2025 02:58:08 GMT+0000 (Coordinated Universal Time)
cuid: cmb7cv5y2000209juhoo3a7cx
slug: creatures-of-habit-devlog-chronicles-part-2
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1748635382254/a7ab8ed8-198f-42c4-ba1f-2c2c5c327084.png
tags: tdd, javascript, ux, web-development, typescript, svelte, ci-cd

---

## **Refining the Foundation and Gearing Up +1**

As you can see from the new terrain in this cover image vs the last article's, we've made it out of the "Wacced out Woods" and have arrived at "Finessin' Fields". Time to gear up ✊🏾.

Over the last couple of months, I've been working on improving the quality of the code and my testing implementation. I also needed to get a workflow set for automation since this is turning into a pretty big codebase. I never knew how much would need to go into an app like this…..or this is just a lesson on choosing a more fitting tech stack next time lol.

![](https://media0.giphy.com/media/v1.Y2lkPTc5MGI3NjExNTlqdWN0YjR1d3BsN3l4cm5kanJ2NnV6NGs0bnlhYTFuMHZobDFnbyZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/ogb8RQdu8zQyc/giphy.gif align="center")

For this write up I’ll go over the following:

* ### 🧪 Testing & Quality:
    
    **\- Test Driven Development (TDD) Implementation- Component Testing Templates- TypeScript Import Fixes**
    
* ### 📊 User Experience:
    
    **\- Responsive Dashboard with Daily Habit Overview- Visual Progress Bars for Habit Completion- Quick-Complete Functionality from Dashboard**
    
* ### 🔄 Developer Workflow:
    
    **\- Biome for Code Quality (Replacing ESLint)- CI Workflow with TypeScript & Style Checks- Pre-commit & Pre-push Hooks**
    

As always, you can check out the code on the repo here → [https://github.com/kdleonard93/creatures-of-habit](https://github.com/kdleonard93/creatures-of-habit). Let's dive into the details **Testing & Quality Assurance**

One of the biggest shifts in my development approach has been embracing Test Driven Development (TDD). Word on the street is that for the type of app im making, which will be extremely component heavy, benefits from this type of approach to avoid unforeseen troubles down the line when I have actual users….which will be friends, family, and whoever is bored enough to sign up 😏 so maybe i could have stuck with my OG approach. I digress, the point is implementing this way for testing required me to yet again, learn something new and say goodby to some other knowledge i recently gained for a totally diff project or for the job that actually feeds me.

### Test Driven Development Implementation

So here I am, embracing the TDD workflow: write tests first, implement the minimum code to make them pass, then refactor while keeping tests green. This approach has already caught several bugs before they made snuck their way into a future production build and has forced me to think more clearly about component interfaces and responsibilities.

The TDD cycle looks a little something like this:

1. Write a test that defines how the code should work
    
2. Run the test (it should fail)
    
3. Write the minimum code to make the test pass
    
4. Run the test again (it should pass)
    
5. Refactor the code while keeping tests passing
    
6. Repeat for additional features or edge cases
    

Here's a real example from my implementation of the `DailyProgressSummary` component:

```typescript
// First, I wrote the test
it('calculates completion percentage correctly', () => {
  const habits = [
    { id: '1', completedToday: true },
    { id: '2', completedToday: false },
    { id: '3', completedToday: true }
  ];
  
  const { getByText } = render(DailyProgressSummary, { props: { habits } });
  expect(getByText('67%')).toBeInTheDocument();
  expect(getByText('(2/3)')).toBeInTheDocument();
});
```

Then I implemented the component with just enough code to make the test pass:

```svelte
<script lang="ts">
  export let habits: { id: string, completedToday: boolean }[] = [];
  
  $: totalHabits = habits.length;
  $: completedHabits = habits.filter(h => h.completedToday).length;
  $: completionPercentage = totalHabits > 0 
    ? Math.round((completedHabits / totalHabits) * 100) 
    : 0;
</script>

<div class="bg-card p-3 rounded-lg border shadow-sm flex flex-col items-center">
  <p class="text-sm font-medium mb-1">Today's Progress</p>
  <div class="flex items-center gap-2">
    <div class="text-2xl font-bold">{completionPercentage}%</div>
    <div class="text-muted-foreground text-sm">({completedHabits}/{totalHabits})</div>
  </div>
</div>
```

### **Component Testing Templates**

To standardize my testing approach, I created reusable testing templates for different types of components:

* **UIComponentTest**: For Svelte UI components
    
* **APIEndpointTest**: For API endpoints and server routes
    
* **UtilityTest**: For utility functions and helpers
    

These templates include best practices, common test patterns, and examples that make it much easier to write consistent, high-quality tests. No more staring at a blank file wondering how to structure a test!

### **TypeScript Fun & Import Fixes**

I ran into an annoying issue with TypeScript not recognizing Svelte component imports in test files. Here’s the error:

```bash
Cannot find module '$lib/components/habits/HabitForm.svelte' or its corresponding type declarations
```

Initially, I used the `@ts-ignore` hack to bypass the issue, but I knew that wasn't sustainable. After some research, I implemented a proper solution by creating type declarations for Svelte components in my test environment. This ensures TypeScript understands the imports and provides proper type checking. The `svelte.d.ts` is below for a quick reference:

```typescript
// General declaration for all Svelte files
declare module '*.svelte' {
  import type { ComponentType } from 'svelte';
  const component: ComponentType<any>;
  export default component;
}

// Specific declaration for the component causing the error
declare module '$lib/components/dashboard/DailyProgressSummary.svelte' {
  import type { ComponentType } from 'svelte';
  const component: ComponentType<any>;
  export default component;
}

// Add other specific component paths as needed
declare module '$lib/components/habits/HabitForm.svelte' {
  import type { ComponentType } from 'svelte';
  const component: ComponentType<any>;
  export default component;
}

// Server module declarations
declare module '$lib/server/streaks/calculations' {
  export interface StreakStatus {
    streakMaintained: boolean;
    daysInStreak: number;
    streakWeeks?: number;
  }
  
  export interface StreakUpdateResult {
    currentStreak: number;
    longestStreak: number;
    lastCompletedAt: string;
  }
  
  export function determineStreakStatus(
    habitData: { id: string; userId: string; frequencyId: string },
    currentDate: Date
  ): Promise<StreakStatus>;
  
  export function updateStreakAfterCompletion(
    habitId: string,
    userId: string
  ): Promise<StreakUpdateResult>;
}

declare module '$lib/server/db' {
  type MockFunction<T = any> = T & {
    mockReturnThis: () => MockFunction<T>;
    mockImplementation: (fn: (...args: any[]) => any) => MockFunction<T>;
    mockImplementationOnce: (fn: (...args: any[]) => any) => MockFunction<T>;
    mockReturnValue: (value: any) => MockFunction<T>;
  };

  type MockDB = {
    select: MockFunction<() => MockDB>;
    from: MockFunction<(table: any) => MockDB>;
    where: MockFunction<(condition: any) => MockDB>;
    orderBy: MockFunction<(field: any) => MockDB>;
    limit: MockFunction<(num: number) => MockDB>;
    update: MockFunction<(table: any) => MockDB>;
    set: MockFunction<(data: any) => MockDB>;
    execute: MockFunction<() => any[]>;
  };

  export const db: MockDB;
}
```

I think there is an update being proposed that should make the components accessible from server files, making imports in test files much simpler.

## **📊 User Experience Enhancements**

### **Responsive Dashboard with Daily Habit Overview**

The dashboard has been completely revamped to provide users with a clear overview of their daily progress. The centerpiece is the new component that shows:

* Overall completion percentage for the day
    
* Visual progress bar showing completion status
    
* Fraction of completed habits (e.g., "2/5")
    

This gives users immediate feedback on how they're doing for the day, creating that dopamine hit when they see their progress increase.

But here’s the kicker…..it doesn’t actually work as expected 😂. And that pointed out a major issue in the component tests that I’ve created thus far, which is that they work fine when using mock data but when trying to use the actual data stored in my db, I get a bunch of new errors that I haven’t been able to figure out. For now though, the mock data will be just fine and this is just gonna have to be one of the areas I come back to in the future.

### **Visual Progress Bars for Habit Completion**

Every habit now has its own progress visualization that clearly shows completion status at a glance. The dashboard implementation provides immediate visual feedback on habit tracking progress.

The progress bars are complemented by a color-coding system based on the habit's difficulty:

* Easy habits: Green
    
* Medium habits: Yellow
    
* Hard habits: Red
    

This intuitive color scheme helps users quickly identify the difficulty level of each habit, making it easier to prioritize and manage their daily tasks. The visual indicators add both functionality and a splash of color to the interface, enhancing both usability and visual appeal.

**Quick-Complete Functionality from Dashboard**

Users can now complete habits directly from the dashboard with a single click, eliminating the need to navigate to individual habit pages. This seemingly small change has dramatically improved the user experience - it's all about reducing friction for those daily habit completions

The quick-complete buttons use the existing success variant in the Button component, maintaining visual and logical consistency.

## **🔄 Developer Workflow Improvements**

### **Biome for Code Quality**

I've switched from ESLint to Biome for code quality checks. Biome is faster, more integrated, and provides both linting and formatting in a single tool. The configuration is simpler, and it plays nicely with the rest of my toolchain. I also can’t help myself when I see newer tools get a bunch of praise.

Setting up Biome was straightforward:

```json
// package.json scripts
"format": "biome format --write .",
"format:check": "biome check",
"lint": "biome lint .",
"lint:fix": "biome lint . --apply"
```

### **CI Workflow with TypeScript & Style Checks**

The continuous integration workflow now includes:

1. TypeScript type checking
    
2. Biome code style checks
    
3. Automated testing
    
4. Build verification
    

So now I have a pretty [decent set of tests](https://www.loom.com/i/fa6e8b856df047549c8aa88fa1662a0f) that need to pass before the PR is merged into `master`. The CI workflow runs on GitHub Actions and prevents merging code that doesn't meet the quality standards.

### **Pre-commit & Pre-push Hooks**

To catch issues before they even reach the repository, I've set up pre-commit hooks that run:

* TypeScript type checking
    
* Biome style checks
    
* All of the tests I have set up
    

And a pre-push hook that ensures the project builds successfully before pushing code.

This multi-layered approach to quality assurance has already prevented several bugs from entering the codebase and has made the development process more robust. I’ve gained most of my CI knowledge from the work being done at my current company, and it’s been extremely helpful in catching errors as I continue developing the app.

## **Quick Peek of What’s Ahead**

While I've made significant progress on the engineering practices and user experience, there's still plenty on the roadmap:

1. **Complete the XP System**: Implement experience points for character progression and refine creature creation statistics.
    
2. **Enhance Dashboard Visualizations**: Add streak tracking and long-term progress visualizations, plus fix habit completion data accuracy.
    
3. **Offline Support Research**: Investigate offline capabilities for potential mobile app development.
    

With our improved development practices in place, we're well-positioned to implement new features efficiently and maintain high quality standards….well that’s he hope at least 😉. Stay tuned for what's next on deck 🤘🏾.

#### **If you want to keep up with my work or want to connect as peers, check out my social links below and give me a follow!**

* [**🦋 Bluesky**](https://bsky.app/profile/digitaldopamine.dev)
    
* [**💻 Github**](https://github.com/kdleonard93)
    
* [**👾 Discord**](https://discord.com/users/407639833146818570)
    
* [**👔 LinkedIn**](https://www.linkedin.com/in/kyle-leonard93/)