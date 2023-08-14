---
layout: post
title: Fireside (AI) chat on site reliability engineering
date: 2023-08-15
---

Welcome to my fireside chat with ChatGPT all about site reliability engineering.

![fireside](/public/images/fireside.jpeg)

On a whim I asked ChatGPT to generate 10 questions to ask an SRE about core concepts and how to problem-solve certain situations.

Reader, beware! This is a long read, make a cup of tea and grab a biscuit.

Here's what we "chatted" about.

### Can you explain the concept of "Error Budget" in the context of SRE? How is it calculated and how would you prioritise between new features and reliability?

Sure! An error budget is the amount of acceptable unreliability a service can have before end user happiness is affected. I like the Google description of error budget as the user pain tolerance in different parts of a system.

Error budgets are based on service level indicators, objectives, and agreements. SLIs are calculated by finding the number of “good events” divided by the number of “valid events” displayed as a percentage. Like this:

SLI = { good events / valid events } x 100

So for example, if we measure service availability as the amount of requests responded with an error, divided by all the valid requests the home page receives (as a percentage). We can then create an objective availability, say 99.9%, which gives us an error budget of 0.1%. This means we can negatively impact availability by 0.1% and our users will still be happy.

**And how would you prioritise between new features and reliability?**

Well, once we have an error budget we can discuss where new features fit in that budget. If we have a mature testing environment we can measure the impact of a new feature on our remaining error budget. The goal is to balance innovation and stability though I believe this should be an on-going conversation.

### Describe a situation where you had to handle a critical incident in a production environment. What steps did you take to mitigate the issue and prevent it from happening in the future?

Great question. 

I once worked on a product which used an SMS help number. An SMS robo-marketing campaign stumbled on our public helpline and the two automated systems got into a vicious, and for us expensive, SMS cycle.

The first step was to declare an incident and form an incident team with the goal to resolve the incident as soon as possible. Our team had pre-assigned roles during incidents so there wasn’t confusion about responsibilities.

We triaged the situation, agreed a Px level, and then started on our designated paths. The comms lead (our product manager) updated our stakeholders and status page (templates make this so much easier), while two engineers paired on diagnosing the issue.

We found it helpful to pair SREs and developers when diagnosing because the combined skills set and familiarity with our stack is *chef kiss*. The incident lead (typically the tech lead or infra lead) monitored the situation and provided guidance, especially at critical decision points.

The pair found the root cause in our code, an unaccounted for edge case in our SMS controller, and we agreed to deploy a temporary fix.

After the incident was resolved we implemented a longer term solution and organised a post-incident retrospective where we reviewed the timeline of events, actions, and decisions.

We discovered in the retro that preventing a similar occurrence would be a challenge because our team didn’t have oversight over SMS costs. This was managed by a separate team who initially alerted us to the issue. A compromise was to create an alert for our engineers when our SMS count exceeded a certain number in a given time frame.

### How would you approach designing and implementing a monitoring and alerting system for a complex distributed application?

Well, as a first step I’d work with stakeholders and product teams to understand the non-functional requirements. What do we as a business want/need to optimise for? Once we’ve established the non-functional requirements and their priority then we can begin designing a monitoring and alerting system.

The next question I’d want to know is whether we need to implement observability or monitoring because to me the two are distinct. In some contexts it makes sense to implement both (e.g., for your known unknowns and your unknown unknowns) Honeycomb.io has a [good piece on this distinction](https://www.honeycomb.io/blog/observability-differs-traditional-monitoring). I particularly like this quote, “Monitoring works for me when I already know the question I want answered. But observability is for when I don't yet know what I'm looking for.”

Let’s assume we’re implementing just a monitoring system. My primary goal would be to work with the team to figure out the relevant metrics, agree and implement structured logs, and establish a modicum of traceability (request IDs etc).

If, however, we want to implement a more observability-based system then I’d lean towards structured events, [distributed tracing](https://www.datadoghq.com/knowledge-center/distributed-tracing), and aim for each request to emit telemetry. Charity Majors has an [excellent blog](https://charity.wtf/2019/02/05/logs-vs-structured-events/) about structured events.

From there I’d work with the team on an alerting system based on agreed Px levels, scenarios we want to be alerted for, and various alert channels. Alerts must be calls to action for human intervention. Ideally they’d point to documentation to help the person on-call resolve the issue (there are downsides to this approach).

I’m in favour of alerting on only a specified list of critical scenarios instead of many alerts generated from every post-incident retro ever. Alert noise is real. I’m also less keen on FYIs from a system: unless latency issues are having a catastrophic impact I’m not sure I want to know about them.

I tentatively take a similar approach to graphs: fewer, simpler, and targeted graphs are ideal. Visual overload, like alert fatigue, is real.

It’s critical to treat monitoring and alerting systems as works in progress. What worked six months ago won’t necessarily work for a team today. The system should be iterative and adaptable.

**And what metrics and indicators would you consider crucial?**

My answer is evasive but genuine: it depends on the business and the system. Common metrics and indicators include: response time, throughput, error rate, CPU usage, latency and uptime, error rates, memory usage, average response time, custom application-specific metrics.

### Explain the differences between horizontal and vertical scaling. When would you recommend using each approach, and what challenges might arise with each method?

I explain this concept to my family by asking: would you rather have one giant dog (aka Clifford The Big Red Dog approach) or many dogs?

But I digress.

Vertical scaling is when we add more power (e.g., CPU, RAM, storage, etc) to a component in order to accommodate usage changes. Horizontal scaling means adding more instances of the same component thus distributing the load.

There are [many](https://www.section.io/blog/scaling-horizontally-vs-vertically/), [many](https://www.cockroachlabs.com/blog/vertical-scaling-vs-horizontal-scaling/) [blogs](https://www.nops.io/blog/horizontal-vs-vertical-scaling/) which expand on the various challenges that arise with each approach.

I consider these factors when faced with this decision: cost, difficulty or impact of parallelising logic, performance, added complexity, flexibility, redundancy, geographic distribution.

In general, horizontal scaling is useful for distributing high traffic and ensuring availability while vertical scaling is suited for enhancing performance of an individual component.

### Discuss the importance of automated testing and continuous integration/continuous deployment (CI/CD) in ensuring the reliability of a system. 

Automated tests save time, catch potential regressions, and can (but not always) improve code quality. They remove the need to manually test, a time-consuming and costly process. Ideally automated tests should cover unit, integration, and end-to-end scenarios.

Continuous integration (CI) is the regular merging of developers’ code changes into a single repository. Automated CI improves release frequency, catches regressions and/or code conflicts early, and ensures consistent deployments.

Continuous deployment (CD) automates the deployment process to help developers release code into production faster. CD removes human intervention from the release process and encourages small, frequent releases as well as easy rollback options.

**How would you set up a robust CI/CD pipeline?**

A robust pipeline contains stages for building, testing, deploying, monitoring, and rolling back. Stages should be well documented and the pipeline should include an automated test suite for code quality and syntax style.

I have a preference for clear visuals (Concourse does this well imho) and accessible output/logging for each deployment (again, I prefer Concourse but I’ve also used Jenkins and AWS CodeDeploy neither of which wowed me).

This New Relic [blog](https://newrelic.com/blog/best-practices/continuous-delivery-continuous-deployment-continuous-integration) provides a deep dive into the difference between continuous integration, continuous delivery, and continuous deployment.

### Imagine a scenario where a software update causes a performance degradation in a production system. How would you troubleshoot the issue and identify the root cause?

Oof, that’s a good question and always an interesting problem to solve.

“What’s changed recently?” is one of the first questions I ask during an incident or a noticeable performance degradation. I look at deployment logs and/or release notes to check the recent change list and potential impact. If I’m lucky, I can easily tell if a recent deployment will have an impact on performance but that’s not always the case.

If the problem is a bit more opaque, one way to sense check the root cause is to cross reference the performance monitoring with the recent deployments and see if there’s any connection between the time of a deployment and the start of degradation (though correlation does not always mean causation).

In most cases the solution is to roll back to a previous release and see what impact that has on the performance. CI/CD pipelines should make this straightforward to do.

To prevent future occurrences I advocate for improving testing practices and am a big fan of canary deployments and/or feature flags.

### Can you describe your experience with incident response and post-incident analysis? How do you ensure that incidents are thoroughly investigated and learnings are applied to prevent future occurrences?

I’ve already described an experience with an incident response, but I can talk about some post-incident analyses I’ve experienced.

For me the best way to ensure incidents are investigated and learnings applied is through post-incident retrospectives (aka postmortems).

During an incident it’s critical to keep a log of the actions and decisions made. Imo incident log scribe is a vital and underrated role in an incident. This log becomes the foundation for the post-incident retrospective. It helps the team remember the incident and also can pinpoint lessons for next time.

A post-incident retro ensures all contributing factors are analysed. Learnings must be shared across teams, hopefully leading to process improvements and preventing similar incidents.

### In the context of disaster recovery, what strategies and techniques would you employ to ensure high availability and data integrity for a critical application?

I worked with an incredible technical architect on my last team (here’s his [LinkedIn profile](https://www.linkedin.com/in/sebitpro/) if you’re curious) who taught me three key strategies to disaster recovery:

**Redundancy**: Deploying across multiple availability zones and/or regions.
**Backup and Restore**: Regularly back up data and test restoration procedures.
**Failover**: Automatically switch to standby systems in case of failure.

A final one I’d add is chaos engineering, intentionally introducing failures to test a system’s resilience.

### Explain the concept of "circuit breakers" and their role in preventing cascading failures in a microservices architecture. How would you implement and manage circuit breakers effectively?

Whew, that's not a term I've heard in a while!

A circuit breaker prevents failures from snowballing and impacting the rest of a system. They do this by detecting service degradation and halting requests to the failing service.
They can isolate failing components and give them time to recover.

You can implement circuit breakers by setting thresholds for errors or latency. These are managed dynamically, opening and closing based on real-time performance.

This Cisco [blog](https://techblog.cisco.com/blog/how-to-implement-circuit-breaker-patterns) on circuit breakers provides a bit more detail.

### Can you provide an example of a challenging situation where you had to work closely with development teams to achieve both reliability and innovation?

I think I’ve been lucky. In general, my experience has been fairly positive when collaborating between SRE and development teams, normally because we’re all one team.

In the rare times we’ve had friction between reliability and innovation I’ve used the following approaches.

**Return to common ground**
We both want the business/product to succeed. Affirm this goal and our shared identity as a team. It’s fundamental that the team invests in bonding and feels connected. Lunches out are not a waste of time.

**Build a strong communication tool set**
Ensure people know how to communicate effectively, engage in conflict with openness and curiosity, actively listen to each other, practice vulnerability. Also encourage self-awareness about communication and conflict styles.

**Use data to drive discussions**
I worked with the amazing [Steve Hayes](https://www.linkedin.com/in/steve-hayes-8233a9259/) and one of my favourite things he’d say is “some is not a number and soon is not a time” (it’s a quote from [Don Berwick](https://www.ihi.org/communities/blogs/_layouts/15/ihi/community/blog/itemview.aspx?List=7d1126ec-8f63-4a3b-9926-c44ea3036813&ID=69)). I find it's imperative when collaborating to use data to drive a discussion. “Feeling” like a service is reliable or unreliable is not the same as being able to say we exceeded our error budget five times in the last month.

**Treat failures as lessons/opportunities**
When systems fail or incidents occur it’s a moment to reflect on the missed opportunities to implement reliability engineering techniques. Often a team needs to experience the pain of an incident in order to implement a solution. Experience is the best teacher/convincer.

**Work together towards reliability**
As obvious as this sounds, it's crucial. People are invested in reliability they work to build together instead of being given metrics delivered from on high. I believe engineers need to feel invested in reliability work and feel incentivised to continually improve it.
