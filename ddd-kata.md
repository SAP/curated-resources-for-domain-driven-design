# Domain-Driven Design Kata

## What is a Kata?

A kata is a specific sequence of movements and techniques practiced in the martial arts. The word "kata" is Japanese and is used in many martial arts originating from Japan, such as karate, judo, and aikido. Kata is usually taught by a sensei, who will demonstrate the movements and then guide the students as they practice the kata. The practice of kata can help martial artists to develop proper technique, balance, and control, and to learn the application of various techniques in a practical context. Some martial arts styles have kata that are performed solo, while others require a partner.
Additionally, kata is also commonly used in software development to practice writing software that accomplishes specific tasks, by following a predetermined set of steps. The goal of the practice is to create software that is reliable, easy to maintain and flexible. These principles are now applied in practicing Domain-Driven Design.

## Follow the DDD starter modelling process

![DDD starter Modelling Process (CC-BY-SA-4.0 license)](./images/ddd-starter-modelling-process-colored.png)

This [process](https://github.com/ddd-crew/ddd-starter-modelling-process) walks you through each stage of understanding and executing Domain-Driven Design (DDD), from understanding an organization's business model to coding a domain model.



After a few cycles of the process, you understand the core DDD theory as well as practical experience to go deeper into DDD. You will then be able to alter and develop the procedure to meet your demands in every situation. In a real project, you'll frequently switch back and forth between these processes.

Please note, that the DDD Kata will not touch all aspects of the DDD Starter Modelling Process. We have selected only a subset of tools.

## Selected Tooling for the DDD Kata

![Tooling of the DDD Kata](./images/ddd-starter-selected-tools.png)

In the DDD Kata you can experience a selected subset of tools proposed by the DDD starter Modelling Process.

| Tool                                                                             | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| -------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [EventStorming](https://www.eventstorming.com/)                                  | EventStorming is a versatile workshop model for exploring complicated business subjects together. It comes in a variety of flavors that may be utilized in a variety of situations: to evaluate the health of an existing line of business and identify the most effective areas for improvement; to investigate the viability of a new startup business model; to imagine new services that maximize positive outcomes for all parties involved; and to design clean and maintainable Event-Driven software to support rapidly evolving businesses. EventStorming's adaptable nature enables sophisticated cross-discipline interaction amongst stakeholders from various backgrounds, offering a new sort of cooperation that transcends silos and specialism barriers. |
| [Domain Message Flow](https://github.com/ddd-crew/domain-message-flow-modelling) | Developing loosely linked systems involves more than just neatly drawn boundaries. Interactions between bounded contexts must also be carefully described. A bounded context is a subsystem in a software architecture that is aligned with a certain domain. It may be built as a microservice or as a monolithic module. A Domain Message Flow Diagram (DMFD) is a basic visual representation of the flow of messages (commands, events, and inquiries) between actors, bounded contexts, and systems in a single scenario.                                                                                                                                                                                                                                            |
| [Bounded Context Canvas](https://github.com/ddd-crew/bounded-context-canvas)     | The Bounded Context Canvas is a collaborative design tool for creating and documenting a single bounded context. The canvas walks you through the process of developing a bounded context by pushing you to examine and make decisions about essential design components such as nomenclature, responsibilities, public interface, and dependencies.                                                                                                                                                                                                                                                                                                                                                                                                                      |
| [Aggregate Canvas](https://github.com/ddd-crew/aggregate-design-canvas)          | The Aggregate Design Canvas is a modeling tool that should be used in conjunction with design-level domain modeling efforts. Eric Evans first described aggregates as a lifecycle pattern. We define aggregate as a network of objects that serves as a consistency boundary for our domain regulations. Depending on how the aggregate is designed, we can either enforce them (making them invariant) or be compelled to implement corrective measures. As a result, it is critical to carefully establish aggregate borders, as they influence the behaviors modeled inside our domain. The canvas features a suggested working order that aids in iteratively discussing various components of the overall design.                                                    |

## The DDD Kata

* Select a collaboration tool for your choice. In SAP we are using Mural. In the DDD Community Miro is used a lot.
* **Form a working group** (up to 8 people). Declare one member a domain expert (maybe a substitute) and one member as facilitator / moderator
* Perform a **Big Picture Event Storming** with your group in collaboration tool of choice
* **Identify the bounded context and aggregates** within evaluated process in collaboration tool of choice
* Establish the message flow from Bounded Context to Bounded Context using the **Domain Message Flow** Diagrams in collaboration tool of choice.
* For each identified Bounded Context, specify using the **Bounded Context Canvas** in collaboration tool of choice.
* Within the defined Bounded Contexts, defined the aggregates using the **Aggregate canvases** in collaboration tool of choice.

### The Requirements

Let’s assume you are a start-up, and you want to provide software for parking lots & garages for all major cities in Europe and for various park area providers.

1. You can enter and leave the parking lot or the parking garage through several entrances and exits.
2. There are specific parking spots for different types of vehicles (motorcycles, car, electric car, truck/bus, handicapped persons, family-friendly parking spots)
3. Each parking spot has a unique identifier (for parking garage – number & floor or for parking lot – number &  area)
4. The customer may collect a ticket at each entrance and leave via any exit.
5. The ticket given to customer contains a parking spot ID where to park
6. The ticketing information must be stored for 10 years due to tax reasons.
7. There are three types of terminals:
   1. The terminals at the entrances have a way for the customer to communicate the vehicle details to the system.
   2. Customer drive into the parking garage / lot via entrance terminals where the collect the tickets
   3. The terminals near the exits have a way to pay the ticket.
   4. Detail out the actual payment process like select payment method, put in credit card, enter PIN are not relevant here.
8. The terminals at the exit gates collect the paid ticket.
9. The ticket has a read/write magnetic stripe containing information including a position to park.
10. The magnetic stripe can be changed by the terminals.
11. Parking garages have a parking guiding system, that guides customers to the correct parking spot. The guiding system recognizes the vehicle and guides it to the right parking spot.
12. Parking lots do not have such a system.

As domain expert, please stay from requirements perspective within these guardrails. You can detail them out as much as you want.

### The Process

#### Define the Team

![Team Setup](./images/team-setup.png)

As a **Moderator / Facilitator**, your task is to organize the workshops and conduct the workshops.

As a **Domain Expert**, your tasks are:

* Mimics the expert for parking lot software & management
* Takes business decisions, has the last say on requirements
* Researches and creates requirements

As a **Team Member** your tasks are:

* Interview the Domain Expert
* Create the deliverables
* Participate actively in all workshops

#### Plan your timeline

We recommend from our experience within the DDD Community at SAP the following timeline:

![Timeline Proposal](./images/timeline-proposal.png)

* Plan to have ~4h a week of modelling sessions
* Work iteratively (e.g. while working on Aggregate Canvas you might want to adjust your Event Storming)
* As a moderator, strife for consensus and alignment in the team
* Plan your time carefully. Timebox your efforts.
* Most importantly, **have fun modelling**.
