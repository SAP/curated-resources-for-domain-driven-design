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

## **When to Use Each Pattern: Decision Guide**

Choosing the right Context Mapping pattern depends on several factors:

| Question | Pattern Recommendation |
|----------|----------------------|
| Do both teams need to succeed together? | **Partnership** |
| Can we share a tiny portion of the model? | **Shared Kernel** (keep minimal!) |
| Does downstream need to influence upstream? | **Customer-Supplier** |
| Can upstream accommodate downstream needs? | **Customer-Supplier** or **Open Host Service** |
| Is upstream unwilling to accommodate? | **Conformist** or **Anti-Corruption Layer** |
| Is upstream model poor quality or legacy? | **Anti-Corruption Layer** |
| Do multiple contexts need the same capability? | **Open Host Service** + **Published Language** |
| Is integration cost higher than benefit? | **Separate Ways** |

### Pattern Selection Flowchart

```
Start: Two contexts need to integrate
    │
    ├─ Do both teams share common goal and fail/succeed together?
    │  YES → Partnership
    │  NO  → Continue
    │
    ├─ Is upstream willing to accommodate downstream?
    │  YES → Can downstream influence roadmap?
    │       YES → Customer-Supplier
    │       NO  → Continue
    │  NO  → Continue
    │
    ├─ Does downstream have rich domain model to protect?
    │  YES → Anti-Corruption Layer
    │  NO  → Continue
    │
    ├─ Does upstream provide well-defined API for many consumers?
    │  YES → Open Host Service (downstream is Conformist)
    │  NO  → Continue
    │
    └─ Is integration benefit worth the cost?
       YES → Conformist (simple integration)
       NO  → Separate Ways
```

## **Anti-Patterns to Avoid**

### 1. Too Many Shared Kernels

**Problem**: Multiple contexts share large portions of model

**Impact**: High coordination cost, reduced autonomy, difficult to evolve contexts independently

**Fix**: Minimize shared kernel (typically <5% of domain model) or switch to Customer-Supplier with Published Language

**Example**: Five contexts sharing `Customer`, `Order`, `Product` models create tight coupling. Better: Each context owns its view, coordinates via events or APIs.

### 2. Conformist Everywhere

**Problem**: All downstream contexts conform to upstream models without translation

**Impact**: Upstream design decisions pollute entire system, downstream contexts lose domain richness

**Fix**: Add Anti-Corruption Layers for critical downstream contexts with rich domain models

**Example**: Modern e-commerce platform conforming entirely to legacy ERP's awkward data structures. Better: Use ACL to translate ERP model to e-commerce domain concepts.

### 3. Hidden Dependencies

**Problem**: Context map shows no relationship, but contexts share database, cache, or filesystem

**Impact**: Unexpected coupling, hard to reason about changes, surprise breakages

**Fix**: Make implicit dependencies explicit on context map. If contexts share infrastructure, document it.

**Example**: Two "separate" contexts both read/write same database tables. Better: Explicitly model as Shared Kernel or establish clear ownership with integration pattern.

### 4. God Context

**Problem**: One context integrates with everyone (hub-and-spoke architecture)

**Impact**: Single point of failure, bottleneck for changes, overloaded team

**Fix**: Decompose god context into smaller contexts, use event-driven choreography instead of orchestration

**Example**: "Integration Hub" that all contexts must go through. Better: Contexts publish events to message bus, consumers subscribe to what they need.

### 5. Circular Dependencies

**Problem**: Context A depends on B, B depends on C, C depends on A

**Impact**: Cannot deploy independently, complex coordination, high risk of breakage

**Fix**: Break cycle by introducing events, reversing dependency direction, or extracting shared concern

**Example**: Order → Inventory → Shipping → Order. Better: Order publishes events, Inventory and Shipping subscribe, Order doesn't call back.

## **Creating a Context Map: Workshop Approach**

### Workshop Format (2-3 hours)

**Participants**: Architects, tech leads, domain experts, product owners

**Materials**: Large whiteboard or Miro board, sticky notes in different colors, markers

#### Step 1: Identify Bounded Contexts (30 min)

1. List all bounded contexts in the system
2. Write each on a large sticky note (one color, e.g., yellow)
3. Arrange spatially on board (no connections yet)
4. For each context, note:
   - Responsible team
   - Core domain concepts
   - Primary capabilities

#### Step 2: Draw Integration Lines (45 min)

1. For each pair of contexts that integrate, draw a line connecting them
2. Mark direction with arrows:
   - Single arrow (→): Uni-directional dependency
   - Double arrow (↔): Bi-directional dependency
3. Label line with integration mechanism:
   - REST API
   - Domain Events
   - Message Queue
   - Shared Database (flag as concern!)
   - Batch File Transfer
   - gRPC, GraphQL, etc.

#### Step 3: Classify Relationships (45 min)

1. For each integration line, determine the Context Mapping pattern
2. Use abbreviations on the line:
   - **P**: Partnership
   - **SK**: Shared Kernel
   - **U/D**: Upstream/Downstream (Customer-Supplier)
   - **CF**: Conformist
   - **ACL**: Anti-Corruption Layer
   - **OHS**: Open Host Service
   - **PL**: Published Language
   - **SW**: Separate Ways
3. For asymmetric relationships, mark **U** (Upstream) and **D** (Downstream)

#### Step 4: Identify Issues and Opportunities (30 min)

**Red Flags** (mark with red sticky notes):
- Circular dependencies
- Excessive Conformist patterns (downstream context losing domain integrity)
- Too many Shared Kernels (high coordination cost)
- God Context (one context integrating with everyone)
- Hidden dependencies (shared database not on map)

**Opportunities** (mark with green sticky notes):
- Extract Open Host Service from point-to-point integrations
- Add ACL to protect critical downstream context
- Simplify to Separate Ways where integration cost exceeds benefit
- Replace Shared Kernel with Customer-Supplier + Published Language

**Deliverable**: Documented context map showing all contexts, relationships, patterns, and action items

## **Context Map Visual Notation**

### Example Context Map

```
┌─────────────────┐                    ┌─────────────────┐
│   Order Mgmt    │ ───── OHS/PL ────→ │   Shipping      │
│   (Upstream)    │                    │  (Downstream)   │
│   Team: Orders  │                    │   Team: Ops     │
└─────────────────┘                    └─────────────────┘
                                               │
                                               │ CF
                                               ↓
                                       ┌─────────────────┐
                                       │  External       │
                                       │  Carrier API    │
                                       │  (3rd Party)    │
                                       └─────────────────┘

┌─────────────────┐                    ┌─────────────────┐
│   Billing       │ ←───── P ────────→ │   Payments      │
│   Team: Finance │                    │   Team: Finance │
└─────────────────┘                    └─────────────────┘
         │                                      │
         └──────────────── SK ─────────────────┘
              (Shared: Money, CustomerId)

┌─────────────────┐         ACL         ┌─────────────────┐
│  Modern CRM     │ ←──────────────────  │  Legacy ERP     │
│  (Downstream)   │                      │  (Upstream)     │
│  Team: Sales    │                      │  Team: Legacy   │
└─────────────────┘                      └─────────────────┘
```

### Notation Legend

- **Box**: Bounded Context with team ownership
- **Arrow**: Direction of dependency
- **Label on Line**: Context Mapping pattern abbreviation
- **Double Arrow**: Bi-directional dependency (Partnership)
- **Single Arrow**: Uni-directional dependency (Upstream/Downstream)

## **Evolution and Maintenance**

Context Maps are **living documents**. They should be updated when:

- New bounded contexts are introduced
- Integration patterns change (e.g., adding ACL, migrating from Conformist to OHS)
- Organizational structure changes (team ownership transfers)
- Major architectural decisions are made
- Teams discover hidden dependencies

**Recommendation**:
- Review context map **quarterly** with architecture team
- Use it as input for roadmap planning and team capacity allocation
- Store context map in version control (as diagrams or code-as-diagram tools)
- Present context map in architecture reviews and onboarding sessions

## **Relationship to Agentic AI**

In multi-agent AI systems, Context Mapping patterns apply directly to [Agent-to-Agent Communication](../concepts/emerging-practices/agentic-ai/a2a-communication.md):

- **MCP Servers**: Implement Open Host Service pattern
- **AI Agents**: Can be Conformist (adopt tool schemas), use ACL (translate external agent models), or form Partnerships (peer collaboration)
- **Multi-Agent Systems**: Context Map shows which agents integrate and how

See [Agentic AI and DDD](../concepts/emerging-practices/agentic-ai/index.md) for detailed application to autonomous agent systems.

## **Conclusion**

Context mapping is a powerful technique in Domain-Driven Design that helps teams visualize and understand the complex relationships between bounded contexts and the teams working on them. By using defined patterns and recognizing team relationships, organizations can plan and coordinate more effectively, manage dependencies, and prevent issues related to model propagation and system integration.

Key takeaways:

- **Choose patterns deliberately**: Use the decision guide to select appropriate integration patterns
- **Avoid anti-patterns**: Watch for too many Shared Kernels, Conformist everywhere, hidden dependencies
- **Make it visual**: Workshop approach and clear notation make context maps accessible
- **Keep it current**: Context maps are living documents that evolve with the system
- **Use for planning**: Context maps inform roadmap, team structure, and architectural decisions

Adhering to best practices such as creating focused context maps, documenting patterns, and tailoring views for different perspectives ensures that context mapping remains a valuable tool for both analysis and design in complex systems.
