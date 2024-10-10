# The Core Concepts of Domain-Driven Design

We all want to create better code as software development teams, and Domain-Driven Design (DDD) is one collaborative approach that can assist us in doing so. DDD, at its heart, is a methodology to software development that emphasizes the business area and the issues we're attempting to resolve rather than just the technical execution.

The ability to establish a shared language between business experts and team members with a technical background like developers is one of the main advantages of DDD. We can communicate and work together more effectively if we use words and ideas that everyone engaged in the endeavor is familiar with. This shared understanding plays a vital role in making sure that everyone is pursuing the same objectives and prevents misunderstandings.

Modular design is promoted by DDD, which is an additional advantage. By dividing a system down into smaller, more manageable components, we can think about it more readily and make changes without affecting other portions of the software. Long term, this should result in a more adaptable and manageable system.

Testing and feedback processes are also emphasized in DDD. We can make sure that we are creating the correct thing and moving closer to our objectives by regularly verifying our ideas and getting input from business users, domain experts, and technical peers.

At the heart of DDD are several core concepts, including:

## Strategic Design

Strategic design is a pillar of Domain-Driven Design (DDD) that focuses on defining the Bounded Contexts, Ubiquitous Language, and Context Maps of a project. It involves collaboration between domain experts and the technical team to ensure that the software model accurately reflects the business domain.

Bounded Context is one of the most important concepts of DDD. It represents a conceptual boundary within which a domain model is applicable. As you try to model a large domain, you may encounter difficulties because different groups of people may use subtly different terms and sentences. A Bounded Context helps to mitigate this issue by providing a linguistic delimitation where any use of vocabulary outside of that limit will probably mean something different.

Ubiquitous Language is another key concept in DDD. It is modeled within a Bounded Context and represents the terms and concepts of the business domain where there should be no ambiguity. The development of an efficient Ubiquitous Language requires an understanding of the business and should be developed in agreement with the entire project team.

Context Maps help to understand the relationships between different Bounded Contexts. There are several ways to relate Bounded Contexts, including Shared Kernel, Customer/Supplier, Conformist, Partner, and Anti-Corruption Layer.

In summary, strategic design in DDD involves defining the Bounded Contexts, Ubiquitous Language, and Context Maps of a project in collaboration with domain experts and the technical team. This helps to ensure that the software model accurately reflects the business domain.

## Tactical design

Tactical design in Domain-Driven Design (DDD) involves refining the domain model to a stage where it can be converted into working code. It is a set of design patterns and building blocks that can be used to design domain-driven systems.

Compared to strategic domain-driven design, tactical design is much more hands-on and closer to the actual code. It deals with classes and modules rather than abstract wholes.

One of the most important concepts in tactical DDD is the value object. A value object is an object whose value is of importance. This means that two value objects with the same value might be deemed the same and hence interchangeable. As a result, value objects should always be immutable.

Value objects are not only containers of data - they can also contain business logic. The fact that the value objects are also immutable makes the business operations both thread-safe and side-effect free.

Another important concept in tactical DDD is the aggregate. An aggregate defines a consistency boundary around one or more entities. Exactly one entity in an aggregate is the root. Lookup is done using the root entity's identifier. Any other entities in the aggregate are children of the root, and are referenced by following pointers from the root. As such, a very important correlate of this is that during communication between Bounded Contexts one context never explicitly references ids below the aggregate root's id.

## Ubiquitous language

Ubiquitous Language is a key concept of Domain-Driven Design (DDD). It is a common and consistent way of naming and describing the domain entities, rules, and scenarios.

The purpose of Ubiquitous Language is to build a language shared by the team, developers, domain experts, and other participants. It is modeled within a Bounded Context, where the terms and concepts of the business domain are identified, and there should be no ambiguity ².

Ubiquitous Language must be expressed in the Domain Model. It unites the people of the project team and eliminates inaccuracies and contradictions from domain experts.

Developing a clear Ubiquitous Language requires an understanding of the business. It evolves over time and is not defined entirely in a single meeting. Concepts that are not part of the Ubiquitous Language should be rejected.

## Domains and subdomains

Domains and Subdomains in Domain-Driven Design

In Domain-Driven Design (DDD), a domain is the most vital concept. It refers to the space of the problem for which we are acting, its aggregates and entities, its behavior and rules.

A domain can have several meanings within DDD. It can refer to the totality of the company's domain, an area, sector or process of the company, or a domain that serves as support for the business.

DDD necessitates the division of the domain into subdomains, which aids human comprehension. In this method, we can distinguish what actually provides value and financial return for the organization.

A subdomain is a domain division. Every domain, regardless of company size, can be subdivided. We separate the total complexity of the company's domain into smaller segments by doing so.

There are three types of subdomains: Core, Supporting, Generic. The Core subdomain is where we must put our best efforts. The Supporting subdomain complements the main domain. The Generic subdomain typically can be supported by ready-made commercial or open-source software or services.

### Core Domain

The core domain is where we want to excel as a business and our specific skills here really differentiate us from the rest of the market. It is so critical and fundamental to the business that it gives you a competitive advantage and is a foundational concept behind the business.

DDD advocates modeling based on the reality of business as relevant to your use cases. It describes independent problem areas as Bounded Contexts (each Bounded Context usually correlates to a microservice or a module within a well-structured monolith), and emphasizes a common language to talk about these problems.

The core domain gives you a competitive advantage and is a foundational concept behind the business.

### Supporting Domain

The supporting domain is key to providing value in the core domain. These types of pieces help perform ancillary or supporting functions related directly to what the business does.

In these cases, high-quality code and perfectly designed structure are not necessary. You could get by with assigning more inexperienced developers or even outsourcing these pieces. Just be sure that these concepts do not bleed into your core domain—you want to maintain a rigid separation with a context map to keep separate things separate. 

Note that even if you assign less experienced teams or outsource this work, it can be very advantageous to have automated test cases written by your core teams to ensure that any implementation of the subdomain fulfills the explicit business needs. This provides confidence in the correctness of the behavior and allows for future refactoring to improve the code quality or performance while retaining comfidence in its behavioral correctness.

### Generic Domain

The generic domain is an area where the market has expertise that we can exploit. When developing or redeveloping an enterprise application, there will be parts of the system that aid the business but are not critical to the operation.

Most businesses, for example, have a concept of invoicing—sending bills to customers. While this is a critical business concept, it is not "core" to the organization. In general, these elements can be acquired from a vendor or outsourced and then packaged in such a way that they can connect with the rest of the organization as needed.

The generic domain leverages expertise in the market for areas that facilitate the business but are not core to it.

## Events and commands

Domain events and commands are two key concepts in domain-driven design (DDD), a software development approach that focuses on the core business domain and its logic.

Domain events are facts that have happened in the past and affect the state of the domain, such as an order placed or a payment received. An important benefit of domain events is that side effects can be expressed explicitly.

A command is a message that is sent to the domain expressing an intention to change state or invoke some behavior. A command is processed by a dedicated command handler. A command should be named with a verb in an imperative mood plus the aggregate name which it operates on. A command request can be rejected due to the data the command holds being invalid/inconsistent. There should be exactly 1 handler for each command.

Events and commands express side effects explicitly and handling state changes in the domain.

## Bounded Contexts

Bounded Context is a central pattern in Domain-Driven Design (DDD). It is the focus of DDD's strategic design section which is all about dealing with large models and teams.

DDD deals with large models by dividing them into different Bounded Contexts and being explicit about their interrelationships. A Bounded Context is primarily a linguistic delimitation, that is to say that terms and sentences can mean different things, according to the context in which they are employed.

This linguistic delimitation refers to ubiquitous language, which is another essential element in DDD. It is also important to understand that Bounded Context is where the Model is implemented, that is, a Bounded Context is the solution implementation in a technical way.

Bounded Contexts divide large models into different contexts and being explicit about their interrelationships.

## Aggregates

A DDD aggregate is a cluster of domain objects that can be treated as a single unit.

An example may be an order and its line-items, these will be separate objects, but it's useful to treat the order (together with its line items) as a single aggregate. An aggregate will have one of its component objects be the aggregate root ¹.

Any references from outside the aggregate should only go to the aggregate root. The root can thus ensure the integrity of the aggregate as a whole. Aggregates are the basic element of transfer of data storage - you request to load or save whole aggregates. Transactions should not cross aggregate boundaries ¹.

Aggregates treat a cluster of domain objects as a single unit.

## Conclusion

We can begin to implement DDD principles to our own projects and enjoy the advantages that come with it once we have a solid grasp of these ideas and how they work together. Finally, Domain-Driven Design is a potent method of software development that can aid groups in producing better, more enduring code. We can build a more collaborative and adaptable development process by concentrating on the business area and employing a shared language. The first step to implementing DDD in our own initiatives and gaining these advantages is comprehending its fundamental ideas.

## Resources

- [What is Strategic Design ? - DDD - The Domain Driven Design](https://thedomaindrivendesign.io/what-is-strategic-design/)
- [DDD Part 1: Strategic Domain-Driven Design | Vaadin](https://vaadin.com/blog/ddd-part-1-strategic-domain-driven-design)
- [I. Strategic Design - Learning Domain-Driven Design [Book]](https://www.oreilly.com/library/view/learning-domain-driven-design/9781098100124/part01.html)
- [Strategic Domain-Driven Design - Medium.](https://medium.com/@chatuev/ddd-for-microservices-4778a363c071).
- [Using tactical DDD to design microservices - Azure Architecture Center](https://learn.microsoft.com/en-us/azure/architecture/microservices/model/tactical-ddd)
- [DDD Part 2: Tactical Domain-Driven Design | Vaadin](https://vaadin.com/blog/ddd-part-2-tactical-domain-driven-design)
- [Domain-Driven Design Part II: Tactical Design | by Can Güt | Medium](https://medium.com/@lifelongstudent/domain-driven-design-part-ii-tactical-design-16bc527c6263)
- [Ubiquitous Language: Documenting and Communicating Tips - LinkedIn](https://www.linkedin.com/advice/0/how-do-you-document-communicate-your-ubiquitous)
- [Developing the ubiquitous language - DDD - The Domain Driven Design](https://thedomaindrivendesign.io/developing-the-ubiquitous-language)
- [UbiquitousLanguage - Martin Fowler](https://www.martinfowler.com/bliki/UbiquitousLanguage.html)
- [Domain-driven design - Wikipedia](https://en.wikipedia.org/wiki/Domain-driven_design)
- [Domains and Subdomains - DDD - The Domain Driven Design](https://thedomaindrivendesign.io/domains-and-subdomains/)
- [Domain, Subdomain, Bounded Context, Problem/Solution Space in ... - Medium](https://medium.com/nick-tune-tech-strategy-blog/domains-subdomain-problem-solution-space-in-ddd-clearly-defined-e0b49c7b586c)
- [Domain-Driven Design for Microservice Decomposition - LinkedIn](https://www.linkedin.com/advice/1/how-do-you-apply-principles-domain-driven)
- [Domain Driven Design (DDD): Core concepts and Enterprise Architecture](https://alok-mishra.com/2021/06/30/domain-driven-design-ddd-core-concepts-explained/)
- [DDD: Strategic Design: Core, Supporting, and Generic Subdomains](https://blog.jonathanoliver.com/ddd-strategic-design-core-supporting-and-generic-subdomains/)
- [Designing a DDD-oriented microservice | Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/architecture/microservices/microservice-ddd-cqrs-patterns/ddd-oriented-microservice)
- [Domain Event vs Command: Versioning and Evolution in DDD - LinkedIn](https://www.linkedin.com/advice/1/how-do-you-evolve-version-domain-events)
- [Domain events: Design and implementation | Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/architecture/microservices/microservice-ddd-cqrs-patterns/domain-events-design-implementation)
- [Command vs. Event in Domain Driven Design - Medium](https://medium.com/ingeniouslysimple/command-vs-event-in-domain-driven-design-be6c45be52a9)
- [BoundedContext - Martin Fowler.](https://www.martinfowler.com/bliki/BoundedContext.html)
- [Bounded Context - DDD - The Domain Driven Design](https://thedomaindrivendesign.io/bounded-context/).
- [Balancing Consistency and Autonomy in Bounded Contexts - LinkedIn.](https://www.linkedin.com/advice/0/how-do-you-balance-between-consistency-autonomy)
- [DDD_Aggregate - Martin Fowler](https://www.martinfowler.com/bliki/DDD_Aggregate.html)
- [What Are Aggregates In Domain-Driven Design? - James Hickey](https://www.jamesmichaelhickey.com/domain-driven-design-aggregates/)
- [Understanding Aggregates in Domain-Driven Design - DZone](https://dzone.com/articles/domain-driven-design-aggregate)
- [domain driven design - What's the difference between an Aggregate and a ...](https://softwareengineering.stackexchange.com/questions/443173/whats-the-difference-between-an-aggregate-and-a-model)

