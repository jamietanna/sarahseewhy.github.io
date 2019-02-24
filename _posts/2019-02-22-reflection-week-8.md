---
layout: post
title: Reflection week 8
date: 2019-02-22
---

I'm trialling a new format for my Week Notes: a summary for each day. The last few weeks I've noticed I sneak in tidbits of long-form topics into my reflections. 

This makes them more engaging (hopefully), but it also takes longer to write. I'd like to spend more time on long format posts, to really delve into a topic.

We'll see how this goes.


## Monday

I worked with AWS and Terraform with a particular eye to IAM roles, users, groups, and policies. Although familiar with these concepts at a high level, digging into them more deeply was engaging. 

Previously, I'd sort of brushed over the distinction between roles and users but on Monday I got a chance to think more critically about them. 

Roles are like articles of clothing, on which policies can be attached. This process reminded me of the way social meaning is ascribed to clothing. A pilot's hat can be worn by any person and once donned, it implies this person has specific social permissions (to fly a plane for example).

Users are different, they can't be "donned" by other users. 

Users are typically assigned a Group (which comes with its own policy outlining a set of permissions). This reminded me of [_Cows Pigs Wars And Witches: The Riddles of Culture_](https://www.penguinrandomhouse.com/books/75826/cows-pigs-wars-and-witches-by-marvin-harris/9780679724681/), an intriguing anthropology study (though a bit dated). It explores the diversity of social mores and taboos throughout history. 

Now I can't stop thinking about AWS Users/Groups in anything but anthropological terms.

## Tuesday

Tuesday was a heavy Terraform (TF) day – I (re)learned a lot: practice with `terraform import`, `terraform state move`, and using TF to be sensible about security.

I did leave that day pondering a bit about approaching tasks in TF. Is it more productive to complete work first in the console and then TF it, or vice versa? 

AWS console obfuscates some granular, background configuration which has to be completed in TF. There were one or two "face-palm" moments in the day when we realised we'd missed a critical step because it wasn't as obvious in the console.

I don't have answer.

## Wednesday

20% Time! I do love this aspect of the company where I work. I spent the day working on my [meeting-tracker](https://github.com/sarahseewhy/meeting-tracker) project.

I finished the spike, getting the whole thing to work end to end. I can now run my script and retrieve this:

```bash
ACME team events since February 13, 2019
{'meeting': 2, 'social': 1, 'huddle': 3, 'retro': 1, '1-1': 3}
```

I got to do some refactoring which I love and experimented with a different approach to naming.

Normally, I use verbs to name methods and nouns for variables (actions and things). I focus on readability and articulating the purpose of each object. Pretty standard.

This time I refactored my code to read more like a narrative, even if it meant individual method names may not be clear when viewed in isolation:

```python
def main():
    calendar = build('calendar', 'v3', 
                      credentials=authorized_credentials())
                      
    calendar_items = retrieve_calendar_items_from(calendar, 
                                                  for_time_range())
                                                  
    event_types = extract_types_from(calendar_items.get('items', []))

    display(collated_event_types_and_frequency_from(event_types))
```

It was interesting to experiment but I'm still on the fence as to whether I prefer it.

## Thursday & Friday

Python, python, and more python. 

I'm really enjoying working with this language, both for my personal project and in my team. 

I've never been particularly precious about which language I use, nor do I feel passionately that there's one language to rule them all, one langauge to find them, etc.

In terms of preference, I probably lean towards programming languages which sound more like a natural language (e.g., ruby, python). 

However, it does make me a tad jittery working with dynamically typed languages. 

I like the confidence I feel when writing Golang or Java that the proverbial frog won't end up being a member of a royal family because of a type conversion that's gone haywire.