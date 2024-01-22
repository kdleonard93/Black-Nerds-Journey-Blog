---
title: "Whipping Up a Film Catalogue With the DUST Stack"
seoTitle: "Whipping Up a Film Catalogue With the DUST Stack"
seoDescription: "Dive into the DUST stack, combining Django, UI Library, Svelte, and TypeScript for an innovative web development project."
datePublished: Mon Jan 22 2024 00:10:55 GMT+0000 (Coordinated Universal Time)
cuid: clro690gz000008lceapx4f9i
slug: whipping-up-a-film-catalogue-with-the-dust-stack
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1705881768686/c2bce49d-e3e4-459f-93d5-a2c387d0606e.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1705881933697/df966bc1-055b-48d2-ad16-38a6c8007fb9.png
tags: app-development, django, web-development, typescript, svelte, movies, sveltekit

---

## Project Intro

Flashing back to my previous post, I mentioned I was working on a "Movie List" project using Django, Svelte, and TypeScript. Typescript was an addition to this project as I've been wanting to learn it for some time now to have better type safety in my projects helping me catch errors early in my text editor instead of in the browser. I feel it also encourages better coding practices in general, so I wanted to embrace and use it moving forward instead of just using JS. I'd like to coin the **DUST** **stack** (**D**anjgo **U**I **S**velte **T**ypescript) for the project. I know, super cool right?😏? I was also thinking of other stack names like CESN (pronounced season) which would be **C**ockroachDB, **E**xpress, **S**velte, and **N**ode but let's not go down a tech-stack acronym rabbit hole lol.

The project, at first glance, appears straightforward but is quite intricate under the hood. My primary learning curve was working with Django for the first time. Although I've done some setup work with Django and Flask before, this is my first complete project with a functioning database. Django's handling of the heavy lifting, like WSGI and ORM setup, allowed me to focus more on the documentation, styling, and additional functionalities.

## Frontend Finesse

Svelte is increasingly becoming my preferred frontend framework. It's much easier for me to grasp core concepts in Svelte compared to React. Having recently used Vue at work, I'd rank my framework preferences as Svelte, Vue, Qwik, and then React. I've never used Qwik, but that's a testament to my aversion to React (big feels 😤). But enough of my rambling, let us get into what I used in full and what I learned along the way.

### SkeletonUI

I initiated the project using [Sveltekit](https://kit.svelte.dev/) and [Skeleton](https://www.skeleton.dev/) as the UI library. Skeleton, being tightly integrated with Svelte, is like a component library for Tailwind CSS but specifically tailored for Svelte and Sveltekit. It includes components, stores, and actions. The theme generator on their site is a standout feature, allowing users to experiment with pre-designed themes or create their own. This is especially helpful for those, like myself, who aren't inherently skilled in design. I experimented with several themes before settling on a pre-designed one to adhere to best color practice standards.  
Unlike my recent [Dev Portfolio](https://digitaldopamine.dev/) update, which was just working with basic Svelte components, I dove deeper into Sveltekit's core concepts such as Filesystem-Based Routing, Loading Data, and Form Actions.

### Routing

This routing system is CLUTCH for readability and file structure. Each route of the app, let's say for example: `src/routes/about`, is the actual page URL and in this instance, the URL would be `http://localhost:5173/about`. Now within the project directory, the `/about/` route is a folder that would contain the actual svelte files for the page.

### +page

For a quick definition: A `+page.svelte` component defines a page of your app. By default, pages are rendered both on the server ([SSR](https://kit.svelte.dev/docs/glossary#ssr)) for the initial request and in the browser ([CSR](https://kit.svelte.dev/docs/glossary#csr)) for subsequent navigation. According to the docs, often times a +page.js/ts will be added in the same folder to load actual data for the page to render.

### Loading Data

The docs explained this very clearly so I'll just echo what they said for the most part. A `+page.svelte` file can have a sibling `+page.js` that exports a `load` function, the return value of which is available to the page via the `data` prop. For example in my case, below I've added what my load function looks is:

```typescript
export function load({ params }) {
  return {
    id: params.id,
  };
}
```

Essentially, this function is designed to run when a specific film's route is accessed. The `{params}` object is passed to the function as an argument containing the route parameters. `params.id` refers to the unique identifier of a film and the purpose of the `load` function is to extract the `id` from the route parameters and return it. The `id` is then used to load or fetch the specific film data from your Django or whatever backend/data source you use. By doing this, the application can dynamically display the details of the film that corresponds to the unique `id` in the URL. This is pretty much the butter to the bread which we call `+page.svelte`.

### TypeScript Tortur......I Mean *Fun* 🙃

\*MR. PBH voice\* Oooooooweeeee, this one was a doozie! I haven't touched or even looked at the docs of Typescript before adding it to this project but sometime late last year, there was a podcast I was listening to talking about how it'll change the way you code and look at JS forever once you dive in and work with it in a couple of projects. I was never a rockstar at JS in the first place so at first, I was telling myself I needed to get better at JS before getting into TS but then I thought.....why wait 😂. Let me tell you the struggle was real but well worth it. There are a handful of things I would have missed or didn't realize would have caused issues during runtime. The things that I got the most errors for were related to naming my variables and how data was passed in functions. There was a need to explicitly provide a data type or give it a type of `any`, but you'd do good to try and avoid using `any` since that's a cop-out that can bite you in the ass down the road with a bigger project as it grows. For example, I needed to define variables related to the data keys in my model so that my movie cards populate and update properly. In JS you'd just create a `let` or `const` like so:

```javascript
  let name;
  let director;
  let release_year;
  let description;
  let imageFile;
  let film;
  let id;
```

Seems pretty simple right? But a lot of things can go wrong with this data. In my case, with the Django model only accepting certain data types for each input field when receiving and retrieving the data, it's important to make sure that my logic is solid when it submits that data during runtime. The Typescript way of defining these variables is:

```typescript
  let name: string = "";
  let director: string = "";
  let release_year: string = "";
  let description: string = "";
  let imageFile: File | null = null;
  let film: Film | null = null;
  let id: number;
```

Here you can see the need to explicitly classify these variables as they are. There are a few caveats with each value, like strings needing to be set to an empty or default value. But when it comes to handling images, "Typescript got hands" is how I would describe how it kicked my ass trying to figure out how the hell I needed to work with the `imageFile` variable. But through some digging and questions, I was led to the docs for the [File Interface](https://developer.mozilla.org/en-US/docs/Web/API/File). I'm not going to go into specifics on that particular interface but I will elaborate on what I learned about Typescript interfaces in general.

#### Interfaces

TypeScript's main thing is that it checks types based on the shape of values. This approach is often referred to as “duck typing” or “structural subtyping”. In TypeScript, interfaces are key. They're used to name these types and are an effective tool for defining agreements within your code and also with code that's outside of your project.  
I only needed to create one interface for Films and you can see how the `film-store.ts` file was structured with my Film interface here:

```typescript
import { writable } from "svelte/store";

export interface Film {
  id: number;
  name: string;
  director: string;
  description: string;
  release_year: number | null;
  image: string;
}

export const FilmStore = writable<Film[]>([]);
```

This code sets up a Svelte store to manage a list of films in my application. As you might see in my repo, I am now able to access/subscribe to `FilmStore` in other parts of the application, super useful and power-charged with TS. Other parts of the frontend aren't new concepts to me so we won't dive into every little thing I did before I started working on my backend branch.

## Build-A-Backend

This is the first project in which I used Django. I decided to stick with learning and working with Django over Flask because I found their documentation to be much more organized and maintained. Django is also a better fit when it comes to working with Postgres or any SQL database. I can still do it with Flask, but there would have been much more setup needed and additional libraries, like `Gunicorn` for the WSGI Server, `Alembic` for database migrations, and `SQLAlchemy` for ORM just to name a few. There is a bunch more to add for a full-fledged app and not having to worry about that each time is a time saver. One downside though, is that some projects (including this one) don't use all that Django offers. That's just a small inconvenience though as I would have had a way larger inconvenience working with Flask down the line with my main project since it's not easy to use CockroachDB with Flask. The main reason is because of Django's built-in ORM, which can handle the nuances of the database like connection management, transactions, and data integrity. Cockroach Labs only has documentation for Django as well so that swayed me as well.  
I'll do a project with Flask at some point this year but right now, I'm leaning on the tools with better learning resources. With that being said, let's get into the backend of my project

### Django ⛓️ Unchained

Working with Django started pretty slow. There's a lot to understand about how things work with the framework but after the basic setup was complete, building out the needed models and views was easy enough to code up. I'll admit that I will still need to go over docs the next few times when starting up my backend since I'm still trying to wrap my head around some of the concepts. The core concepts I'd note for Django that stuck with me would be MTV (Model-Template-View) Architecture, ORM (Object-Relational Mapper), Admin Interface, and Migrations.

**MTV (Model-Template-View) Architecture**

**Model:** Represents the data structure and manages the business logic of the application. It is responsible for retrieving and storing data, as well as performing any necessary data processing.

**Template**: Defines how the data is presented to the user. It is responsible for rendering the HTML and displaying the data from the Model.

**View:** Acts as a bridge between the Model and Template. It receives user input from the Template, processes it, and updates the Model accordingly. The View also retrieves data from the Model and passes it to the Template for rendering.

**ORM (Object-Relational Mapper)**

I've spoken about the ORM before but just to hammer it in, Django’s ORM allows me to interact with the database using Python code instead of SQL. That's about the simplest definition I can provide.

**Admin Interface**

The admin interface was my favorite aspect of working with Django and i read into libraries that can accomplish this with Flask as well. But having an admin panel in general is a great tool for working with the DB and being able to create a SuperUser and account with just a few commands makes the admin setup as smooth as Prince-permed hair.

**Migrations**

I didn't work with migration other than migrating my initial model setup. Any changes to your models and views would require you to make another migration but again, very straightforward scripts that have already been set up in the framework made the updates easy.

I'd say I spent more time on the front end than I did on the backend setup so there isn't much to talk about other than creating the models.

#### Film Model

Creating the Film model required fields like Name, Release Year, Description, Director, and Image. I used SQLite over CockroachDb for this one for its simplicity and compatibility with Django's default settings. The Film model in Django is intuitive and ensures clean data inputs:

```python
from django.db import models
from django.core.validators import MinValueValidator, MaxValueValidator
from datetime import datetime


class Film(models.Model):
    name = models.CharField(max_length=128)
    release_year = models.IntegerField(validators=[
        MinValueValidator(1900),
        MaxValueValidator(datetime.now().year)
    ],
        default=datetime.now().year
    )
    description = models.TextField(max_length=356)
    director = models.CharField(max_length=128)
    image = models.ImageField(upload_to='images/')

    def __str__(self):
        return self.name
```

As you can see here, I have my imports so I can utilize Django's model class. A new Film class is created and it inherits from `models.Model`, making it a Django model, so it's tied to a database table. Within this Film class, you see all of my model keys mentioned earlier with constraints tied to them for cleaner data inputs. I want to highlight my image key and note that for the images to be stored, I created a media and image folder (`/media/images/`), and directed the image uploads to be managed there. One thing I didn't get added was the removal of those images from the folder when a film is deleted. What happens now is, that the data is removed from the DB and the state + store is reset/removed from the front end, but the actual image file lingers in the repo so this can cause a major issue with a bigger app that takes in a bunch of create and delete requests a day. But I'll be my only enemy here so that's a feature I was going to try and add to this project for improvement.

## Complete But Room For Improvement

With all that said, the project is complete and works. You can run both the front end and back end of the site to start. The homepage is just a title and this is 1 section that I plan to improve by just adding some basic designs and content about the project. To run the project, you would need to open up 2 terminal tabs, 1 for the front end and 1 for the back end. You can check out the [README](https://github.com/kdleonard93/film-fan) on the git repo for a detailed doc on how to get started but below is a video of me booting up both the front-end and back-end + navigating through the app a bit:

%[https://www.loom.com/share/06b92e88eda6474f8028743cd23d7623] 

## Conclusion

That wraps up my project! Folks should expect more features to come to this project like Tagging/Sorting, Authentication, and Deployment, but I knocked out the deliverable for my 1st Svelte + Django project and everyone is welcome to test it out and and tell me everything I did wrong or can do better 😄.  
My next goal is to choose one of 2 tasks:

**A)** Work on a project that involves CockroachDB. Most likely a workshop they have on their "University" site [https://university.cockroachlabs.com/](https://university.cockroachlabs.com/).

**B)** Build a stock analysis app with Svletekit to get more practice with consuming third-party APIs and working with Svelte store and local storage.

I'm leaning towards **B** since I do need more work with APIs but I also want to get through a small project using Cockroach to get my feet wet there. I'll make my decision and provide an update in my next post, which will be "Day 26 of 100-Days-of-Python-Code". I think I'm pretty on pace with the phases I made for myself. My Goal for the full-fledged Personal Finance Tracker app was to have it complete within a year, which is double the total time of the phases (6 months) since I'm not doing this full time and like to enjoy the other things in life as well. But here is the Repo for the project -&gt; [https://github.com/kdleonard93/film-fan](https://github.com/kdleonard93/film-fan) so check it out!

#### **If you want to keep up with my writing or want to connect as peers, check out my social links below and give me a follow!**

* [**𝕏 Twitter**](https://twitter.com/RingoMandingo93)
    
* [**💻 Github**](https://github.com/kdleonard93)
    
* [**👾 Discord**](https://discord.com/users/407639833146818570)
    
* [**👔 LinkedIn**](https://www.linkedin.com/in/kyle-leonard93/)