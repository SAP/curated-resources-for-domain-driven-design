# Encapsulation in Domain-Driven Design

## Introduction

**Encapsulation** is a foundational principle in object-oriented programming and a critical best practice in Domain-Driven Design. It refers to bundling data and the methods that operate on that data within a single unit, while hiding internal implementation details from external access. In DDD, proper encapsulation ensures that domain invariants are consistently enforced, business rules are protected, and the domain model remains expressive and maintainable.

Encapsulation is not merely about making fields private—it is about designing aggregates, entities, and value objects that expose behavior rather than data, ensuring that the domain model accurately reflects business concepts while preventing invalid states.

## Why Encapsulation Matters in DDD

Encapsulation provides several critical benefits in domain-driven design:

- **Invariant Protection**: Ensures business rules are enforced at all times by controlling how state can be modified.
- **Reduced Complexity**: Hides implementation details, allowing clients to interact with domain objects through clear, intention-revealing interfaces.
- **Maintainability**: Changes to internal implementation do not affect external clients, making refactoring safer.
- **Expressiveness**: Well-encapsulated objects communicate their purpose and constraints through their public API.
- **Consistency Boundaries**: Aggregates use encapsulation to maintain transactional consistency within their boundaries.

## Information Hiding Principles

**Information hiding** is the core concept behind encapsulation. In DDD, this means:

1. **Hide Implementation Details**: Internal state and logic should be hidden from external clients.
2. **Expose Behavior, Not Data**: Objects should provide methods that perform operations rather than exposing getters and setters for all fields.
3. **Use Intention-Revealing Interfaces**: Public methods should clearly communicate what they do in domain terms.
4. **Protect Invariants**: All modifications to state should pass through controlled entry points that validate business rules.

### Example: Payment Domain

```java
// Poor encapsulation - exposes internal state
public class Payment {
    public BigDecimal amount;
    public PaymentStatus status;
    public LocalDateTime processedAt;
}

// Good encapsulation - hides implementation, exposes behavior
public class Payment {
    private final PaymentId id;
    private final BigDecimal amount;
    private PaymentStatus status;
    private LocalDateTime processedAt;

    public Payment(PaymentId id, BigDecimal amount) {
        if (amount.compareTo(BigDecimal.ZERO) <= 0) {
            throw new IllegalArgumentException("Payment amount must be positive");
        }
        this.id = id;
        this.amount = amount;
        this.status = PaymentStatus.PENDING;
    }

    public void process() {
        if (status != PaymentStatus.PENDING) {
            throw new IllegalStateException("Only pending payments can be processed");
        }
        this.status = PaymentStatus.PROCESSED;
        this.processedAt = LocalDateTime.now();
    }

    public boolean isProcessed() {
        return status == PaymentStatus.PROCESSED;
    }

    public BigDecimal getAmount() {
        return amount; // Safe - BigDecimal is immutable
    }
}
```

## Encapsulation in Aggregates

[Aggregates](../tactical-concepts/aggregate.md) are the primary consistency boundary in DDD, and encapsulation is essential to their design. The **aggregate root** controls all access to entities and value objects within the aggregate boundary.

### Aggregate Root Responsibilities

1. **Single Entry Point**: All modifications to the aggregate must go through the aggregate root.
2. **Invariant Enforcement**: The root ensures that all business rules spanning multiple entities are maintained.
3. **Identity Management**: Only the aggregate root is referenced from outside the boundary; internal entities are not directly accessible.
4. **Transactional Boundary**: The aggregate root defines what must change together in a transaction.

### Example: Order Aggregate

```java
public class Order {
    private final OrderId orderId;
    private final CustomerId customerId;
    private final List<OrderLine> orderLines;
    private OrderStatus status;
    private BigDecimal totalAmount;

    // Private constructor - use factory method
    private Order(OrderId orderId, CustomerId customerId) {
        this.orderId = orderId;
        this.customerId = customerId;
        this.orderLines = new ArrayList<>();
        this.status = OrderStatus.DRAFT;
        this.totalAmount = BigDecimal.ZERO;
    }

    public static Order create(OrderId orderId, CustomerId customerId) {
        return new Order(orderId, customerId);
    }

    // Behavior-focused method that maintains invariants
    public void addProduct(ProductId productId, int quantity, BigDecimal unitPrice) {
        if (status != OrderStatus.DRAFT) {
            throw new IllegalStateException("Cannot add products to a submitted order");
        }
        if (quantity <= 0) {
            throw new IllegalArgumentException("Quantity must be positive");
        }

        OrderLine orderLine = new OrderLine(productId, quantity, unitPrice);
        orderLines.add(orderLine);
        recalculateTotalAmount();
    }

    public void submit() {
        if (orderLines.isEmpty()) {
            throw new IllegalStateException("Cannot submit an empty order");
        }
        if (status != OrderStatus.DRAFT) {
            throw new IllegalStateException("Order has already been submitted");
        }
        this.status = OrderStatus.SUBMITTED;
    }

    // Encapsulated calculation - not exposed externally
    private void recalculateTotalAmount() {
        this.totalAmount = orderLines.stream()
            .map(OrderLine::getLineTotal)
            .reduce(BigDecimal.ZERO, BigDecimal::add);
    }

    // Safe read-only access
    public BigDecimal getTotalAmount() {
        return totalAmount;
    }

    public OrderStatus getStatus() {
        return status;
    }

    // Returns defensive copy to prevent external modification
    public List<OrderLine> getOrderLines() {
        return Collections.unmodifiableList(orderLines);
    }
}

// Internal entity - not exposed outside aggregate
class OrderLine {
    private final ProductId productId;
    private final int quantity;
    private final BigDecimal unitPrice;

    OrderLine(ProductId productId, int quantity, BigDecimal unitPrice) {
        this.productId = productId;
        this.quantity = quantity;
        this.unitPrice = unitPrice;
    }

    BigDecimal getLineTotal() {
        return unitPrice.multiply(BigDecimal.valueOf(quantity));
    }
}
```

### Key Encapsulation Patterns in Aggregates

- **Factory Methods**: Use static factory methods instead of public constructors to control object creation.
- **Defensive Copies**: Return copies of collections to prevent external modification.
- **Immutable Collections**: Use `Collections.unmodifiableList()` or similar to prevent modification.
- **Package-Private Internal Entities**: Make internal entities accessible only within the aggregate package.

## Encapsulation in Value Objects

[Value Objects](../tactical-concepts/value-objects.md) are immutable and defined by their attributes rather than identity. Encapsulation in value objects focuses on:

1. **Immutability**: All fields are final and cannot be changed after construction.
2. **Validation**: Constructor enforces all constraints.
3. **Self-Contained Behavior**: Operations return new value objects rather than modifying state.

### Example: Money Value Object

```java
public final class Money {
    private final BigDecimal amount;
    private final Currency currency;

    public Money(BigDecimal amount, Currency currency) {
        if (amount == null || currency == null) {
            throw new IllegalArgumentException("Amount and currency cannot be null");
        }
        if (amount.compareTo(BigDecimal.ZERO) < 0) {
            throw new IllegalArgumentException("Amount cannot be negative");
        }
        this.amount = amount.setScale(2, RoundingMode.HALF_UP);
        this.currency = currency;
    }

    public Money add(Money other) {
        if (!this.currency.equals(other.currency)) {
            throw new IllegalArgumentException("Cannot add money with different currencies");
        }
        return new Money(this.amount.add(other.amount), this.currency);
    }

    public Money multiply(BigDecimal factor) {
        return new Money(this.amount.multiply(factor), this.currency);
    }

    public BigDecimal getAmount() {
        return amount; // Safe - BigDecimal is immutable
    }

    public Currency getCurrency() {
        return currency; // Safe - Currency is immutable
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (!(o instanceof Money)) return false;
        Money money = (Money) o;
        return amount.compareTo(money.amount) == 0 &&
               currency.equals(money.currency);
    }

    @Override
    public int hashCode() {
        return Objects.hash(amount, currency);
    }
}
```

## Encapsulation in Entities

[Entities](../tactical-concepts/entities.md) have identity and may change over time. Encapsulation in entities focuses on:

1. **Identity Protection**: Identity should be immutable and assigned at creation.
2. **Controlled Mutations**: State changes occur through intention-revealing methods.
3. **Lifecycle Management**: State transitions follow business rules.

### Example: Customer Entity

```java
public class Customer {
    private final CustomerId customerId;
    private PersonalInfo personalInfo;
    private CustomerStatus status;
    private Address shippingAddress;

    public Customer(CustomerId customerId, PersonalInfo personalInfo) {
        this.customerId = Objects.requireNonNull(customerId);
        this.personalInfo = Objects.requireNonNull(personalInfo);
        this.status = CustomerStatus.ACTIVE;
    }

    public void updatePersonalInfo(PersonalInfo newInfo) {
        if (status == CustomerStatus.SUSPENDED) {
            throw new IllegalStateException("Cannot update info for suspended customer");
        }
        this.personalInfo = Objects.requireNonNull(newInfo);
    }

    public void suspend() {
        if (status == CustomerStatus.CLOSED) {
            throw new IllegalStateException("Cannot suspend a closed customer account");
        }
        this.status = CustomerStatus.SUSPENDED;
    }

    public void reactivate() {
        if (status != CustomerStatus.SUSPENDED) {
            throw new IllegalStateException("Only suspended customers can be reactivated");
        }
        this.status = CustomerStatus.ACTIVE;
    }

    public CustomerId getId() {
        return customerId; // Identity is immutable
    }

    public boolean isActive() {
        return status == CustomerStatus.ACTIVE;
    }
}
```

## The Tell, Don't Ask Principle

The **Tell, Don't Ask** principle is closely related to encapsulation. Instead of asking an object for its data and then making decisions based on that data, tell the object what to do and let it make the decision internally.

### Anti-Pattern: Ask Then Act

```java
// Asking for data and making decisions externally
if (order.getStatus() == OrderStatus.DRAFT &&
    order.getOrderLines().size() > 0 &&
    order.getTotalAmount().compareTo(BigDecimal.ZERO) > 0) {
    order.setStatus(OrderStatus.SUBMITTED);
}
```

### Better Pattern: Tell

```java
// Tell the object what to do, let it enforce its rules
order.submit();

// Inside Order class:
public void submit() {
    if (status != OrderStatus.DRAFT) {
        throw new IllegalStateException("Order has already been submitted");
    }
    if (orderLines.isEmpty()) {
        throw new IllegalStateException("Cannot submit an empty order");
    }
    if (totalAmount.compareTo(BigDecimal.ZERO) <= 0) {
        throw new IllegalStateException("Order total must be positive");
    }
    this.status = OrderStatus.SUBMITTED;
}
```

## Anti-Patterns in Encapsulation

### 1. Anemic Domain Model

The **anemic domain model** is a major anti-pattern where domain objects contain only data with getters and setters, while business logic resides in separate service classes.

```java
// Anemic model - bad encapsulation
public class Order {
    private OrderStatus status;
    private List<OrderLine> lines;

    public OrderStatus getStatus() { return status; }
    public void setStatus(OrderStatus status) { this.status = status; }
    public List<OrderLine> getLines() { return lines; }
    public void setLines(List<OrderLine> lines) { this.lines = lines; }
}

public class OrderService {
    public void submitOrder(Order order) {
        // Business logic in service, not in domain object
        if (order.getLines().size() > 0) {
            order.setStatus(OrderStatus.SUBMITTED);
        }
    }
}

// Rich domain model - good encapsulation
public class Order {
    private OrderStatus status;
    private final List<OrderLine> lines = new ArrayList<>();

    public void submit() {
        if (lines.isEmpty()) {
            throw new IllegalStateException("Cannot submit empty order");
        }
        this.status = OrderStatus.SUBMITTED;
    }
}
```

### 2. Public Setters

Public setters break encapsulation by allowing unrestricted modification of state without validation.

```java
// Bad: Public setters allow invalid states
public class Account {
    private BigDecimal balance;

    public void setBalance(BigDecimal balance) {
        this.balance = balance; // No validation!
    }
}

// Someone can do this:
account.setBalance(BigDecimal.valueOf(-1000)); // Invalid state!

// Good: Behavior-focused methods with validation
public class Account {
    private BigDecimal balance = BigDecimal.ZERO;

    public void deposit(BigDecimal amount) {
        if (amount.compareTo(BigDecimal.ZERO) <= 0) {
            throw new IllegalArgumentException("Deposit amount must be positive");
        }
        this.balance = this.balance.add(amount);
    }

    public void withdraw(BigDecimal amount) {
        if (amount.compareTo(BigDecimal.ZERO) <= 0) {
            throw new IllegalArgumentException("Withdrawal amount must be positive");
        }
        if (balance.compareTo(amount) < 0) {
            throw new InsufficientFundsException("Insufficient funds");
        }
        this.balance = this.balance.subtract(amount);
    }
}
```

### 3. Exposing Collections

Directly exposing mutable collections allows external modification that bypasses validation.

```java
// Bad: Direct exposure allows bypass
public List<OrderLine> getOrderLines() {
    return orderLines; // Direct reference!
}

// External code can do:
order.getOrderLines().add(invalidOrderLine); // Bypasses validation!

// Good: Return defensive copy or unmodifiable view
public List<OrderLine> getOrderLines() {
    return Collections.unmodifiableList(orderLines);
}

// Or provide controlled modification method
public void addOrderLine(ProductId productId, int quantity, BigDecimal unitPrice) {
    // Validation happens here
    if (status != OrderStatus.DRAFT) {
        throw new IllegalStateException("Cannot modify submitted order");
    }
    orderLines.add(new OrderLine(productId, quantity, unitPrice));
}
```

## Best Practices for Encapsulation in DDD

1. **Design from Behavior**: Start with the operations the domain requires, not the data structures.
2. **Make Fields Private and Final**: Use `private final` for immutable fields, `private` for mutable state.
3. **Avoid Public Setters**: Expose behavior through intention-revealing methods instead.
4. **Validate in Constructors**: Ensure objects are created in a valid state.
5. **Use Factory Methods**: Control object creation with static factory methods that express intent.
6. **Return Defensive Copies**: When exposing collections or mutable objects, return copies.
7. **Prefer Immutability**: Make value objects and as many fields as possible immutable.
8. **Package-Private for Internal Entities**: Keep internal aggregate entities inaccessible outside their package.
9. **Meaningful Method Names**: Use domain language in method names to reveal intent.
10. **Fail Fast**: Throw exceptions immediately when invariants are violated.

## Conclusion

Encapsulation is fundamental to creating expressive, maintainable, and robust domain models in Domain-Driven Design. By hiding implementation details, exposing behavior rather than data, and rigorously protecting invariants, domain objects accurately model business concepts while preventing invalid states.

Well-encapsulated aggregates, entities, and value objects enable the domain model to serve as the authoritative source of business logic, reducing the need for defensive coding in application services and ensuring consistency throughout the system. The Tell, Don't Ask principle and avoidance of anti-patterns like anemic domain models are essential to achieving proper encapsulation in DDD.

## Further References and Resources

### Books

- _Domain-Driven Design: Tackling Complexity in the Heart of Software_ by Eric Evans
- _Implementing Domain-Driven Design_ by Vaughn Vernon
- _Domain-Driven Design Distilled_ by Vaughn Vernon

### Articles

- [Anemic Domain Model - Martin Fowler](https://www.martinfowler.com/bliki/AnemicDomainModel.html)
- [Tell Don't Ask - Martin Fowler](https://martinfowler.com/bliki/TellDontAsk.html)
- [Encapsulation in Object-Oriented Design](https://www.yegor256.com/2014/11/20/seven-virtues-of-good-object.html)

### Related Concepts

- [Aggregates](../tactical-concepts/aggregate.md)
- [Entities](../tactical-concepts/entities.md)
- [Value Objects](../tactical-concepts/value-objects.md)
- [Domain Services](../tactical-concepts/domain-services.md)
