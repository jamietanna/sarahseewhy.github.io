---
layout: post
title: Confidently changing code
date: 2023-08-13
---

I was recently chatting with some developers and the topic of changing code came up. 

We were all debating the question: how do you confidently make changes to an existing codebase?

It was a really fun question to discuss and contemplate so I thought I'd share my 2¢ (and more).

In my opinion there are four layers to creating confidence when delivering changes in software: **team communication**, **software engineering practices**, **reliability engineering techniques**, and a **security-first approach**.

-----------------------

## Team communication

Confident changes happen in teams with strong communication foundations. 

I’m confident delivering changes to software when teams practise open communication and vulnerability, accept and take accountability for their mistakes, support each other through those mistakes with empathy and curiosity, and find joy, laughter, and connection in their work. 

My confidence grows when I see engineers connected to their end users and work in harmony with product developers to ensure the team is delivering software based on user centred needs. 

I appreciate teams which practise lean software development, feel confident in their stand-ups and retrospectives, and involve the whole team in product development.

## Software engineering practices

I feel confident making changes to software which is test driven (unit, integration, and end-to-end) and where TDD has been part of the software development culture since day one. 

My confidence grows when I know the code has been paired on and if individual work occurs, there are code reviews in place. 

Confident and clear use of version control is also essential in both pairing and individual work (I’m partial to a style guide for commits). 

It’s also heartening to see well maintained documentation and software style guides when pairing on teams. 

I’m impressed by teams which make small and frequent commits that can be easily and quickly released to production (or rolled back). 

Fast feedback loops are amazing! These approaches are supported by the use of feature toggles, A/B testing, canary testing, and a strong inclination towards software crafting and clean code.

## Reliability engineering techniques

I feel confident in making changes to systems if I see the team has implemented some reliability engineering best practices. 

Fundamentally I want practices in place to help me understand how, where, and why my change has impacted a system and how my changes relate to the team’s SLAs, SLIs, and SLOs. This includes developing the appropriate type of monitoring for the team and customer needs. 

I feel much easier making changes when I know the logs have been structured in a meaningful way, I feel confident I will be notified when something goes awry (I appreciate alerts which are descriptive and actionable), and I can measure the impact of my change. 

Moreover, if using multiple environments I feel confident making changes when I know my development, staging, and production environments are in alignment; or if using trunk-based development, the CI/CD pipeline process is clear, fast, and efficient for releases and rollbacks. 

I love teams which look for ways to automate mundane tasks, have clear processes for incidents and post-incident retrospectives, keep infrastructure costs in mind, and reliability engineering is part of the product development.

## Security

Finally, a note on security. 

In a lot of ways security practices overlap between software and reliability engineering best practices. 

I feel confident making changes to code when I know there are regular updates to our libraries and OS (preferably automated). It also helps when I’m able to code defensively or work with people who have experience doing so. 

I want there to be processes in place for securing customer data and following GDPR guidelines and teams practise the principle of least privilege in their infrastructure (or are on that path).

Ideally credentials are managed securely (automatically rotated and encrypted), network traffic is secured, and on-boarding and off-boarding is fast and efficient.

Fundamentally security should be part of the product development cycle.
