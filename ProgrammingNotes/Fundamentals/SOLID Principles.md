The SOLID principles are not just important to mobile iOS development, but to any software development. Whether you move on to a different engineering path or not, being familiar with these concepts, even if you can't remember the exact acronym will be massively beneficial.

1.  Single Responsibility: Every class should have their own responsibility
2. Open-Close: Software entities should be open for extension but closed for modification.
3. Liskov Substitution: Functions that use pointers or references to base classes must be able to use objects from derived classes without knowing it.
4. Interface Segregation: Clients should not be forced to depend on interfaces that they do not use.
5. Dependency Inversion: Depend on abstractions, not concretions.

### Single Responsibility Principle
_A Chef's only job should be to cook, not serve or handle plumbing._

- A type should only have one reason to change- just one focus or purpose.
- When a class handles too many concerns, it becomes harder to maintain, test, or reuse.
- One job per class or struct.

**Negative Example**
- `Order` 's responsibility is to process order data calculations *and* logging.

```
class Order {
    var items: [Double]
    init(items: [Double]) {
        self.items = items
    }
    
    func calculateTotal() -> Double {
        items.reduce(0, +)
    }

    func printReceipt() {
        print("Total: \(calculateTotal())")
    }
}
```

**Positive Example**
- `Order`'s responsibility is to manage order data and calculations.
- `ReceiptPrinter`'s responsibility is to handle logging.

```
class Order {
    var items: [Double]

    init(items: [Double]) {
        self.items = items
    }

    func calculateTotal() -> Double {
        items.reduce(0, +)
    }
}
```

```
class ReceiptPrinter {
    func printReceipt(for order: Order) {
        print("Total: \(order.calculateTotal())")
    }
}
```

in the positive example, each type has *one reason to change*, satisfying the Single Responsibility Principle.

### Open-Close Principle
**Negative Example**

**Positive Example**

### Liskov's Substitution Principle
**Negative Example**

**Positive Example**

### Interface Segregation Principle
**Negative Example**

**Positive Example**

### Dependency Inversion Principle
**Negative Example**

**Positive Example**