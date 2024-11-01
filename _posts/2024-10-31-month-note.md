---
layout: post
title: Month note
date: 2024-10-31
---

A return to month notes! I enjoyed writing these. It's a chance for me to reflect on the past month and highlight the things I'm working on or thinking about.

I won't guarantee the cadence will be monthly, my time commitments are different now, but I'll do my best.

Here goes.

--------

## Refactoring Terraform

We're doing a major refactor of our entire Terraform codebase. We've orchestrated our CI/CD to enforce a build order for the modules. 

This allows us to remove implicit resource dependencies, data lookups, and be more explicit about dependencies between modules.

We looked at a few options but as a team settled on using the `terraform_remote_state` data source (see [docs](https://developer.hashicorp.com/terraform/language/state/remote-state-data)). This works well for our codebase because it's relatively simple and our running order isn't complicated.

It has meant a heck of a lot refactoring and I've learned a lot.

After a rather gnarly `remove`/`import` piece of work I learned the hard way that the `remove` work _needs_ to be propagated throughout all the infrastructure in order for the `import` work to succeed.

I had to do some careful state file surgery with a pair but it ended up ok.

My pair also taught me about `cd -` (how have I lived without it!?).

## Pairing

The last month has involved a lot more pairing. 

This is to help upskill a junior SRE and also helps me practice my pairing skills.

The experience has been useful for us both. I'm so grateful to my time working at an XP company because it taught me everything I know about how to pair effectively.

It's also gotten me thinking about the lessons from teaching, especially teaching English language learners, and how these lessons can be applied to pairing.

Top in my mind is _Krashen's Five Hypotheses of Second Language Acquisition_ (link to [blog](https://beelinguapp.com/blog/stephen-krashens-five-hypotheses-of-second-language-acquisition)) as well as some specific teaching techniques.

Some day I'll write a blog about this, maybe even do a talk.

## Learning and development

I don't do enough of this. I try every Friday to spend half the day learning but more times than I'd like to admit I end up doing work.

Perhaps part of the problem is I've not settled on a side project so I don't feel as motivated to pick something up.

I'm still working on this. Let's see how the month of November goes.

---------------

Currently reading:

* [_Sacred Rest_](https://www.amazon.co.uk/Sacred-Rest-Recover-Energy-Restore/dp/1478921676). I got through the introduction and realised I didn't like the book. I much prefer [_4000 Weeks_](https://www.amazon.co.uk/Four-Thousand-Weeks-Time-How/dp/1847924018).
* Anything by Georgette Heyer. Easy reading, not much thinking. Sometimes just what I need.
* [_Wilding_](https://www.amazon.co.uk/Wilding-Return-Nature-British-Farm/dp/1509805109). Wonderful book but a bit too depressing for me to finish (does contain glimmers of hope).

Since I continue to co-sleep with my daughter I read via audiobooks. I don't find listening to non-fiction has helpful as physical reading so stick to fiction or history (itself a kind of fiction).

My toddler sleeps with fewer interruptions now so I'm thinking of moving to reading physical books or perhaps ebooks. I need to find the right one.