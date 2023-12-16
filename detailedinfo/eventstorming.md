# Event Storming

## What is EventStorming?

EventStorming is a workshop format for quickly exploring complex business domains. It is based on the idea of using sticky notes to represent domain events, commands, aggregates, actors, external systems, and views. EventStorming allows cross-discipline collaboration between stakeholders with different backgrounds, such as software developers, domain experts, product owners, and business analysts. EventStorming can be used for different purposes, such as:

- Assessing the health of an existing line of business and discovering the most effective areas for improvements
- Exploring the viability of a new startup business model
- Envisioning new services that maximise positive outcomes to every party involved
- Designing clean and maintainable Event-Driven software to support rapidly evolving businesses

## How did EventStorming come to be?

EventStorming was invented by Alberto Brandolini, an Italian programmer and consultant, in 2013. EventStorming is inspired by Daniel Kahneman's Thinking, Fast and Slow, a book about cognitive biases and decision making. Brandolini came up with the idea of using sticky notes to capture the essence of a complex domain, and to expose the hidden assumptions and contradictions. He called his method EventStorming, to emphasize the focus on domain events and the similarity to brainstorming or agile modeling's model storming. Brandolini started to use EventStorming in his consulting work, and soon it became popular among the DDD community and beyond.

## Elements of EventStorming

![Grammar](./images/Restaurant%20DDD%20Kata%20Example%20Grammar.png)

| Element         | Symbol                        | Description                                                                                                                                                                                                                                                                                                                                                  |
| --------------- | ----------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Domain Event    | Orange Sticky                 | A domain event is something that happened in the domain that is relevant for the domain experts or the system. It is usually represented by a past-tense verb and some data. For example: "Order Placed", "Customer Registered", "Payment Processed".                                                                                                        |
| Policy          | Purple Sticky                 | A policy is a rule or a set of rules that governs the behavior of the system or a part of it. It is usually expressed in terms of domain events and commands. For example: "When an order is placed, send a confirmation email to the customer", "When a payment is overdue, cancel the order and notify the customer".                                      |
| Command         | Blue Stick                    | A command is a request or an instruction to change the state of the system or a part of it. It is usually represented by an imperative verb and some data. For example: "Place Order", "Register Customer", "Process Payment".                                                                                                                               |
| Aggregate       | Yellow rectangle Sticky       | An aggregate is a cluster of domain objects that can be treated as a single unit. It has a root entity and a boundary that defines what is inside the aggregate and what is outside. It enforces the invariants of the domain and ensures consistency. For example: "Order", "Customer", "Payment".                                                          |
| Read Model      | Green Sticky                  | A query or data is a request or an instruction to read the state of the system or a part of it. It is usually represented by a noun or a question and some data. For example: "Order Details", "Customer Profile", "Payment Status".                                                                                                                         |
| External System | Pink Rectangle Sticky         | An external system is a system that is outside the boundary of the domain model and interacts with it through interfaces. It can be a source of domain events or a target of commands or queries. For example: "Email Service", "Payment Gateway", "Inventory System".                                                                                       |
| UI              | White Sticky                  | A UI is a user interface that allows users to interact with the system. It can be a web page, a mobile app, a desktop application, or any other form of presentation. It can display domain events, send commands or queries, and receive responses from the system. For example: "Order Page", "Customer Registration Form", "Payment Confirmation Screen". |
| Hotspot         | Dark Purple Sticky 45° turned | A hotspot is a concept in EventStorming that is used to visualise and capture hot conflicts. Conflicts caused by, and not exclusive to, inconsistencies (in language), frictions, questions, dissent, objections, issues or procrastinating going deep to explore for later.                                                                                 |
| Pivotal Events  | Yellow long rectangle blocks  | Pivotal Events in Event Storming are significant occurrences that change the course of the business process. They are often the events with the highest number of people interested and can trigger reactions in other departments.                                                                                                                          |

## What do you need for an EventStorming workshop?

To run an EventStorming workshop, you will need the following:

- A **facilitator**: The facilitator is the person who guides the workshop and ensures that everyone is engaged and productive. The facilitator should have some knowledge of the domain and the process that is being analyzed, but not too much, so that they can ask the right questions and challenge the assumptions.
- The **right people**: The participants are the people who have the domain knowledge and the expertise to model the domain and the process. They should include domain experts, developers, testers, product owners, business analysts, and any other relevant stakeholders. The ideal number of participants is between 6 and 12, but it can vary depending on the scope and complexity of the domain.
- A **modeling space**: The modeling space is the place where the participants will write down and arrange the sticky notes that represent the events and other elements of the domain. The modeling space should be large enough to accommodate all the sticky notes and allow the participants to move around and interact with each other. A wall or a whiteboard is a good option for the modeling space.
- **Sticky notes**: The sticky notes are the main tool for modeling the domain and the process. They should be of different colors and shapes to represent different types of elements, such as events, commands, aggregates, policies, external systems, users, etc. The sticky notes should be easy to write on and stick to the modeling space. You will need a lot of sticky notes, so make sure you have enough supply.
- **Markers**: The markers are used to write on the sticky notes and to draw arrows or lines to show the relationships between the elements. The markers should be of different colors to match the sticky notes and to make the model more readable. The markers should be easy to hold and write with, and have a fine tip to fit the text on the sticky notes.

## How to run a EventStorming workshop?

It aims to identify the main domains and subdomains that are involved in the business process or the business application that is being analyzed. The EventStorming workshop consists of these steps:

### Chaotic Exploration

![Chaotic Exploration](./images/Restaurant%20DDD%20Kata%20Example_Chaotic_Exploration.png)

As a facilitator, you provide an overview, outlining objectives and guidelines for the workshop. Request participants to use sticky notes to jot down pertinent events in the domain and the studied process.
Use a verb and a noun in the past tense, such as "Coffee Ordered," "Order Handed Out," or "Order Requested." Without editing or passing judgment, invite participants to record as many experiences as they can recall.
The participants write down **events** using **orange** sticky notes.
Instruct participants to place their sticky notes on the modeling surface in whatever order they prefer, creating a disorganized cloud of questions and occurrences.

### Enforce the Timeline

![Enforce the timeline](./images/Restaurant%20DDD%20Kata%20Example_Enforce_Timeline.png)

Instruct the participants to organize the sticky notes chronologically on the modeling space, moving from left to right.
Assist them in identifying the starting and ending points of the process, aligning events and questions along a horizontal line.
Guide participants in identifying gaps, duplicates, inconsistencies, or ambiguities in the events and questions. Encourage collaboration among Participants to resolve these issues.
Ask participants to use arrows or lines to illustrate causal relationships between events, for example, "Table Assigned -> Order Requested -> Coffee Ordered."
Mark questions or doubts as "hotspots".These have to be answered or resolved later before the EventStorming Workshop is over.

### Enforce Consistency

![Enforce Consistency](./images/Restaurant%20DDD%20Kata%20Example_Enforce_Consistency.png)

Please instruct participants to review the timeline and assess its accuracy in portraying the process and domain.
Encourage them to ask questions such as "What happens next?" "What triggers this event?" and similar inquiries. Do not shy away from renaming, removing or reordering events.

### Identify the Bounded Contexts

![Identify the Bounded Contexts](./images/Restaurant%20DDD%20Kata%20Example_Identify_Bounded_Contexts.png)

As a facilitator, instruct participants to group events and other elements into logical clusters representing different subdomains or areas of responsibility within the domain.

These clusters are referred to as bounded contexts—a coherent and consistent set of events and elements sharing a common language and meaning.
Guide participants in identifying the boundaries of each bounded context, using different shapes or colors to highlight them. Assist participants in naming each bounded context and labeling its main purpose or goal.

For instance, direct participants to identify the "Delivery and Payment" bounded context, responsible for managing delivery of food and payments. Instruct them to use the long rectangle yellow blocks to mark boundary. After identifying them, they can draw boxes to capture Bounded Contexts with a semantic relevant and speaking name.

### Detailed Design in several iterations

#### First Iteration

![Detailed Design I](./images/Restaurant%20DDD%20Kata%20Example_Detailed_Design_I.png)

Request participants to incorporate other elements such as policies and commands to capture the business behavior.
Discover the business rules (aka policies) are triggered after each event. Incorporate the actions or intents which are executed after each decision (aka. policy). Add the events corresponding to incorporated commands.

#### Second Iteration

![Detail Design II](./images/Restaurant%20DDD%20Kata%20Example_Detailed_Design_II.png.png)

Iterate again on pivotal events. Verify that initial identified pivotal events are still relevant.

#### Third Iteration

![Detailed Design III](./images/Restaurant%20DDD%20Kata%20Example_Detailed_Design_III.png.png)

Identify and name the bounded contexts according to their semantics. Try to find a speaking name. Names "... Management" or "... Service" are considered antipatterns. Keep a name that is relevant for the business.

#### Fourth Iteration

![Detailed Design IV](./images/Restaurant%20DDD%20Kata%20Example_Detailed_Design_IV.png)

Start adding aggregates as owners of business behavior. Try to find invariants and rules per Bounded Context which belong together and give them a business relevant name. Add them between a command and an events. Later in the code they execute the actual business logic.
If additional data might be required to take decision (policy) or execute a command, add a Read Model which provides and overview.

Model actors like users or system components of commands and policies, request the participants to write them down in round yellow stickies.

If required not depicted in the example you can also add UI by giving them a name.

## Some hints and tips how to run a workshop

Some tips for facilitating an EventStorming workshop are:

- **Set a clear goal for the workshop and communicate it to the participants:** For example, you can say "We are here to explore the domain of X and to identify the main events, commands, aggregates, actors, external systems, and views that are involved in the process of Y."
- **Plan for more than just a day:** EventStorming is a technique that can be used for different purposes, such as assessing, exploring, envisioning, or designing a domain or a process. Depending on the scope and complexity of the domain, you may need more than one session to achieve your goal. You can use the high-level EventStorming to identify the domains and subdomains, and then use the detailed EventStorming to focus on a specific subdomain or a core domain.
- **Prepare for the unexpected:** EventStorming is a dynamic and collaborative method that can generate a lot of insights and discoveries. You may encounter surprises, conflicts, disagreements, or new opportunities during the workshop. Be ready to adapt and adjust your plan and your facilitation style accordingly. You can use techniques such as voting, prioritizing, grouping, or splitting to deal with the unexpected situations.
- **Set the scene:** Make sure you have a suitable space and tools for the workshop. You will need a large wall or a whiteboard to stick the sticky notes on, and enough sticky notes and markers of different colors and shapes to represent the different elements of the domain. You can also use online tools such as Lucidspark, Miro or Mural to run a remote or virtual EventStorming workshop. At SAP, we tend to use Mural. You can also use a legend or a cheat sheet to explain the meaning and the rules of each color and shape of the sticky notes.
- **Complete a check-in:** At the beginning of the workshop, introduce yourself and the participants, and ask them to share their name, role, and expectations for the workshop. This will help to create a positive and respectful atmosphere, and to align the participants around the goal and the approach of the workshop.
- **Go over the ground rules:** Establish some ground rules for the workshop, such as respecting each other's opinions, listening actively, asking questions, challenging assumptions, and having fun. You can also ask the participants to suggest or agree on some ground rules. This will help to create a safe and productive environment, and to avoid or resolve any conflicts or misunderstandings.
- **Share the agenda and set expectations:** Explain the agenda and the structure of the workshop, and how much time you have for each step or activity. You can also explain the role and the responsibilities of the facilitator and the participants, and what are the expected outcomes and deliverables of the workshop. This will help to create a clear and common understanding of the workshop, and to manage the time and the energy of the participants.
- **Build trust with an icebreaker:**. Use an icebreaker or a warm-up activity to break the ice and to build trust and rapport among the participants. You can use a simple or a fun question, such as "What is your favorite movie or book?", or "What is something that you are proud of or excited about?". This will help to create a relaxed and friendly atmosphere, and to encourage the participants to share and interact with each other.

## What are the benefits of EventStorming?

EventStorming has many benefits for exploring complex business domains, such as:

- **It is fast and cheap:** It does not require any special tools or software, only sticky notes and a wall. It can be done in a few hours or days, depending on the scope and complexity of the domain.
- It is collaborative and inclusive: It brings together people with different perspectives and expertise, and encourages them to share their knowledge and insights. It creates a common language and a shared understanding of the domain among the participants.
- **It is visual and interactive:** It uses colors and shapes to represent different concepts and relationships. It allows participants to move, add, remove, or modify sticky notes as they discover new information or validate assumptions. It creates a tangible and dynamic representation of the domain that can be easily inspected and discussed.
- **It is creative and innovative:** It stimulates creativity and innovation by allowing participants to explore different scenarios and alternatives. It helps participants to identify problems, opportunities, and solutions that might otherwise be overlooked or ignored.

## Resources

1. **[EventStorming](https://www.eventstorming.com/)**: The official website dedicated to EventStorming, a collaborative workshop technique for solving complex business problems.

2. **[Event storming - Wikipedia](https://en.wikipedia.org/wiki/Event_Storming)**: The Wikipedia page on Event Storming provides an overview of the technique, its origin, and key concepts.

3. **[Event storming - IBM Cloud Architecture Center](https://www.ibm.com/cloud/architecture/architecture/practices/event-storming-methodology-architecture/)**: IBM Cloud Architecture Center's resource on Event Storming, offering insights into the methodology and its application in architecture.

4. **[Event Storming | VMware Tanzu Developer Center](https://tanzu.vmware.com/developer/practices/event-storming/)**: The VMware Tanzu Developer Center provides information on Event Storming as a practice and its relevance in the development process.

5. **[Brandolini's law - Wikipedia](https://en.wikipedia.org/wiki/Brandolini%27s_law)**: Learn about Brandolini's law, often referenced in the context of misinformation and the challenges of debunking false information.

6. **[Alberto Brandolini | Avanscoperta](https://www.avanscoperta.it/en/trainer/a-brandolini/)**: Alberto Brandolini is the creator of EventStorming. This page provides information about him and his role in the development of EventStorming.

7. **[Introducing EventStorming - EventStorming](https://www.eventstorming.com/book/)**: Explore the book "Introducing EventStorming" on the official EventStorming website for a detailed guide and resources on the methodology.

8. **[How to Run an Event Storming Workshop | Lucidspark](https://lucidspark.com/blog/how-to-run-an-event-storming-workshop):** Lucidspark provides insights into running an Event Storming workshop, offering guidance on the process.

9. **[How To Run Your First Event Storming Session - Selleo](https://selleo.com/blog/how-to-run-your-first-event-storming-session):** Selleo's blog post guides you through running your first Event Storming session, covering the essentials.

10. **[How to facilitate a workshop in 18 simple steps - Howspace](https://howspace.com/blog/how-to-facilitate-a-workshop/):** Howspace outlines 18 simple steps to facilitate a workshop effectively, including aspects relevant to Event Storming.

11. **[How To Run A Remote Event Storming Session? - Selleo](https://selleo.com/blog/how-to-run-a-remote-event-storming-session):** Selleo provides insights into running remote Event Storming sessions, addressing the challenges of virtual collaboration.

12. **[A list of random tips for Event Storming facilitators - Marijn Huizendveld](https://marijn.huizendveld.com/blog/a-list-of-random-tips-for-event-storming-facilitators):** Marijn Huizendveld shares a list of random tips for Event Storming facilitators, offering practical advice.

13. **[Introducing EventStorming - EventStorming](https://www.eventstorming.com/book/):** Explore the book "Introducing EventStorming" on the official EventStorming website for a detailed guide and resources on the methodology.
