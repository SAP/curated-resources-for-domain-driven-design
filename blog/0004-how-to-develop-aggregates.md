# Aggregates: A Practical Guide for Developers

Domain-Driven Design (DDD) is a software design discipline that focuses on modeling the domain and its concepts. DDD enables developers in creating software that is expressive, maintainable, and aligned with business demands and goals.

The **aggregate** a is crucial concept in DDD. Aggregates are groups of domain objects that belong in one transactional boundary by managing complexity, ensuring consistency, and defining limits in their domain models.

> **Remark:** The code examples are meant as an inspiration and might be neither functional nor complete.

## What are Domain-Driven Design Aggregates?

An aggregate is a pattern in DDD that defines a group of domain objects that belong together and change together. An aggregate has the following characteristics:

- It has a **root entity**, which is the main entry point to access the aggregate. The root entity is responsible for enforcing the business rules and invariants of the aggregate.
- It has one or more **entities** and **value objects** that represent the concepts and behaviors of the domain. Entities are objects that have a unique identity and a lifecycle, while value objects are immutable objects that represent attributes or measurements.
- It has a **boundary**, which defines what is inside and outside of the aggregate. The boundary also determines the scope of consistency and transactions for the aggregate.
- It has an **identity**, which is usually derived from the root entity. The identity allows the aggregate to be referenced and manipulated by other aggregates or services.

An example of an aggregate is an order and its line items. The order is the root entity, which has an identity (order number), a state (status, total amount, etc.), and a behavior (place, cancel, ship, etc.). The line items are value objects, which represent the products and quantities ordered. The order and its line items form an aggregate, which has a boundary that separates it from other aggregates (such as customers or products). The order aggregate ensures that the business rules and invariants are satisfied, such as:

- An order cannot have zero or negative line items.
- An order cannot be shipped if it is canceled or unpaid.
- An order cannot be modified after it is shipped.

Aggregates are useful in software development because they:

- Reduce the amount of linkages and dependencies between domain objects to simplify the domain model.
- Increase performance by reducing the quantity of data that must be loaded or stored.
- Ensure that any changes inside an aggregate are atomic and isolated to improve consistency.
- Define what is relevant and irrelevant for a certain use case or situation to clarify limits.

## Designing Aggregates: Best Practices and Tips

> **Remark:** People often assume that using these tactical patterns is essential to "do DDD the right way". This is comparable to the patterns in the book ["Design Patterns"](https://en.wikipedia.org/wiki/Design_Patterns): you can also write good software without implementing every pattern in your product.
> Aggregates as well as patterns are tools that can help you to fulfill your requirements depending your use case.

Designing aggregates requires a deep understanding of the domain and its rules, as well as a balance between simplicity and flexibility:

- Create a clear and consistent domain model that reflects the ubiquitous language of the domain experts. Use nouns and verbs that are meaningful and unambiguous in the domain context.
- Avoid creating aggregates based on data structures or technical requirements. Aggregates should represent domain concepts, not just a generic collections of domain objects. For example, instead of having an aggregate for a list of products, you can have an aggregate for a catalog or a inventory.
- Aim for smaller aggregates that capture only the essential state and behavior of a domain concept. Smaller aggregates reduce transactional locking and consistency complexities, as well as improve performance and scalability. Please also consider compensation handling like SAGA in your business logic, if something goes wrong.
- Qualify associations by adding constraints or filters to reduce technical complexity. For example, instead of having a direct association between an order and a customer, you can have an association between an order and a customer with a specific status or type.
- Avoid creating aggregates based on data structures or technical requirements. Aggregates should represent domain concepts, not just a generic collections of domain objects. For example, instead of having an aggregate for a list of products, you can have an aggregate for a catalog or a inventory.
- Use value objects to represent attributes or measurements that do not have identity or lifecycle. Value objects are immutable and can be shared across aggregates without affecting consistency. For example, you can use value objects to represent money, quantity, address, etc.

## Aggregates in Context

An aggregate lives within one bounded context. It can be interpreted as a container for state. The container can be moved from one state to another. These state transitions are triggered by commands. Whenever the container is in one state it is completely consistent. The consistency is defined from a business perspective by the invariants basically telling what is allowed and what is not allowed.
Whenever a state change happens (or cannot happen due to invariants one or more business events are raised, informing the "world" about the change. Whenever an aggregate is in a (consistent) state it can be persisted

The scalability of the system and the size of the aggregate are in direct relation.
However, this has impact on the handling of cross-aggregate consistency. It is easier from a developer perspective to have one aggregate per bounded context and keep that consistent. The price is that your system will only scale (or not) based on this one big aggregate. The other way round when the design foresees smaller aggregates you can scale them independently but will probably have to wrap you head around compensation.

**Non-business example: A chess tournament.**

The aggregate in this case will probably be a single chess game/board. The actions are the movements of the chess pieces on the board and the invariants are the rule of the chess game wrt to the allowed movements of the chess pieces.
With this design/size of the aggregate you can cover basically every size of a tournament as the unit is the single game which can scale independently. One could now make some thought-experiments and gets an idea about the consequences concerning changing the size of the aggregate even to the extreme to have a whole tournament as one aggregate.

## Implementing Aggregates: Examples and Strategies

Implementing aggregates depends on the programming language and framework you use. However, there are some common strategies and tips that can help you implement aggregates effectively:

- Use object-oriented principles such as encapsulation, inheritance, polymorphism, and abstraction to model your aggregates. Encapsulation ensures that only the root entity can access and modify the internal state of the aggregate. Inheritance allows you to reuse common behavior across different types of aggregates. Polymorphism enables you to handle different scenarios based on the type of aggregate. Abstraction hides the implementation details from the outside world.
- Use repositories to abstract away the persistence mechanism of your aggregates. Repositories are interfaces that provide methods to load or save whole aggregates. They hide the details of how aggregates are stored or retrieved from databases or other sources. Repositories also ensure that only one instance of an aggregate exists in memory at any given time.
- Use factories to create instances of your aggregates. Factories are classes or methods that encapsulate the logic of creating aggregates with valid initial state. They ensure that all required fields are populated and all invariants are satisfied. Factories also simplify testing by providing mock or stub instances of aggregates.
- Use domain events to communicate changes between aggregates or services. Domain events are messages that capture something important that happened in the domain. They can be used to trigger actions or reactions across different boundaries or contexts. Domain events also decouple aggregates from each other by avoiding direct references or dependencies.

Here is an example of how to implement an order aggregate in Java. The classes such as OrderId, ProductId, Money, Quantity, etc. are examples of value objects in DDD. Value objects are immutable objects that represent attributes or measurements that do not have identity or lifecycle. They can be shared across aggregates without affecting consistency.

To utilize these classes, you must:

- Instantiate them by utilizing constructors that validate their values and assign them to final fields.
- Give getters for their values but no setters or modifiers.
- Carry out arithmetic operations for them using methods that yield new instances of the same class.
- Create comparison methods for them that compare their values.
- Provide equality and hash code methods for them by comparing their values.

```java
// Order.java
public class Order {

  // Order identity
  private final OrderId id;

  // Order state
  private OrderStatus status;
  private Money totalAmount;
  private List<LineItem> lineItems;

  // Order behavior
  public Order(OrderId id) {
    // Validate id
    if (id == null) {
      throw new IllegalArgumentException("Order id cannot be null");
    }
    this.id = id;

    // Initialize state
    this.status = OrderStatus.NEW;
    this.totalAmount = Money.ZERO;
    this.lineItems = new ArrayList<>();
  }

  public void addLineItem(Product product, Quantity quantity) {
    // Validate product and quantity
    if (product == null) {
      throw new IllegalArgumentException("Product cannot be null");
    }
    if (quantity == null || quantity.isZeroOrNegative()) {
      throw new IllegalArgumentException("Quantity must be positive");
    }

    // Check order status
    if (this.status != OrderStatus.NEW) {
      throw new IllegalStateException("Cannot add line item to non-new order");
    }

    // Create line item
    LineItem lineItem = new LineItem(product.getId(), product.getName(), product.getPrice(), quantity);

    // Add line item to list
    this.lineItems.add(lineItem);

    // Update total amount
    this.totalAmount = this.totalAmount.add(lineItem.getAmount());
  }

  public void place() {
    // Check order status
    if (this.status != OrderStatus.NEW) {
      throw new IllegalStateException("Cannot place non-new order");
    }

    // Check line items
    if (this.lineItems.isEmpty()) {
      throw new IllegalStateException("Cannot place empty order");
    }

    // Change order status
    this.status = OrderStatus.PLACED;

    // Publish domain event
    DomainEvents.publish(new OrderPlacedEvent(this.id));
  }

  public void cancel() {
    // Check order status
    if (this.status != OrderStatus.PLACED) {
      throw new IllegalStateException("Cannot cancel non-placed order");
    }

    // Change order status
    this.status = OrderStatus.CANCELED;

    // Publish domain event
    DomainEvents.publish(new OrderCanceledEvent(this.id));
  }

  public void ship() {
    // Check order status
    if (this.status != OrderStatus.PLACED) {
      throw new IllegalStateException("Cannot ship non-placed order");
    }

    // Change order status
    this.status = OrderStatus.SHIPPED;

    // Publish domain event
    DomainEvents.publish(new OrderShippedEvent(this.id));
  }

  // Getters

  public OrderId getId() {
    return id;
  }

  public OrderStatus getStatus() {
    return status;
  }

  public Money getTotalAmount() {
    return totalAmount;
  }

  public List<LineItem> getLineItems() {
    return Collections.unmodifiableList(lineItems);
  }
}

// LineItem.java
public class LineItem {

  // Line item attributes
  private final ProductId productId;
  private final String productName;
  private final Money productPrice;
  private final Quantity quantity;

  public LineItem(ProductId productId, String productName, Money productPrice,
      Quantity quantity) {
    
     // Validate attributes
     if (productId == null) {
       throw new IllegalArgumentException("Product id cannot be null");
     }
     if (productName == null || productName.isEmpty()) {
       throw new IllegalArgumentException("Product name cannot be null or empty");
     }
     if (productPrice == null || productPrice.isZeroOrNegative()) {
       throw new IllegalArgumentException("Product price must be positive");
     }
     if (quantity == null || quantity.isZeroOrNegative()) {
       throw new IllegalArgumentException("Quantity must be positive");
     }

     // Assign attributes
     this.productId = productId;
     this.productName = productName;
     this.productPrice = productPrice;
     this.quantity = quantity;
  }

  // Getters

  public ProductId getProductId() {
    return productId;
  }

  public String getProductName() {
    return productName;
  }

  public Money getProductPrice() {
    return productPrice;
  }

  public Quantity getQuantity() {
    return quantity;
  }

  // Derived attribute

  public Money getAmount() {
    return productPrice.multiply(quantity);
  }

  // Equality based on value

  @Override
  public boolean equals(Object obj) {
    if (this == obj) {
      return true;
    }
    if (obj == null || getClass() != obj.getClass()) {
      return false;
    }
    LineItem other = (LineItem) obj;
    return Objects.equals(productId, other.productId)
        && Objects.equals(productName, other.productName)
        && Objects.equals(productPrice, other.productPrice)
        && Objects.equals(quantity, other.quantity);
  }

  @Override
  public int hashCode() {
    return Objects.hash(productId, productName, productPrice, quantity);
  }

}
```

Okay, here is the code for the repository and factory classes for Order:

```java
// OrderRepository.java
public interface OrderRepository {

  // Load an order by its id
  Order load(OrderId id);

  // Save an order
  void save(Order order);
}

// OrderFactory.java
public class OrderFactory {

  // Create a new order with a unique id
  public Order createNewOrder() {
    // Generate a unique id
    OrderId id = IdGenerator.generate();

    // Create a new order
    Order order = new Order(id);

    // Return the order
    return order;
  }
}
```

```java
// OrderId.java
public class OrderId {

  // Order id value
  private final String value;

  public OrderId(String value) {
    // Validate value
    if (value == null || value.isEmpty()) {
      throw new IllegalArgumentException("Order id value cannot be null or empty");
    }

    // Assign value
    this.value = value;
  }

  // Getters

  public String getValue() {
    return value;
  }

  // Equality based on value

  @Override
  public boolean equals(Object obj) {
    if (this == obj) {
      return true;
    }
    if (obj == null || getClass() != obj.getClass()) {
      return false;
    }
    OrderId other = (OrderId) obj;
    return Objects.equals(value, other.value);
  }

  @Override
  public int hashCode() {
    return Objects.hash(value);
  }

}

// ProductId.java
public class ProductId {

  // Product id value
  private final String value;

  public ProductId(String value) {
    // Validate value
    if (value == null || value.isEmpty()) {
      throw new IllegalArgumentException("Product id value cannot be null or empty");
    }

    // Assign value
    this.value = value;
  }

  // Getters

  public String getValue() {
    return value;
  }

  // Equality based on value

  @Override
  public boolean equals(Object obj) {
    if (this == obj) {
      return true;
    }
    if (obj == null || getClass() != obj.getClass()) {
      return false;
    }
    ProductId other = (ProductId) obj;
    return Objects.equals(value, other.value);
  }

  @Override
  public int hashCode() {
    return Objects.hash(value);
  }

}

// Money.java
public class Money {

  // Money value
  private final BigDecimal value;

  // Zero money constant
  public static final Money ZERO = new Money(BigDecimal.ZERO);

  public Money(BigDecimal value) {
    // Validate value
    if (value == null || value.signum() < 0) {
      throw new IllegalArgumentException("Money value must be non-negative");
    }

    // Assign value
    this.value = value;
  }

  // Getters

  public BigDecimal getValue() {
    return value;
  }

  // Arithmetic operations

  public Money add(Money other) {
    // Validate other
    if (other == null) {
      throw new IllegalArgumentException("Other money cannot be null");
    }

    // Add values and return new money
    return new Money(this.value.add(other.value));
  }

  public Money subtract(Money other) {
     // Validate other
     if (other == null) {
       throw new IllegalArgumentException("Other money cannot be null");
     }

     // Subtract values and return new money
     return new Money(this.value.subtract(other.value));
   }

   public Money multiply(Quantity quantity) {
     // Validate quantity
     if (quantity == null || quantity.isZeroOrNegative()) {
       throw new IllegalArgumentException("Quantity must be positive");
     }

     // Multiply values and return new money
     return new Money(this.value.multiply(quantity.getValue()));
   }

   // Comparison methods

   public boolean isZeroOrNegative() {
     return this.value.signum() <= 0;
   }

   public boolean isGreaterThan(Money other) {
     // Validate other
     if (other == null) {
       throw new IllegalArgumentException("Other money cannot be null");
     }

     // Compare values and return result
     return this.value.compareTo(other.value) > 0;
   }

   public boolean isLessThan(Money other) {
     // Validate other
     if (other == null) {
       throw new IllegalArgumentException("Other money cannot be null");
     }

     // Compare values and return result
     return this.value.compareTo(other.value) < 0;
   }

   public boolean isEqualTo(Money other) {
     // Validate other
     if (other == null) {
       throw new IllegalArgumentException("Other money cannot be null");
     }

     // Compare values and return result
     return this.value.compareTo(other.value) == 0;
   }

   // Equality based on value

   @Override
   public boolean equals(Object obj) {
     if (this == obj) {
       return true;
     }
     if (obj == null || getClass() != obj.getClass()) {
       return false;
     }
     Money other = (Money) obj;
     return Objects.equals(value, other.value);
   }

   @Override
   public int hashCode() {
     return Objects.hash(value);
   }
}

// Quantity.java
public class Quantity {

  // Quantity value
  private final BigDecimal value;

  // Zero quantity constant
  public static final Quantity ZERO = new Quantity(BigDecimal.ZERO);

  public Quantity(BigDecimal value) {
    // Validate value
    if (value == null || value.signum() < 0) {
      throw new IllegalArgumentException("Quantity value must be non-negative");
    }

    // Assign value
    this.value = value;
  }

´´´java

Okay, here is the code for Quantity.java:

```java
// Quantity.java
public class Quantity {

  // Quantity value
  private final BigDecimal value;

  // Zero quantity constant
  public static final Quantity ZERO = new Quantity(BigDecimal.ZERO);

  public Quantity(BigDecimal value) {
    // Validate value
    if (value == null || value.signum() < 0) {
      throw new IllegalArgumentException("Quantity value must be non-negative");
    }

    // Assign value
    this.value = value;
  }

  // Getters

  public BigDecimal getValue() {
    return value;
  }

  // Arithmetic operations

  public Quantity add(Quantity other) {
    // Validate other
    if (other == null) {
      throw new IllegalArgumentException("Other quantity cannot be null");
    }

    // Add values and return new quantity
    return new Quantity(this.value.add(other.value));
  }

  public Quantity subtract(Quantity other) {
     // Validate other
     if (other == null) {
       throw new IllegalArgumentException("Other quantity cannot be null");
     }

     // Subtract values and return new quantity
     return new Quantity(this.value.subtract(other.value));
   }

   // Comparison methods

   public boolean isZeroOrNegative() {
     return this.value.signum() <= 0;
   }

   public boolean isGreaterThan(Quantity other) {
     // Validate other
     if (other == null) {
       throw new IllegalArgumentException("Other quantity cannot be null");
     }

     // Compare values and return result
     return this.value.compareTo(other.value) > 0;
   }

   public boolean isLessThan(Quantity other) {
     // Validate other
     if (other == null) {
       throw new IllegalArgumentException("Other quantity cannot be null");
     }

     // Compare values and return result
     return this.value.compareTo(other.value) < 0;
   }

   public boolean isEqualTo(Quantity other) {
     // Validate other
     if (other == null) {
       throw new IllegalArgumentException("Other quantity cannot be null");
     }

     // Compare values and return result
     return this.value.compareTo(other.value) == 0;
   }

   // Equality based on value

   @Override
   public boolean equals(Object obj) {
     if (this == obj) {
       return true;
     }
     if (obj == null || getClass() != obj.getClass()) {
       return false;
     }
     Quantity other = (Quantity) obj;
     return Objects.equals(value, other.value);
   }

   @Override
   public int hashCode() {
     return Objects.hash(value);
   }
}
```

```java
// OrderPlacedEvent.java
public class OrderPlacedEvent {

  // Order id
  private final OrderId orderId;

  public OrderPlacedEvent(OrderId orderId) {
    // Validate order id
    if (orderId == null) {
      throw new IllegalArgumentException("Order id cannot be null");
    }

    // Assign order id
    this.orderId = orderId;
  }

  // Getters

  public OrderId getOrderId() {
    return orderId;
  }
}

// OrderCanceledEvent.java
public class OrderCanceledEvent {

  // Order id
  private final OrderId orderId;

  public OrderCanceledEvent(OrderId orderId) {
    // Validate order id
    if (orderId == null) {
      throw new IllegalArgumentException("Order id cannot be null");
    }

    // Assign order id
    this.orderId = orderId;
  }

  // Getters

  public OrderId getOrderId() {
    return orderId;
  }
}

// OrderShippedEvent.java
public class OrderShippedEvent {

  // Order id
  private final OrderId orderId;

  public OrderShippedEvent(OrderId orderId) {
    // Validate order id
    if (orderId == null) {
      throw new IllegalArgumentException("Order id cannot be null");
    }

    // Assign order id
    this.orderId = orderId;
  }

  // Getters

  public OrderId getOrderId() {
    return orderId;
  }
}
```

```java
// Create a money instance with a value of 10.00
Money money = new Money(new BigDecimal("10.00"));

// Get the value of the money instance
BigDecimal value = money.getValue();

// Add another money instance with a value of 5.00 and get a new money instance with a value of 15.00
Money anotherMoney = new Money(new BigDecimal("5.00"));
Money resultMoney = money.add(anotherMoney);

// Compare the money instance with another money instance and get a boolean result
boolean isGreaterThan = money.isGreaterThan(anotherMoney);
boolean isLessThan = money.isLessThan(anotherMoney);
boolean isEqualTo = money.isEqualTo(anotherMoney);

// Check if the money instance is zero or negative and get a boolean result
boolean isZeroOrNegative = money.isZeroOrNegative();

// Check if the money instance is equal to another object and get a boolean result
boolean equals = money.equals(anotherObject);

// Get the hash code of the money instance
int hashCode = money.hashCode();
```

## Testing Aggregates: Strategies and Techniques

Testing aggregates may be difficult, especially when working with complex systems and scenarios. Nonetheless, testing aggregates is necessary to guarantee that they function properly and fulfill business needs. These are several DDD testing procedures and approaches for aggregates:

- Use unit tests to verify the behavior and state of individual aggregates. Unit tests are isolated tests that check the logic and rules of a single aggregate. They do not depend on external resources or services. Unit tests can use mock or stub instances of other aggregates or repositories to simulate interactions or dependencies.
- Use integration tests to verify the interaction and integration of aggregates with other components. Integration tests are tests that check how aggregates work with other parts of the system, such as databases, services, or events. They require access to real or simulated resources or services. Integration tests can use real or fake instances of other aggregates or repositories to test the communication or collaboration between them.
- Use scenario tests to verify the end-to-end functionality and behavior of aggregates. Scenario tests are tests that check how aggregates perform in a realistic or complex situation. They simulate a user story or a use case that involves multiple aggregates or services. They require a complete or partial setup of the system. Scenario tests can use real or fake instances of other aggregates or repositories to test the outcome or result of a scenario.

**Example:**

```java
// OrderTest.java
public class OrderTest {

  // Test data
  private OrderId orderId;
  private ProductId productId;
  private String productName;
  private Money productPrice;
  private Quantity quantity;

  // Test objects
  private Order order;
  private Product product;
  private LineItem lineItem;

  // Test setup
  @Before
  public void setUp() {
    // Create test data
    orderId = new OrderId("O-123");
    productId = new ProductId("P-456");
    productName = "Test Product";
    productPrice = new Money(new BigDecimal("10.00"));
    quantity = new Quantity(new BigDecimal("2"));

    // Create test objects
    order = new Order(orderId);
    product = new Product(productId, productName, productPrice);
    lineItem = new LineItem(productId, productName, productPrice, quantity);
  }

  // Test adding a line item to a new order
  @Test
  public void testAddLineItemToNewOrder() {
    // Add line item to order
    order.addLineItem(product, quantity);

    // Verify order state
    assertEquals(OrderStatus.NEW, order.getStatus());
    assertEquals(new Money(new BigDecimal("20.00")), order.getTotalAmount());
    assertEquals(1, order.getLineItems().size());
    assertTrue(order.getLineItems().contains(lineItem));
  }

  // Test placing a non-empty order
  @Test
  public void testPlaceNonEmptyOrder() {
    // Add line item to order
    order.addLineItem(product, quantity);

    // Place order
    order.place();

    // Verify order state
    assertEquals(OrderStatus.PLACED, order.getStatus());
    assertEquals(new Money(new BigDecimal("20.00")), order.getTotalAmount());
    assertEquals(1, order.getLineItems().size());
    assertTrue(order.getLineItems().contains(lineItem));

    // Verify domain event
    assertTrue(DomainEvents.contains(new OrderPlacedEvent(orderId)));
  }

  // Test canceling a placed order
  @Test
  public void testCancelPlacedOrder() {
     // Add line item to order
     order.addLineItem(product, quantity);

     // Place order
     order.place();

     // Cancel order
     order.cancel();

     // Verify order state
     assertEquals(OrderStatus.CANCELED, order.getStatus());
     assertEquals(new Money(new BigDecimal("20.00")), order.getTotalAmount());
     assertEquals(1, order.getLineItems().size());
     assertTrue(order.getLineItems().contains(lineItem));

     // Verify domain event
     assertTrue(DomainEvents.contains(new OrderCanceledEvent(orderId)));
   }

   // Test shipping a placed order
   @Test
   public void testShipPlacedOrder() {
      // Add line item to order
      order.addLineItem(product, quantity);

      // Place order
      order.place();

      // Ship order
      order.ship();

      // Verify order state
      assertEquals(OrderStatus.SHIPPED, order.getStatus());
      assertEquals(new Money(new BigDecimal("20.00")), order.getTotalAmount());
      assertEquals(1, order.getLineItems().size());
      assertTrue(order.getLineItems().contains(lineItem));

      // Verify domain event
      assertTrue(DomainEvents.contains(new OrderShippedEvent(orderId)));
   }

   // Test adding a line item to a non-new order (should throw exception)
   @Test(expected = IllegalStateException.class)
   public void testAddLineItemToNonNewOrder() {
      // Add line item to order
      order.addLineItem(product, quantity);

      // Place order
      order.place();

      // Add another line item to order (should throw exception)
      Product anotherProduct = new Product(
          new ProductId("P-789"),
          "Another Product",
          new Money(new BigDecimal("5.00"))
      );
      Quantity anotherQuantity = new Quantity(new BigDecimal("3"));
      LineItem anotherLineItem = new LineItem(
          anotherProduct.getId(),
          anotherProduct.getName(),
          anotherProduct.getPrice(),
          anotherQuantity
      );
      order.addLineItem(anotherProduct, anotherQuantity);
   }

   // Test placing an empty order (should throw exception)
   @Test(expected = IllegalStateException.class)
   public void testPlaceEmptyOrder() {
       // Place empty order (should throw exception)
       order.place();
   }

   // Test canceling a non-placed order (should throw exception)
   @Test(expected = IllegalStateException.class)
   public void testCancelNonPlacedOrder() {
       // Cancel new order (should throw exception)
       order.cancel();
   }

   // Test shipping a non-placed order (should throw exception)
   @Test(expected = IllegalStateException.class)
   public void testShipNonPlacedOrder() {
       // Ship new order (should throw exception)
       order.ship();
   }
}
```

## Conclusion

To design aggregates, you need to create a clear and consistent domain model that reflects the ubiquitous language of the domain experts. You also need to identify boundaries and entities that belong together in an aggregate based on domain invariants. You should aim for smaller aggregates that capture only the essential state and behavior of a domain concept. You should also qualify associations by adding constraints or filters to reduce technical complexity.

To implement aggregates, you should model your aggregates using object-oriented principles like encapsulation, inheritance, polymorphism, and abstraction. You should also use repositories to abstract away the aggregates' persistence mechanism. You should also use factories to create aggregate instances with a valid initial state. Domain events are also required for communicating changes between aggregates or services.

To test aggregates, use unit tests to verify the behavior and state of individual aggregates. You must also use integration tests to validate the interaction and integration of aggregates with other components. You must also use scenario tests to validate aggregates' end-to-end functionality and behavior.

If you want start learning about DDD we can recommend the following books:

1. “Domain-Driven Design: Tackling Complexity in the Heart of Software” by Eric Evans
2. “Implementing Domain-Driven Design” by Vaughn Vernon
3. “Learning Domain-Driven Design” by Vlad Khononov
4. “Domain-Driven Design Distilled” by Vaughn Vernon

## Resources

- DDD_Aggregate - Martin Fowler. <https://www.martinfowler.com/bliki/DDD_Aggregate.html>.
- What Are Aggregates In Domain-Driven Design? - James Hickey. <https://www.jamesmichaelhickey.com/domain-driven-design-aggregates/>.
- Understanding Aggregates in Domain-Driven Design - DZone. <https://dzone.com/articles/domain-driven-design-aggregate>.
