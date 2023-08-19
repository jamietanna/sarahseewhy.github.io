---
layout: post
title: If Terraform best practices were Taylor Swift songs
date: 2023-08-16
---

Today I got asked: what are your favourite Terraform best practices?

That's a big question, and it got me thinking about Terraform best practices and what if they were written by Taylor Swift 🤔

More specifically, what if Taylor Swift song titles were actually about Terraform best practices?[^1]

I paired my favourite practices with Taylor Swift songs (at least the titles).[^2]

For all non-Swifities here's a quick list:

|:--------------------------------------------------:|:-----------------------------------------------------------------------------------:|
|       [Write clean code](#write-clean-code)        |      [Use Single Responsibility](#use-the-single-responsibility-principle)          |
|   [Know your system](#know-your-system-and-self)   |  [Split infrastructure from configuration](#split-infrastructure-from-configuration)|
|     [YAGNI](#the-problem-with-future-proofing)     |       [Be idempotent and declarative](#idempotent-and-declarative-for-the-win)      |
|[Be readable _and_ DRY](#balance-dry-and-readability) |   [Don't worry about cloud-agnostic](#notes-on-the-cloudvendor-agnosticism-myth)    |                                  

-------------

### Clean • _1989_
#### Write clean code

This is a big one for me.

When writing Terraform code it's imperative for it to be human-readable. 

The computer doesn't care if you name a resource "snake" in one file and "cat" in another. But your future self and anyone else reading the code will definitely care.

This means using clear, sensible, and consistent naming patterns, limiting line length to make code easier to read, writing small functions which do a specific action, implementing DRY principles (more on that later) and splitting large files into smaller ones (if possible). 

I recommend naming conventions mentioned in [Terraform Best Practices](https://www.terraform-best-practices.com/naming).

One way to help encourage clean Terraform code is to use a linter like [`tflint`](https://github.com/terraform-linters/tflint). Plus you get the benefit of finding errors and syntax depracation warnings.

Side note: I'd also file tagging all your resources under "clean code" for Terraform. It's such a time saver in the long run and can really help with tracking costs.

### ME! • _Lover_
#### Know your system (and self)

🎶 "I promise that you'll never find another like me" 🎶

Or in this case you. There's no one like you or your codebase. You are on your own unique journey in infrastructure, lean into that.

To me this means it's ok to play around in the console first. Click-ops your way to understanding if you will. Manually building in the console provides a fast discovery feedback loop (e.g., a resource's mandatory fields or parameters). 

I've experienced both approaches: learning a system through code first and learning a system through the console. I have a slight preference for the latter if only because I'm a visual learner.

As long as there are guardrails in place (ideally a dev or sandbox environment) then the console is a great way to learn. Make sure you enable other guardrails as well, I'm thinking a git pre-commit hook or a pipeline job which scans for sensitive data

Once you feel confident then it's important to understand your unique system's requirements. Take the time to diagram and really understand the whole picture, especially what is being built by the Terraform code you write.

Most of the time I'd recommend building your own stuff from scratch. I've not used third-party modules because I believe one size does not fit all. Also, many of these pre-cooked modules come with a host of parameters which aren't applicable to every system.

### The 1 • _folklore_
#### Use the Single Responsibility Principle

If you're going to do one thing, do just that one thing (and do it well).

This is otherwise known as the single responsibility principle. It's one of the [SOLID](https://en.wikipedia.org/wiki/SOLID) design principles well-loved by software engineers.

In the context of Terraform, this means creating modules which have a small, specific purpose. You don't need a module to do All The Things. 

It's ok to create a module for a specific scenario and then create another one for a separate scenario. Naturally this doesn't apply across the board, Terraform really is context based and one size does not fit all.

The point is that Terraform can lend itself to creating monolithic files and modules, and I'd argue it's good practice to work against that tendency.

In my humble opinion small, dedicated modules are easier to read and change.

There is of course a balance between duplicated code and readability/extension.

### This Is Me Trying • _folklore_
#### Balance DRY and readability

Terraform code with too much repetition is hard to read and maintain, especially if it means changing values in multiple places.

Terraform now offers more built-in expressions and functions (e.g., `for-loops` in v.0.13) which helps reduce repetition. It's a lot easier to create a set of EC2 instances with an iterator than write 10 resource declarations.

This is undoubtedly helpful, more efficient, and often creates easier to read code.

However. I think when we use expressions/functions to the point where it impacts readability then they lose their usefulness. Multiple if-else clauses which depend on a host of conditionals sounds like a recipe for disaster to me.

I'd much rather write two similar, if slightly different, resources because there is a genuine difference between both. Sometimes it's important to surface those differences through duplication.

There is no right answer here. It takes trying.

### I Forgot You Existed • _Lover_
#### The problem with future proofing

The problem with future proofing in Terraform is a lot of what's possible to build falls into category of YAGNI (You Aren't Gonna Need It).

Understand the requirements of a feature and then build those...and no more. If one day you need another feature  you can implement it then. Not today.

This speaks to the earlier point about knowing your system. 

As weird as it sounds not every system will need a remote backend or a CI tool to run your Terraform (though many will).

Often we create technical debt that we forget exists when we try to future proof infrastructure as code (IaC) by adding more than we need.

This line from Tiexin Guo's blog on Terraform Best Practices[^3] really hit home:

> why bother wasting time creating a remote state with state lock and executing the job from a CI running in K8s in the cloud and creating ridiculously small modules just to have modules because others told you it's "best practice" to do so?

### State of Grace • _Red_
#### Split infrastructure from configuration

First, what's the difference between infrastructure code and configuration?

Infrastructure code will help you create an EC2 instance in AWS, adjust the CPU, and connect it to security group rules. It will not manage the dependencies or maintain the software on that instance. 

That is what configuration management is for. Configuration will install a set of dependencies (tied to various versions), launch servers, or tell programs to run specific software.

Technically Terraform can also do configuration management. 

I worked on a product with one EC2 instance and we managed its configuration in Terraform because introducing Puppet or Ansible for one instance would've been over-engineering.

However, in most scenarios it's best to separate your IaC from configuration especially for large-scale systems. It can help reduce complexity and maintain idempotency.

Achieving a state of grace if you will.

### Forever & Always • _Fearless_
#### Idempotent and declarative for the win

What does it mean to be idempotent? It means that no matter how many times you do something (with the same starting inputs) you will always get the same end result. 

I'd like to think I achieve idempotency with my cookies (they're always amazing) but I know this isn't the case. Sigh.

IaC is meant to be idempotent. No matter how many times you run `terraform apply` on the same starting state you will always have the same end state (obviously if you've changed something in between that's different).

Idempotency is critical because we don't want inconsistent results in our infrastructure.

We can achieve idempotency by writing Terraform declaratively.

Our code should "declare" the desired end state, not the commands to run in that end state. 

The example Guo provides from his blog is useful here:

> For example, you want to install an HTTP webserver. The task should be described as "ensure an HTTP server is installed" (i.e., if the HTTP server isn't installed, install it; if already installed, do nothing), instead of "run this apt command to install the server."

A big lesson for me over the last few years is to pause whenever I encounter a potential side effect: what will happen to this script if I rerun my Terraform pipeline again?

### Shake It Off • _1989_
#### Notes on the cloud/vendor agnosticism myth

I'll end on this note: shake off the notion of cloud agnosticism. Just shake it off.

When I was tech lead and discussing disaster recovery plans someone raised the idea of cloud or vendor agnosticism. What happens if Thanos snaps his fingers and suddenly AWS turns to dust? Shouldn't we write our Terraform so it can be interchangeable between GCP and AWS?

My problem with both these questions is that it's just not feasible. 

The configuration for AWS, GCP, and Azure are not interchangeable, they just aren't. You would effectively have to rewrite an entire Terraform codebase to make it fit with a new provider. The code isn't reusable.

One option is to pick and choose vendor or tech based on a unique and useful feature for your New Thing. That approach has a downside: you end up with a tech stack list longer than necessary.

In general, I'm more in favour of standardising a tool set and accepting I'll be using a particular vendor until the landscape changes.

------------
[^1]: Tiexin Guo has a superb piece, ["9 Extraordinary Terraform Best Practices That Will Rock Your Infrastructure"](https://blog.gitguardian.com/9-extraordinary-terraform-best-practices/) which I honestly can't improve on. Do check it out.

[^2]: Full disclosure: I'd loosely, _loosely_ describe myself as a Swift fan (which made this blog both fun and a bit challenging to write tbh). I like her music, have a few favourite songs, and look forward to her album releases. I'm mostly really impressed by her Eras tour and wish I'd gotten tickets.

[^3]: See Note 1.