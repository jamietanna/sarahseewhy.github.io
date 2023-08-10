---
layout: post
title: Stumbling on Google’s secret recruitment tool
date: 2023-03-12
---

I recently got invited to Google’s secret recruitment tool called `foobar` (aww, thanks Google!).

It’s a series of coding challenges similar to what you’d find on [LeetCode](https://leetcode.com) [etc](https://www.freecodecamp.org/news/the-10-most-popular-coding-challenge-websites-of-2016-fb8a5672d22f/).

If you’re curious here are [some](https://itsmohitt.medium.com/things-you-should-know-about-google-foobar-invitation-703a535bf30f) [other](https://www.turing.com/kb/foobar-google-secret-hiring-technique) [blogs](https://www.freecodecamp.org/news/the-foobar-challenge-googles-hidden-test-for-developers-ed8027c1184/) about it.

The following is my experience.

## The problem

A couple of other blogs go into a lot more detail on the various challenges and levels. 

Suffice it to say they’re (relatively) simple coding problems that increase in complexity as you progress through the five stages.

I started out on and decided to only complete the first stage (more on that later).

I don’t want to spill the beans too much though Google probably rotates the problems.

My task was to use math to calculate a result based on an input.

I know, I know, that’s extremely vague and describes pretty much all code everywhere, but I really don’t want to divulge too much. Let’s just say there were some square area issues, finding roots of squares, and lists of perfect squares.

I was given example outputs and told I had to fulfil specific, undisclosed, test cases.

Fun fun fun!

## Implementation goes well

I read the problem through a couple of times and then got out a pad of paper to think and visualise my way through how I’d solve the problem.

Once happy with my paper solution I was ready to put it into code.

I chose to use Python (Java was also an option) and started by TDD-ing.

The flow of TDD is so rewarding, it was fun to get back into that groove.

I completed the logic to my satisfaction and moved on to edge cases (i.e., what if the input were a string, `None`, etc).

This brought me to a bit of a rabbit hole on how to test exceptions with Python `unittest`. 

At this point I could’ve used a pair partner to problem-solve through some testing issues. Sadly I only had my rubber duck and they were only moderately helpful.

The exception handling in the script could be improved but all in all I was pretty proud of my code and the accompanying tests.

I was ready to verify my solution with `foobar`'s test cases.

## BANG! Frustration, headache, pain

All of `foobar`'s tests failed. Repeatedly. No matter what I changed.

Possibly the most frustrating moment was hard coding the example output (test passes) and then my result (test fails). The two outputs appeared the same when I ran the script in interactive Python.

However, this approach of hardcoding a success clued me into the root cause of the test failures.

It was a head-desk, facepalm moment if I ever had one.

## Solution

I used `floor()` to do a calculation in the script. `floor()` returns a `float` not an `int` (I only discovered this when I double-checked the docs…always, always read the docs).

On the command line my `float` answer looked like an `int` but it wasn’t. Not to a computer or `foobar`’s test suite (possibly a drop in the bucket for using a more statically typed language like Java).

I only realised this a couple of days into banging my head on my desk and after my rubber duck had rage quit in frustration.

Once I tweaked the logic to ensure my `float` answer was an `int` all the tests passed and I could sit back and have a biscuit and a cup of tea.

(the rubber duck also returned for the tea and biscuit)

## Reflection

### Do this for fun because it is genuinely fun

I had a lot of fun doing the challenge and it made me curious to do similar challenges on other platforms.

I flexed my code problem-solving skills, learnt a few things about Python, and got some solid TDD practice in.

I’m glad I treated the problem as fun instead of in a stressful, I-**must**-get-to-the-next-level way (it helps I’m not actively looking to be recruited).

If you do get invited, definitely say yes — have a blast!

### `foobar` is limited

I’ve been working in software engineering for nearly a decade and been through countless interviews, both as interviewee and interviewer.

These coding challenges only demonstrate a fraction of what it takes to do software engineering well. There are so, so, so many other skills and perspectives which imho are more valuable to a team.

It’s rare in my time as an engineer that a previous coding challenge has helped me solve a problem on a product or during an incident.

I’m not saying this type of practice has no value (especially given the lesson I learned about `floats` vs `ints`) but it feels a bit limited in its recruitment potential.

It’s a filter of sorts –– which creates a new question in my mind: who or what type of skillsets is Google filtering out inadvertently?

### Why I stopped at Level 1

I have other things I’d like to do. My time is finite.

While I enjoy coding problems, and probably will try to do more now, I really want to delve into site reliability engineering.

I’d like to think about and practice working more in the infrastructure space.

There are *other* aspects of software engineering which bring me joy and I'd also like to pursue those more deeply: communication, team culture and psychology, conflict resolution, extreme programming.

However, thank you Google for the chance to participate!