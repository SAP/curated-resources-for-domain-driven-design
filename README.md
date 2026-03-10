[![REUSE status](https://api.reuse.software/badge/github.com/SAP/curated-resources-for-domain-driven-design)](https://api.reuse.software/info/github.com/SAP/curated-resources-for-domain-driven-design)

# Curated Resources for Domain-Driven Design (DDD)

## About this project

This repository contains curated resources on the topic of **Domain Driven Design** (DDD) and **Event Storming** that we recommend internally at SAP and love to share with the community.

Besides providing a collection of great resources we also tried to structure the learning path from a first introduction to deep dives and content specializing on certain aspects. Where we think it adds value, we are giving some hints how to work with the material and what to keep in mind.

Having said that, enjoy the ride 🤠.

## Requirements

There are no prerequisites needed.

## 🤷 What is DDD all about?

DDD is fundamentally hard to explain in 10 minutes.
At its core, DDD says that your problem/business *domain* is what should first and foremost *drive* the *design* of your software system.
Technology comes later.
DDD offers principles, patterns and tools that help you *collaboratively* explore your domain, develop a common understanding and express this common understanding in useful models.
Last but not least it provides guidance on how to express these models in code, architecture and organization.

You can find a bit more extensive but still brief description of what DDD is about in Mathias Verraes' article [What is Domain-Driven Design?](https://verraes.net/2021/09/what-is-domain-driven-design-ddd/).

Note: In DDD, people often distinguish between *strategic design* and *tactical design*.
Broadly speaking, strategic design is about understanding the problem domain and splitting it into so-called *bounded contexts* (think of them as modules for now – separate things with a distinct boundary between them), while tactical design is about modelling bounded contexts in more detail and diving into actual implementation details.
While both are important and together form a holistic design toolkit, we believe strategic design to be the better starting point for newcomers.
Strategic design has many touch points with other important aspects of software development, such as architecture and organization – which is exactly what makes it so valuable.
It's also the pool to draw techniques and principles from when being tasked with understanding a new problem domain.

That being said, there's no wrong way to approach DDD.
We hope that this gives you the ability to better judge which resource is helpful for you at the moment.

## 🧑‍🎓 DDD & Event Storming 101 - Let's get things started

Not yet sure what DDD and Event Storming is all about and you want to get an overview on the topic?
We've got you covered.
In this section we present some material that should hook you up on the topic and at the same time give you a good explanation and overview.
This is a perfect starting point for your DDD journey.
From there you can dive deeper into DDD and investigate the topics that are of specific interest to you in more detail.

> 🧑‍💻 *Recommendation* Although you can specialize on aspects of DDD we recommend to approach DDD with a broader perspective and not to hyper-focus on just one aspect.

### Books

| Book | Our 2 cents |
| ---- | ----------- |
| Vernon, V. (2016). *Domain-Driven Design Distilled*. Addison-Wesley Professional. [O'Reilly](https://www.oreilly.com/library/view/domain-driven-design-distilled/9780134434964/) | Perfect entry point for newcomers. Vernon distills DDD's essential concepts into a concise, readable format covering both strategic design (bounded contexts, context mapping) and tactical patterns (aggregates, entities, value objects). Read this first before diving into the Blue Book or Red Book. |

### Videos

| Link                                                                                                   | Our 2 cents (where applicable) |
| ------------------------------------------------------------------------------------------------------ | ------------------------------ |
| [What is DDD - Eric Evans - DDD Europe 2019](https://youtu.be/pMuiVlnGqjk) (~1h)                       | -                              |
| [Event Storming - Alberto Brandolini - DDD Europe 2019](https://youtu.be/mLXQIYEwK24) (~0:30h)         | -                              |
| [50.000 Orange Stickies Later - Alberto Brandolini - GOTO 2018](https://youtu.be/NGXl1D-KwRI) (~0:50h) | -                              |

## 🧑‍🔬 DDD & Event Storming 201 - Give me more

The following resources should be seen as good summary of important aspects of DDD and Event Storming. It is in their nature that they will not necessarily give you the appreciation of the topic as a whole.

### Books and Articles

| Book | Our 2 cents |
| ---- | ----------- |
| Khononov, V. (2021). *Learning Domain-Driven Design: Aligning Software Architecture and Business Strategy*. O'Reilly Media. [O'Reilly](https://www.oreilly.com/library/view/learning-domain-driven-design/9781098100124/) | Excellent intermediate resource with a clear learning path. Khononov provides practical examples showing how to apply DDD from business strategy through implementation. Covers both strategic and tactical patterns with real-world scenarios. Great follow-up to DDD Distilled when you're ready for more depth. |
| [DDD Core Concepts](./blog/0002-core-concepts.md) | A quick summary of the core concepts of DDD from our community |
| Plöd, M. (2020). *Hands-on Domain-driven Design - by example*. Leanpub. [Leanpub](https://leanpub.com/ddd-by-example) | Practical, code-focused introduction to DDD implementation. Plöd walks through tactical patterns with concrete examples, making it valuable for developers who learn by doing. Note: Leanpub book, work-in-progress format with regular updates. |

### Videos

| Link                                                                                              | Our 2 cents (where applicable)                                                          |
| ------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| [1st Event Storming Session - Agnieszka Pawlicka](https://youtu.be/a0lWpjlSRA0)                   | Doesn't elaborate too much on the why                                                   |
| [100,000 Orange Stickies Later - Alberto Brandolini -  Øredev 2019](https://youtu.be/fGm62ra_mQ8) | Good follow-up on the "50.000 Orange Stickies Later" talk referenced in the 101 section |

## 🦸 DDD & Event Storming 301 and beyond - Going all in

So you really want to dive deep into DDD and event storming, then the following resources are the right ones. To give you a better overview we distinguish between DDD and event storming in the following sections.

> 🧑‍💻 *Recommendation* we don’t recommend these resources to get started with the topic. Working through the resources is worth it, but require some dedicated (reading) time.

### DDD

#### Books and Articles

##### Core DDD Canon

| Book | Our 2 cents |
| ---- | ----------- |
| Evans, E. (2003). *Domain-Driven Design: Tackling Complexity in the Heart of Software*. Addison-Wesley Professional. [Amazon](https://www.amazon.com/Domain-Driven-Design-Tackling-Complexity-Software/dp/0321125215/) | The foundational "Blue Book" that established DDD. Dense but essential reading for serious practitioners. **Reading strategy**: Start with the introduction to grasp the philosophy, then jump to Part 4 (Strategic Design) to understand bounded contexts and context mapping, then return to earlier chapters on tactical patterns. This approach builds strategic thinking first, which is often more immediately valuable. |
| Vernon, V. (2013). *Implementing Domain-Driven Design*. Addison-Wesley Professional. [Amazon](https://www.amazon.com/Implementing-Domain-Driven-Design-Vaughn-Vernon/dp/0321834577) | The "Red Book" - your practical implementation guide. More hands-on than Evans’ Blue Book, with concrete patterns for aggregates, repositories, domain events, and bounded context integration. Read after DDD Distilled and the Blue Book’s strategic design sections. Vernon bridges theory to practice effectively. |

##### Modern DDD Practice

| Book | Our 2 cents |
| ---- | ----------- |
| Colla, P., & Acerbis, R. (2025). *Domain-Driven Refactoring: Enhancing Software Architecture and Design*. Packt Publishing. [Packt](https://www.packtpub.com/product/domain-driven-refactoring/9781835889107) | Contemporary guide focusing on applying DDD to existing codebases. Particularly valuable for teams dealing with legacy systems or transitioning to DDD. Covers practical refactoring strategies using DDD principles. Published 2025, reflects modern practices and tooling. |
| Lilienthal, C., & Schwentner, H. (2023). *Domain-Driven Transformation: Monolith Breakup and the Building of Microservices*. dpunkt.verlag (German) / Addison-Wesley Professional (English translation expected). [Amazon (German)](https://www.amazon.de/-/en/Carola-Lilienthal/dp/3864907985) | Essential for organizational DDD adoption. Addresses the socio-technical challenges of breaking up monoliths using DDD strategic patterns. Covers team structure, communication, and migration strategies. Currently available in German; English translation forthcoming. |
| Khononov, V. (2024). *Balancing Coupling in Software Design: Universal Design Principles and Solutions for Any Platform or Language*. O’Reilly Media. [O’Reilly](https://www.oreilly.com/library/view/balancing-coupling-in/9781098157692/) | Advanced architectural thinking about coupling - the fundamental challenge DDD addresses. Khononov (author of Learning DDD) explores when tight coupling is appropriate and when to decouple. Complements DDD by providing deeper patterns for managing dependencies between bounded contexts. |

##### Organizational & Architectural Context

| Book | Our 2 cents |
| ---- | ----------- |
| Tune, N., & Perrin, J.-G. (2023). *Architecture Modernization: Socio-technical alignment of software, strategy, and structure*. Manning Publications. [Manning](https://www.manning.com/books/architecture-modernization) | Comprehensive guide connecting DDD to broader architectural modernization. Integrates Domain-Driven Design, EventStorming, Wardley Mapping, and Team Topologies into a cohesive approach. Essential reading for architects and technical leaders working on large-scale system evolution. Full of practical examples and real-world stories. |
| Kaiser, S. (2025). *Architecture for Flow: From Event Storming to Software Delivery*. Addison-Wesley Professional. [Amazon](https://www.amazon.com/Architecture-Flow-Storming-Software-Delivery/dp/0137393032) | Bridges EventStorming workshops to production architecture. Shows how to translate collaborative design sessions into working systems optimized for flow. Practical guide for teams wanting to maintain alignment from discovery through delivery. |
| Skelton, M., & Pais, M. (2019). *Team Topologies: Organizing Business and Technology Teams for Fast Flow*. IT Revolution Press. [Official Site](https://teamtopologies.com/book) | Critical companion to DDD for organizational design. Defines four team types and three interaction patterns that align with bounded contexts. Essential for implementing DDD at scale - your architecture must match your team structure. Read alongside Architecture Modernization for complete socio-technical perspective. |
| Forsgren, N., Humble, J., & Kim, G. (2018). *Accelerate: The Science of Lean Software and DevOps: Building and Scaling High Performing Technology Organizations*. IT Revolution Press. [Amazon](https://www.amazon.com/Accelerate-Software-Performing-Technology-Organizations/dp/1942788339) | Research-backed insights into high-performing software delivery. While not DDD-specific, provides the organizational context and metrics that make DDD adoption successful. Explains why architecture (including bounded contexts) impacts delivery performance. |

#### Videos

🥺 Nothing here yet - maybe you have something for us see ["How to contribute"](#how-to-contribute).

### Event Storming

#### Books and Articles

| Book | Our 2 cents |
| ---- | ----------- |
| [Introducing EventStorming](./detailedinfo/eventstorming.md) | Our Community take how to run an EventStorming Workshop |
| Brandolini, A. (n.d.). *Introducing EventStorming: An Act of Deliberate Collective Learning*. Leanpub. [Leanpub](https://leanpub.com/introducing_eventstorming) | The definitive guide from EventStorming's creator. Explains the philosophy, mechanics, and facilitation of EventStorming workshops. Covers both Big Picture and Process Level EventStorming. Note: Leanpub work-in-progress, regularly updated with new insights from Brandolini's practice. Essential reading for anyone facilitating EventStorming sessions. |
| Lawrence, D. (2025). *Implementing DDD, CQRS and Event Sourcing*. Leanpub. [Leanpub](https://leanpub.com/implementing-ddd-cqrs-and-event-sourcing) | Practical implementation guide for event-driven DDD systems. Covers CQRS (Command Query Responsibility Segregation) and Event Sourcing patterns that often emerge from EventStorming workshops. Bridges collaborative design to technical implementation. Note: Leanpub work-in-progress. |

#### Videos

| Link                                                                                                                       | Our 2 cents (where applicable)                                                                                                |
| -------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| [What is Event Storming by Paul Rayner](https://www.youtube.com/watch?v=Y7NzXl-ahtU)                                       | -                                                                                                                             |
| [Event Storming Workshop @Bucharest Software Craftsmanship Community](https://youtu.be/xVSaDdj3PVE)                        | -                                                                                                                             |
| [Event Storming demo & discussion](https://youtu.be/xIB_VQVVWKk)                                                           | -                                                                                                                             |
| [Remote EventStorming: Redesigning Everything](https://www.youtube.com/watch?v=v4xLxmpAFdI)                                | This is mostly relevant for moderators. Additionally, at 49:55, Alberto explains how to extract backlog items from the board. |
| [Trying out online EventStorming](https://youtu.be/CbPEibNUe0s)                                                            | This is rather long, but includes some interesting meta discussions. Can be interesting for moderators.                       |
| [Event Storming - How to deal with complexity and improve your domain design](https://www.youtube.com/watch?v=R1UJS41I-Gc) | -                                                                                                                             |
| [Event Storming - Alberto Brandolini - DDD Europe 2019](https://www.youtube.com/watch?v=mLXQIYEwK24&t)                     | -                                                                                                                             |

## Courses

Of course there are also dedicated courses and learning paths available. They are usually paid offerings (maybe your company has a subscription) and go into the details quite quickly. They therefore are recommendations especially for more advanced learners who want to broaden and deepen their knowledge:

| Link                                                                                                      | Our 2 cents (where applicable) |
| --------------------------------------------------------------------------------------------------------- | ------------------------------ |
| [Pluralsight Learning Path: Domain-Driven Design](https://www.pluralsight.com/paths/domain-driven-design) | -                              |

## DDD and Legacy

The application of DDD on legacy software is a special topic, but of importance as most of us will not start on a green field. This section is dedicated to resources that cover this aspect.

### Books and Articles

| Book | Our 2 cents |
| ---- | ----------- |
| [Getting Started with DDD When Surrounded by Legacy Systems](https://www.domainlanguage.com/wp-content/uploads/2016/04/GettingStartedWithDDDWhenSurroundedByLegacySystemsV1.pdf) | Essential Eric Evans paper for brownfield DDD adoption. Practical guidance on introducing DDD concepts and patterns when working with existing systems. |
| Colla, P., & Acerbis, R. (2025). *Domain-Driven Refactoring: Enhancing Software Architecture and Design*. Packt Publishing. [Packt](https://www.packtpub.com/product/domain-driven-refactoring/9781835889107) | See DDD 301+ section. Focuses specifically on refactoring existing code using DDD principles. |
| Lilienthal, C., & Schwentner, H. (2023). *Domain-Driven Transformation: Monolith Breakup and the Building of Microservices*. dpunkt.verlag / Addison-Wesley Professional. [Amazon (German)](https://www.amazon.de/-/en/Carola-Lilienthal/dp/3864907985) | See DDD 301+ section. Comprehensive guide to organizational transformation and monolith decomposition using DDD. |

### Videos

| Link                                                                                                    | Our 2 cents (where applicable)                      |
| ------------------------------------------------------------------------------------------------------- | --------------------------------------------------- |
| [Eric Evans "Getting Started with DDD When Surrounded by Legacy Systems"](https://youtu.be/ZbnF0Dn6dAA) | in German; walk through the paper by Eberhard Wolff |

## Templates and Samples

If you want to facilitate a DDD or Event Storming workshop and are looking for templates and sample, you find useful resources here:

| Link                                                                                                                            | Our 2 cents (where applicable)                                                         |
| ------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------- |
| [Domain-Driven Design Starter Modelling Process](https://github.com/ddd-crew/ddd-starter-modelling-process)                     | Super valuable resource with tons of templates for an end-to-end DDD modeling process  |
| [DDD Toolbox - Event Storming](https://dddtoolbox.com/event-storming) ([Source Code](https://github.com/poulainpi/ddd-toolbox)) | Open-source Event Storming tool with modern web interface  (use on your own risk - not approved by SAP yet)      |

## DDD Community

Maybe you want to touch base with the DDD community or visit a conference. Then this section is the right place for you.

## Meetups

## Conferences

| Link                                                  | Our 2 cents (where applicable)                       |
| ----------------------------------------------------- | ---------------------------------------------------- |
| [Domain Driven Design Europe](https://dddeurope.com/) | **The** DDD conference in Europe, highly recommended |
| [KanDDDinsky](https://kandddinsky.de/)                | Annual Berlin-based DDD conference                   |

## Further DDD Goodies

As in every collection there might be some resources that are worth to mention, but do not perfectly fit into the structure. They are collected here as additional goodies

> 🧑‍💻 *Recommendation* The content here is not related to a "learning path" for DDD but complements it with further aspects and discussions.

### Books and Articles

🥺 Nothing here yet - maybe you have something for us see ["How to contribute"](#how-to-contribute).

#### Videos

| Link                                                                                            | Our 2 cents (where applicable)                                                              |
| ----------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| [Is Domain-Driven Design Overrated? (Stefan Tilkov at GOTO 2021)](https://youtu.be/ZZp9RQEGeqQ) | interesting talk around the sometimes maybe too evangelistic application of DDD in the wild |

## DDD Kata

We believe DDD is something that you must practice yourself to properly understand.
If you want to try out DDD in your team, we came up with a [DDD Kata](ddd-kata.md) that allows you to get hands-on experience.
Give it a shot!

## Support, Feedback, Contributing

Of course this list is open to contributions:

- If you find a bug 🐞 like a typo, missing link etc., please open a [bug](https://github.com/SAP/curated-resources-for-domain-driven-design/issues/new?assignees=&labels=bug&template=bug-report.yml&title=%5BBUG%5D+%3Ctitle%3E)
- If you like to have a resource added to the list 🚀, please open a [feature request](https://github.com/SAP/curated-resources-for-domain-driven-design/issues/new?assignees=&labels=enhancement&template=feature-request.yml&title=%5BFEATURE+REQUEST%5D+%3Ctitle%3E). We will review the contribution and add it.

In addition, we are alo leveraging [GitHub Discussions](https://github.com/SAP/curated-resources-for-domain-driven-design/discussions) to foster the exchange. In case you want to ask questions you’re wondering about, share ideas or engage with other community members, this is the place to go.

Your friendly DDD crew from the SAP neighborhood 😎

## Blog

1. [An Introduction to Domain-Driven Design](./blog/0001-ddd-introduction.md)
2. [The Core Concepts of Domain-Driven Design](./blog/0002-core-concepts.md)
3. [How to model Aggregates](./blog/0003-how-to-model-aggregates.md)
4. [How to develop Aggregates](./blog/0004-how-to-develop-aggregates.md)

## Code of Conduct

We as members, contributors, and leaders pledge to make participation in our community a harassment-free experience for everyone. By participating in this project, you agree to abide by its [Code of Conduct](CODE_OF_CONDUCT.md) at all times.

## Licensing

Copyright 2022 SAP SE or an SAP affiliate company and "Curated Resources for Domain-Driven Design (DDD)" contributors. Please see our [LICENSE](LICENSE) for copyright and license information. Detailed information including third-party components and their licensing/copyright information is available.
