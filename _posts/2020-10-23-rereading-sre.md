---
layout: post
title: (Re)reading Site Reliability Engineering
date: 2020-10-23
---

Picking up [_Site Reliability Engineering: how Google runs production systems_](https://landing.google.com/sre/sre-book/toc/index.html) again has felt like a breath of fresh air. 

It reminded my why I fell in love with reliability engineering: being able to focus on the big picture but also feel the joy of _building_ services.

This is a quick reflection on the the first chapter.

---------------------------------

#### Monitoring

The first chapter's section on monitoring really spoke to me. 

I appreciated their point that "monitoring should never require a human to interpret the alerting domain". 

One of my biggest pet peeves are alerts with no, or poorly worded, descriptions. 

I also <ins>completely</ins> agreed with the authors: alerts to should be a call to action, not an FYI from the system.

We achieved this at my last workplace and need to get to this point on the team I've just joined (the infrastructure needs a bit of TLC).

The task can feel insurmountable, especially if there are lots of alerts.

On my last team, we started by inventorying all our alerts, creating a wiki which explained what the alert meant and tips on how to resolve it (a pseudo-playbook if you will).

We then iterated on the doc and began to ask whether we needed the alert at all or in a different form (e.g., grafana graph). There was room for further iteration towards more automation (hello chat-ops!) but I'd said farewell by that time.

One of the things I appreciate about my current organisation is their use of playbooks. I know playbooks aren't universally popular, but it made on-boarding to on-call so much easier and quicker. 

The downside of course is maintaining the alert documentation which can get exhausting with too many alerts.

#### Change management, demand forecasting, & capacity management

The two areas where I'd love to work with an SRE team that's "got it right" is change management and demand forecasting/capacity planning.

At my last company we used trunk-based development and small commits. Rolling back was straight forward but perhaps could've been more automated. 

We were automatically alerted if we'd introduced a regression but also relied on incremental changes and isolated experiments.

Although there's more automation where I work now, I wonder if there are ways it could be improved.

I'd also like to see improvements in demand forecasting and capacity planning –– but first I'd like to see what "good" looks like to get a sense of direction.

#### Finally...

All in all I'm really glad I've picked up the SRE book again to reground myself. I look forward to reading more and expanding my SRE reading list ([this looks like a good start](https://github.com/dastergon/awesome-sre), and [this](https://blog.catchpoint.com/2020/02/26/20-essential-books-for-site-reliability-engineers/)). 

Suggestions welcome.