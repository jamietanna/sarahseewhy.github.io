---
layout: post
title: Structured logging
date: 2022-04-30
---

The individual contribution I've been doing has got me thinking about logging on our service. I've been leading on incidents, doing support work, and exploring our codebase for fixes. I've noticed we have room for growth when it comes to our logging, in particular could we move to structured logging?

### What is structured logging

Charity Majors does a great job outlining [logs vs structured events](https://charity.wtf/2019/02/05/logs-vs-structured-events/) as well as a deeper dive into ["structured events"](https://charity.wtf/2022/08/15/live-your-best-life-with-structured-events/).

I can't improve on what Charity wrote, go read it.

### Why it's important

Structured logging makes log analysis, diagnosing issues, and finding patterns a lot simpler.

It can help identify bottlenecks in a system much faster than currently possible in our service.

There are a lot of other benefits but for the purpose of our system those are the main ones I care about.

### Where it fits on a legacy project

From my experience and general reading, structured logging is especially useful in a large, distributed systems (I'm looking at you _SRE Handbook_).

However, this is not our system. 

Ours is actually pretty straightforward, we don't have hundreds of servers processing millions of requests per second.

This partly explains our logging situation. 

I don't think the original developers believed the system was complex enough to warrant the time it would take to implement structured logs –– or it just wasn't a priority.

I also wonder if some of the "Monolithic System Assumptions" outlined in Charity Major's blog applied to the service when it was created:

> * We have a monolith service, or a very small number of services. We can model the system in our heads.
> * Logging is done to local disk, which can impact performance
> * Disks are expensive
> * Log lines are spat out inline with execution.  A poorly placed printf can take the whole system down.
> * Investigation is rare, and usually means a human reading error logs.
> * Logging is of poor utility for understanding internal states or execution paths; you should just read the code or use a debugger.  (There are few or network hops between functions.)
> * Logging is mostly useful for detecting certain terminal crash states or connection errors.
 
However, I sense a gap between what we have now and where we could be.

This is especially true for diagnosing issues and running sophisticated queries on our logs.

I believe there's real value in investing time to improve our logging...and implementing at least some type of structure onto our logs.

#### A note on FreeRADIUS

It's a bit of a pickle. 

We're constrained by FreeRADIUS, one of our key components, because its approach to logging is less than ideal (imo). 

The verbose logging setting logs every packet line received by the RADIUS server which is a bit _too_ verbose for our needs.

Eduroam has implemented some promising [custom logging in its FreeRADIUS configuration](https://www.youtube.com/watch?v=mER_HUMB7l0) which I think is worth exploring further.

### Next steps

#### FreeRADIUS logging

The biggest gain would be in advancing our FreeRADIUS logging capabilities because this is where most things which can go "wrong" in our system do.

It would be great to have more visibility (dare I say observability?) over this component.

Like I mentioned, Eduroam has produced some interesting material on how to improve logging for FreeRADIUS and if you're curious start there.

My [10% project](https://github.com/alphagov/govwifi-frontend/tree/test_freeradius_locally_project/test) spiked their approach and is ready to be picked up by other members of the team.

#### Agree on vision

I'd like to get the team together to discuss what "good" logging looks like across our applications and infrastructure.

I'm especially curious about the assumptions and habits around logging each person has developed.

Once we get a sense of the direction we'd like to go as a team we can begin to propose work and develop a plan for implementation.