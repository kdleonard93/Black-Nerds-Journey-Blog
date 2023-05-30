---
title: "Day 18 - The Hirst Project, GitHub Workflows, and Package Management Woes"
seoTitle: "Python Package Troubleshooting & Hirst Painting | BlackNerd's Journey"
seoDescription: "Join BlackNerd on Day 18 as he resolves Python package issues, creates a Hirst mockup, and improves his GitHub workflow."
datePublished: Tue May 30 2023 19:44:18 GMT+0000 (Coordinated Universal Time)
cuid: cliaot3t7000i09kxd1aq5luy
slug: day-18-the-hirst-project-github-workflows-and-package-management-woes
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1685475231574/cc70d025-addf-4d3d-9a22-dd10e3a2fba4.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1685475248243/ef9961cd-e932-409f-8cf7-7687d07b3aae.png
tags: python, coding, 100daysofcode, githubworkflow

---

## Today's Objective

Today, I finished the second part of this module, which involved creating a mock Hirst painting. The project was fairly challenging but not mind-boggling; however, I encountered a few obstacles along the way. This article primarily discusses the issues I faced, serving as a reference for myself or anyone else who may encounter similar problems in the future.

## Package Management Madness

So, starting the project was a pain since I had a lot of conflicting issues with the package managers I had installed on my local machine. This probably won't apply to most people using Python, but after exploring and trying out a bunch of different tools while getting into Python itself, I had a bunch of different managers (pipenv, conda, and miniconda) installed on my local machine. Within these package managers, I had various libraries installed, and when trying to access certain modules in my project, I kept getting "module not found" (specifically for colorgram.py). I would try to reinstall, and it would say it's already installed. Just to provide context, this is how my list of environments looked:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685473152490/c1c2d871-672d-4bed-a39e-94b4477dee1e.png align="center")

Yeah... it's a mess 😅.  
Once I figured out my needed configurations and removed Anaconda completely (more on that later). I was able to get my modules working fine.

## The Project

As mentioned in the intro, the project was to create a mock Hirst Painting. The fact that this man sold a painting that [looked like this](https://loom.com/i/a2e0869889f44be08422ec59114a78ca) for over a million dollars is beyond me, but maybe I don't "get it" lol. Nonetheless, it's a bunch of random colored dots in a 10 x 10 square, stare in awe as you watch this masterpiece generate: [Loom screen recording](https://www.loom.com/share/4866b8c88be7404b9b502e12749065d0).  
The code can be found here -&gt; [https://github.com/kdleonard93/100-Days-Of-Code\_Python/commit/e059d6d2fd128e0c67043f3c3e34bd38c166c857](https://github.com/kdleonard93/100-Days-Of-Code_Python/commit/e059d6d2fd128e0c67043f3c3e34bd38c166c857). The reason the branch is no longer available to look at on remote was that I successfully created my first GitHub workflow to mimic repo management behaviors as I have at work, where we use Bitbucket.

#### New Github Workflow

The new workflow's job is to delete the remote branch after the pull request is merged. I have it set to also ignore this action if the branch is `main` or `master`. The code for this workflow is below:

```yaml
name: Delete merged branch

on:
  pull_request:
    types: [closed]

jobs:
  cleanup:
    runs-on: ubuntu-latest
    if: github.event.pull_request.merged == true
    steps:
      - name: Delete branch
        uses: actions/github-script@v6
        with:
          github-token: ${{ secrets.GITHUB_TOKEN }}
          script: |
            const { owner, repo } = context.repo
            const branch = context.payload.pull_request.head.ref
            console.log(`Deleting ${branch}...`)
            if (branch !== 'main' && branch !== 'master') {
              return github.rest.git.deleteRef({
                owner,
                repo,
                ref: 'heads/' + branch
              })
            } else {
              console.log(`Not deleting ${branch} because it is a protected branch.`)
            }
```

## Settling on Environment

Circling back to the issues I had with `pipenv` and `conda`, I still plan to use `conda` in the long run, but `pipenv` is just so much lighter and I don't see myself needing a lot of the included tools and libraries that come with Conda at the moment. I will slowly start using `miniconda` first, then move to `conda` completely when I start to hit bigger projects during this journey.

## EOD

So that wraps up Day 18 as a whole. Hopefully, people can take away a little bit of knowledge from this one regarding GH workflows and environment setups but ultimately, as you know from reading the first few articles, this is just a journal to serve as a resource for myself and if there are a few golden nuggets that people find helpful, then all the better ✌🏾.

#### If you want to keep up with my progress or just want to connect as peers, check out my social links below and give me a follow!

* [🐦 Twitter](https://twitter.com/RingoMandingo93)
    
* [💻 Github](https://github.com/kdleonard93)
    
* [👾 Discord](https://discord.com/users/407639833146818570)
    
* [👔 LinkedIn](https://www.linkedin.com/in/kyle-leonard93/)