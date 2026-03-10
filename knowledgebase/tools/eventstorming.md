# Event Storming

## What is Event Storming?

Event Storming is a rapid, collaborative workshop technique for exploring complex business domains and software requirements. Created by Alberto Brandolini in 2013, it brings together domain experts, developers, and stakeholders to build a shared understanding of how a business process works by focusing on **Domain Events**—things that happen in the domain.

The technique uses colored sticky notes on a large surface (physical wall or virtual whiteboard) to create a visual, temporal model of a business process. It is called "storming" because it is fast, energetic, and leverages group intelligence to rapidly uncover domain complexity.

Event Storming can be used for different purposes, such as:

- Assessing the health of an existing line of business and discovering the most effective areas for improvements
- Exploring the viability of a new startup business model
- Envisioning new services that maximize positive outcomes to every party involved
- Designing clean and maintainable event-driven software to support rapidly evolving businesses

## Why Event Storming?

Event Storming addresses several critical problems in software development:

1. **Communication Gap**: Bridges domain experts and developers through visual, concrete examples
2. **Hidden Complexity**: Surfaces implicit knowledge, edge cases, and business rules that don't appear in documentation
3. **Shared Understanding**: Creates [Ubiquitous Language](../concepts/strategic-concepts/ubiquitouslanguage.md) through collaborative exploration
4. **Rapid Discovery**: Achieves in 4-8 hours what might take weeks of interviews
5. **Domain Boundaries**: Reveals natural [Bounded Contexts](../concepts/strategic-concepts/boundedcontext.md) through clustering of related events

**Core Principle**: Focus on **what happens** (events), not what something **is** (data structures). Events are the language of the business and reveal true domain complexity.

## How did Event Storming come to be?

Event Storming was invented by Alberto Brandolini, an Italian programmer and consultant, in 2013. Event Storming is inspired by Daniel Kahneman's *Thinking, Fast and Slow*, a book about cognitive biases and decision making. Brandolini came up with the idea of using sticky notes to capture the essence of a complex domain, and to expose the hidden assumptions and contradictions. He called his method Event Storming, to emphasize the focus on domain events and the similarity to brainstorming or agile modeling's model storming. Brandolini started to use Event Storming in his consulting work, and soon it became popular among the DDD community and beyond.

## Elements of Event Storming

![Grammar](./images/Restaurant%20DDD%20Kata%20Example%20Grammar.png)

| Element         | Symbol                        | Description                                                                                                                                                                                                                                                                                                                                                  |
| --------------- | ----------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Domain Event    | Orange Sticky                 | A domain event is something that happened in the domain that is relevant for the domain experts or the system. It is usually represented by a past-tense verb and some data. For example: "Order Placed", "Customer Registered", "Payment Processed".                                                                                                        |
| Policy          | Purple Sticky                 | A policy is a rule or a set of rules that governs the behavior of the system or a part of it. It is usually expressed in terms of domain events and commands. For example: "When an order is placed, send a confirmation email to the customer", "When a payment is overdue, cancel the order and notify the customer".                                      |
| Command         | Blue Sticky                    | A command is a request or an instruction to change the state of the system or a part of it. It is usually represented by an imperative verb and some data. For example: "Place Order", "Register Customer", "Process Payment".                                                                                                                               |
| Aggregate       | Yellow rectangle Sticky       | An aggregate is a cluster of domain objects that can be treated as a single unit. It has a root entity and a boundary that defines what is inside the aggregate and what is outside. It enforces the invariants of the domain and ensures consistency. For example: "Order", "Customer", "Payment".                                                          |
| Read Model      | Green Sticky                  | A query or data is a request or an instruction to read the state of the system or a part of it. It is usually represented by a noun or a question and some data. For example: "Order Details", "Customer Profile", "Payment Status".                                                                                                                         |
| External System | Pink Rectangle Sticky         | An external system is a system that is outside the boundary of the domain model and interacts with it through interfaces. It can be a source of domain events or a target of commands or queries. For example: "Email Service", "Payment Gateway", "Inventory System".                                                                                       |
| Actor/User      | Small Yellow Sticky                  | An actor or user is a person or system that performs commands. For example: "Customer", "Sales Manager", "Warehouse Staff", "Payment Gateway".                                                                                |
| UI              | White Sticky                  | A UI is a user interface that allows users to interact with the system. It can be a web page, a mobile app, a desktop application, or any other form of presentation. It can display domain events, send commands or queries, and receive responses from the system. For example: "Order Page", "Customer Registration Form", "Payment Confirmation Screen". |
| Hotspot         | Red/Dark Purple Sticky 45° turned | A hotspot is a concept in Event Storming that is used to visualize and capture hot conflicts. Conflicts caused by, and not exclusive to, inconsistencies (in language), frictions, questions, dissent, objections, issues or procrastinating going deep to explore for later.                                                                                 |
| Pivotal Events  | Yellow long rectangle blocks  | Pivotal Events in Event Storming are significant occurrences that change the course of the business process. They are often the events with the highest number of people interested and can trigger reactions in other departments.                                                                                                                          |

## Event Storming Formats

Event Storming has different formats depending on the goal:

### 1. Big Picture Event Storming (4-8 hours)

**Goal**: Explore the entire business domain at high level

**Participants**: 10-30 people (domain experts, developers, managers, stakeholders)

**Outcome**: Complete domain timeline, identified bounded contexts, list of hot spots

**Use When**:
- Starting a new project
- Understanding a complex legacy system
- Organizational alignment on domain scope
- Assessing the health of an existing line of business

### 2. Process Modeling Event Storming (4-6 hours)

**Goal**: Deep dive into a specific business process

**Participants**: 5-12 people (domain experts, developers for that process)

**Outcome**: Detailed command-event flow, policies, aggregates, external systems

**Use When**:
- Designing a new feature
- Refactoring existing process
- Preparing for implementation sprint
- Exploring edge cases and error scenarios

### 3. Software Design Event Storming (2-4 hours)

**Goal**: Transition from domain model to software design

**Participants**: Development team + 1-2 domain experts

**Outcome**: Aggregate boundaries, commands, events, policies mapped to code structure

**Use When**:
- After Process Modeling, before coding
- Designing microservices boundaries
- Creating event-sourced systems
- Defining API contracts

## What do you need for an Event Storming workshop?

To run an Event Storming workshop, you will need the following:

- **A facilitator**: The facilitator is the person who guides the workshop and ensures that everyone is engaged and productive. The facilitator should have some knowledge of the domain and the process that is being analyzed, but not too much, so that they can ask the right questions and challenge the assumptions.
- **The right people**: The participants are the people who have the domain knowledge and the expertise to model the domain and the process. They should include domain experts, developers, testers, product owners, business analysts, and any other relevant stakeholders. The ideal number of participants is between 6 and 12, but it can vary depending on the scope and complexity of the domain.
- **A modeling space**: The modeling space is the place where the participants will write down and arrange the sticky notes that represent the events and other elements of the domain. The modeling space should be large enough to accommodate all the sticky notes and allow the participants to move around and interact with each other. A wall or a whiteboard is a good option for the modeling space. For remote workshops, use tools like Miro, Mural, or FigJam.
- **Sticky notes**: The sticky notes are the main tool for modeling the domain and the process. They should be of different colors and shapes to represent different types of elements, such as events, commands, aggregates, policies, external systems, users, etc. The sticky notes should be easy to write on and stick to the modeling space. You will need a lot of sticky notes, so make sure you have enough supply.
- **Markers**: The markers are used to write on the sticky notes and to draw arrows or lines to show the relationships between the elements. The markers should be of different colors to match the sticky notes and to make the model more readable. The markers should be easy to hold and write with, and have a fine tip to fit the text on the sticky notes.

## How to run a Big Picture Event Storming workshop

The Big Picture Event Storming aims to identify the main domains and subdomains that are involved in the business process or the business application that is being analyzed. The Event Storming workshop consists of these steps:

### Phase 1: Chaotic Exploration (60-90 min)

![Chaotic Exploration](./images/Restaurant%20DDD%20Kata%20Example_Chaotic_Exploration.png)

**Goal**: Brain dump ALL domain events without structure

As a facilitator, you provide an overview, outlining objectives and guidelines for the workshop. Request participants to use sticky notes to jot down pertinent events in the domain and the studied process.

**Instructions**:
1. Explain: "Write down everything that happens in this domain on orange sticky notes. Use past tense. No discussion, just write and stick."
2. Use a verb and a noun in the past tense, such as "Coffee Ordered," "Order Handed Out," or "Order Requested"
3. Participants silently write events (1 event per note): `OrderPlaced`, `PaymentFailed`, `CustomerRegistered`
4. Everyone sticks notes on wall in approximate chronological order (left to right)
5. Without editing or passing judgment, invite participants to record as many experiences as they can recall
6. Instruct participants to place their sticky notes on the modeling surface in whatever order they prefer, creating a disorganized cloud of questions and occurrences

**Facilitator Tips**:
- Encourage silence initially (prevents groupthink)
- Keep energy high ("Don't stop! Keep writing!")
- Watch for duplicates (it's okay for now)
- Look for participants not contributing—invite them

**Output**: 50-200 orange sticky notes covering the wall

### Phase 2: Enforce the Timeline (45-60 min)

![Enforce the timeline](./images/Restaurant%20DDD%20Kata%20Example_Enforce_Timeline.png)

**Goal**: Arrange events in strict chronological order

Instruct the participants to organize the sticky notes chronologically on the modeling space, moving from left to right.

**Instructions**:
1. "Now let's organize. Which event happens FIRST in the domain?"
2. Assist them in identifying the starting and ending points of the process, aligning events and questions along a horizontal line
3. Group discusses and moves events left-to-right in time order
4. Identify parallel flows (events happening simultaneously in different parts of domain)
5. Guide participants in identifying gaps, duplicates, inconsistencies, or ambiguities in the events and questions
6. Encourage collaboration among participants to resolve these issues
7. Ask participants to use arrows or lines to illustrate causal relationships between events, for example, "Table Assigned → Order Requested → Coffee Ordered"
8. Remove duplicate events (consolidate similar concepts)
9. Mark questions or doubts as "hotspots". These have to be answered or resolved later before the Event Storming Workshop is over

**Questions to Ask**:
- "What happens next?"
- "What happens before this?"
- "What triggers this event?"
- "Can these happen in different orders?"

**Output**: Organized timeline with clear start and end points

### Phase 3: Enforce Consistency (30-45 min)

![Enforce Consistency](./images/Restaurant%20DDD%20Kata%20Example_Enforce_Consistency.png)

**Goal**: Validate and refine the timeline

Please instruct participants to review the timeline and assess its accuracy in portraying the process and domain.
Encourage them to ask questions such as "What happens next?" "What triggers this event?" and similar inquiries. Do not shy away from renaming, removing or reordering events.

### Phase 4: Add Commands and Actors (45-60 min)

**Goal**: Identify WHO does WHAT to cause events

**Instructions**:
1. For each event (or cluster of events), ask: "What action caused this?"
2. Write command on blue sticky note, place it **before** the event
3. Write actor on small yellow sticky note, place it **above** the command
4. Pattern: `[Actor] → [Command] → [Event]`

**Example**:
```
[Customer] → [PlaceOrder] → [OrderPlaced]
[Warehouse Staff] → [PickItems] → [ItemsPicked]
```

**Output**: Commands and actors for all major events

### Phase 5: Discover Policies and Read Models (45-60 min)

**Goal**: Surface business rules and information needs

**Instructions for Policies**:
1. Look for automatic reactions: "When X happens, then Y happens"
2. Write policy on lilac/purple sticky note: "When [Event], then [Command]"
3. Place between event and resulting command

**Example**:
```
[PaymentReceived] → [Policy: "When payment received, confirm order"] → [ConfirmOrder] → [OrderConfirmed]
```

**Instructions for Read Models**:
1. Ask: "What information does the actor need to make this decision?"
2. Write read model on green sticky note, place **before** command
3. Example: Actor needs `AvailableInventory` to execute `PlaceOrder` command

**Output**: Business rules made explicit, information dependencies visible

### Phase 6: Identify the Bounded Contexts (60-90 min)

![Identify the Bounded Contexts](./images/Restaurant%20DDD%20Kata%20Example_Identify_Bounded_Contexts.png)

**Goal**: Find natural boundaries where domain splits

As a facilitator, instruct participants to group events and other elements into logical clusters representing different subdomains or areas of responsibility within the domain.

**Instructions**:
1. Look for clusters of related events and commands
2. These clusters are referred to as bounded contexts—a coherent and consistent set of events and elements sharing a common language and meaning
3. Guide participants in identifying the boundaries of each bounded context, using different shapes or colors to highlight them
4. Draw boxes around clusters with masking tape or virtual boundaries
5. Assist participants in naming each bounded context and labeling its main purpose or goal
6. Name each cluster (potential bounded context): `Order Management`, `Inventory`, `Shipping`, `Billing`
7. Identify events that cross boundaries (integration points)

For instance, direct participants to identify the "Delivery and Payment" bounded context, responsible for managing delivery of food and payments. Instruct them to use the long rectangle yellow blocks to mark boundary. After identifying them, they can draw boxes to capture Bounded Contexts with a semantic relevant and speaking name.

**Heuristics for Boundaries**:
- Different teams own different clusters
- Different vocabularies (same word, different meaning)
- Natural transaction boundaries (these events must be consistent)
- Different rates of change

**Output**: 3-8 bounded contexts with clear names and boundaries

### Phase 7: Surface Hot Spots (30 min)

**Goal**: Capture problems, questions, and conflicts

**Instructions**:
1. Ask: "What are we unsure about? Where might things go wrong?"
2. Write hot spots on red sticky notes (or dark purple sticky notes turned 45°)
3. Examples:
   - "What if payment fails after 3 days?"
   - "Inventory vs. Order Management: who owns stock allocation?"
   - "This policy contradicts that policy"

**Output**: Prioritized list of issues to investigate

### Phase 8: Wrap-Up and Next Steps (30 min)

**Facilitator Actions**:
1. Take photos of the wall (or export virtual board)
2. Document context map showing relationships between bounded contexts
3. Assign owners to hot spots for follow-up
4. Schedule follow-up: Process Modeling sessions for critical contexts

**Deliverables**:
- Event timeline (100-200 events)
- Context map (3-8 bounded contexts)
- Hot spot list (10-30 issues)
- Ubiquitous Language glossary (start)

## Process Modeling Event Storming: Detailed Design

After identifying bounded contexts in Big Picture Event Storming, dive deep into ONE process with multiple iterations:

### First Iteration: Add Commands and Policies

![Detailed Design I](./images/Restaurant%20DDD%20Kata%20Example_Detailed_Design_I.png)

Request participants to incorporate other elements such as policies and commands to capture the business behavior.
Discover the business rules (aka policies) that are triggered after each event. Incorporate the actions or intents which are executed after each decision (aka. policy). Add the events corresponding to incorporated commands.

### Second Iteration: Verify Pivotal Events

![Detail Design II](./images/Restaurant%20DDD%20Kata%20Example_Detailed_Design_II.png.png)

Iterate again on pivotal events. Verify that initial identified pivotal events are still relevant.

### Third Iteration: Refine Bounded Contexts

![Detailed Design III](./images/Restaurant%20DDD%20Kata%20Example_Detailed_Design_III.png.png)

Identify and name the bounded contexts according to their semantics. Try to find a speaking name. Names "... Management" or "... Service" are considered antipatterns. Keep a name that is relevant for the business.

### Fourth Iteration: Add Aggregates and Read Models

![Detailed Design IV](./images/Restaurant%20DDD%20Kata%20Example_Detailed_Design_IV.png)

Start adding aggregates as owners of business behavior. Try to find invariants and rules per Bounded Context which belong together and give them a business relevant name. Add them between a command and an events. Later in the code they execute the actual business logic.

If additional data might be required to take decision (policy) or execute a command, add a Read Model which provides an overview.

Model actors like users or system components of commands and policies, request the participants to write them down in round yellow stickies.

If required not depicted in the example you can also add UI by giving them a name.

### Key Differences from Big Picture

1. **Narrower Scope**: One business process (e.g., "Order Fulfillment")
2. **More Detail**: Every edge case, validation rule, and error scenario
3. **Aggregates Added**: Draw yellow boxes around events to show consistency boundaries
4. **External Systems**: Mark dependencies on systems outside our control

**Outcome**: Ready for Software Design Event Storming or direct implementation

## Software Design Event Storming

Convert domain model into implementation design.

### Focus Areas

1. **Aggregate Design**:
   - Commands → Aggregate methods
   - Events → State changes
   - Policies → Event handlers

2. **Event Schema Definition**:
   - For each event, define JSON structure
   - Identify versioning strategy

3. **Repository and Service Design**:
   - Where does data persist?
   - What external services are called?

**Outcome**: Architecture Decision Records, code structure, API contracts

## Facilitation Tips and Best Practices

### For Facilitators

1. **Set the Pace**: Keep energy high, move fast, don't let one person dominate
2. **Embrace Chaos**: The messy phase (Chaotic Exploration) is where insights emerge
3. **Ask, Don't Tell**: Guide with questions, don't impose structure prematurely
4. **Protect Experts**: Ensure domain experts feel heard, translate jargon for developers
5. **Watch Body Language**: If energy drops, take a break or change activity
6. **Timebox Ruthlessly**: Use a visible timer for each phase

### Setting Up the Workshop

- **Set a clear goal for the workshop and communicate it to the participants:** For example, you can say "We are here to explore the domain of X and to identify the main events, commands, aggregates, actors, external systems, and views that are involved in the process of Y."
- **Plan for more than just a day:** Event Storming is a technique that can be used for different purposes, such as assessing, exploring, envisioning, or designing a domain or a process. Depending on the scope and complexity of the domain, you may need more than one session to achieve your goal. You can use the high-level Event Storming to identify the domains and subdomains, and then use the detailed Event Storming to focus on a specific subdomain or a core domain.
- **Prepare for the unexpected:** Event Storming is a dynamic and collaborative method that can generate a lot of insights and discoveries. You may encounter surprises, conflicts, disagreements, or new opportunities during the workshop. Be ready to adapt and adjust your plan and your facilitation style accordingly. You can use techniques such as voting, prioritizing, grouping, or splitting to deal with the unexpected situations.
- **Set the scene:** Make sure you have a suitable space and tools for the workshop. You will need a large wall or a whiteboard to stick the sticky notes on, and enough sticky notes and markers of different colors and shapes to represent the different elements of the domain. You can also use online tools such as Lucidspark, Miro or Mural to run a remote or virtual Event Storming workshop. At SAP, we tend to use Mural. You can also use a legend or a cheat sheet to explain the meaning and the rules of each color and shape of the sticky notes.
- **Complete a check-in:** At the beginning of the workshop, introduce yourself and the participants, and ask them to share their name, role, and expectations for the workshop. This will help to create a positive and respectful atmosphere, and to align the participants around the goal and the approach of the workshop.
- **Go over the ground rules:** Establish some ground rules for the workshop, such as respecting each other's opinions, listening actively, asking questions, challenging assumptions, and having fun. You can also ask the participants to suggest or agree on some ground rules. This will help to create a safe and productive environment, and to avoid or resolve any conflicts or misunderstandings.
- **Share the agenda and set expectations:** Explain the agenda and the structure of the workshop, and how much time you have for each step or activity. You can also explain the role and the responsibilities of the facilitator and the participants, and what are the expected outcomes and deliverables of the workshop. This will help to create a clear and common understanding of the workshop, and to manage the time and the energy of the participants.
- **Build trust with an icebreaker:** Use an icebreaker or a warm-up activity to break the ice and to build trust and rapport among the participants. You can use a simple or a fun question, such as "What is your favorite movie or book?", or "What is something that you are proud of or excited about?". This will help to create a relaxed and friendly atmosphere, and to encourage the participants to share and interact with each other.

### Common Pitfalls

| Pitfall | Impact | Solution |
|---------|--------|----------|
| **Starting with aggregates** | Misses discovery, premature design | Always start with events (orange notes) |
| **Too much structure too soon** | Kills creativity | Allow chaos in early phases |
| **Facilitator as expert** | Groupthink | Facilitator guides process, doesn't provide domain answers |
| **Skipping hot spots** | Problems reappear later | Dedicate time to surface conflicts and questions |
| **One person dominates** | Missing perspectives | Use silent writing phases, round-robin contributions |

## Remote Event Storming

### Tools

- **Miro**: Infinite canvas, sticky notes, voting, timers
- **Mural**: Similar to Miro, good collaboration features (used at SAP)
- **FigJam**: Figma's whiteboard tool, integrates with design work
- **Lucidspark**: Lucid's collaboration tool

### Remote Adaptations

1. **Pre-work**: Send example events ahead of time so participants understand format
2. **Breakout Rooms**: Split into smaller groups for Chaotic Exploration, then merge
3. **Async Mode**: Allow participants to add notes between sessions
4. **Time Limits**: Remote fatigue is real—limit to 3-4 hours max, split across days
5. **Camera On**: Essential for reading energy and engagement

## What are the benefits of Event Storming?

Event Storming has many benefits for exploring complex business domains, such as:

- **It is fast and cheap:** It does not require any special tools or software, only sticky notes and a wall. It can be done in a few hours or days, depending on the scope and complexity of the domain.
- **It is collaborative and inclusive:** It brings together people with different perspectives and expertise, and encourages them to share their knowledge and insights. It creates a common language and a shared understanding of the domain among the participants.
- **It is visual and interactive:** It uses colors and shapes to represent different concepts and relationships. It allows participants to move, add, remove, or modify sticky notes as they discover new information or validate assumptions. It creates a tangible and dynamic representation of the domain that can be easily inspected and discussed.
- **It is creative and innovative:** It stimulates creativity and innovation by allowing participants to explore different scenarios and alternatives. It helps participants to identify problems, opportunities, and solutions that might otherwise be overlooked or ignored.

## When NOT to Use Event Storming

Event Storming is not always the right tool:

- **Simple CRUD applications**: Overkill for basic data management
- **Well-understood domains**: If everyone already agrees, use lighter modeling
- **Unwilling participants**: Requires active engagement from domain experts
- **Distributed team across many time zones**: Synchronous collaboration is critical

## Relationship to Other DDD Practices

- **[Context Mapping](./contextmapping.md)**: Event Storming reveals bounded contexts; Context Mapping documents relationships between them
- **[Ubiquitous Language](../concepts/strategic-concepts/ubiquitouslanguage.md)**: Emerges naturally from Event Storming discussions
- **[Aggregates](../concepts/tactical-concepts/aggregate.md)**: Software Design Event Storming defines aggregate boundaries
- **[Domain Events](../concepts/tactical-concepts/domain-events.md)**: Event Storming events → Implementation events in code

## Further Reading and Resources

### Books

- Brandolini, Alberto. *Introducing EventStorming* (The definitive guide)
- Rayner, Paul. *Event Storming Handbook* (Practical facilitation guide)
- Tune, Nick and Jean-Georges Perrin. *Architecture Modernization* (Event Storming for legacy system understanding)

### Websites and Articles

1. **[EventStorming](https://www.eventstorming.com/)**: The official website dedicated to EventStorming
2. **[Event storming - Wikipedia](https://en.wikipedia.org/wiki/Event_Storming)**: The Wikipedia page on Event Storming provides an overview of the technique, its origin, and key concepts
3. **[Event storming - IBM Cloud Architecture Center](https://www.ibm.com/cloud/architecture/architecture/practices/event-storming-methodology-architecture/)**: IBM Cloud Architecture Center's resource on Event Storming
4. **[Event Storming | VMware Tanzu Developer Center](https://tanzu.vmware.com/developer/practices/event-storming/)**: VMware Tanzu Developer Center provides information on Event Storming as a practice
5. **[Alberto Brandolini | Avanscoperta](https://www.avanscoperta.it/en/trainer/a-brandolini/)**: Alberto Brandolini is the creator of EventStorming
6. **[Introducing EventStorming - EventStorming](https://www.eventstorming.com/book/)**: The book "Introducing EventStorming" on the official EventStorming website
7. **[How to Run an Event Storming Workshop | Lucidspark](https://lucidspark.com/blog/how-to-run-an-event-storming-workshop):** Lucidspark provides insights into running an Event Storming workshop
8. **[How To Run Your First Event Storming Session - Selleo](https://selleo.com/blog/how-to-run-your-first-event-storming-session):** Selleo's blog post guides you through running your first Event Storming session
9. **[How to facilitate a workshop in 18 simple steps - Howspace](https://howspace.com/blog/how-to-facilitate-a-workshop/):** Howspace outlines 18 simple steps to facilitate a workshop effectively
10. **[How To Run A Remote Event Storming Session? - Selleo](https://selleo.com/blog/how-to-run-a-remote-event-storming-session):** Selleo provides insights into running remote Event Storming sessions
11. **[A list of random tips for Event Storming facilitators - Marijn Huizendveld](https://marijn.huizendveld.com/blog/a-list-of-random-tips-for-event-storming-facilitators):** Marijn Huizendveld shares practical tips for Event Storming facilitators
12. Brandolini, Alberto. "EventStorming Recipes" (blog series with practical tips)

### Related Topics

- **[Brandolini's law - Wikipedia](https://en.wikipedia.org/wiki/Brandolini%27s_law)**: Learn about Brandolini's law, often referenced in the context of misinformation
