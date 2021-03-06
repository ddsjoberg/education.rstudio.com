---
title: 'Teach R with learnr: a powerful tool for remote teaching'
author:
  - '[Allison Horst](https://www.allisonhorst.com/)'
date: '2020-05-19'
categories:
  - teach
tags:
  - learnr
  - rmarkdown
description: |
  Why and how I created a learnr tutorial on *Exploring missing data in naniar*
slug: learnr-for-remote
photo:
  url: https://www.allisonhorst.com/
  author: Allison Horst
---



The unexpected switch to remote instruction has been a challenge for teachers and learners, and has inspired - or for some, forced - the use of innovative teaching methods and tools. Coding lessons pose a unique challenge for remote instruction as teachers are unavailable for in-person troubleshooting, and beginning students are unlikely to have developed debugging or [reprex](https://reprex.tidyverse.org/)-building skills. On top of coding-related challenges, students might not have access to a device on which they can install R and RStudio.

So, how can we create live coding lessons to include participants who... 

- ...have not used or installed R and RStudio?
- ...are unable to quickly get in-person troubleshooting help during live lessons? 

The [learnr](https://rstudio.github.io/learnr/) package offers a solution to both. In this post, I describe why and how I created a learnr tutorial on [*Exploring missing data in naniar*](https://allisonhorst.shinyapps.io/missingexplorer/) with both first-time and experienced R-users in mind.

<a href="https://allisonhorst.shinyapps.io/missingexplorer/" target="_blank"><img src="naniar.jpg" width="90%" style="display: block; margin: auto;" /></a>

## 1. Approachable for first-time R users

For my remote lesson on exploring missing data (using [Dr. Nick Tierney](https://www.njtierney.com/)’s [`naniar`](https://cran.r-project.org/web/packages/naniar/vignettes/getting-started-w-naniar.html) package), I expected a combination of: 

- Advanced R users
- Beginning R learners
- Attendees who had never used or seen R & RStudio before

Usually, I have students fork and clone materials from a GitHub repo so that they can follow along in the RStudio IDE (Desktop, or through [RStudio Cloud](https://rstudio.cloud/)). For my live lesson, I wanted *everyone* - even those who had never used or seen R/RStudio before - to be able to write and run R code successfully, and I didn’t want those first-time R-users to need to navigate the IDE at the same time. 

### learnr tutorials look and feel like a simple website 

I love the RStudio IDE. If you’re reading this, you probably do, too. But try to remember what it felt like the first time you opened it. There is a lot there, and it takes a long time to feel really comfortable navigating it. Eventually, most R-users will need to become good friends with the RStudio IDE. But for first-time users working remotely and without hands-on help, a learnr tutorial - which looks like a simple, easy-to-navigate website - could be a more familiar and welcoming entry. 

For example, here is what my [*Exploring missing values in naniar*](https://allisonhorst.shinyapps.io/missingexplorer/) tutorial looks like: 

<a href="https://allisonhorst.shinyapps.io/missingexplorer/" target="_blank"><img src="tutorial_home.png" width="90%" style="display: block; margin: auto;" /></a>

### No installing or importing necessary

Both [RStudio Cloud](https://rstudio.cloud/) and learnr solve this problem. No need for R, RStudio, or package installation for learners to get up-and-running. And in learnr, learners don’t even need to read in data; it can already exist as a pre-stored object (e.g. data frame) that can be directly referred to throughout the tutorial. That means that **tutorial users can immediately start exploring and playing with the data at virtually no start-up cost**. Again, reading in data and naming objects are critical skills that every user will eventually need to learn. Let them learn it later. Let the first time be just the awesome stuff with learnr.

## 2. Customized hints and solutions

Another major hurdle of remote teaching is how to help students when they get stuck. learnr solves this problem in several ways. 

### You decide the starting point

Writing code from scratch can be intimidating for first-time users. In learnr tutorials you decide what code already exists, and users can build on that. 

For example, you can pre-populate a code example for a basic graph with `ggplot2`, and users could just add or update variables for the x- and y- aesthetic. Even better: there is no risk of them breaking it. For each code example, there is a button in the top left to “Start Over,” which will return the code to the original. 

In the exercise below, there is existing code to make an UpSet plot to explore co-occurrence of missing  values:

<img src="example_code.png" width="60%" style="display: block; margin: auto;" />

### Hints

This might be my favorite thing about learnr - it’s easy to add one or more customized hints that students can look to when they get stuck. When learners are working through tutorials on their own, I think this is an awesome option to lead them along without giving away the answer. 

<img src="hint.png" width="60%" style="display: block; margin: auto;" />

### Solutions

If you want users to be able to see the full solution, you can make that easily available too. This is especially useful in a live-coding demo, when participants can fall behind if they need to troubleshoot or read through a sequence of Hints. Once a solution is created, a Solution button will appear in the code exercise. There’s even a convenient ‘Copy to Clipboard’ button built-in. 

<img src="solution.png" width="60%" style="display: block; margin: auto;" />

Learn how to add solutions, hints and more to your learnr tutorial [here](https://rstudio.github.io/learnr/)!

## 3. Customize your tutorial with CSS

I wanted the look of my learnr tutorial be highly customized. That meant some CSS, and involved just a few steps:

- Making a new /css directory in my tutorial project
- Creating a new .css file in it
- Adding that to the YAML output format (see more in Section 3.1.4.1 [here](https://bookdown.org/yihui/rmarkdown/html-document.html))
- Update CSS with a lot of googling, ‘Inspect Element’ and trial & error

Here are some of the custom CSS changes I made for the biggest differences with the smallest effort: 

### Update header color and font

Customizing \<h3> header:


```css
h3 {
  color: teal;
  font-family: 'Roboto Slab', serif;
}
```

...and similar to customize other heading levels (h1, h2, etc.).

Remember that if you are using google fonts (like Roboto Slab here) you’ll need to set that up. 

### Update body background & font


```css
body {
  background-color: white;
  font-family: 'Source Sans Pro', sans-serif;
  font-size: 12;
}
```

### Update menu aesthetics

Tons of options to update the overall menu look: 


```css
.topicsList .topic {
    font-family: 'Roboto Slab', serif;
    line-height: 40px;
    font-size: 15px;
    padding-left: 10px;
    cursor: pointer;
    background-repeat: no-repeat;
    background-size: 2px 80px;
    background-position: left 100%;
        background-position-y: 100%;
    background-image: url(images/topicProgress.png);
    border-bottom: 1px solid teal;
    -webkit-transition-property: background-position;
    transition-property: background-position;
    -webkit-transition-duration: 0.25s;
    transition-duration: 0.25s;
}
```

And this stuff changes the look & color of the menu item you click on: 


```css
.topicsList .topic.current {
    font-family: 'Roboto Slab', serif;
    background-color: orange;
    color: #ffffff;
    border: 0px;
}
```

...plus a bunch more stuff, but those are some that made me the happiest with the look of my tutorial with minimal effort. 

### Font awesome icons! 

Icons are great for organization and visual interest in course materials. I used icons to indicate coding examples, exercises, and critical thinking questions. Install and attach the [`fontawesome`](https://github.com/rstudio/fontawesome) package in R to add [Font Awesome](https://fontawesome.com/) icons directly to your tutorial. 

For example, this...  

```r
fa("fas fa-bug", fill = "orange")
```

...adds this: 

<svg style="height:0.8em;top:.04em;position:relative;fill:orange;" viewBox="0 0 512 512"><path d="M511.988 288.9c-.478 17.43-15.217 31.1-32.653 31.1H424v16c0 21.864-4.882 42.584-13.6 61.145l60.228 60.228c12.496 12.497 12.496 32.758 0 45.255-12.498 12.497-32.759 12.496-45.256 0l-54.736-54.736C345.886 467.965 314.351 480 280 480V236c0-6.627-5.373-12-12-12h-24c-6.627 0-12 5.373-12 12v244c-34.351 0-65.886-12.035-90.636-32.108l-54.736 54.736c-12.498 12.497-32.759 12.496-45.256 0-12.496-12.497-12.496-32.758 0-45.255l60.228-60.228C92.882 378.584 88 357.864 88 336v-16H32.666C15.23 320 .491 306.33.013 288.9-.484 270.816 14.028 256 32 256h56v-58.745l-46.628-46.628c-12.496-12.497-12.496-32.758 0-45.255 12.498-12.497 32.758-12.497 45.256 0L141.255 160h229.489l54.627-54.627c12.498-12.497 32.758-12.497 45.256 0 12.496 12.497 12.496 32.758 0 45.255L424 197.255V256h56c17.972 0 32.484 14.816 31.988 32.9zM257 0c-61.856 0-112 50.144-112 112h224C369 50.144 318.856 0 257 0z"/></svg>


## 4. Sounds great, but can it handle my class size and usage? 

This was one of my biggest concerns about running a live lesson with a learnr tutorial: given limitations on hours & data, would the app (hosted through [shinyapps.io](https://www.shinyapps.io/)) crash when everyone tried to use it?

RStudio’s [Barret Schloerke](http://schloerke.com/) directed me to this [essential post](https://cran.r-project.org/web/packages/learnr/vignettes/shinyapps-publishing.html) by Angela Li (<a href="https://twitter.com/CivicAngela"><i class="fab fa-twitter"></i></a>), which answers this question exactly. Following Angela’s super helpful post, and expecting ~75 people to simultaneously start and use the app for ~30 min during the lesson, I decided to: 

- Upgrade my subscription to Basic ($99/month - check with your school / university to see if they already have a shinyapps.io subscription or could get one to support teaching)
- Max out instances (to 5 with a Basic subscription)
- Max out instance size (XXXL - 8 GB)
- Set Max Worker Processes to 2
- Set Max Connections to 17
- Set Start Count to 5

See Angela’s post for more information on what these actually do, and to help you decide on settings for your tutorial based on class size and needs.

## 5. Summary

I feel that learnr is a great option for coding lessons and activities, especially for remote instruction with beginning R users.

For me, the biggest benefits of learnr are: 

- Looks and feels like a simple website (great for first-time R users, knowing that eventually they’ll need to work in RStudio IDE)
- No account, login, or installations necessary
- Pre-populated code exercises, hints and solutions ensure no one gets left behind in the absence of in-person troubleshooting
- Data / objects already exist - no need for beginners to import data or store objects
- Easy to publish and share (no forking/cloning/emailing materials)
- Relatively easy to customize with CSS

Some potential drawbacks: 

- You may need to upgrade shinyapps.io subscription to suit course needs
- If you hate CSS, you might not love customizing (I did a lot of Inspecting Elements, and ended up really enjoying it and learning a lot)

My overall rating of learnr as a teaching tool: five stars. Give it a shot, and have fun teaching and learning with a learnr tutorial! 

