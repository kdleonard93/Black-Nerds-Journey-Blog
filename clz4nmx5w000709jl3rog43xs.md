---
title: "Leo Ledger in All Its Pleasure"
seoTitle: "Leo Ledger in All Its Pleasure"
seoDescription: "Leo Ledger: The ultimate finance tracking app that simplifies budgeting, enhances financial awareness, and ensures secure, effortless money management"
datePublished: Sat Jul 27 2024 21:39:53 GMT+0000 (Coordinated Universal Time)
cuid: clz4nmx5w000709jl3rog43xs
slug: leo-ledger-in-all-its-pleasure
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1722116142297/c9b98772-7c80-4e8f-a4ef-bbd55d89b738.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1722116242521/feb5fab9-2053-425c-94fc-00cb7de50025.png
tags: app-development, python, django, web-development, testing, htmx

---

## Pulling Another Switcharoo

Yeah... it happened again. The tech stack I was planning to use for this project has yet again been altered. But this time, I'm sure most of you would agree that this change was for the better and I'll break down the reasoning and the result. But with that being said, I got a working web app that is live on Render!

###### If you wanna jump right into the code and skip over this post, pop over to the repo **\-&gt;**[https://github.com/kdleonard93/Leo\_Ledger](https://github.com/kdleonard93/Leo_Ledger) or check out the live site -&gt; [https://leo-ledger.onrender.com/](https://leo-ledger.onrender.com/)

To refresh everyone's memory, one of my main goals this year was to create a Finance Tracking app as I leveled up my Python knowledge. I've been fascinated with everything Svelte for frontend work and had recently finished a project that was a web app for film enthusiasts to save and categorize their favorite films, so I initially chose to use Svelte as my frontend for the finance tracker project.

The problem though was that I had issues trying to get this project live on Netlify. At the time, I didn't understand how to properly get both the frontend and backend running and served on Netlify until I found out that there was no easy way to do this. I would need to use an SSG and at the time I found some threads pointing to [Cactus](https://github.com/eudicots/Cactus?tab=readme-ov-file).

But over time, as I was *very* slowly diving into the repo for Cactus, I started to hear frequent and consecutive praise on Podcasts and YouTube channels I subscribe to about this new "alternative" to using a framework. And that's who I'm blaming for changing my stack for this project yet again 😆. I can no longer be liable for my impulses when these new shiny tools sound so good and then get put on a pedestal while it's hot by these devs I listen to lol. The library in question is HTMX and *I know*, that replacing a relatively new framework with an even ***newer*** library seems like a recipe for disaster, but it actually turned out to be a recipe for success.

I was convinced to give things a shot after seeing this video of this team getting rid of Next.js, Sveltekit, & Golang to use just HTMX & Golang. I'm thinking, "A library that removes the dependency on a frontend framework for smooth UX?? Isn't that a framework in itself 😅". I always thought of HTMX as a complement to traditional server-side frameworks by helping to handle the AJAX requests or that it was used for simple and smaller projects but, come to find out, people around the web LOVE using HTMX with Django as well. So considering that, in theory, this switch would reduce my development time for the finance app, I was sold.

## New Stack, New Plan

I ended up making a few changes altogether, not just on the frontend framework that I planned to use. What I came to realize was that I was overcomplicating my project, which led to a lot of frustration when I hit roadblocks early on. So my goal was to re-evaluate the need for some of these "bleeding-edge" tools and frameworks I wanted to use. I also couldn't find any examples out there in the world that used this stack for the type of app I was trying to make. This made kicking things off very difficult since I've never done a finance app of any kind. But this is why Phase One was `Conceptualization and Planning` 😂, shit changes. Let's dive into the new choices for my stack which will kick off with the change of DB choice.

### Too Many Roaches 🪳 Not Enough Solutions

The first choice was the most frustrating, only because I spent so much time looking into both of these two new awesome DBs, Fauna and Cockroach DB, and decided to go with Cockroach DB due to its strong Data consistency model. I was convinced that this was the choice to move forward with and was determined to learn about it while implementing it. Now, in a lot of cases, that usually works for me. I’ve said time and time again that repetition and getting my hands dirty is the best way for me to retain new info. But as I got into building out models and trying to test the connection with CockroachDB Cloud, it became clear that I was doing too much for this project. Even if I did plan to expand on this app, I could deal with the migration during that time. The setup is more complex to set up than SQLite + Postgres. The latter, I didn't even plan on using it until I read in Render's doc that for the PROD DB, I should use Postgres. There are a handful of benefits to making this move:

1. As I mentioned, this reduces the complexity of setting things up on the likes of Heroku or Render.
    
2. The cost of running separate services for the app and database could have increased cost due to using more resources than needed for the project.
    
3. While CockroachDB has a PostgreSQL-compatible layer and is designed to work well with Postgres, I was having issues with some Django ORM incompatibilities (or just a lack of knowledge on how to get the job done 😅).
    
4. Lastly, CockroachDB, like Fauna DB, has its own concepts and operations. So the learning curve was proving to be a bit steeper than I had expected.
    

With all that being said, I'm not completely pushing CDB (that's how I'm phrasing it now lol) to the side. I just decided that I might have made the wrong move there for this project, but we adjusted and things fell in line a lot better. I'm Using SQLite for my DEV environment and Postgres for my PROD.

### I *Svelte* Some `Type` of Way About My Frontend Choice

I still like Svelte over any other framework or JS libraries, including HTMX (so far at least) but the benefits I saw with using HTMX for this project over Svelte + Typescript were pretty clear. With me not knowing much of HTMX outside of what I heard and watched Podcasts and YouTube, I needed a bit of a helping hand to understand how this library worked. YouTube became my best friend for a couple of weeks 😄. There were benefits and drawbacks to this and I'll briefly highlight some below:

##### **SSR Simplicity:**

HTMX enables server-driven UI updates through HTML, which can reduce the need for JavaScript-heavy front-end frameworks.

**Reduced Client-Side Complexity:**

HTMX uses HTML attributes to manage client-server interactions, reducing the need for extensive JavaScript code on the client side. Makes the codebase easier to read.

**SEO and Initial Load Performance:**

With HTMX, most of the content is rendered on the server, which is more SEO-friendly because search engines can crawl the fully rendered HTML and provides faster initial load times compared to client-side rendering approaches. However, I doubt I'll be getting any wild traffic to this site anyway lol.

**Progressive Enhancement**:

HTMX supports a progressive enhancement approach, meaning your site can function without JavaScript if needed, enhancing accessibility and user experience.

**Ease of Integration with Django**:

HTMX can integrate seamlessly with Django templates and views and ease the pain of integration.

Working with HTMX has made this project easier after getting ahold of the concepts. Even though this project is bigger than my [Film Fan](https://github.com/kdleonard93/film-fan) app (Sveltkit + Django), I think it's still easier to digest by looking at the code. Having everything in one context instead of split between Frontend and Backend also helps a bit when it comes to deploying (even though I think I figured out how to also deploy that way after getting over road bumps with this deployment).

These were the only big changes I made. I was ***this*** close to using GoLang instead of Python and Django to complete my shit show of tech stack changes...JK JK. But in all seriousness, This felt good working through and there is a high chance that I will continue to use HTMX and Django for small-medium scale projects. Enough of the changes though, let's get into the project itself!

## Live and Ready For Scrutiny

Boom -&gt; [Leo Ledger Finance Tracker](https://leo-ledger.onrender.com/), the app in all its glory! It's very simple, in terms of design which I plan to overhaul over the next month or so. Everything works as intended; You can create an account, and test the app's functionality.

**Note: The site is hosted on Render's Free service so it might take a while to load since they spin down the DB during inactivity. But once it's loaded, it should be ⚡️fast.**

There are a few areas that were great learning lessons and instead of posting a bunch of code snippets, I'll focus on just the key areas and just link the file directly from GitHub.

### HTMXcellent

So HTXM is pretty dope when it comes to sending form submissions. Below is my create-transactions.html partial:

```xml
{% load widget_tweaks %}

<h1 class="mt-8 mb-4 prose prose-2xl text-white">
    Create Transaction
</h1>

<form hx-post="{% url 'create-transaction' %}">
    {% include 'tracker/partials/transaction-form.html' %}
    <button class="btn btn-success">
        Add
    </button>
    <button class="btn btn-error"
        hx-get="{% url 'transactions-list' %}"
        hx-target="#transaction-block"
        hx-push-url='/transactions'>
        Cancel
    </button>
</form>
```

* Reusable components, like `{% include 'tracker/partials/transaction-form.html'%}`, are also clear-cut and show that form fields are in a separate partial template, and I can ensure this within any other template or partial. I work with partials at my day job with PHP so the file structure was very familiar to me compared to how doing the same things in Svelte.
    
* URL [handling](https://htmx.org/docs/#triggers) using the `{% url`[`%}` templ](https://htmx.org/docs/#triggers)ate tag Generates URLs, ensuring that changes to URL patterns in Django's [urls.py](http://urls.py) file are automatically reflected in the template.
    
* The form uses HTMX attributes (`hx-post`, `hx-get`, `hx-target`, `hx-push-url`) to handle form submission and navigation without full page reloads. This gives the app a SPA like feel with minimal Javascript. Below I have pasted the section explaining AJAX request within the library:
    

#### **AJAX**

The core of HTMX is a set of attributes that allow you to issue AJAX requests directly from HTML:

| Attribute | Description |
| --- | --- |
| [hx-get](https://htmx.org/attributes/hx-get/) | Issues a `GET` request to the given URL |
| [hx-post](https://htmx.org/attributes/hx-post/) | Issues a `POST` request to the given URL |
| [hx](https://htmx.org/attributes/hx-put/)[\-put](https://htmx.org/attributes/hx-get/) | Issues a `PUT` request to the given URL |
| [hx-patch](https://htmx.org/attributes/hx-patch/) | Issues a `PATCH` request to the given URL |
| [hx-](https://htmx.org/attributes/hx-put/)[del](https://htmx.org/attributes/hx-delete/)[ete](https://htmx.org/attributes/hx-post/) | Issues a `DELETE` request to the given URL |

Each of these attributes takes a URL to issue an AJAX request to. The element will issue a request of the specified type to the given URL when the element is triggered:

```html
<button hx-put="/messages">
    Put To Messages
</button>
```

This tells the browser:

> When a user clicks on this button, issue a PUT request to the URL /messages and load the response into the button

Pretty damn straight forward right?!?! There is a lot of genius going on behind the scenes here for sure because HTXM uses Javascript to do its gymnastics to make it feel like magic. So it's not like we're making a whole web app without ANY Javascript.

The one issue I have is working with additional reactivity. I have this added function where I have the category filter selection highlighted when selected but after you submit the filters and they load, selecting a new filter works functionality-wise, but it doesn't highlight. Minor visual bug, but an annoying one. Other than that, Tailwind + Daisy UI makes it really easy to style up the project.

### Backend Bumppin'

There are only a few "new" areas I feel we need to touch on here since nothing changed from the planned language and framework. I touched on what I learned about Django in my last project post -&gt; [DUST Stack App](https://blacknerd.dev/whipping-up-a-film-catalogue-with-the-dust-stack). But I'll get into the new libraries and concepts I learned while building everything out.

**factory\_boy**, **django-allauth**, and **django-filters** are the three new libraries that were used heavily in this project. I'll keep it simple and go through the general description, use cases, and how I implemented them in my project.

#### **factory\_boy**

`factory_boy` is a fixtures replacement tool for Python, primarily used in testing. It allows devs to create simple to complex objects for tests with minimal code. It's greatly supported in Django and helps in generating test data that is both realistic and varied.

**Typical Uses**:

* Generating test data for unit tests.
    
* Creating instances of models with predefined or random attributes.
    
* Simplifying the setup of test environments by providing easy-to-use factories.
    

**Implementation in Leo\_Ledger**: In my project, `factory_boy` is used to create test instances of `User`, `Category`, and `Transaction` models. The factories defined ensure that tests run with realistic data without manually creating instances. Here’s an example of how the factories are implemented:

```python
from datetime import datetime
import factory 
from tracker.models import Category, Transaction, User

class UserFactory(factory.django.DjangoModelFactory):
    class Meta:
        model = User  # Equivalent to ``model = myapp.models.User``
        django_get_or_create = ('username',)

    first_name = factory.Faker('first_name')
    last_name = factory.Faker('last_name')
    username = factory.Sequence(lambda n: 'user%d' % n)

class CategoryFactory(factory.django.DjangoModelFactory):
    class Meta:
        model = Category
        django_get_or_create = ('name',)

    name = factory.Iterator(
        ['Bills', 'Housing', 'Salary', 'Food', 'Social']
    )

class TransactionFactory(factory.django.DjangoModelFactory):
    class Meta:
        model = Transaction

    user = factory.SubFactory(UserFactory)
    category = factory.SubFactory(CategoryFactory)
    amount = 5
    date = factory.Faker(
        'date_between',
        start_date=datetime(year=2022, month=1, day=1).date(),
        end_date=datetime.now().date()
    )
    type = factory.Iterator(
        [
            x[0] for x in Transaction.TRANSACTION_TYPE_CHOICES
        ]
    )
```

#### django-allauth

`django-allauth` is an integrated set of Django applications addressing authentication, registration, account management, and social account authentication from third parties. It is highly customizable and simplifies the process of handling user authentication and social account connections.

**Typical Uses**:

* User registration and login functionality.
    
* Social account authentication (EX: logging in with Google, Facebook, etc.).
    
* Managing user accounts and profiles.
    

**Project Implementation**: `django-allauth` is used to manage user authentication and social login. This allows users to register, log in, and connect their social accounts seamlessly. However, I don't have the social account connection implemented in my views at the moment so that can be ignored when testing this app out. The configuration typically involves adding `django-allauth` to the installed apps, updating the authentication backends, and configuring the URLs and settings.

##### settings.py

```python
INSTALLED_APPS = [
    "django.contrib.admin",
    "django.contrib.auth",
    "django.contrib.contenttypes",
    "django.contrib.sessions",
    'django.contrib.sites',
    "django.contrib.messages",
    "django.contrib.staticfiles",
    "django.contrib.humanize",
    
    # external apps
    "django_extensions",
    "debug_toolbar",
    "widget_tweaks",
    'allauth',
    'allauth.account',
    'allauth.socialaccount',
    'django_filters',
    'django_htmx',
    'template_partials',
        
    # project apps
    "tracker",
    
    
]

SITE_ID = 1

#Other settings#

# AllAuth settings
ACCOUNT_EMAIL_REQUIRED = False
ACCOUNT_USERNAME_REQUIRED = True
ACCOUNT_AUTHENTICATION_METHOD = 'username_email'
ACCOUNT_EMAIL_VERIFICATION = 'optional'
ACCOUNT_SIGNUP_PASSWORD_ENTER_TWICE = True

EMAIL_BACKEND = 'django.core.mail.backends.console.EmailBackend'

if not DEBUG:
    EMAIL_BACKEND = 'django.core.mail.backends.smtp.EmailBackend'
    EMAIL_HOST = os.getenv('EMAIL_HOST')
    EMAIL_PORT = int(os.getenv('EMAIL_PORT', 587))
    EMAIL_USE_TLS = True
    EMAIL_HOST_USER = os.getenv('EMAIL_HOST_USER')
    EMAIL_HOST_PASSWORD = os.getenv('EMAIL_HOST_PASSWORD')

LOGIN_URL = '/accounts/login/'
LOGIN_REDIRECT_URL = '/' 
LOGOUT_REDIRECT_URL = '/'

CSRF_COOKIE_SECURE = True
SESSION_COOKIE_SECURE = True

LOGGING = {
    'version': 1,
    'disable_existing_loggers': False,
    'handlers': {
        'console': {
            'class': 'logging.StreamHandler',
        },
    },
    'loggers': {
        'django': {
            'handlers': ['console'],
            'level': os.getenv('DJANGO_LOG_LEVEL', 'INFO'),
        },
        'allauth': {
            'handlers': ['console'],
            'level': 'DEBUG',
        },
    },
}
```

##### urls.py

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path("admin/", admin.site.urls),
    path('', include('tracker.urls')),
    path('__debug__/', include('debug_toolbar.urls')),
    path('accounts/', include('allauth.urls')),
]
```

##### django-filters

`django-filters` is a reusable Django application for allowing users to filter querysets dynamically. Works hand in hand with Django's ORM and is used to create slick and user-friendly filtering interfaces.

**Typical Uses**:

* Filtering data in Django views.
    
* Creating dynamic search interfaces.
    
* Providing advanced filtering options for querysets.
    

**Project Implementation**: `django-filters` is used to implement filtering functionality for transactions. This allows users to filter transactions based on various criteria such as date, category, and amount. Here’s an example of how filtering is set up:

##### filters.py

```python
import django_filters
from django import forms
from tracker.models import Transaction, Category


class TransactionFilter(django_filters.FilterSet):
    transaction_type = django_filters.ChoiceFilter(
        choices=Transaction.TRANSACTION_TYPE_CHOICES,
        field_name="type",
        lookup_expr="iexact",
        empty_label="Any",
    )

    start_date = django_filters.DateFilter(
        field_name="date",
        lookup_expr="gte",
        label="Date From",
        widget=forms.DateInput(attrs={"type": "date"}),
    )

    end_date = django_filters.DateFilter(
        field_name="date",
        lookup_expr="lte",
        label="Date To",
        widget=forms.DateInput(attrs={"type": "date"}),
    )

    category = django_filters.ModelMultipleChoiceFilter(
        queryset=Category.objects.all(),
        widget=forms.CheckboxSelectMultiple()
    )

    class Meta:
        model = Transaction
        fields = ("transaction_type", "start_date", "end_date", "category")
```

##### views.py (not the full file)

```python
from django.shortcuts import render, get_object_or_404
from django.contrib.auth.decorators import login_required
from django.views.decorators.http import require_http_methods
from django.core.paginator import Paginator
from django.conf import settings
from tracker.models import Transaction
from tracker.filters import TransactionFilter
from tracker.forms import TransactionForm
from django_htmx.http import retarget
import logging
logger = logging.getLogger(__name__)

# Create your views here.
def index(request):
    return render(request, 'tracker/index.html')


@login_required
def transactions_list(request):
    logger.debug(f"GET parameters: {request.GET}")
    transaction_filter = TransactionFilter(
        request.GET,
        queryset=Transaction.objects.filter(user=request.user).select_related('category')
    )
    logger.debug(f"Filter created: {transaction_filter}")
    logger.debug(f"Filter form: {transaction_filter.form}")
    paginator = Paginator(transaction_filter.qs, settings.PAGE_SIZE)
    transaction_page = paginator.page(1) #default to page 1
    total_income = transaction_filter.qs.get_total_income()
    total_expenses = transaction_filter.qs.get_total_expenses()
    context = {
        'transactions': transaction_page,
        'filter': transaction_filter,
        'total_income': total_income,
        'total_expenses': total_expenses,
        'net_income': total_income - total_expenses
    }

    if request.htmx:
        return render(request, 'tracker/partials/transactions-container.html', context)

    return render(request, 'tracker/transactions-list.html', context)
```

There were a few more things that were new and implemented and new like the managers.py and forms.py files but both are pretty simple, short, and self-explanatory if you peep the code. If you've hung around until this point, 🫡 . I know I can ramble and there is no link to the live site yet, but fear not, it'll reveal itself in the next section about how I deployed and the roadblocks I hit along the way.

### 🛳️ ALL DEPLOYYYY!!!!! W/ Render

As I mentioned previously, had issues trying to deploy my Film Fan project and I assumed it was an issue with me not knowing how to do it properly but after a bit more research, I learned that Netlify is NOT the ideal host for an app where you are managing the server and database. So that led me to render when I started this project and I now believe I can make my custom build scripts to run front-end and back-end and setup the PROD DB just like I have with this project. So there is a chance I start working on that again after having some fun re-doing the design for Leo Ledger. But let's dive into how I needed to create new scripts and update my settings.py file to get things deployed with Render.

#### Multitude of Failed Attempts For The 1st Deploy

If you have any sort of Git GUI, all you need to do is take a look at the plethora of commits on `master` when I was trying to get this deployed for the 1st time ([Screenshot](https://www.loom.com/i/dc0612b7c12643b696e84161c7236f03)). I was ready to buy some HIMs Hair Growth Snake Oil and grow a few more strings of hair just to pull them out again. After asking real and artificial intelligence a bunch of questions, I finally figured out that I needed a few adjustments to my settings file, how I was serving up my static files, and (as mentioned earlier) learned that Postgres will be needed for the production database setup. Render's doc only explains how to switch it from what you have, not add it as an additional rule. So this was quite the hurdle with adjusting how I was serving my DBs. But all was figured out and here are the main takeaways:

* **Setting up Postgres as a PROD-only DB:** Resolving this took some time but once I figured it out, it was a GREAT weight off my shoulders and It also set up a great example for me to go back to my last project to get that one deployed too.
    

```python
if os.getenv('RENDER'):
    DATABASE_URL = os.getenv('DATABASE_URL')
    print("Database URL:", DATABASE_URL) 
    if DATABASE_URL:
        DATABASES = {
            'default': dj_database_url.parse(DATABASE_URL, conn_max_age=600)
        }
    else:
        raise ValueError("DATABASE_URL environment variable not set")
else:
    DATABASES = {
        "default": {
            "ENGINE": "django.db.backends.sqlite3",
            "NAME": BASE_DIR / "db.sqlite3",
        }
    }
```

Here ^ you can see that I needed to wrap my DB logic in an if/else statement and pass the `Render` argument for PROD databases. The Variables are set on my RENDER dashboard so I don't have to worry about adding them to a `.env` file.

* **Whitenoise for static file generation:** I was having issues with my views on PROD even though I saw them on DEV and I was running in circles for a bit because I thought it was related to me switching up my DB on PROD. So I went down a rabbit hole until I finally got some clear direction to use Whitenoise. No code really to add here other than showing that just made a rule that if the app is not in DEBUG, then it uses whitenoise for static file storage:
    

```python
# Static files (CSS, JavaScript, Images)
# https://docs.djangoproject.com/en/4.2/howto/static-files/

STATIC_URL = '/static/'
STATICFILES_DIRS = [os.path.join(BASE_DIR, 'static')]
STATIC_ROOT = os.path.join(BASE_DIR, 'staticfiles')

if not DEBUG:
    # Enable WhiteNoise for production
    STATICFILES_STORAGE = 'whitenoise.storage.CompressedManifestStaticFilesStorage'
```

* **render.yaml, build.sh and start.sh files:** For render, create and configure a render.yaml file so it knows how to ingest my app and boot it up. Below is the file:
    
    ```yaml
    databases:
      - name: ledgerdb
        plan: free
        databaseName: ledgerdb
        user: admin
    
    services:
      - type: web
        plan: free
        name: Leo_Ledger
        runtime: python
        buildCommand: "./build.sh"
        startCommand: "./start.sh"
        envVars:
          - key: DATABASE_URL
            fromDatabase:
              name: ledgerdb
              property: connectionString
          - key: SECRET_KEY
            generateValue: true
          - key: WEB_CONCURRENCY
            value: 4
    ```
    
    I want to focus on the `buildCommand` and `startCommand`. I could, in theory, put both commands here, but it's good to separate the logic into their own files.
    
    **build.sh**
    
    ```bash
    #!/usr/bin/env bash
    # Exit on error
    set -o errexit
    
    # Modify this line as needed for your package manager (pip, poetry, etc.)
    pip install -r requirements.txt
    
    # Convert static asset files
    python manage.py collectstatic --no-input
    
    # Apply any outstanding database migrations
    python manage.py migrate
    
    # Custom management command to create categories
    python manage.py create_categories
    ```
    
    **start.sh**
    
    ```bash
    #!/usr/bin/env bash
    
    # Exit on error
    set -o errexit
    
    # Start Gunicorn with Uvicorn workers
    exec gunicorn finance_project.asgi:application \
        --bind 0.0.0.0:$PORT \
        --workers 4 \
        --worker-class uvicorn.workers.UvicornWorker \
        --log-file -
    ```
    
    In my build script, I have all of my commands that will get the proper packages, static files, any new database migrations, and the initial set of categories.
    
    In my start.sh file, you just see the simple command of starting Gunicorn with Uvicorn workers. Here is where I learned that, if needed, I can build off both of these scripts to include bootstrapping and running both the frontend & backend folders of the project, resolving the issues I was having deploying my film fan app.
    

Let me tell you, the moment these wrinkles were ironed out and the live site was functioning as intended, you would think I was a dancer from the "Not Like Us" video on how I celebrated that W.

![Dance Dancing GIF by Kendrick Lamar](https://media3.giphy.com/media/v1.Y2lkPTc5MGI3NjExb2Z4OHZ0eno4amRpenB5cHZodGVmNWEwaHkwZThwbG8zYnllbmZqMyZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/y8H1JFILjW6LpGn9F7/giphy.gif align="center")

## Conclusion

Through everything, from the initial plan being flipped upside down, upside up, and spun around, to the learning hurdles with the new libraries and tools used, came a pretty dope project and for me, an even better accomplishment. I feel like I ended up wrapping up the foundation of this project ahead of my schedule and that will allow me to calmly improve it, not being rushed by my own deadlines.

In other news, I ended up enrolling in Corsera's [IBM Back-End Development Professional Cert](https://www.coursera.org/professional-certificates/ibm-backend-development?) not too long ago and that has helped me navigate this project a bit better as I was learning new concepts. Within this course, are focuses on Docker & Kubernetes and since my job has been going through a big migration over to containerization, I decided to do the entire course cert instead of enrolling in the individual Docker and Kubernetes courses/modules.

I've also been talking to a new connection and will be doing a portfolio project for them as soon as we plan a bit further and I get the assets I need. Appreciate everyone that read through this and whoever gave the project a fork, thanks for your interest. Feel free to make any suggestions or point out any bugs you see on the live site -&gt; [Leo Ledger](https://leo-ledger.onrender.com/).

#### **If you want to keep up with my work or want to connect as peers, check out my social links below and give me a follow!**

* [**𝕏 Twitter**](https://x.com/kdleo93)
    
* [**💻 Github**](https://github.com/kdleonard93)
    
* [**👾 Discord**](https://discord.com/users/407639833146818570)
    
* [**👔 LinkedIn**](https://www.linkedin.com/in/kyle-leonard93/)