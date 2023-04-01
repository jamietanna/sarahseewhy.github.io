---
layout: post
title: Decoding a trip down memory lane
date: 2023-03-24
---

One of the perks of living in Seattle is I get to spend quality time with my parents which includes being their on-call tech support. 

Recently my mom came to me with a fun problem and here’s how I went about solving it.

## Problem

My mom had files from 1994-1999 which she couldn't open and were therefore unreadable (at least initially). She wanted my help to open and read them.

### Context

These files were originally saved on floppy discs, then CDs, then an external hard drive, and finally her laptop.

They’re from an ancient mac and PC (I think). Most of the files don’t have extensions.

It’s old homework, creative writing from when my brother and I were teenagers (can’t wait to read that angsty poetry), and I believe a journal my mom kept.

All valuable from a sentimental perspective and a bit of a time capsule.

## Approach

### Investigate

When my mom tasked me with the problem the first thing I did was open the files with `vim`.

Success!

But they were littered with special characters: `^@`, `^M`, etc.

Not very human-readable. Plus, my mom is grand but isn’t an ace at `vim` (yet).

### Research

Initially I presumed these were individual characters which could be deleted from the file. 

I imagined I’d have to use some fancy regex in a script to strip out the special characters and leave the human-readable text.

However, after a bit of reading I learned that `^@` and `^M` are their own characters or “digraphs” (presumably the other special characters in the files were as well).

In `vim`, a [digraph](https://vimdoc.sourceforge.net/htmldoc/digraph.html#digraph-table) is “used to enter characters that normally cannot be entered by an ordinary keyboard.”

`^@` is the digraph for Null and `^M` is the digraph for Carriage Return (newline). Using the handy digraph table linked [here]([https://vimdoc.sourceforge.net/htmldoc/digraph.html#digraph-table](https://vimdoc.sourceforge.net/htmldoc/digraph.html#digraph-table)) I identified a few other digraphs in the files.

According to [The School of Stackoverflow]([https://stackoverflow.com/questions/2591277/what-do-these-signs-mean-in-vim](https://stackoverflow.com/questions/2591277/what-do-these-signs-mean-in-vim)) these characters *can* indicate an encoding issue.

### Experiment

I had at least two options: figure out if I could correctly set the encoding to make the files readable or use a find/replace script to remove the characters.

I tried a few attempts at configuring the encoding in `vim` , reading and translating the file on the command line.

None of these experiments led me further but I was also not convinced the effort developing a regex script would be worth it (although it was a tempting to practice scripting and regex).

I returned to reading.

## Solution

I’m glad I did because I found a solution which was simple and more importantly, sustainable for the end user (my mom).

I ultimately found the answer on [StackExchange's `superuser`](https://superuser.com/questions/8225/how-do-i-open-a-file-in-binary-plaintext-format-on-mac-os-x): mac's TextEdit.

Using TextEdit worked, but there were still some random characters at the beginning of the file. However, it was the simplest solution and most mom-friendly.

It meant some copying and pasting for her, but she expected to do that anyway even if I'd removed the special characters.

Problem solved! 🎉

## Reflection

It was fun pairing my mom and although the problem didn't end up being as complex as I initially thought we had a good laugh.

I'm glad we settled on a solution which suited her. 

It reminded me sometimes the best solutions are simple, right in front of us, and don't require any engineering effort.

I also spent some time afterwards reading about how encoding works, the various types of file encodings, and why it differs between operating systems.

A few issues I'd like to investigate further are file degradation, what happens when files get transferred from one saving medium to another (desktop --> floppy disk --> desktop --> CD --> laptop --> external hard drive), and finally how does TextEdit do some of its magic.

More food for thought 🥞.


