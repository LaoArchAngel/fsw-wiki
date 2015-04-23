*Questions related to OO skills, for example: questions around IoC, Encapsulation, Data Abstraction, Polymorphism and Inheritance.*

---

# Phone Screen Questions

## Easy Questions

## Med Questions

## Hard Questions

---

# In-person questions

## Easy Questions

## Med Questions

1. What is polymorphism, and why is it useful?

    `Answer`: Polymorphism describes a pattern in object oriented programming in which classes have different functionality while sharing a common interface.

The beauty of polymorphism is that the code working with the different classes does not need to know which class it is using since they’re all used the same way. A real world analogy for polymorphism is a button. Everyone knows how to use a button: you simply apply pressure to it. What a button “does,” however, depends on what it is connected to and the context in which it is used — but the result does not affect how it is used. If your boss tells you to press a button, you already have all the information needed to perform the task.

In the programming world, polymorphism is used to make applications more modular and extensible. Instead of messy conditional statements describing different courses of action, you create interchangeable objects that you select based on your needs. That is the basic goal of polymorphism.

    `Examples`:
* A good example is if you were to write a Mechanic class, it may operate on `IMaintainable`, which might promise a function called `ChangeOil()` and `ChangeTire()` in its contract.  Concrete classes like `Car`, `FreightTruck`, and `Motorcycle` can implement `IMaintainable` and have their own `ChangeOil` and `ChangeTire` implementations that differ.  Due to polymorphism, you could have the Mechanic class operate on an `IMaintainable` and never need to know the underlying type or the specific implementation of those functions.

    'Side Note': In C# there are technically 3 types of Polymorphism:
1. Run-time Polymorphism: The type discussed above
2. Parametric Polymorphism: Basically, Generics, which accept an unknown type as a parameter.
3. Compile-time Polymorphism: Method overloading, which most people do not think of as polymorphism

## Hard Questions

---

# Whiteboard questions

## Easy Questions

## Med Questions

## Hard Questions