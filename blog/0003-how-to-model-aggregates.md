# Aggregates: How to Model Complex Domains with Consistency and Cohesion

## Introduction

Domain-Driven Design (DDD) places more emphasis on conceptual modeling of the issue domain than it does on implementation and technical specifics. The business logic and domain rules are captured in expressive, consistent, and coherent domain models that are produced with the aid of DDD. The aggregate, which is a collection of domain objects that may be handled as a single entity, is one of the essential patterns in DDD. This blog article will go over aggregates, their importance, how to build them, and how to use various technologies to execute them. You will have a better knowledge of how to utilize aggregates to represent complicated domains with consistency and cohesion by the end of this blog article.

## What Are Domain Invariants, and Why Do They Matter?

The business rules and restrictions that must always apply in the domain are known as domain invariants. They reflect the domain's fundamental logic and presumptions, ensuring the accuracy and integrity of the domain model and the data. For instance, a domain invariant in the banking industry may be the prohibition of negative balances on bank accounts. The fact that an order cannot have a negative total amount may be a domain invariant in the e-commerce industry.

Since they help in defining the boundaries and behaviors of the domain objects and aggregates, domain invariants are significant. Also, they aid in stopping the domain model's faulty or inconsistent states and activities. Any action that would contradict, for instance, the domain invariant that an order cannot have a negative total amount should be blocked or rejected by the order aggregate.

The expression of domain invariants can take many forms, including preconditions, postconditions, assertions, validations, exceptions, etc. Making them clear and enforcing them inside the domain model is crucial. Depending on the degree of consistency and performance demanded by the domain, domain invariants may also differ in their extent and amount of detail. As an illustration, whereas certain domain invariants may only apply to a single entity or value object, others may do so for an entire aggregate or even several aggregates.

## How to Discover Aggregates and Their Limits?

One of the hardest and most crucial jobs in Domain-Driven Design is identifying aggregates and their bounds. Aggregates are significant clusters of domain items that change collectively and provide a consistency boundary, not merely random groupings of domain objects. Aggregates should be built to safeguard and enforce the domain invariants contained inside them while allowing for eventual or asynchronous consistency of other aggregates.

There are different techniques and heuristics that can help to identify aggregates and their boundaries, such as:

- Using the ubiquitous language and the domain experts' knowledge to identify the main concepts and relationships in the domain. The ubiquitous language is the common and expressive language that is used by the domain experts and the developers to communicate about the domain. The ubiquitous language can help to discover the nouns and verbs of the domain, which can be mapped to entities, value objects, and behaviors. The domain experts can also provide valuable insights and feedback on how the domain works and what are the important rules and constraints.

- Identifying the interactions and behaviors of the domain objects using scenarios and use cases. Use cases and scenarios both describe how domain objects work together to complete a task or deal with a problem. The people, activities, inputs, outputs, and consequences of the domain may be identified with the use of scenarios and use cases. Also, they can aid in locating the causal and temporal relationships between domain items, which may point to prospective aggregates.

- Finding groups of domain objects that change collectively and build aggregates using domain invariants. The business laws and restrictions that must always apply in the domain are known as domain invariants. By assembling domain objects that have common invariants and must always be consistent, domain invariants can aid in the identification of aggregates. For instance, if a domain invariant of an order states that it cannot have a negative total amount, then all of the order's line items must be a part of the same aggregate.

- Reducing the complexity and size of aggregates using qualifiers and restrictions. Additional criteria or conditions, like constraints and qualifiers, can be used to restrict or filter the associations between domain items. By removing pointless or superfluous linkages or dependencies, qualifiers and constraints can aid in reducing the complexity and size of aggregates. A qualifier like "active" might be used to lower the size of the team aggregate, for instance, if a team has numerous staff members affiliated with it but only part of them are active at any one moment.

Using these techniques and heuristics, we may find aggregates and their limitations in a variety of domains. Yet, since aggregates and their bounds depend on the circumstances and requirements of each domain, there is no precise or standardized way to identify them. Thus it's essential to test out several designs and evaluate them based on things like expressiveness, consistency, performance, scalability, etc.

## How to Design Aggregates and Their Roots?

Once we have identified the aggregates and their boundaries in our domain, we need to design them and their roots. An aggregate root is the entity or value object that acts as a single point of access and control for the aggregate. The aggregate root is responsible for encapsulating the aggregate's state and behavior, and ensuring its consistency and validity. The aggregate root is also the only object that can be directly referenced by other aggregates, using its identity or identifier.

There are different aspects and considerations that we need to take into account when designing aggregates and their roots, such as:

- Selecting an entity or value object based on its identity, lifetime, and responsibilities as an aggregate root. An item with a distinct identity and a changeable state is called an entity. An object with an unchanging state and no identity is referred to as a value object. If an entity has a unique identity that sets it apart from other entities of the same kind and a lengthy or complex lifespan with numerous modifications and interactions, it may be a good candidate for an aggregate root. If a value object has a brief or simple lifespan and no identification or if its identity is unimportant, it may be a good candidate for an aggregate root.

- Designing the aggregate root's interface and methods to encapsulate the aggregate's state and behavior. The aggregate root's interface and methods should reflect the ubiquitous language and the domain concepts, rather than the technical details or implementation. The aggregate root's interface and methods should also follow the principle of least astonishment, meaning that they should behave in a way that is expected and consistent with the domain. The aggregate root's methods should also follow the command-query separation principle, meaning that they should either change the state of the aggregate (commands) or return information about the state of the aggregate (queries), but not both.

- Designing the aggregate root's relationships with other aggregates using references or identifiers. The aggregate root's relationships with other aggregates should be based on the domain concepts and rules, rather than on the data model or persistence technology. The aggregate root's relationships with other aggregates should also be as loose and decoupled as possible, to avoid unnecessary dependencies or coupling. One way to achieve this is to use references or identifiers to link aggregates, rather than direct object references or pointers. References or identifiers are simple values that represent the identity of another aggregate, without exposing its internal structure or state. References or identifiers can also facilitate asynchronous or eventual consistency between aggregates, by allowing them to communicate through messages or events.

We may create aggregates and their antecedents in many different fields using these elements and problems. The context and requirements of each domain determine aggregates and their roots. There is no easy way to design aggregates, you can use following criteria like expressiveness, consistency, performance, scalability, etc. to design them.

## How to Implement Aggregates and Their Persistence?

After designing the aggregates and their roots in our domain, we must implement them and ensure their persistence. Choosing the programming languages, frameworks, and data storage technologies that best meet our domain and requirements is the first step in implementing aggregates and their durability:

- Object-oriented programming languages and frameworks can be used to implement aggregates. They deliver the capabilities and object-oriented patterns that we require for our domain to build aggregates. Object-oriented programming languages and frameworks often employ object-relational mapping (ORM) tools or libraries to facilitate the mapping of the domain model to the data model.

- Using functional programming languages and frameworks to implement aggregates. Functions, expressions, immutability, purity, recursion, higher-order functions, and other related ideas constitute the foundation of functional programming languages and frameworks. If they provide the features and patterns that we want for our domain, such as records, unions, pattern matching, partial application, currying, etc., functional programming languages and frameworks might be an excellent alternative for developing aggregates. By utilizing event streams or observables, functional programming languages and frameworks can aid in the construction of event sourcing or reactive systems.

- Long-term aggregates may require specific data persistence technique such as relational databases, document databases, key-value stores, graph databases, event stores, and so on. Depending on the requirements of our domain, they have to provide capabilities, such as transactions, concurrency management, indexing, querying, caching, replication, sharding, and so on,to become a viable alternative for preserving aggregates. Data persistence strategies are crucial to ensure the the integrity and performance of our aggregates by applying the correct consistency mechanism.

We can create aggregates and their durability using various technologies by taking these options and trade-offs into account. Since aggregates and their persistence depend on the context and needs of each domain, there is no clear-cut or universal approach to their implementation. Here,you should try out several technologies and assess them according to the factors mentioned above like expressiveness, consistency, performance, scalability, etc.

## Conclusion

We have examined aggregates in this blog article, including what they are, why they are significant, how to design them, and how to use various technologies to create them. Aggregates are groups of domain objects that may be handled as a single entity and can safeguard and enforce the domain invariants inside their borders, according to what we have learnt. We have also discovered that the ubiquitous language, the ideas and laws of the domain, the scenarios and use cases, and the domain invariants are all used in the design and implementation of aggregates. According to the situation and demands of each area, aggregates can be developed and maintained utilizing a variety of programming languages, frameworks, and data storage systems.

We may build expressive, coherent domain models that represent the rules and business logic of the domain by utilizing aggregates. By lowering the size and quantity of linkages and dependencies between domain objects, aggregates may also assist us in solving complexity and enhancing the efficiency of our domain models. By utilizing references or IDs, messages or events, transactions, or eventual consistency, aggregates can also assist us in achieving various levels of consistency across aggregates.

## Further References and Resources

- Books:
  - Domain-Driven Design: Tackling Complexity in the Heart of Software by Eric Evans
  - Implementing Domain-Driven Design by Vaughn Vernon
  - Domain-Driven Design Reference by Eric Evans
  - Domain-Driven Design Distilled by Vaughn Vernon
- Blogs
  - <https://www.jamesmichaelhickey.com/domain-driven-design-aggregates/>
  - <https://dzone.com/articles/domain-driven-design-aggregate>
  - <https://www.martinfowler.com/bliki/DDD_Aggregate.html>
- Youtube
  - Vaughn Vernon - How to Use Aggregates for Tactical Design: <https://www.youtube.com/watch?v=Xf_aLAK1RfE>
  - Vaughn Version - Effective Aggregate Design Part II: <https://www.youtube.com/watch?v=JOsv01y8dlw>
  - Thomas Ploch: The One Question To Haunt Everyone: What is a DDD Aggregate? - Thomas Ploch - DDD Europe 2022: <https://www.youtube.com/watch?v=zlFqjD2LKlE>
  - Codewrinkles: M****ing DDD Aggregate Modeling With THESE 3 Steps: <https://www.youtube.com/watch?v=E2ctgrKhqBw>
  - Amichai Mantinband: Aggregates, Entities & Value Objects | Modeling Rules of Thumb + Modeling Steps: <https://www.youtube.com/watch?v=UEtmOW8uZZY>
  - Milan Jovanović: Aggregate Root Design 101 | DDD, Clean Architecture, .NET 6 - <https://www.youtube.com/watch?v=0D3EB2jvQ44>
