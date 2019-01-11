---
layout: post
title: Reflection week 2
date: 2019-01-11
---

This week: learning golang, a reminder to check All The Things, and what I'm currently reading. Our CTO gave an interesting talk on delivering value which sparked some reflections which I've not been able to fully articulate. More to come later.

### _Learning golang_

We've decided to use golang (go) for one of the tools we're building. This is a new language for the team and it's been a mix of fun and frustrating. From my experience this is a normal reaction to picking up a new language. 

**Loved**: I find the first few times practicing a new language to be the most fun. There's this exhilaration about looking at the world in a different way and being introduced to new ways of solving a problem. I've only just started on a tutorial but already there are some things I really enjoy, like the testing/auto-documentation aspects of go.

**Lacked**: Some of the mocking/spying capabilities I'm more familiar with in Java aren't easily available in go (from what we can currently tell). My intuition says this is in fact a Good Thing. Mocking can be a useful way of integrating parts of a codebase, but I've also seen mocks be an indication of overly complex code. I suspect this is purposeful in go.

**Learned**: It's hard not be anchored by previous languages I've learned. The first bit of go I wrote looked remarkably like Java until my pair partner and I refactored it to be more go-like. 

### _Check All The Things_

This week we ran in to a peculiar problem which ultimately reminded me that despite what you think is true, it's important to check your assumptions.

For initially inexplicable reasons a newly brought up server was not sending metrics to Grafana. Everything looked fine in Puppet (cert and node: check), everything appeared fine in Terraform (...or so we thought), but the connection to Graphite was timing out.

The root cause? `domain` was being incorrectly set. All other facts were fine, so checking them led us to believe that the server creation process was not a factor. Since the `domain` was incorrectly set, it failed a filter which ultimately impacted how the server connected to Graphite.

How could we have found this sooner? By checking our assumptions. If we'd gone through the various filters and confirmed the values on the server were in fact what we'd expected them to be then we would've caught the error. 

Lesson learned...again.

### _Currently Reading_
    
I typically have two books on the go: one for my bedside table and one for my commute. This division is due to book size, I dislike carrying around heavy, hardback books on the Tube.

**Bedside**: [_The Golden Thread_](https://www.hodder.co.uk/books/detail.page?isbn=9781473659049)

This is an engaging global history of fabric and its impact societies, cultures, and economics. I've just finished the pre-historic period and am still trying to fathom how groups 40,000 years ago developed the complex technology to process fibres like flax into linen.

**Commute**: [_Black Studies in the University_](https://www.amazon.com/Black-Studies-University-Armstead-Robinson/dp/0300011679)

I find the history of academic fields to be fascinating, especially the introduction of academic fields fueled by the Civil Rights movements of the 1960s, 70s, and 80s.

This book is a collection of lectures given at a Yale conference in 1969. It's an intellectual exploration of the concept and implementation of Black Studies. 

It's both an artifact of history, considered a primary source, and a window into a particular moment in time.