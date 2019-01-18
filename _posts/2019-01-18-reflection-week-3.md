---
layout: post
title: Reflection week 3
date: 2019-01-17
---

This week: testing scripting languages and what obligations do software developers have as historical actors? Leaving aside the tone of levity it's been an interesting, one of the things I love about being a developer is that it's rarely dull. I'm always learning and often challenging myself to the point of frustration. But perhaps that's a good thing.


### Testing scripting languages

As with many companies we use bash as a scripting language for a bunch of our scripts. It’s a solid tool for scripting and typically gets the job done. 

As an XP team we also believe in TDD and over the past year have been experimenting with [BATS](https://github.com/sstephenson/bats) to test our bash scripts.

This week we were refactoring a script we don’t touch frequently but when we do, we’ve committed to making small improvements. 

Which brings me to testing bash with BATS and why I think it’s worth learning the process.

BATS has changed how I choose which language I want to use for scripting – _assuming_ I also want to test my scripts. 

BATS supports testing ‘simple’ (perhaps in the [Cynefin](https://en.wikipedia.org/wiki/Cynefin_framework) sense) bash and it does this pretty well. 

However, we found in test driving bash scripts that BATS became a burden not an enabler when our logic moved from simple to [complicated]() (again, Cynefin). The feedback from BATS was unhelpful, especially for failing tests.

It was no longer as useful a tool to use which encouraged us to think about our logic (can we simplify it?) or consider another scripting tool (Python, Go, etc).

Working with BATS this week increased my appreciation for Go's testing features ([autodocumentation]()) and the readability of pytest.

### A question of history

By the end of this week I will have finished [_Black Studies in the University_](https://www.amazon.com/Black-Studies-University-Armstead-Robinson/dp/0300011679). So much in the book was thought provoking and will probably linger awhile, however a few passages in particular stood out and have left me asking more questions than answering any. 

In [Dr. Nathan Hare's](https://en.wikipedia.org/wiki/Nathan_Hare) essay, "A Radical Perspective on Social Science Curricula", he writes: 

> Persons who make history or help to make history in a sense are writing history, because they dictate to some degree what is that the persons who write history will write.
<sup>1</sup>

This idea, that individuals in the present are historical actors and every day are writing history with their actions, drew me to study history. It felt empowering to know that our words and actions could have resonance for generations to come. It's a bit overwhelming really. 

In this model, where does the role of software developer fit? What will future historians write about software development of the early 21<sup>st</sup> century? At a high level, how are we writing history by our actions today? Is it in how we 'police' the idea of software developer (i.e., who do we include/exclude)? What about the tools we build and the code we write? 

Thinking at a more granular level, we also 'make' history whenever we write code (leaving aside the historical implications of the products we build). The evidence we produce is commit messages and documentation (to name two) – how can we improve this evidence to help our future selves better understand the choices we're making now? 

The [Karma commit](http://karma-runner.github.io/3.0/dev/git-commit-msg.html) conventions has worked well on my team to preserve history in a meaningful and future-empathetic way. Documenting design choices like we've done on our [open source project](https://github.com/unruly/unruly-puppet/tree/master/architecture_decisions) is another.

Having empathy for a future self or selves pushes me to think about the decisions or actions I commit to in the present. 

To some extent this is embodied by Edwin Redkey's point in his essay "On Teaching and Learning Black History":

> [we] search for origins in the past of the problems of the present in hopes of bringing justice and peace in the future.  

This is true both for historians but to some extent for developers. We do search for origins in the past (commit history) to better understand the problems in the present – and do we hope to bring justice and peace in the future? Probably not, but perhaps it's worth thinking about.

We _are_ historical actors.


