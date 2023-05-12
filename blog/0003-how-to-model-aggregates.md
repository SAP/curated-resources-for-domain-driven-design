# Aggregates: How to Model Complex Domains with Consistency and Cohesion

## Introduction

Domain-Driven Design (DDD) places more emphasis on conceptual modeling of the issue domain than it does on implementation and technical specifics.
The business logic and domain rules are captured in expressive, consistent, and coherent domain models.

The aggregate is a collection of domain objects that is handled as a single unit.
It is one of the essential (tactical) patterns in DDD.
This blog article will explain what aggregates are and how to discover them. 
We present an example how you can implement an aggregate in [the next article](0004-how-to-develop-aggregates.md).

## What Are Domain Invariants, and Why Do They Matter?

The business rules and restrictions that must always apply in the domain are known as domain invariants.
They reflect the domain's fundamental logic and presumptions, ensuring the accuracy and integrity of the domain model and the data.
For instance, a domain invariant in the banking domain may be that a bank account's balance may not be negative.
Or, in e-commerce, there may be the invariant that an order cannot have a negative total amount.

Domain invariants are significant, since they help in defining the boundaries and behaviors of the domain objects and aggregates.
Also, they help us to prevent our system from entering faulty or inconsistent states.
Any action that would contradict, for instance, the domain invariant that an order cannot have a negative total amount should be blocked or rejected by the order aggregate.

The expression of domain invariants can take many forms, including preconditions, postconditions, assertions, validations, exceptions, etc.
Making them clear and enforcing them inside the domain model is crucial.
Depending on the degree of consistency and performance demanded by the domain, domain invariants may also differ in their extent and amount of detail.
While certain domain invariants may only apply to a single entity or value object, others may span an entire aggregate or even several aggregates.
It is important to figure out which invariants are truly invariant, i.e. must never be violated, and for which invariants temporal inconsistencies can be tolerated by the business.
If an invariant may never be violated, we must protect it with an aggregate.
Otherwise, we can use domain events to communicate state changes between aggregates and live with the system being eventually consistent.

## How to Discover Aggregates and Their Limits?

One of the hardest and most crucial jobs in DDD is identifying aggregates and their bounds.
Aggregates are significant clusters of domain items that change collectively and provide a consistency boundary, not merely random groupings of domain objects.
Aggregates should be built to safeguard and enforce domain invariants while allowing for eventual or asynchronous consistency of other aggregates.

There are different techniques and heuristics that can help to identify aggregates and their boundaries.

Using the ubiquitous language and the domain experts' knowledge to identify the main concepts and relationships in the domain.
The ubiquitous language is the common and expressive language that is used by the domain experts and the developers to communicate about the domain. 
It can help to discover the nouns and verbs of the domain, which can be mapped to entities, value objects, and behaviors.
Domain experts can also provide valuable insights and feedback on how the domain works and what are the important rules and constraints.

Identifying the interactions and behaviors of domain objects using scenarios and use cases.
Use cases and scenarios both describe how domain objects work together to complete a task or deal with a problem.
The people, activities, inputs, outputs, and consequences of the domain may be identified with the use of scenarios and use cases.
Also, they can aid in locating the causal and temporal relationships between domain items, which may point to prospective aggregates.

Finding groups of domain objects that change collectively and build aggregates using domain invariants. 
The business laws and restrictions that must always apply in the domain are known as domain invariants. 
By assembling domain objects that have common invariants and must always be consistent, domain invariants can aid in the identification of aggregates.
For instance, if a domain invariant of an order states that it cannot have a negative total amount, then all of the order's line items must be a part of the same aggregate.

Reducing the complexity and size of aggregates using qualifiers and restrictions.
Additional criteria or conditions, like constraints and qualifiers, can be used to restrict or filter the associations between domain items.
By removing pointless or superfluous linkages or dependencies, qualifiers and constraints can aid in reducing the complexity and size of aggregates.
A qualifier like "active" might be used to lower the size of the team aggregate, for instance, if a team has numerous staff members affiliated with it but only part of them are active at any one moment.

Using these techniques and heuristics, we may find aggregates and their limitations in a variety of domains.
Yet, since aggregates and their bounds depend on the circumstances and requirements of each domain, there is no precise or standardized way to identify them.
Thus it's essential to test out several designs and evaluate them based on things like expressiveness, consistency, performance, scalability, etc.

## How to Design Aggregates and Their Roots?

Each aggregate has a single, designated root entity.
The aggregate root is responsible for encapsulating the aggregate's state and behavior, and ensuring its consistency and validity.
That means that the domain model should make it impossible to modify an aggregate's state except via the public API exposed by the aggregate.
Aggregates can only be referenced to by the identity of the aggregate root.

The aggregate root's interface and methods should reflect the language and domain concepts, follow the principle of least astonishment, and the command-query separation principle.
Relationships with other aggregates should be modelled using references or identifiers.
References or identifiers are simple values that represent the identity of another aggregate, without exposing its internal structure or state. 

Other criteria like expressiveness, consistency, performance, scalability, etc. can be relevant for aggregate design, but are beyond the scope of this blog post.

## Conclusion

Aggregates are groups of domain objects that can be handled as a single entity and can protect and enforce the domain invariants.
They are designed using the ubiquitous language, the ideas and laws of the domain, the scenarios and use cases, and the domain invariants.
They can help build expressive, coherent domain models, reduce complexity, and improve efficiency.

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
