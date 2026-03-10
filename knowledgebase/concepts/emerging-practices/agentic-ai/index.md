# Emerging Practices: Agentic AI and Domain-Driven Design

## Introduction

This section explores the intersection of **Agentic AI** (autonomous AI agents) and **Domain-Driven Design**. As AI systems evolve from recommendation engines to autonomous agents that make decisions and take actions, the need for rigorous domain modeling becomes critical. These emerging practices represent the current state of applying DDD principles to multi-agent systems.

**Important Disclaimer**: These patterns represent emerging practices in a rapidly evolving field. As agentic AI matures, these patterns will be refined based on real-world experience. They should be viewed as starting points for exploration rather than established best practices.

## What is Agentic AI?

**Agentic AI** refers to AI systems that act autonomously within defined boundaries. Unlike traditional AI that recommends actions, agentic AI:

- **Makes decisions** based on business rules and learned behaviors
- **Takes actions** in software systems (creating orders, updating records, triggering workflows)
- **Coordinates with other agents** to accomplish complex multi-step tasks
- **Operates within guardrails** defined by domain models and business policies

**Examples in Enterprise**:
- A procurement agent that automatically creates purchase orders when inventory falls below threshold
- A customer support agent that resolves routine issues without human intervention
- A finance agent that reconciles accounts and flags anomalies for human review

## Why DDD Matters for Agentic AI

### The Core Challenge

When AI agents operate autonomously in business-critical systems, they must understand the domain with precision. An agent that misunderstands what a "Customer," "Order," or "Payment Term" means can make costly mistakes at scale.

### How DDD Addresses This

Domain-Driven Design provides the structured approach to domain modeling that agentic AI requires:

1. **[Ubiquitous Language](../../strategic-concepts/ubiquitouslanguage.md)**: Creates a shared vocabulary between domain experts, developers, and AI agents
2. **[Bounded Contexts](../../strategic-concepts/boundedcontext.md)**: Defines clear boundaries where specific domain models apply, preventing agents from crossing unsafe boundaries
3. **[Aggregates](../../tactical-concepts/aggregate.md)**: Establishes consistency boundaries that constrain agent autonomy to safe operating perimeters
4. **[Domain Events](../../tactical-concepts/domain-events.md)**: Enables event-driven coordination between agents without tight coupling
5. **[Context Mapping](../../../tools/contextmapping.md)**: Defines relationships between agents operating in different bounded contexts

### Key Benefits

- **Explainability**: Agent actions trace back to domain concepts that business stakeholders recognize
- **Safety**: Aggregates enforce invariants, preventing agents from leaving systems in invalid states
- **Governance**: Bounded contexts enforce data sovereignty and regulatory boundaries
- **Maintainability**: Clear domain models make agent behavior understandable and debuggable
- **Scalability**: Loose coupling through events allows independent agent development and deployment

## Agent-to-Agent (A2A) Communication

**Agent-to-Agent (A2A) communication** represents peer-to-peer coordination between autonomous AI agents. This is fundamentally different from agents consuming tools or APIs.

### A2A vs Tool Use (e.g., MCP)

| Aspect | Tool Use (MCP) | A2A Communication |
|--------|----------------|-------------------|
| **Pattern** | Client-to-Service | Peer-to-Peer |
| **Relationship** | Agent consumes tools | Agents collaborate as peers |
| **Consistency** | Synchronous (request-response) | Eventual consistency (event-driven) |
| **DDD Pattern** | Open Host Service | Full Context Mapping patterns |
| **Use Case** | Agent needs capability | Agents coordinate workflows |

**Key Insight**: Tool use (MCP) solves "agent needs capability." A2A solves "agents need to work together."

### DDD Patterns for A2A

When designing multi-agent systems, all DDD Context Mapping patterns apply:

- **Partnership**: Two agents collaborate as equals (bi-directional events)
- **Customer-Supplier**: Upstream agent provides capabilities to downstream agent
- **Anti-Corruption Layer**: Consuming agent translates external agent's model
- **Shared Kernel**: Multiple agents share a common subdomain model
- **Conformist**: Agent adapts completely to another agent's model

See [Agent-to-Agent Communication and DDD](./a2a-communication.md) for detailed patterns and examples.

## Key Architectural Patterns

### 1. Bounded Context per Agent Type

Group related agents into bounded contexts based on domain responsibilities:

```
┌─────────────────────────────┐
│  Procurement Context        │
│  - Purchase Order Agent     │
│  - Requisition Agent        │
│  - Approval Agent           │
└─────────────────────────────┘

┌─────────────────────────────┐
│  Inventory Context          │
│  - Stock Allocation Agent   │
│  - Replenishment Agent      │
└─────────────────────────────┘
```

**Benefits**:
- Clear domain boundaries
- Independent deployment
- Reduced cognitive load for developers

### 2. Event-Driven Coordination

Agents coordinate through domain events rather than direct calls:

```
[Purchase Order Agent] → publishes: OrderPlaced
                                        ↓
[Inventory Agent] → subscribes → allocates stock → publishes: InventoryAllocated
                                                                       ↓
[Fulfillment Agent] → subscribes → prepares shipment
```

**Benefits**:
- Loose coupling
- Asynchronous processing
- Audit trail of agent actions

### 3. Aggregate-Based Guardrails

Agents interact with aggregates, which enforce business rules:

```typescript
// Agent cannot bypass aggregate rules
class PurchaseOrderAgent {
  async createOrder(customerId: string, items: OrderItem[]) {
    const order = Order.create(customerId); // Factory ensures valid initial state

    for (const item of items) {
      order.addItem(item); // Aggregate validates each addition
    }

    order.submit(); // Aggregate checks all invariants

    await this.orderRepository.save(order);
  }
}
```

**Benefits**:
- Consistent business rule enforcement
- Agent autonomy within safe boundaries
- Testable invariants

## Design Techniques

### EventStorming for Agent Discovery

[EventStorming](../../../tools/eventstorming.md) is the primary technique for discovering agent responsibilities and interactions:

1. **Agent Discovery Phase**: Identify what tasks/decisions could be automated
2. **Event Timeline**: Map events that cross agent boundaries
3. **Command-Event Linking**: Define what agents publish and consume
4. **Bounded Context Identification**: Group agents by domain responsibility
5. **Context Mapping**: Define relationships between agent contexts

**Output**: Agent responsibility matrix, inter-agent event catalog, context map

### Context Mapping for Agent Relationships

[Context Mapping](../../../tools/contextmapping.md) defines how agents relate to each other:

- Draw boxes for each agent or agent group (bounded context)
- Draw relationships between contexts
- Label relationships with DDD patterns (Partnership, Customer-Supplier, ACL)
- Identify published events at each boundary

## Practical Considerations

### When to Use Agentic AI with DDD

**Good Fit**:
- Complex business domains with well-defined rules
- Multi-step workflows requiring coordination
- Systems where explainability is critical
- Regulated industries requiring governance

**Poor Fit**:
- Simple CRUD operations
- Domains with poorly understood or rapidly changing rules
- Systems where deterministic behavior is impossible to define

### Common Pitfalls

1. **Over-Automation**: Automating before the domain is understood
2. **Tight Coupling**: Agents calling each other synchronously instead of using events
3. **Ignoring Bounded Contexts**: Creating "god agents" that try to do everything
4. **Weak Domain Models**: Agents operating without aggregate boundaries or invariants
5. **Missing Anti-Corruption Layers**: Allowing external agents to pollute internal domain models

### Governance and Safety

- **Define Autonomy Levels**: Not all agents should have the same level of autonomy
- **Implement Circuit Breakers**: Agents should detect and handle failure modes
- **Audit Trails**: Log all agent actions as domain events for traceability
- **Human-in-Loop**: Critical decisions should escalate to humans
- **Rollback Mechanisms**: Implement compensating transactions for failed multi-agent workflows

## Relationship to Other DDD Concepts

- **[Strategic Design](../../strategic-concepts/boundedcontext.md)**: Bounded contexts define agent scopes
- **[Tactical Design](../../tactical-concepts/aggregate.md)**: Aggregates provide agent guardrails
- **[Domain Events](../../tactical-concepts/domain-events.md)**: Enable agent coordination
- **[EventStorming](../../../tools/eventstorming.md)**: Discover agent responsibilities
- **[Context Mapping](../../../tools/contextmapping.md)**: Define agent relationships
- **[Cognitive Load](../additional-concepts/cognitive-load-ddd.md)**: Reducing complexity in multi-agent systems

## Contents of This Section

### [Agent-to-Agent Communication and DDD](./a2a-communication.md)

Comprehensive guide to designing peer-to-peer agent coordination using DDD patterns:
- A2A vs MCP architectural comparison
- EventStorming workshop for A2A system discovery
- Context Mapping patterns (Partnership, Customer-Supplier, ACL)
- Event-driven coordination patterns
- Practical implementation examples

## Further Reading

### Books
- Vernon, Vaughn. *Implementing Domain-Driven Design* (Tactical patterns for agent boundaries)
- Khononov, Vlad. *Learning Domain-Driven Design* (Modern perspective on bounded contexts)
- Newman, Sam. *Building Microservices* (Distributed system patterns applicable to agents)

### Articles and Resources
- Brandolini, Alberto. *Introducing EventStorming* (Essential for agent discovery workshops)
- [DDD and AI/ML Systems](https://www.infoq.com/articles/ddd-ml-systems/) - Applying DDD to AI systems
- [Multi-Agent System Design Patterns](https://arxiv.org/abs/2402.01822) - Academic perspective on agent coordination

### Conferences
- **DDD Europe** (https://dddeurope.com/) - Annual conference with emerging AI+DDD content
- **KanDDDinsky** (https://kandddinsky.de/) - Berlin-based DDD conference

## Contributing to These Emerging Practices

These patterns are evolving. If you apply DDD to agentic AI systems:

1. Document your learnings and share with the community
2. Contribute case studies to this repository
3. Participate in DDD conferences and unconferences
4. Join the conversation in DDD community forums

The intersection of DDD and Agentic AI is a frontier. Your experience helps refine these practices for the broader community.
