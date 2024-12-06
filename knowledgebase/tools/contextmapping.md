# Context Mapping in Domain-Driven Design

## **Table of Contents**

- [Context Mapping in Domain-Driven Design](#context-mapping-in-domain-driven-design)
  - [**Table of Contents**](#table-of-contents)
  - [**Introduction**](#introduction)
  - [**Understanding Context Mapping**](#understanding-context-mapping)
  - [**Team Relationships in Context Mapping**](#team-relationships-in-context-mapping)
    - [**Mutually Dependent**](#mutually-dependent)
    - [**Upstream / Downstream**](#upstream--downstream)
    - [**Free**](#free)
  - [**Context Map Patterns**](#context-map-patterns)
    - [**Open-Host Service**](#open-host-service)
    - [**Conformist**](#conformist)
    - [**Anticorruption Layer**](#anticorruption-layer)
    - [**Shared Kernel**](#shared-kernel)
    - [**Partnership**](#partnership)
    - [**Customer/Supplier Development**](#customersupplier-development)
    - [**Published Language**](#published-language)
    - [**Separate Ways**](#separate-ways)
    - [**Big Ball of Mud**](#big-ball-of-mud)
  - [**Best Practices for Context Maps**](#best-practices-for-context-maps)
    - [**Prefer Small Context Maps for Explicit Questions**](#prefer-small-context-maps-for-explicit-questions)
    - [**Document and Explain the Patterns You Are Going to Use**](#document-and-explain-the-patterns-you-are-going-to-use)
    - [**Work with Different Perspectives and Multiple Context Maps**](#work-with-different-perspectives-and-multiple-context-maps)
  - [**Conclusion**](#conclusion)

## **Introduction**

In **Domain-Driven Design (DDD)**, managing the complexity of large systems involves breaking down the domain into **Bounded Contexts**. However, these contexts often need to interact, and understanding the relationships and interactions between them is crucial. **Context Mapping** is a strategic design technique in DDD that provides a holistic view of how different bounded contexts and teams relate and communicate with each other.

## **Understanding Context Mapping**

**Context Maps** describe the relationships between bounded contexts and the teams working on them. They provide a collection of patterns and team relationship types that help visualize and analyze the interactions within a system or across multiple systems.

There are **nine context map patterns** and **three team relationship types** that offer diverse perspectives, such as service provisioning, model propagation, and governance aspects. This diversity enables teams to gain a comprehensive understanding of how different parts of the system influence each other.

Context Maps can be used both for analyzing existing systems and for planning new ones. They help identify dependencies, communication flows, and potential areas of conflict or collaboration between teams and bounded contexts.

## **Team Relationships in Context Mapping**

Understanding team relationships is fundamental in context mapping, as it affects how bounded contexts interact and how teams coordinate their efforts.

### **Mutually Dependent**

**Definition:** Two teams or bounded contexts are **mutually dependent** when their software artifacts or systems need to be delivered together to be successful. There is a close, reciprocal link between their data, functionality, and capabilities, requiring significant communication and coordination between the teams.

**Example:** In a financial services company, the **Billing Team** and the **Subscription Management Team** might be mutually dependent. The billing system relies on subscription data to generate invoices, while the subscription system needs billing information to manage account statuses. Both teams must coordinate releases and changes to ensure compatibility.

### **Upstream / Downstream**

**Definition:** In an **upstream/downstream** relationship, the actions of the upstream team affect the downstream team, but not vice versa. The upstream team can succeed independently, while the downstream team's success is influenced by the upstream team's outputs.

**Example:** An **Inventory Management Team** (upstream) provides product availability data to an **Order Processing Team** (downstream). Changes in the inventory system impact how orders are processed, but the order system does not affect inventory management directly.

### **Free**

**Definition:** A team or bounded context is **free** when changes in other bounded contexts do not influence its success or failure. There are no organizational or technical dependencies, allowing the team to operate independently.

**Example:** A **Marketing Analytics Team** develops tools to analyze campaign performance. Their work does not depend on other systems or teams, and they are free to choose their technologies and timelines without affecting or being affected by others.

## **Context Map Patterns**

Context map patterns define how bounded contexts interact and the nature of their relationships. Here are the nine context map patterns, each with detailed explanations and examples.

### **Open-Host Service**

**Definition:** An **Open-Host Service** provides a protocol or interface that gives access to a subsystem as a set of services. It is open so that any team needing to integrate can use it. The service is enhanced over time to handle new integration requirements, while special cases may use one-off translators to avoid complicating the shared protocol.

**Example:** A **Payment Processing Service** exposes APIs for handling transactions. Multiple teams (e.g., e-commerce, subscription services) use this open-host service to process payments. The service is designed to accommodate various clients without needing direct coordination.

### **Conformist**

**Definition:** In the **Conformist** pattern, a downstream team eliminates the complexity of translation between bounded contexts by strictly adhering to the upstream team's model. This simplifies integration but may limit the downstream team's flexibility.

**Example:** A **Mobile App Team** conforms to the data models and APIs provided by the **Backend Services Team**. Instead of translating or adapting the data, the mobile app uses the same structures, ensuring seamless integration but potentially inheriting limitations of the backend model.

### **Anticorruption Layer**

**Definition:** An **Anticorruption Layer (ACL)** is an isolating layer that provides a way for a downstream system to interact with an upstream system while preserving its own domain model. The ACL translates or adapts the upstream model to fit the downstream context.

**Example:** A **Reporting System** needs data from an **ERP System** with a complex and unsuitable model. The reporting team implements an anticorruption layer that transforms ERP data into a simplified, reporting-friendly model, allowing them to maintain their own domain concepts.

### **Shared Kernel**

**Definition:** A **Shared Kernel** involves an explicit boundary where teams agree to share a subset of the domain model, including code or database design. This shared part requires close collaboration and coordination to manage changes.

**Example:** The **User Management Team** and the **Authentication Team** share a common user identity model. They maintain a shared kernel for user entities and related database schemas, ensuring consistency across authentication and user profile functionalities.

### **Partnership**

**Definition:** In a **Partnership**, two teams have a mutual dependency where the failure of one affects the other. They collaborate closely, with joint planning and management of integration. Features are scheduled to align with shared release cycles.

**Example:** A **Ride-Sharing Platform**'s **Driver Team** and **Rider Team** must work in tandem. Features like real-time location tracking require both teams to coordinate development and releases to ensure functionality works across both driver and rider applications.

### **Customer/Supplier Development**

**Definition:** In a **Customer/Supplier** relationship, the downstream team's needs influence the upstream team's planning. The upstream team (supplier) accommodates the requirements of the downstream team (customer), negotiating and budgeting tasks to meet shared goals.

**Example:** A **Front-End Web Team** (customer) relies on APIs provided by a **Backend API Team** (supplier). The front-end team communicates their needs, and the backend team plans their development to support those requirements, ensuring the front-end team can deliver their features.

### **Published Language**

**Definition:** A **Published Language** is a well-documented, shared language used for communication between bounded contexts. It serves as a common medium, translating as necessary to ensure consistent understanding.

**Example:** Teams across different services use a standard **JSON API Specification** to communicate. This published language ensures all teams interpret data structures consistently, facilitating integration without misunderstandings.

### **Separate Ways**

**Definition:** When bounded contexts have no significant relationship, they follow **Separate Ways**, operating independently. This allows teams to find specialized solutions within their scope without the need for integration.

**Example:** A **Human Resources System** and a **Manufacturing Control System** in a company may have no overlap. Each operates separately, using different technologies and models suited to their specific needs without any dependency.

### **Big Ball of Mud**

**Definition:** A **Big Ball of Mud** refers to a system or bounded context with a disorganized structure, mixed models, and inconsistent boundaries. It represents poor quality and a lack of clear design.

**Example:** An old **Legacy System** that has been patched over years without proper architecture becomes a big ball of mud. Teams working on new systems implement strategies to prevent this messy model from contaminating other contexts, such as by isolating it behind anticorruption layers.

## **Best Practices for Context Maps**

Effectively using context maps requires careful planning and consideration. Here are some best practices to follow:

### **Prefer Small Context Maps for Explicit Questions**

Large context maps can become overwhelming and hard to interpret. Instead, create small, focused context maps aimed at answering specific questions or addressing particular concerns.

**Example:** If you want to understand how data flows between the **Order Management System** and the **Inventory System**, create a context map focusing solely on these two bounded contexts and their relationship.

### **Document and Explain the Patterns You Are Going to Use**

Not all stakeholders may be familiar with context mapping patterns. Before presenting a context map, decide which patterns you will use and provide clear explanations and examples for each.

**Example:** When presenting to a mixed audience of developers and business analysts, include a brief guide explaining patterns like **Anticorruption Layer** or **Shared Kernel**, using language and examples that are accessible to all.

### **Work with Different Perspectives and Multiple Context Maps**

Different stakeholders may have varying perspectives and interests. Use multiple context maps to address these different viewpoints, ensuring that each map remains clear and relevant to its intended audience.

**Example:** Create one context map highlighting technical dependencies for the development team and another focusing on business processes and team interactions for project managers and executives.

## **Conclusion**

Context mapping is a powerful technique in Domain-Driven Design that helps teams visualize and understand the complex relationships between bounded contexts and the teams working on them. By using defined patterns and recognizing team relationships, organizations can plan and coordinate more effectively, manage dependencies, and prevent issues related to model propagation and system integration.

Adhering to best practices such as creating focused context maps, documenting patterns, and tailoring views for different perspectives ensures that context mapping remains a valuable tool for both analysis and design in complex systems.
