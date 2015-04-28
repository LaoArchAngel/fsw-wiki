# Object-Oriented Programming Interview Questions

Questions related to OO skills, for example: questions around IoC, Encapsulation, Data Abstraction, Polymorphism and Inheritance.

---

## Phone Screen Questions

### Easy Questions

__Q: What is an abstract class?__

__A: A class that cannot be instantiated and is used as a base class for other
abstract classes or concrete classes.  Abstract classes can have implemented
members as well as abstract, non-implemented members.__

---

__Q: What is an interface?__

__A: A contract that the implementing class needs to fulfill.  It cannot contain
any implementation.  It only defines a portion of the implementing's class
structure.__

---

__Follow-Up:__ As a rule of thumb, when would you recommend using one (abstract class vs interface) versus the other?

__A:__ Use an interface unless there is a strong 'is-a' relationship between the base *and* derived types as well as common behavior across all derived types.

---

__Q: What is an anti-pattern?__

__A: A common response to a recurring problem that is usually ineffective and risks being highly counter productive.__

---

### Med Questions

__Q: Class taxonomy, or the act of representing classes as a hierarchy of
inherited behavior and attributes, is considered an anti-pattern in most cases.
Why?__

---
__A: Class taxonomy is the act of prefering inheritance over implementation.
Deep inheritance chains conceal properties and functionality of an object and
make SOLID OO harder to achieve.__

---
### Hard Questions

__Q: There are several methods of Inversion of Control.  Name two.__

__A:  Any of the following.  Descriptions added in case terminology is
unknown.__
* Factory
  * The act of unloading the creation of object instances to a factory.
  this factory is often an implemented interface that returns the interface of
  an object, allowing both the factory and the object to be implementation
  details.
* Service Locator
  * Like Dependency Injection, except a Service Locator will instantiate or find
  an instance of the service or object.  Sometimes considered an anti-pattern.
* Dependency Injection
  * The act of passing in a dependency to another class via constructor,
  parameter, setter, or interface.
* Contextualized Lookup
  * A dependency injection container.
* Template Method Design
  * A method that unloads part of its logic to a subclass.
* Strategy Pattern
  * The encapsulation of algorithms (based on an interface) that are
  interchangeable at runtime.
---

## In-person questions

### Easy Questions

### Med Questions

__Q: What is polymorphism, and why is it useful?__

__A: Polymorphism describes a pattern in object oriented programming in which
classes have different functionality while sharing a common interface.__

The beauty of polymorphism is that the code working with the different classes does not need to know which class it is using since they’re all used the same way. A real world analogy for polymorphism is a button. Everyone knows how to use a button: you simply apply pressure to it. What a button “does,” however, depends on what it is connected to and the context in which it is used — but the result does not affect how it is used. If your boss tells you to press a button, you already have all the information needed to perform the task.

In the programming world, polymorphism is used to make applications more modular and extensible. Instead of messy conditional statements describing different courses of action, you create interchangeable objects that you select based on your needs. That is the basic goal of polymorphism.

_Examples:_
* A good example is if you were to write a Mechanic class, it may operate on `IMaintainable`, which might promise a function called `ChangeOil()` and `ChangeTire()` in its contract.  Concrete classes like `Car`, `FreightTruck`, and `Motorcycle` can implement `IMaintainable` and have their own `ChangeOil` and `ChangeTire` implementations that differ.  Due to polymorphism, you could have the Mechanic class operate on an `IMaintainable` and never need to know the underlying type or the specific implementation of those functions.

_Side Note:_ In C# there are technically 3 types of Polymorphism:
1. Run-time Polymorphism: The type discussed above
2. Parametric Polymorphism: Basically, Generics, which accept an unknown type as
a parameter.
3. Compile-time Polymorphism: Method overloading, which most people do not think
 of as polymorphism

---
### Hard Questions

---

## Whiteboard questions

### Easy Questions

### Med Questions

### Hard Questions
