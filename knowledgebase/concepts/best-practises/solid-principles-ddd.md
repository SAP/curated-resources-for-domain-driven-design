# SOLID Principles in Domain-Driven Design

## Introduction

The SOLID principles are a set of five fundamental design principles in object-oriented programming that aim to make software designs more understandable, flexible, and maintainable. While SOLID principles are general software design guidelines, they have particular relevance in Domain-Driven Design (DDD), where they support the creation of rich, expressive domain models.

This guide explores how SOLID principles apply specifically to DDD contexts, focusing on how they enable robust [Aggregates](../tactical-concepts/aggregate.md), maintainable [Bounded Contexts](../strategic-concepts/boundedcontext.md), and clean domain models.

**Note**: This is not a comprehensive SOLID tutorial. It focuses on the intersection of SOLID and DDD patterns, assuming basic familiarity with object-oriented design.

## Single Responsibility Principle (SRP) in DDD

**Principle**: A class should have one, and only one, reason to change.

### Application to DDD

In DDD, SRP manifests at multiple levels:

#### 1. Bounded Contexts as SRP at Architectural Level

Each [Bounded Context](../strategic-concepts/boundedcontext.md) has a single responsibility within the business domain:

```
❌ Bad: Monolithic "Customer Management" Context
- Customer registration
- Order processing
- Billing
- Support tickets
- Loyalty programs

✅ Good: Separate Bounded Contexts
- Sales Context: Customer leads and acquisition
- Order Context: Order processing and fulfillment
- Billing Context: Invoicing and payments
- Support Context: Ticket management
- Loyalty Context: Rewards and points
```

#### 2. Aggregates as SRP at Tactical Level

Each [Aggregate](../tactical-concepts/aggregate.md) enforces consistency for a single transactional boundary:

```java
// ❌ Violation: Order aggregate doing too much
public class Order {
    public void addItem(Product product) { /* ... */ }
    public void applyDiscount(Coupon coupon) { /* ... */ }
    public void processPayment(PaymentMethod method) { /* ... */ } // Payment responsibility
    public void scheduleShipment(Address address) { /* ... */ } // Shipping responsibility
    public void sendNotification(Customer customer) { /* ... */ } // Notification responsibility
}

// ✅ Good: Focused Order aggregate
public class Order {
    private final OrderId orderId;
    private final List<OrderLine> lines;
    private OrderStatus status;
    private Money totalAmount;

    public void addItem(ProductId productId, int quantity, Money unitPrice) {
        if (status != OrderStatus.DRAFT) {
            throw new IllegalStateException("Cannot modify submitted order");
        }
        lines.add(new OrderLine(productId, quantity, unitPrice));
        recalculateTotalAmount();
    }

    public void submit() {
        if (lines.isEmpty()) {
            throw new IllegalStateException("Cannot submit empty order");
        }
        this.status = OrderStatus.SUBMITTED;
        // Publish domain event for other contexts
        DomainEvents.raise(new OrderSubmitted(this.orderId));
    }
}

// Payment and Shipping are separate aggregates in different contexts
public class Payment { /* ... */ }
public class Shipment { /* ... */ }
```

### Benefits for DDD

- **Clear boundaries**: Each aggregate's responsibility is explicit
- **Easier testing**: Test one responsibility at a time
- **Reduced coupling**: Changes to payment logic don't affect order logic

## Open-Closed Principle (OCP) in DDD

**Principle**: Software entities should be open for extension but closed for modification.

### Application to DDD

#### 1. Domain Events for Extensibility

[Domain Events](../tactical-concepts/domain-events.md) allow behavior extension without modifying existing aggregates:

```java
// Aggregate publishes events (closed for modification)
public class Order {
    public void submit() {
        this.status = OrderStatus.SUBMITTED;
        DomainEvents.raise(new OrderSubmitted(
            this.orderId,
            this.customerId,
            this.totalAmount
        ));
    }
}

// New behaviors added by subscribing to events (open for extension)
public class OrderSubmittedHandler {
    public void handle(OrderSubmitted event) {
        // Send confirmation email
        emailService.sendOrderConfirmation(event.getCustomerId());
    }
}

// Add more handlers without touching Order aggregate
public class InventoryAllocationHandler {
    public void handle(OrderSubmitted event) {
        // Allocate inventory
        inventoryService.allocateForOrder(event.getOrderId());
    }
}
```

#### 2. Strategy Pattern in Domain Services

Use abstractions for varying business rules:

```java
// Domain service closed for modification
public class PricingService {
    public Money calculatePrice(Order order, PricingStrategy strategy) {
        return strategy.calculate(order);
    }
}

// Open for extension: add new pricing strategies
public interface PricingStrategy {
    Money calculate(Order order);
}

public class StandardPricingStrategy implements PricingStrategy {
    public Money calculate(Order order) {
        return order.getSubtotal();
    }
}

public class VolumeDiscountStrategy implements PricingStrategy {
    public Money calculate(Order order) {
        Money subtotal = order.getSubtotal();
        if (order.getItemCount() > 10) {
            return subtotal.multiply(0.9); // 10% discount
        }
        return subtotal;
    }
}

// Add seasonal pricing without modifying existing code
public class SeasonalPricingStrategy implements PricingStrategy {
    public Money calculate(Order order) {
        // Seasonal discount logic
        return order.getSubtotal().multiply(0.85);
    }
}
```

### Benefits for DDD

- **Stable domain model**: Core aggregates don't change when business rules evolve
- **Extensible behavior**: New features via events or strategies
- **Reduced regression risk**: Existing code remains untouched

## Liskov Substitution Principle (LSP) in DDD

**Principle**: Objects should be replaceable with instances of their subtypes without altering correctness.

### Application to DDD

#### Polymorphism in Domain Hierarchies

```java
// Base entity
public abstract class Product {
    protected ProductId id;
    protected Money price;

    public abstract Money calculateShippingCost();

    // Common behavior
    public Money getTotalCost() {
        return price.add(calculateShippingCost());
    }
}

// Subtypes must honor the contract
public class PhysicalProduct extends Product {
    private Weight weight;

    @Override
    public Money calculateShippingCost() {
        // Must return valid Money, never null
        return shippingCalculator.calculate(weight);
    }
}

public class DigitalProduct extends Product {
    @Override
    public Money calculateShippingCost() {
        // LSP honored: returns zero cost, not null or error
        return Money.ZERO;
    }
}

// Usage: works correctly with any Product subtype
public class ShoppingCart {
    public Money calculateTotal(List<Product> products) {
        return products.stream()
            .map(Product::getTotalCost) // LSP: works for all subtypes
            .reduce(Money.ZERO, Money::add);
    }
}
```

### Benefits for DDD

- **Polymorphic domain models**: Use base types confidently
- **Consistent behavior**: Subtypes maintain contracts
- **Reduced special cases**: No need for type checking

## Interface Segregation Principle (ISP) in DDD

**Principle**: Clients should not be forced to depend on methods they do not use.

### Application to DDD

#### 1. Segregated Repository Interfaces

```java
// ❌ Fat repository interface (violates ISP)
public interface OrderRepository {
    Order findById(OrderId id);
    List<Order> findAll();
    List<Order> findByCustomer(CustomerId customerId);
    List<Order> findByDateRange(LocalDate start, LocalDate end);
    List<Order> findByStatus(OrderStatus status);
    Order save(Order order);
    void delete(OrderId id);
    int count();
    // ... 20 more methods
}

// ✅ Segregated interfaces (adheres to ISP)
public interface OrderRepository {
    Order findById(OrderId id);
    Order save(Order order);
}

public interface OrderQueryService {
    List<Order> findByCustomer(CustomerId customerId);
    List<Order> findByDateRange(LocalDate start, LocalDate end);
    List<Order> findByStatus(OrderStatus status);
}

// Aggregates only depend on what they need
public class OrderService {
    private final OrderRepository repository; // Only basic CRUD

    public void submitOrder(OrderId orderId) {
        Order order = repository.findById(orderId);
        order.submit();
        repository.save(order);
    }
}

// Query use cases depend on query interface
public class OrderHistoryService {
    private final OrderQueryService queryService;

    public List<Order> getCustomerOrders(CustomerId customerId) {
        return queryService.findByCustomer(customerId);
    }
}
```

#### 2. Role-Based Domain Service Interfaces

```java
// Clients depend only on what they need
public interface PaymentProcessor {
    PaymentResult process(PaymentRequest request);
}

public interface PaymentRefunder {
    RefundResult refund(PaymentId paymentId, Money amount);
}

public interface PaymentQueryService {
    Payment findById(PaymentId id);
    List<Payment> findByOrder(OrderId orderId);
}
```

### Benefits for DDD

- **Focused dependencies**: Aggregates depend only on needed operations
- **Clear boundaries**: Separate command from query responsibilities ([CQRS](../architectural-concepts/cqrs.md))
- **Easier testing**: Mock only what's used

## Dependency Inversion Principle (DIP) in DDD

**Principle**: High-level modules should not depend on low-level modules. Both should depend on abstractions.

### Application to DDD

#### 1. Hexagonal Architecture Alignment

DIP is fundamental to [Hexagonal Architecture](../architectural-concepts/hexagonal-architecture.md), where the domain layer defines ports (interfaces) implemented by infrastructure:

```
┌─────────────────────────────────────┐
│   Domain Layer (High-level)         │
│                                     │
│   ┌─────────────────────────┐      │
│   │  Order Aggregate        │      │
│   │  - addItem()            │      │
│   │  - submit()             │      │
│   └─────────────────────────┘      │
│              │                      │
│              │ uses                 │
│              ↓                      │
│   ┌─────────────────────────┐      │
│   │  OrderRepository        │      │ ← Domain defines interface
│   │  (interface/port)       │      │
│   └─────────────────────────┘      │
└─────────────────────────────────────┘
               ↑
               │ implements (dependency inverted)
               │
┌─────────────────────────────────────┐
│  Infrastructure Layer (Low-level)   │
│                                     │
│   ┌─────────────────────────┐      │
│   │  SqlOrderRepository     │      │
│   │  (concrete impl)        │      │
│   └─────────────────────────┘      │
└─────────────────────────────────────┘
```

**Code Example**:

```java
// Domain layer defines the interface (port)
package com.example.domain.order;

public interface OrderRepository {
    Order findById(OrderId id);
    void save(Order order);
}

// Domain aggregate uses the interface
package com.example.domain.order;

public class OrderService {
    private final OrderRepository repository; // Depends on abstraction

    public OrderService(OrderRepository repository) {
        this.repository = repository;
    }

    public void submitOrder(OrderId orderId) {
        Order order = repository.findById(orderId);
        order.submit();
        repository.save(order);
    }
}

// Infrastructure implements the interface (adapter)
package com.example.infrastructure.persistence;

import com.example.domain.order.*; // Infrastructure depends on domain

public class SqlOrderRepository implements OrderRepository {
    private final DataSource dataSource;

    @Override
    public Order findById(OrderId id) {
        // SQL implementation details
    }

    @Override
    public void save(Order order) {
        // SQL implementation details
    }
}
```

#### 2. Anti-Corruption Layer

When integrating with external systems, domain defines interface, infrastructure adapts:

```java
// Domain defines what it needs (port)
public interface SupplierPricingService {
    Money getQuote(ProductId productId, int quantity);
}

// Domain uses abstraction
public class ProcurementService {
    private final SupplierPricingService pricingService;

    public void createPurchaseRequisition(ProductId productId, int quantity) {
        Money quote = pricingService.getQuote(productId, quantity);
        // Use quote in domain logic
    }
}

// Infrastructure implements anti-corruption layer
public class ExternalSupplierAdapter implements SupplierPricingService {
    private final ThirdPartySupplierApi externalApi;

    @Override
    public Money getQuote(ProductId productId, int quantity) {
        // Call external API
        ExternalQuote externalQuote = externalApi.requestQuote(
            productId.getValue(),
            quantity
        );

        // Translate external model to domain model (ACL)
        return new Money(
            externalQuote.price_amount,
            Currency.getInstance(externalQuote.currency_code)
        );
    }
}
```

### Benefits for DDD

- **Domain independence**: Business logic doesn't depend on infrastructure
- **Testability**: Mock infrastructure dependencies easily
- **Technology flexibility**: Change databases, message brokers without touching domain

## Cohesion and Coupling in Bounded Contexts

Beyond SOLID, cohesion and coupling principles apply to [Bounded Contexts](../strategic-concepts/boundedcontext.md):

### High Cohesion Within Contexts

Related concepts stay together:

```
Ordering Context (High Cohesion):
- Order aggregate
- OrderLine value object
- OrderStatus enumeration
- OrderRepository
- OrderPlaced domain event
```

### Low Coupling Between Contexts

Contexts communicate through well-defined contracts:

```java
// Ordering Context publishes event (loose coupling)
public class Order {
    public void submit() {
        this.status = OrderStatus.SUBMITTED;
        DomainEvents.raise(new OrderSubmitted(this.orderId, this.customerId));
    }
}

// Billing Context subscribes (no direct dependency on Order aggregate)
public class InvoiceService {
    public void handleOrderSubmitted(OrderSubmitted event) {
        Invoice invoice = Invoice.createFromOrder(
            event.getOrderId(),
            event.getCustomerId()
        );
        invoiceRepository.save(invoice);
    }
}
```

See [Context Mapping](../../tools/contextmapping.md) for integration patterns.

## Practical Guidelines

### When Applying SOLID in DDD

1. **Start with the domain**: Model business concepts first, apply SOLID to improve design
2. **Don't over-engineer**: Simple domains don't need complex abstractions
3. **Refactor towards SOLID**: Evolve design as complexity increases
4. **Test as guide**: If testing is hard, SOLID violations may be present

### Warning Signs

- **God Aggregates**: Violates SRP (aggregate doing too much)
- **Anemic Domain Model**: May indicate improper SRP (logic in services, not entities)
- **Tight Coupling**: Infrastructure mixed with domain (DIP violation)
- **Rigid Models**: Hard to extend behavior (OCP violation)

## Conclusion

SOLID principles support DDD by enabling:

- **Single Responsibility**: Clear aggregate and context boundaries
- **Open-Closed**: Extensible domain models via events and strategies
- **Liskov Substitution**: Reliable polymorphic domain hierarchies
- **Interface Segregation**: Focused, role-based interfaces
- **Dependency Inversion**: Domain independence from infrastructure

When applied thoughtfully, SOLID principles help create domain models that are expressive, maintainable, and aligned with business needs—the core goals of Domain-Driven Design.

## Further Reading

- [Aggregates](../tactical-concepts/aggregate.md) - Tactical pattern for consistency boundaries
- [Bounded Context](../strategic-concepts/boundedcontext.md) - Strategic pattern for domain boundaries
- [Domain Events](../tactical-concepts/domain-events.md) - Enabling OCP through events
- [Encapsulation](./encapsulation.md) - Protecting invariants and hiding implementation
- [CQRS](../architectural-concepts/cqrs.md) - Segregating commands and queries (ISP)

### Books

- Martin, Robert C. *Clean Architecture* - DIP and architectural boundaries
- Vernon, Vaughn. *Implementing Domain-Driven Design* - Tactical patterns with SOLID
- Evans, Eric. *Domain-Driven Design* - Strategic and tactical patterns
