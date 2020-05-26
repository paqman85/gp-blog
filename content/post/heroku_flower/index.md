---
title: "Monitoring Celery on Heroku with Flower"
date: May 26, 2020
draft: false
tags: ["python", "celery", "heroku", "dev ops"]
toc: true
---
{{< figureCupper
img="celery_is_good_for_you.jpg" 
caption="Monitoring Celery can be a drag! Use Flower on Heroku for Celery and make watching fun!... or at least less boring... [Credits](Photo by TOPHEE MARQUEZ from Pexels)." 
command="Resize" 
options="700x" >}}

## The Setting

I built a small Django application for a client and launched it on Heroku. It takes posted data from a legacy application that the client is using for inventory management and sends it to their Shopify E-commerce store to keep everything in sync. To keep things running smoothly, I included a Celery worker to have a queue in place and speed up the post calls.

## The Problem
When it came time to test that all was working as it should in production - I realize that Celery's monitoring add-on -- Flower -- will not function on the same Heroku instance... which is unfortunate.

## The Idea

Heroku has a generous free tier -- I thought I could launch Flower on a separate free Heroku instance and connect the Redis broker URL from the Django application.

In my search on Heroku and Github - I did not find a working solution for my situation. While there are a few Flower & Heroku setups, they all had bugs that crashed the application on deployment or simply had vague instructions.

I managed to write a simple solution that worked perfectly for my project. Since I have been thinking of how to contribute to open source lately, so I thought I'd re-write my Heroku-Flower project and share it with the world.

## The Solution

All in all, launching Flower to monitor your Celery worker on Heroku is simple. Flower can be installed by pip; it simply needs to be included on your *requirements.txt* file. 

The tricky part comes in when you need to adapt the Flower app to your own needs. Does your Celery instance run on RabbitMQ or Redis? Do you need persistent storage? What about authentication?

Here's the solution for you -- [Simple Celery Flower For Heroku](https://github.com/paqman85/simple-celery-flower-on-heroku).

It has everything you need to launch a Flower Celery monitor on Heroku, with a Redis broker and basic authentication.
