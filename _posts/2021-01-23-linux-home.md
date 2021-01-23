---
layout: post
title: The Linux Home
date: 2021-01-23
---

Have you ever thought about mapping the Linux filesystem on to rooms in a house?

I have. In fact, I've thought about this a lot over the last few years.

Whenever I connect to a server it feels like I'm entering a house. `cd`-ing into a directory is like opening a door into a new room. It's like I'm inspecting the furniture when I list a directory's contents.

I find filesystems fascinating but at first it was infuriating.

There was always something new to discover yet none if it made sense. 

Why were some files in `lib` but others in `bin`? What did `etc` stand for (was it really _et cetera_)? What was each directory's purpose and why?

This confusion felt particularly frustrating when I was first learning to diagnose issues on a server. It was like urgently needing to find a spoon in a house but not knowing which room was the kitchen.

For the last few years I've wanted to lean into the house analogy: draw the Linux filesystem as an actual house. Each room would corresponded to a directory's purpose.

This month, after a bit of research on filesystems (mainly [here](https://www.howtogeek.com/117435/htg-explains-the-linux-directory-structure-explained/) and [here](https://en.wikipedia.org/wiki/Filesystem_Hierarchy_Standard#Directory_structure)), I finally got around to drawing my first filesystem-house doodle:

![The Linux Home](/public/images/linux_home.png)

# Welcome, let's start exploring

A few up front caveats. 

There is no "right" way of mapping a filesystem to rooms in a house. Everyone will have their own interpretations. In fact, I'd love to hear other points of view. 

I shared the doodle with some developer and SRE friends and it sparked a lively conversation. Some of my favourite suggestions included adding a dollhouse to represent `/usr/local/bin` and having hallways represent `/home`.

The entire house should be viewed as the `/` directory, with each subdirectory a room in the house.

## Basement as `/sbin`

The `/sbin` directory holds system administrator binaries. These are essential binaries for system administration and are usually run by the root user.

I thought this mapped well to a basement: a place where most people don't go but contains essential things for the house (like a boiler and laundry machines). 

Only people who know how to use the boiler go down there (sort of like a root user).

Yes, I know Americans are weird and put their boilers in the basement. I have no idea why either.

## Library as `/usr`

`/usr`, or user binaries, contains all the applications and files used by users on the operating system. This is in contrast to applications and files used by the system (e.g., `root`). 

Non-essential applications are located in the subdirectory `usr/bin`. `usr/sbin` is also home to non-essential applications, but only those used by the system. Finally, locally compiled apps are installed to `usr/local`.

Since the directory is read-only and effectively a "library" of applications, it was the perfect candidate for, well, a library.

I slightly objected to the implication that books are "non-essential" to a house. Yet when I searched deeply into my soul I had to admit they aren't technically essential and moved on.

Plus, I liked the idea that different shelves could represent different subdirectories: a shelf for all the boiler and laundry manuals (`/usr/sbin`) and a shelf for all other books (`/usr/bin`).

## Craft room as `/var`

It seemed sensible to put `/var` next to `/usr` because the two are connected. 

`/var` is short for variable data files and it's the writable counterpart to the read-only `/usr` directory. This means `/var` is where all the applications in `/usr` write data to files, typically logs.

Making `/var` a Victorian "writing room" fit well but I preferred the idea of having an arts and crafts room. Why limit expression to just the written word?

Also, I didn't want to confuse a writing room with a study because I knew I needed the latter for `/etc`.

## Study as `/etc`

This is a bit of a stretch, but bear with me.

`/etc` is responsible for configuration files, and yes it is short for _et cetera_ ([you can read an interesting history of its naming here](https://www.linuxnix.com/linux-directory-structure-explainedetc-folder/)).

It contains, among other things: configuration tables (`crontab`, `fstab`), running configuration (`vimrc`), configuration files (`ntp.conf`), deny/allow files, and some other stuff (hence the et cetera).

So why a study? Well, what's critical to house configuration? I think wifi and electricity are strong contenders. 

I drew a router and a barely visible fuse box on the left wall and decided the most sensible place to put a router would be a study. The fuse box was a bit out there but never mind. 

I also imagined this room as the control centre for all the futuristic IoT devices which super fancy 21<sup>st</sup> century houses now have.

## Bathroom as `/bin`

`/bin` to bathroom is rather fun.

So `/bin` contains essential user binaries which must be present when the system is mounted in single-user mode.

While non-essential applications are located in `/usr/bin`, critical system programs like `bash` exist in `/bin`.

What is an essential room in a house? Well, in my opinion a bathroom with an in-door toilet is _absolutely_ essential.

I've used outhouses on farms and the odd cabin in my life and it's what I'd describe as a character building experience (at least the outhouses I've used, I'm sure there are lovely ones not infested with spiders).

A. **B**athroom. **I**s. **N**ecessary. Or `/bin`

## Boudoir as `/lib`

This might be another stretch but a fun one.

`/lib` holds libraries required by the essential binaries in `/bin` and `/sbin`. 

You'd think `/lib` should map directly to a library but I'd argue you're wrong. 

There is no logical connection between a library and bathroom, unless one is enthusiastic about having available and extensive reading material in close proximity to the loo.

There _is_ a connection between a bathroom and a boudoir. 

Where else would you store bubble bath or epsom salts? Post-bath moisturiser or face oils? A boudoir supports the function of a bathroom in the same way `/lib` supports the function of `/bin`

Boudoirs can also have closets which means I can hang my comfy bathrobe next to my get-stuff-done boiler overalls, and thereby have a connection to both `/bin` and `/sbin`.

Ok fine, it's a bit of a stretch –– but I like it, it feels decadent and a bit outrageous.

## Bedroom as `/home`

This was perhaps the easiest. `/home` contains the folders for each individual user, their data, and user-specific configuration.

It's like a bedroom in a house: personalised and not for everyone. 

You can have whatever furniture or art you'd like. It's not a public room, it's specific to you and your tastes.

## Garage and bins as `/mnt` and `/tmp`

These were also easy to map. `/tmp` is for temporary files which get regularly removed, very much like garbage bins which get emptied on a weekly basis.

`/mnt` is for temporary mount points where you can mount other filesystems. [Historically this was a physical task](https://superuser.com/questions/334115/what-do-we-mean-by-mounting-a-filesystem) involving magnetic tape reels and a tape reader.

I felt a garage was the closest equivalent to this process. You can park vehicles in a garage just as you would mount filesystems on `/mnt`.

## What's missing

Unfortunately I wasn't able to think of a room for each directory in the Linux filesystem.

I nearly made `/proc` the kitchen because something is always cooking just like a process is always running –– but at the time of drawing I wasn't convinced by the analogy. I now regret the omission.

As I said before, suggestions are welcome.

Hope you got as much fun out of the exercise as I did.

