---
layout: post
title: Reflection week 1
date: 2019-01-03
---

Although this has been a short week I wanted to begin the habit of a weekly reflection piece, similar to Alex Wilson's ["Weekly Notes"](https://blog.probablyfine.co.uk/2018/09/21/notes-from-the-week-1.html).

--------

_Joys of problem solving_

This week I ran into an interesting Puppet problem with my pair partner.

A bit of context:

We'd created a way of adding custom nrpe checks for a system (check out the open source [repo](https://github.com/unruly/unruly-puppet)).

The parent definition (`nrpe_custom_check`) has a number of parameters but the two of interest are: `$ensure` (defaulted to 'present') and `$content` (the check's content).

This creates a trickle down configuration that automagically creates the plugin, the plugin config, and any potential sudo config as well. It means creating a check will be a lot easier and more flexible for our end users.

So what's the problem? Well, `$content` is a required parameter. What happens if a user just wants to ensure a check is absent? They must include `$content` even if it's just "foo".

We wanted to be able to have our cake and eat it too. We wanted both this:

```
nrpe_custom_check { 'some-cool-check':
    ensure => 'absent',
}
```

and this:

```
nrpe_custom_check { 'some-cool-check':
    content => file('/path/to/some-cool-check.sh'),
}
```

to be possible...and it's not.

We spent some time discussing the pros/cons of various approaches, what was the balance between ease/flexibility and quirky edge case behaviour?

In the end it reminded me of the joys of problem solving, the pleasure of thinking about a problem from various angles, trying off-the wall suggestions, following a logic path to its result.

These are the moments when I'm glad I switched from being a historian to software development.

___________

_Pairing when talking is difficult_

I recently discovered I have [pleurisy](https://en.wikipedia.org/wiki/Pleurisy), a nasty (temporary) consequence of a bog-standard chest infection. Normal, day-to-day speaking ends up feeling like a cheese grater on my lungs or the occasional stabbing Italian [stiletto](https://en.wikipedia.org/wiki/Stiletto). Tremendous fun.

The pleurisy has made pairing a bit difficult because (gasp) pairing involves *a lot* of speaking: clarifications, spit-balling, discussion. Where I work we pair on all production code and I've had to learn to adjust my communication/pairing style.

I'm more judicious about expending speaking energy which allows my pair partner more time to experiment or notice a typo on their own. It's reminded me that sometimes a more patient approach to navigating can foster learning or creativity in driving.

The same is somewhat true for when I drive, since asking for reassurance means speaking I'm more likely to just crack on and learn from my mistakes.

I've heard about code a retreat where pairs completed a kata without speaking.

I think I'd like to try this...especially right now.
