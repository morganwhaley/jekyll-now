---
layout: post
title: Location Matters
---

Sometimes I have a day where I just want to write a damn event binder but this happens instead:

![Just WHY](http://i.imgur.com/s32cy.gif)

A couple weeks ago someone in LivingSocial slack asked what the diff is between putting script files in the `head` vs lower in the file, below the DOM. I had no hard evidence at the time but had a notion putting the file at the bottom, say just inside the `body` tag, would ensure DOM elements were fully loaded before the script runs.

So today I just spent about an hour beating my head against a wall wondering why a `.click` event wasn't binding.

When this goes wrong, I try two basic things:
- Run a `console.log` or `debugger` in the binder to see if it's even binding.
- If that doesn't hit, log the DOM element I'm trying to hit and check its length.

For some reason, step 2 didn't occur to me for an hour.

The Problem:  
The script I was calling was coming from Rails asset pipeline and was loading in the document `head`. So, surprise, the length on that DOM selector was a big fat zero.

![Where is it?](https://media.giphy.com/media/2vlC9FMLSmqGs/giphy.gif)

The Solution:  
Move that sucker into the bottom of my ERB for the time being and woooot, it works!

Script location. It's a thing.
