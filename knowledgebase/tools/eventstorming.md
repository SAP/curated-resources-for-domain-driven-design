# EventStorming in Domain-Driven Design

## **Table of Contents**

- [EventStorming in Domain-Driven Design](#eventstorming-in-domain-driven-design)
  - [**Table of Contents**](#table-of-contents)
  - [**Introduction**](#introduction)
  - [**What Is EventStorming?**](#what-is-eventstorming)
  - [**Origins of EventStorming**](#origins-of-eventstorming)
  - [**Elements of EventStorming**](#elements-of-eventstorming)
    - [**Domain Events**](#domain-events)
    - [**Commands**](#commands)
    - [**Aggregates**](#aggregates)
    - [**Policies**](#policies)
    - [**Actors**](#actors)
    - [**External Systems**](#external-systems)
    - [**Read Models**](#read-models)
    - [**User Interfaces**](#user-interfaces)
    - [**Hotspots**](#hotspots)
    - [**Bounded Contexts**](#bounded-contexts)
    - [**Pivotal Events**](#pivotal-events)
  - [**Preparing for an EventStorming Workshop**](#preparing-for-an-eventstorming-workshop)
  - [**Running an EventStorming Workshop**](#running-an-eventstorming-workshop)
    - [**1. Chaotic Exploration**](#1-chaotic-exploration)
    - [**2. Enforcing the Timeline**](#2-enforcing-the-timeline)
    - [**3. Identifying Hotspots and Inconsistencies**](#3-identifying-hotspots-and-inconsistencies)
    - [**4. Identifying Bounded Contexts**](#4-identifying-bounded-contexts)
    - [**5. Detailed Design Iterations**](#5-detailed-design-iterations)
      - [**First Iteration**](#first-iteration)
      - [**Second Iteration**](#second-iteration)
      - [**Third Iteration**](#third-iteration)
      - [**Fourth Iteration**](#fourth-iteration)
  - [**Patterns and Relationships in EventStorming**](#patterns-and-relationships-in-eventstorming)
    - [**Synchronous Dependencies**](#synchronous-dependencies)
    - [**Starfish Pattern**](#starfish-pattern)
  - [**Tips for Facilitating an EventStorming Workshop**](#tips-for-facilitating-an-eventstorming-workshop)
  - [**Benefits of EventStorming**](#benefits-of-eventstorming)
  - [**Conclusion**](#conclusion)

## **Introduction**

In **Domain-Driven Design (DDD)**, understanding complex business domains is crucial for building effective software solutions. **EventStorming** is a collaborative workshop format designed to facilitate the exploration and modeling of these domains. By bringing together stakeholders from different backgrounds, EventStorming enables teams to uncover domain insights, identify key events, and design systems that align closely with business needs.

## **What Is EventStorming?**

**EventStorming** is a workshop-based method that uses visual collaboration to model complex business processes. It involves participants writing domain events on sticky notes and arranging them on a large modeling surface to represent the flow of a system or process. EventStorming allows for:

- **Rapid Exploration:** Quickly mapping out the entire domain within hours.
- **Cross-Disciplinary Collaboration:** Involving developers, domain experts, product owners, and other stakeholders.
- **Flexible Usage:** Applying to various scenarios such as assessing existing businesses, exploring new models, envisioning services, and designing event-driven software.

## **Origins of EventStorming**

EventStorming was created by **Alberto Brandolini** in 2013. Inspired by cognitive science and collaborative modeling techniques, Brandolini sought a method that could bridge the communication gap between different stakeholders in software development. EventStorming emphasizes the use of domain events as the central element, facilitating a shared understanding and enabling effective problem-solving.

## **Elements of EventStorming**

EventStorming uses a set of standardized elements, each represented by different colored sticky notes or shapes. Understanding these elements is key to effectively modeling the domain.

### **Domain Events**

- **Symbol:** Orange Sticky Note
- **Description:** Significant occurrences within the domain, described using past-tense verbs (e.g., "Order Placed", "Payment Processed").
- **Example:** In an e-commerce system, "Item Added to Cart" represents a domain event when a user selects a product.

### **Commands**

- **Symbol:** Blue Sticky Note
- **Description:** Actions or requests to change the system's state, often initiated by an actor (e.g., "Place Order", "Update Profile").
- **Example:** "Submit Order" is a command issued by a customer to finalize a purchase.

### **Aggregates**

- **Symbol:** Yellow Rectangle Sticky Note
- **Description:** A cluster of domain objects treated as a single unit, enforcing consistency and business rules.
- **Example:** An "Order" aggregate encompasses order items, totals, and shipping information, ensuring the integrity of the order.

### **Policies**

- **Symbol:** Purple Sticky Note
- **Description:** Business rules or reactions to certain events, often triggering commands or other events.
- **Example:** "When Inventory Level Falls Below Threshold, Generate Restock Order" is a policy ensuring stock levels are maintained.

### **Actors**

- **Symbol:** Yellow Circle Sticky Note
- **Description:** Individuals or systems that interact with the domain by issuing commands or triggering events.
- **Example:** A "Customer" actor initiates the "Place Order" command.

### **External Systems**

- **Symbol:** Pink Rectangle Sticky Note
- **Description:** Systems outside the domain boundary that interact with it (e.g., payment gateways, email services).
- **Example:** A "Payment Gateway" processes transactions initiated within the domain.

### **Read Models**

- **Symbol:** Green Sticky Note
- **Description:** Representations of data used to fulfill queries or display information to users.
- **Example:** "Order Summary" provides a customer with details of their purchase.

### **User Interfaces**

- **Symbol:** White Sticky Note
- **Description:** Interfaces through which actors interact with the system (e.g., web pages, mobile apps).
- **Example:** The "Checkout Page" UI allows customers to review and submit their orders.

### **Hotspots**

- **Symbol:** Dark Purple Sticky Note (Turned 45°)
- **Description:** Areas of uncertainty, conflict, or concern that require further exploration.
- **Example:** A hotspot may be placed on "Delivery Time Calculation" if there's ambiguity in how it's determined.

### **Bounded Contexts**

- **Symbol:** Enclosed Areas or Long Yellow Rectangles
- **Description:** Logical boundaries within the domain where specific models and language apply consistently.
- **Example:** A "Shipping" bounded context handles all logistics-related events and commands.

### **Pivotal Events**

- **Symbol:** Long Yellow Rectangle Blocks
- **Description:** Critical events that significantly alter the process flow or state.
- **Example:** "Order Confirmed" is a pivotal event triggering billing and fulfillment processes.

## **Preparing for an EventStorming Workshop**

To run a successful EventStorming workshop, consider the following preparations:

- **Assemble the Right Team:**

  - **Facilitator:** Guides the workshop, keeps focus, and encourages participation.
  - **Domain Experts:** Individuals with in-depth knowledge of the business processes.
  - **Developers and Technical Staff:** Understand technical constraints and opportunities.
  - **Stakeholders:** Product owners, business analysts, or anyone invested in the outcome.

- **Gather Materials:**

  - Large modeling surface (e.g., wall space with paper rolls).
  - Sticky notes in various colors corresponding to the elements.
  - Markers with fine tips for legibility.
  - Optional: Online collaboration tools for remote participants.

- **Set Clear Objectives:**
  - Define the scope of the workshop (e.g., mapping a specific process).
  - Communicate goals to all participants.

## **Running an EventStorming Workshop**

An EventStorming workshop typically follows these steps:

### **1. Chaotic Exploration**

- **Objective:** Brainstorm domain events without concern for order or structure.
- **Process:**
  - Participants write down as many domain events as they can think of on orange sticky notes.
  - Use past-tense verbs (e.g., "Invoice Generated").
  - Place notes randomly on the modeling surface to create a cloud of events.
- **Example:** In a restaurant scenario, events like "Table Reserved," "Order Placed," "Meal Served" are noted.

### **2. Enforcing the Timeline**

- **Objective:** Organize events chronologically to form a narrative flow.
- **Process:**
  - Arrange the orange sticky notes from left to right in the order they occur.
  - Discuss and agree on the sequence of events.
- **Example:** "Customer Seated" precedes "Order Taken," which precedes "Meal Prepared."

### **3. Identifying Hotspots and Inconsistencies**

- **Objective:** Detect areas of uncertainty or conflict for further investigation.
- **Process:**
  - Place dark purple sticky notes (hotspots) on events that need clarification.
  - Encourage participants to ask questions and highlight issues.
- **Example:** A hotspot on "Payment Processed" if there's confusion about payment methods.

### **4. Identifying Bounded Contexts**

- **Objective:** Define logical groupings of related events and elements.
- **Process:**
  - Cluster events into bounded contexts based on domain relevance.
  - Use long yellow rectangles or draw boundaries to encapsulate contexts.
  - Name each bounded context meaningfully.
- **Example:** Grouping "Order Placed," "Meal Prepared," and "Meal Served" into a "Kitchen Operations" context.

### **5. Detailed Design Iterations**

#### **First Iteration**

- **Add Commands and Policies:**
  - Introduce blue sticky notes for commands initiating events.
  - Use purple sticky notes for policies that govern reactions.
- **Example:** Command "Place Order" leads to event "Order Placed"; policy "If Order Delayed, Notify Customer."

#### **Second Iteration**

- **Refine Pivotal Events:**
  - Identify key events that significantly impact the process.
- **Example:** "Order Completed" triggers billing and customer feedback processes.

#### **Third Iteration**

- **Solidify Bounded Contexts:**
  - Reassess and adjust bounded contexts based on new insights.
- **Example:** Separate "Payment Processing" into its own context due to specialized rules.

#### **Fourth Iteration**

- **Introduce Aggregates and Actors:**
  - Add yellow rectangle stickies for aggregates between commands and events.
  - Include yellow circle stickies for actors initiating commands.
- **Example:** Aggregate "Order" handles the "Update Order" command; actor "Waiter" initiates "Submit Order" command.

## **Patterns and Relationships in EventStorming**

Understanding patterns and relationships helps in identifying potential issues and designing effective systems.

### **Synchronous Dependencies**

- **Description:** Occurs when a command requires an immediate response before proceeding.
- **Implications:**
  - Tight coupling between components.
  - Potential for delays or failures if dependencies are unavailable.
- **Example:** A "Process Payment" command that waits for a real-time response from a payment gateway.

### **Starfish Pattern**

- **Description:** A central component (hub) connected to multiple others (spokes), creating a potential single point of failure.
- **Implications:**
  - Reduced system reliability if the hub fails.
  - Bottlenecks affecting performance and scalability.
- **Example:** A central "Authentication Service" required by all other services; if it goes down, access is blocked.

## **Tips for Facilitating an EventStorming Workshop**

- **Set Clear Goals:** Communicate the workshop's objectives to all participants.
- **Prepare the Environment:** Ensure the modeling space is ample and materials are ready.
- **Establish Ground Rules:** Encourage open communication, respect, and active participation.
- **Use Icebreakers:** Build trust and rapport among participants at the start.
- **Be Adaptive:** Be prepared to adjust the agenda based on the group's needs.
- **Encourage Collaboration:** Facilitate discussions and guide the group without dominating.
- **Document Hotspots:** Keep track of unresolved questions for follow-up.
- **Keep Time:** Manage the schedule to cover all planned activities.

## **Benefits of EventStorming**

- **Rapid Knowledge Sharing:** Quickly aligns understanding among diverse stakeholders.
- **Visual Clarity:** Provides a tangible model that is easy to grasp and discuss.
- **Identifies Issues Early:** Exposes conflicts, gaps, and assumptions in the domain.
- **Facilitates Collaboration:** Breaks down silos between departments and disciplines.
- **Enhances Domain Models:** Leads to more accurate and effective system designs.
- **Supports Agile Practices:** Integrates well with iterative development and continuous improvement.

## **Conclusion**

EventStorming is a powerful tool in Domain-Driven Design for exploring and modeling complex domains. By focusing on domain events and fostering collaborative participation, it enables teams to gain deep insights, align on objectives, and design systems that truly meet business needs. Whether assessing existing processes or envisioning new services, EventStorming provides a flexible and effective approach to tackle the challenges of modern software development.
