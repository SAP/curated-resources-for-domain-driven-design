# Agent-to-Agent (A2A) Communication and Domain-Driven Design

## Overview

Agent-to-Agent (A2A) communication represents **peer-to-peer coordination** between autonomous AI agents, fundamentally different from the **client-to-service** pattern embodied by Model Context Protocol (MCP) or traditional APIs. While MCP servers act as Open Host Services exposing tools to agents, A2A requires full [Context Mapping](../../../tools/contextmapping.md) patterns to manage the complexity of distributed, autonomous systems.

## A2A vs MCP: Architectural Comparison

| Aspect | MCP | A2A Communication |
|--------|-----|-------------------|
| **Communication Pattern** | Client-to-Service (Conformist) | Peer-to-Peer (Partnership/Customer-Supplier/ACL) |
| **Protocol Standardization** | Standardized (JSON-RPC 2.0) | No universal standard (framework-dependent) |
| **Context Mapping Pattern** | Open Host Service + Published Language | All patterns: Partnership, CS, ACL, Shared Kernel |
| **Agent Autonomy** | Agent consumes tools passively | Agents negotiate, coordinate, collaborate |
| **Consistency Model** | Synchronous (request-response) | Eventual consistency (event-driven) |
| **Bounded Context Relationship** | Agent → External Service | Agent ↔ Agent (peer contexts) |
| **Primary Use Case** | Tool/capability exposure | Multi-agent orchestration, workflow delegation |

**Key Insight**: MCP solves the "agent needs capability" problem. A2A solves the "agents need to work together" problem.

## EventStorming for A2A System Discovery

[EventStorming](../../../tools/eventstorming.md) is the **primary tool** for discovering A2A communication patterns. The technique maps directly to multi-agent design:

### Standard EventStorming → A2A Mapping

| EventStorming Element | A2A Equivalent | Purpose |
|----------------------|----------------|---------|
| **Domain Event** (orange) | Inter-agent message | What happened that other agents care about? |
| **Command** (blue) | Agent action/task | What does an agent do? |
| **Actor** (yellow) | AI Agent | Who performs the action? |
| **Policy** (lilac) | Agent coordination rule | "When X happens, Agent Y should..." |
| **Aggregate** (yellow box) | Agent internal state | Consistency boundary within single agent |
| **External System** (pink) | MCP Server or human | Non-agent participants |
| **Read Model** (green) | Shared context/memory | What information do agents query? |

### A2A-Specific EventStorming Workshop

**Duration**: 6 hours
**Participants**: Domain experts, architects, agent designers, product owners

#### Part 1: Agent Discovery (90 min)

1. **Brain dump agent responsibilities** (30 min)
   - Exercise: "What tasks/decisions could agents automate in this domain?"
   - Group by capability: reasoning, action, coordination, memory

2. **Define agent identities** (30 min)
   - Name each agent (e.g., "PurchaseOrderAgent", "InventoryAgent")
   - Draft agent charter: "Responsible for..." (1-2 sentences)

3. **Map agent autonomy levels** (30 min)
   - Level 0: No autonomy (human-in-loop for every decision)
   - Level 1: Recommender (suggests actions)
   - Level 2: Conditional autonomy (acts within policy boundaries)
   - Level 3: Full autonomy (acts independently, reports outcomes)

#### Part 2: Event-Driven Interaction Design (120 min)

1. **Domain event timeline** (45 min)
   - Walk through a critical business flow (e.g., "Procure-to-Pay")
   - Identify events that **cross agent boundaries**
   - Example: `PurchaseOrderCreated`, `SupplierQuoteReceived`, `InventoryThresholdBreached`

2. **Command-event linking** (45 min)
   - For each event, identify which agent **publishes** it (source)
   - For each event, identify which agents **subscribe** to it (consumers)
   - Draw arrows: Event → Consuming Agent → Command

3. **Policy-driven coordination** (30 min)
   - Identify reactive policies: "When `InventoryThresholdBreached`, then `PurchaseAgent.CreateOrder`"
   - Mark policies with agent ownership: Which agent enforces this rule?

#### Part 3: Bounded Context Identification (90 min)

1. **Cluster agents by responsibility** (30 min)
   - Group agents that share a common domain language
   - Example: `PurchaseOrderAgent`, `RequisitionAgent`, `ApprovalAgent` → **Procurement Context**

2. **Identify context boundaries** (30 min)
   - Draw boxes around clusters
   - Mark boundary-crossing events (inter-context communication)

3. **Context Mapping** (30 min)
   - For each boundary-crossing event, determine relationship:
     - **Partnership**: Agents collaborate as peers (bi-directional events)
     - **Customer-Supplier**: Upstream agent serves downstream (uni-directional)
     - **Anti-Corruption Layer**: Consuming agent translates external agent's model

#### Part 4: Message Flow and Contract Definition (90 min)

1. **Define event schemas** (45 min)
   - For each boundary-crossing event, draft JSON Schema
   - Identify: Event name, payload structure, versioning strategy

2. **Identify conversation patterns** (30 min)
   - Request-Reply: Agent A asks, Agent B responds
   - Publish-Subscribe: Agent A announces, multiple agents react
   - Saga: Multi-step workflow requiring coordination

3. **Red flags and risks** (15 min)
   - Circular dependencies (Agent A waits for Agent B, which waits for Agent A)
   - Single point of failure (all agents depend on one agent)
   - Tight temporal coupling (Agent A must respond within 100ms)

**Workshop Deliverables**:
- Agent responsibility matrix (agents × domains)
- Inter-agent event catalog (50-100 events)
- Context map showing agent groupings and relationships
- Critical conversation pattern diagrams (3-5 key flows)

## Context Mapping Patterns for A2A

### Pattern 1: Partnership (Peer Agents)

**Definition**: Two agents collaborate as equals, sharing a common goal with bi-directional communication.

**When to Use**:
- Agents co-own a business process
- Both agents need to coordinate decisions
- Failure of one agent affects the other

**Example: Order Fulfillment**

```
┌─────────────────────┐         ┌─────────────────────┐
│  InventoryAgent     │ ←─────→ │  FulfillmentAgent   │
│  (Procurement BC)   │         │  (Logistics BC)     │
└─────────────────────┘         └─────────────────────┘

Events exchanged:
- InventoryAgent → FulfillmentAgent: InventoryAllocated
- FulfillmentAgent → InventoryAgent: ShipmentPrepared
- Both publish: OrderReadyForShipment (jointly)
```

**DDD Guidance**:
- Define **shared event schema** (Published Language)
- Both agents must handle eventual consistency
- Use **Saga pattern** for multi-step workflows requiring both agents
- Implement **compensating transactions** if one agent fails mid-process

**Implementation Sketch**:

```typescript
// Published Language: Shared event definitions
interface InventoryAllocated {
  eventType: "InventoryAllocated";
  orderId: string;
  items: Array<{ sku: string; quantity: number; warehouseId: string }>;
  allocationId: string;
  timestamp: string;
}

interface ShipmentPrepared {
  eventType: "ShipmentPrepared";
  orderId: string;
  shipmentId: string;
  estimatedDeparture: string;
  timestamp: string;
}

// InventoryAgent (Partner 1)
class InventoryAgent {
  async handleOrderPlaced(event: OrderPlaced): Promise<void> {
    const allocation = await this.allocateInventory(event.orderId);
    await this.eventBus.publish<InventoryAllocated>({
      eventType: "InventoryAllocated",
      orderId: event.orderId,
      items: allocation.items,
      allocationId: allocation.id,
      timestamp: new Date().toISOString(),
    });
  }

  async handleShipmentPrepared(event: ShipmentPrepared): Promise<void> {
    // React to partner's event
    await this.confirmAllocation(event.orderId, event.shipmentId);
  }
}

// FulfillmentAgent (Partner 2)
class FulfillmentAgent {
  async handleInventoryAllocated(event: InventoryAllocated): Promise<void> {
    const shipment = await this.prepareShipment(event.orderId, event.items);
    await this.eventBus.publish<ShipmentPrepared>({
      eventType: "ShipmentPrepared",
      orderId: event.orderId,
      shipmentId: shipment.id,
      estimatedDeparture: shipment.departureTime,
      timestamp: new Date().toISOString(),
    });
  }
}
```

### Pattern 2: Customer-Supplier (Hierarchical Agents)

**Definition**: Upstream agent (Supplier) provides capabilities to downstream agent (Customer). Uni-directional relationship.

**When to Use**:
- Clear provider-consumer relationship
- Upstream agent exposes well-defined capabilities
- Downstream agent depends on upstream for task completion

**Example: Approval Workflow**

```
┌─────────────────────┐
│  ApprovalAgent      │ (Supplier)
│  (Governance BC)    │
└──────────┬──────────┘
           │ publishes: ApprovalDecisionMade
           ↓
┌─────────────────────┐
│  PurchaseAgent      │ (Customer)
│  (Procurement BC)   │
└─────────────────────┘
```

**DDD Guidance**:
- Supplier defines Published Language (event schema)
- Customer **may** use Anti-Corruption Layer if internal model differs
- Supplier should be stable; Customer adapts to Supplier changes
- Use **Customer-Supplier Development**: Customer influences Supplier roadmap

**Implementation Sketch**:

```typescript
// Supplier (ApprovalAgent) defines Published Language
interface ApprovalDecisionMade {
  eventType: "ApprovalDecisionMade";
  approvalRequestId: string;
  decision: "APPROVED" | "REJECTED" | "ESCALATED";
  approver: string;
  comments?: string;
  timestamp: string;
}

// Supplier publishes events
class ApprovalAgent {
  async handleApprovalRequest(request: ApprovalRequest): Promise<void> {
    const decision = await this.evaluateRequest(request);
    await this.eventBus.publish<ApprovalDecisionMade>({
      eventType: "ApprovalDecisionMade",
      approvalRequestId: request.id,
      decision: decision.outcome,
      approver: decision.approver,
      comments: decision.rationale,
      timestamp: new Date().toISOString(),
    });
  }
}

// Customer (PurchaseAgent) consumes events
class PurchaseAgent {
  async handleApprovalDecisionMade(event: ApprovalDecisionMade): Promise<void> {
    const order = await this.orderRepository.findByApprovalRequest(
      event.approvalRequestId
    );

    if (event.decision === "APPROVED") {
      await order.markApproved();
      await this.placeOrderWithSupplier(order);
    } else if (event.decision === "REJECTED") {
      await order.cancel("Approval rejected: " + event.comments);
    }

    await this.orderRepository.save(order);
  }
}
```

### Pattern 3: Anti-Corruption Layer (Protecting Agent Domains)

**Definition**: Downstream agent uses ACL to translate upstream agent's model into its own domain language.

**When to Use**:
- Upstream agent uses different domain concepts/terminology
- Downstream agent has rich internal domain model to protect
- Upstream agent's model is unstable or frequently changing

**Example: External Agent Integration**

```
┌─────────────────────┐
│  External AI Agent  │ (Upstream - outside our control)
│  (3rd party)        │
└──────────┬──────────┘
           │ publishes: ThirdPartyEventFormat
           ↓
     ┌──────────┐
     │   ACL    │ (Translation Layer)
     └────┬─────┘
          │ translates to: InternalDomainEvent
          ↓
┌─────────────────────┐
│  Internal Agent     │
│  (Our Domain)       │
└─────────────────────┘
```

**DDD Guidance**:
- ACL is owned by **downstream** team
- ACL translates events, not just field mapping (semantic translation)
- Protects internal agents from external model changes
- May enrich/filter data based on internal needs

**Implementation Sketch**:

```typescript
// External agent's model (we don't control this)
interface ThirdPartySupplierEvent {
  event_name: "supplier_response";
  req_id: string;
  vendor_id: string;
  price_amount: number;
  price_currency: string;
  delivery_days: number;
}

// Our internal domain model
interface SupplierQuoteReceived {
  eventType: "SupplierQuoteReceived";
  requisitionId: string;
  supplier: SupplierId;
  quote: MoneyValue;
  estimatedDelivery: DeliveryTimeframe;
  timestamp: string;
}

// Anti-Corruption Layer (owned by our team)
class SupplierIntegrationACL {
  async translateExternalEvent(
    external: ThirdPartySupplierEvent
  ): Promise<SupplierQuoteReceived> {
    return {
      eventType: "SupplierQuoteReceived",
      requisitionId: await this.mapRequestId(external.req_id),
      supplier: new SupplierId(external.vendor_id),
      quote: new MoneyValue(external.price_amount, external.price_currency),
      estimatedDelivery: DeliveryTimeframe.fromDays(external.delivery_days),
      timestamp: new Date().toISOString(),
    };
  }

  private async mapRequestId(externalId: string): Promise<string> {
    // Look up internal requisition ID from external request ID
    return await this.requisitionMappingService.getInternalId(externalId);
  }
}

// Our procurement agent consumes the translated event
class ProcurementAgent {
  async handleSupplierQuoteReceived(event: SupplierQuoteReceived): Promise<void> {
    // Works with our internal domain model, unaware of external format
    const requisition = await this.requisitionRepository.find(event.requisitionId);
    await requisition.addQuote(event.supplier, event.quote, event.estimatedDelivery);
    await this.requisitionRepository.save(requisition);
  }
}
```

## Event-Driven Coordination Patterns

### Pattern 1: Fire-and-Forget (Publish-Subscribe)

**Use When**: Source agent doesn't need confirmation, multiple consumers may react

```typescript
class InventoryAgent {
  async checkStockLevels(): Promise<void> {
    for (const product of await this.getTrackedProducts()) {
      if (product.stockLevel < product.reorderPoint) {
        // Publish event - don't wait for response
        await this.eventBus.publish({
          eventType: "InventoryThresholdBreached",
          productId: product.id,
          currentStock: product.stockLevel,
          reorderPoint: product.reorderPoint,
          timestamp: new Date().toISOString(),
        });
      }
    }
  }
}

// Multiple agents can subscribe
class ProcurementAgent {
  async handleInventoryThresholdBreached(event: InventoryThresholdBreached) {
    await this.createPurchaseRequisition(event.productId);
  }
}

class AlertingAgent {
  async handleInventoryThresholdBreached(event: InventoryThresholdBreached) {
    await this.notifyWarehouseManager(event);
  }
}
```

### Pattern 2: Request-Reply (Synchronous Query)

**Use When**: Agent needs immediate response to proceed

```typescript
class OrderAgent {
  async processOrder(orderId: string): Promise<void> {
    // Query inventory agent synchronously
    const availabilityResponse = await this.sendRequest<InventoryAvailabilityQuery>({
      requestType: "InventoryAvailabilityQuery",
      productIds: order.items.map(i => i.productId),
      requestId: generateId(),
    });

    if (availabilityResponse.allAvailable) {
      await this.confirmOrder(orderId);
    } else {
      await this.backorderOrder(orderId, availabilityResponse.unavailableItems);
    }
  }
}
```

**Warning**: Synchronous calls create tight coupling. Use sparingly, prefer eventual consistency.

### Pattern 3: Saga (Distributed Transaction)

**Use When**: Multi-step workflow requires coordination across agents with rollback capability

```typescript
// Order Fulfillment Saga
class OrderFulfillmentSaga {
  async execute(orderId: string): Promise<void> {
    const sagaState = new SagaState(orderId);

    try {
      // Step 1: Reserve inventory
      await this.reserveInventory(orderId);
      sagaState.markStepComplete("inventory_reserved");

      // Step 2: Process payment
      await this.processPayment(orderId);
      sagaState.markStepComplete("payment_processed");

      // Step 3: Schedule shipment
      await this.scheduleShipment(orderId);
      sagaState.markStepComplete("shipment_scheduled");

      await sagaState.markComplete();
    } catch (error) {
      // Rollback completed steps in reverse order
      await this.compensate(sagaState);
    }
  }

  private async compensate(state: SagaState): Promise<void> {
    if (state.isStepComplete("shipment_scheduled")) {
      await this.cancelShipment(state.orderId);
    }
    if (state.isStepComplete("payment_processed")) {
      await this.refundPayment(state.orderId);
    }
    if (state.isStepComplete("inventory_reserved")) {
      await this.releaseInventory(state.orderId);
    }
  }
}
```

## Practical Considerations

### Agent Scope and Autonomy

Define clear boundaries for each agent:

```typescript
interface AgentCapabilityProfile {
  agentId: string;
  autonomyLevel: 0 | 1 | 2 | 3; // 0 = no autonomy, 3 = full autonomy
  boundedContext: string;
  capabilities: string[];
  constraints: {
    maxTransactionValue?: number;
    requiresApprovalFor?: string[];
    cannotModify?: string[];
  };
}
```

### Event Schema Versioning

Plan for schema evolution:

```typescript
interface DomainEvent {
  eventType: string;
  eventVersion: string; // Semantic versioning: "1.0.0"
  eventId: string;
  timestamp: string;
  payload: unknown;
}

// Agents handle multiple versions
class PurchaseAgent {
  async handleOrderPlaced(event: DomainEvent): Promise<void> {
    switch (event.eventVersion) {
      case "1.0.0":
        return this.handleOrderPlacedV1(event.payload);
      case "2.0.0":
        return this.handleOrderPlacedV2(event.payload);
      default:
        throw new Error(`Unsupported event version: ${event.eventVersion}`);
    }
  }
}
```

### Monitoring and Observability

Instrument agent interactions:

- **Trace IDs**: Propagate correlation IDs across agent boundaries
- **Agent Action Logs**: Log all decisions with reasoning
- **Event Audit Trail**: Store all published events for debugging
- **Performance Metrics**: Track latency between agents
- **Circuit Breakers**: Detect and handle cascading failures

## Anti-Patterns to Avoid

### 1. Chatty Agents

**Problem**: Agents making frequent synchronous calls to each other

**Solution**: Batch requests, use eventual consistency, publish-subscribe instead of request-reply

### 2. God Agent

**Problem**: Single agent responsible for too many domains

**Solution**: Split into bounded contexts, define clear responsibilities

### 3. Implicit Dependencies

**Problem**: Agent depends on another agent's internal state

**Solution**: Communicate only through published events, use explicit contracts

### 4. Missing Compensations

**Problem**: No rollback logic when multi-agent workflows fail

**Solution**: Implement Saga pattern with compensating transactions

### 5. Unbounded Autonomy

**Problem**: Agents can perform any action without constraints

**Solution**: Use [Aggregates](../../tactical-concepts/aggregate.md) to enforce invariants, define explicit capability profiles

## Conclusion

Agent-to-Agent communication requires rigorous application of Domain-Driven Design patterns. By treating agents as bounded contexts, using Context Mapping to define relationships, and coordinating through domain events, teams can build multi-agent systems that are:

- **Maintainable**: Clear boundaries and explicit contracts
- **Scalable**: Loose coupling enables independent evolution
- **Governable**: Audit trails and constraints built into the design
- **Explainable**: Domain language makes agent behavior understandable

The techniques presented here—EventStorming for agent discovery, Context Mapping for relationship definition, and event-driven coordination—provide a structured approach to designing reliable, business-aligned multi-agent systems.

## Further Reading

- [EventStorming](../../../tools/eventstorming.md) - Workshop technique for agent discovery
- [Context Mapping](../../../tools/contextmapping.md) - Define agent relationships
- [Domain Events](../../tactical-concepts/domain-events.md) - Event-driven architecture
- [Bounded Context](../../strategic-concepts/boundedcontext.md) - Define agent scopes
- [Aggregates](../../tactical-concepts/aggregate.md) - Enforce agent guardrails
