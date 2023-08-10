---
layout: post
title: What is...site reliability engineering?
date: 2023-08-10
---

I'm starting a series called "What is..." (yes Marvel fans, I see you), where I dive into a tool or concept I use regularly.

Sometimes the best way to refresh our minds is to pretend we're looking at something for the first time.

Today's dive is into site reliability engineering (SRE). I'll cover the basics and a tad more.

[Other people have written plenty on the topic](#further-reading), do check out their work.

## So what is SRE

The explanation I give my parents:

```text
Site reliability engineering focuses on maintaining or enhancing the reliability of a service. A reliable service is one with minimal failures and infrequent periods where the service is unavailable. 
```

Sometimes I just tell my family SRE is like the plumbing or electricity in a house: you only notice it when it's not working or the service is unreliable. 

For something more official we can turn to [Google](https://sre.google) (specifically [Benjamin Treynor Sloss](https://landing.google.com/sre/interview/ben-treynor.html)), who effectively created the field:

> Fundamentally, it’s what happens when you ask a software engineer to design an operations function…So SRE is fundamentally doing work that has historically been done by an operations team, but using engineers with software expertise....

### A bit of context

The field grew out of a contradiction.  

The goal of a traditional operations teams was to minimise risk to production systems. Risks occurred through code changes or system changes. In contrast, the goal of software engineers was to roll out new features, change code, i.e., introduce risk.

The incentive of each team was in opposition to the other. Not only that, each group had a different set of experiences, tools, vocabulary, and way of conceptualising reliability and risk.

SRE was developed to bridge the gap between these two teams.

## Top things to know (imho)

1. SRE is a mindset
2. It's also a set of practices and principles
3. SRE is cross-disciplinary, one size does not fit all

## Digging a bit deeper

### Mindset

Yes, SRE _is_ a job title, but more importantly it's a mindset.

In practice, it's seeing a repetitive operations task and figuring out how we can utilise code/programming concepts to automate or improve it. 

It's a mindset that views systems holistically, sees connections between components, and patterns in design, almost always looking for ways to enhance, automate, or improve service reliability. It's also a mindset that enjoys the minutiae of operating systems, networking protocols, or database threads.

Moreover, I'd argue being an SRE also requires a strong set of interpersonal and communication skills. SREs do change work, they evangelise, they need to communicate decisions with developers and stakeholders, they need to make the inaccessible accessible (aka teaching). 

It can be full on.

### Principles and practices[^1]

SRE principles can be summarised around some core concepts: **observability** (how do we know what's happening in a system), **automation** (how can we optimise a system by removing/reducing repetition), and **simplicity** (how can we design or refactor system to be simpler). 

Observability encompasses things like service level indicators/objectives/agreements, monitoring, and even attitudes to risk (our appetite to risk is related to our confidence in observing a system).

Automation exists both to optimise a system but also to free up time for engineers to do other things.

And simplicity? Simpler systems and designs often, but not always, lend themselves to reliability.

### Cross-disciplinary

This goes back to my earlier point about mindset. 

SRE is a cross-disciplinary field, a mix of software engineering, traditional operations, and ideally a dollop of emotional intelligence.

It's a dynamic field which adjusts to developments in software engineering, hardware advancements, and business changes (e.g., on-premise servers to cloud).

This means there's no one-size-fits-all model of doing SRE. The principles and practices are especially applicable in scaling or maintaining large systems, but can also be strategically applied to smaller teams. The important thing is to be flexible and iterate.

Also, because the field is cross-disciplinary and often touches a number of different teams, it can be useful to develop standards for tooling and approaches. It's a bit of a nightmare supporting 10 different software teams who all use different CI/CD tooling. Yikes!

Yet the overarching mission does not change: to ensure the services we build––which are used by consumers, customers, clients, humans––are more reliable.

## My experience as an SRE

I've always liked [Krishelle Hardson-Hurley’s](https://hackernoon.com/so-you-want-to-be-an-sre-34e832357a8c) formula: Site Reliability Engineer = Software Engineer + Systems Enthusiast. 

In my case that's how I fell into the field.

I started as a software engineer, joined an infrastructure team, and quickly became a systems enthusiast.

I was drawn to how could use my love of teaching when doing SRE as well as the integral role communication and psychology play in the role. 

I also loved the mix of big picture and in-depth problem-solving, although I tend to feel more confident looking at systems holistically instead of unpacking an I/O issue. 

I'm a visual thinker and learner so enjoy drawing diagrams which turn into system designs and ultimately servers (or containers).

Another fun aspect of SRE is all the collaboration you get to do. 

You work with stakeholders to develop SLxs, talk with developers about how they use tooling (checkout [developer experience](https://draft.dev/learn/what-is-developer-experience)), collaborate with architects to bake reliability into the design, work with cybersecurity experts to ensure security is also baked in from the start, and that's just Monday!

Just kidding, you collaborate every day.

The only downside I've discovered is how immense the field feels, I don't know if I'll ever be completely confident in all aspects of SRE because there's just so much to learn.

## Further reading

* [_Site Reliability Engineering: How Google Runs Production Systems_](https://sre.google/sre-book/introduction/). Literally THE book on SRE.
* [Krishelle Hardson-Hurley’s blog "So you want to be an SRE?"](https://hackernoon.com/so-you-want-to-be-an-sre-34e832357a8c). Excellent!
* Pretty much anything from [Google's curated list of resources](https://sre.google/resources/).
* The [`awesome-sre` repo](https://github.com/dastergon/awesome-sre). A staggering list of books, blogs, videos, newsletters, conferences, and other resources.
* This New Relic blog ["7 habits of highly successful site reliability engineers"](https://newrelic.com/blog/best-practices/site-reliability-engineer-sre-habits).

----------------------

[^1]: The _Site Reliability Engineering_ book has an entire [section about principles](https://sre.google/sre-book/part-II-principles/) and [practices](https://sre.google/sre-book/part-III-practices/). I recommend both.