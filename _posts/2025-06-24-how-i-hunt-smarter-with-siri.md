---
layout: post
category: posts
title: How I hunt smarter with Siri
date: 2025-06-24 21:19:04
---

When I first started hunting, one of the things my wife hated most about it was how much time it took. Early on, I thought that my time spent hunting was equivalent to my time spent in the field. I might hunt from 6 AM to 10 AM, which would be four hours of hunting. But add in an hour and a half of driving each way and a couple of hours packing and preparing the night before, plus cleaning gear and processing birds the next day, and what started as a four hour estimate was really a multi-day expenditure. I slowly realized my wife didn't hate the four hours I was in the marsh, my wife hated the Friday night that we couldn't go on a date night because I was packing, the Saturday night I was falling asleep at 8 PM from being up early, and the Sunday I spent cleaning gear and plucking birds.

Once I understood that all of this time _outside_ of the actual hunting was one of the big constraints on how often I could hunt, I decided to invest a lot of time in optimizing that workflow. The less burden that hunting put on my wife, the more often I could do it.

One of the most time-consuming parts of hunting is the planning and preparation, particularly with duck hunting, which involves a lot of gear. As such, it’s something that I've spent a lot of time trying to optimize.

## The blueprint for a successful hunt

My goal is that I should be able to pack for any duck hunt in under one hour, including hunting with a kayak. Hitting this goal means I can spend an hour or less getting ready on Friday afternoon and still enjoy a night out with my wife.

Implicit in this goal is the fact that the process is reliable, meaning I don't forget anything. You can imagine a process in which I frantically sprinted around the house for 30 minutes, haphazardly throwing granola bars and decoys in the car, but arrive at the parking lot having forgotten my license or a flashlight (a "technique" my hunting buddies are fond of).

There are also dozens of small tasks that are important to do before a hunt, like sharing my itinerary with my wife, prepping coffee, checking batteries, and filling up the car with gas.

Trying to keep track of all these in your head is difficult and error prone. To manage all of this I use a hunt blueprint with a checklist of all of the items I might need to pack, preparation tasks to complete, and details about the hunt (e.g. location, weather, tides). This is stored in the iOS/macOS Notes app. The Notes app syncs across all of my devices, which means that it is easy to update from my laptop, iPad, or phone. I can start a new planning note from my phone while walking the dog at lunch, and then pick it up in the evening from my iPad while I'm working down the checklist.

![A screenshot of my hunt planning note in the Notes app](https://i.imgur.com/SrY02Lf.png)

## Making it delightful

In general, this Notes-based system works great. The only thing I don't like about it is that I find it tedious to have to make a new copy of the note for each hunt.

Doing this requires eleven separate finger taps on my phone. It doesn't take _that_ long, but as someone whose job it is to automate things with computers, it feels unnecessarily tedious.

To make it even easier I used Apple Shortcuts to build a flow that makes a copy of a template note and puts the current date in the title. This shortcut can then be activated with Siri by saying the title "Plan a duck hunt".

## Leveraging voice transcription

My motto is that every hunt is a success if I learned something new from it. In order to facilitate that constant improvement, you need to be regularly reflecting on what worked well or poorly on a hunt. Having a written log of each hunt both helps to clarify your thinking, and serves as a record to reference in the future.

Building and maintaining this log can be very time consuming though. A tool that has been critical in being able to create logs in a timely fashion is voice transcription. I have a "Log" section in my Notes template, and I use the dictate function to list bullet-point items of what happened and when, along with a list of takeaways (e.g. "Put my gloves in my jacket the night before"). Dictating allows me to write hunting logs during times that I would otherwise be unable to, such as walking the dog, and then come back to it on my laptop later to clean it up.

One of the challenges with maintaining a hunt journal is that the more time that passes between the hunt and when I document it, the more likely I am to forget useful details. By using voice transcription, I’m able to record the log sooner, which means I generally capture more detail about the hunt.

Siri transcribes a bunch of things awkwardly, particularly slang and acronyms, but it’s generally close enough that I can make out the intent. Like my hunt logs, most of this blog post was dictated in Notes while walking the dog. Afterwards I could easily access it from my computer and clean it up.

Leveraging voice transcription is another powerful way to make use of time that might otherwise be lost to mindless scrolling by creating a body of historical data that can be mined for insights.

## Conclusion

I've slowly gotten better at duck hunting over the years, going from complete novice to competent hunter, without much mentorship. A lot of this I credit to eliminating unforced errors ("I forgot my calls!") and regularly reflecting on the outcomes of hunts.

If I could make two recommendations to any new hunter, it would be:

1.  Create a blueprint for your hunt with everything you need to pack and prepare in advance.
2.  Keep a hunt journal to help you reflect and store your insights in a durable manner.

As James Clear says, “You do not rise to the level of your goals. You fall to the level of your systems.” If you want to regularly kill more ducks, that means having a system that facilitates that.

And for me, that system starts with “Hey Siri, plan a duck hunt.”

---

### Sidebar - Technical Details

The shortcut is pretty simple overall, but there are a couple of technical details worth noting.

The end goal is to end up with a checklist, but surprisingly Apple doesn't make that easy. Apple provides a “Rich text from Markdown“ action, but it does not support the Markdown checkbox feature. In order to get around this it is necessary to convert the rich text format to plain text, use a regular expression to replace the bullet points with check boxes, and then convert the file back to Rich text format.

The second issue I ran into when developing this is that doing that rich text conversion strips out the white space between the section headers and the proceeding checklist. This isn't a dealbreaker, but it does make the lists harder to read as they’re all pushed together.

To work around this I include Markdown horizontal rules (`---`) in the template and then perform a new line replacement which replaces a single return character `\n` with two return characters `\n\n`. This preserves the lines between the different sections of my checklist.

![A screenshot of Shortcut details for RTF conversion](https://i.imgur.com/cckuMl5.png)
