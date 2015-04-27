# .NET / C# Interview Questions

Questions related to .NET and C#, such as readonly vs. constant, how GC works,
how reflection works.

---

# Phone Screen Questions

## Easy Questions

__Q:__ What is the difference between reference types and value types?

__A:__
* Reference types are allocated on the heap. When passed into a method, the
reference is copied, which means any changes to the object will affect the outer
scope.
* Value types are allocated on the stack. When passed into a method, the value
is copied, which means changes to the value will not affect the outer scope.

---
__Q:__ What are the different access modifiers and what does each one mean?

__A:__
* `private`: Can be used only within the same class.
* `protected`: Can only be used within the same class or its subclasses.
* `internal`: Can only be used from within the same assembly.
* `public`: Can be used from anywhere.

**Follow-up:** What is the default access modifier (implied, if one is not
explicitly provided) for:
- Classes? `internal`
- Member variables? `private`
- Methods? `private`

---
__Q:__ What is the `virtual` keyword used for?

__A:__ The `virtual` keyword can be applied only to a method, to indicate that
it can be overridden. Methods without the `virtual` keyword cannot be overridden
in C# (unlike Java where methods are virtual by default and can only be made
`final`).

## Med Questions

__Q:__ In C#, what is the difference between the 3 keywords `static`,
`constant`, and `readonly`?

__A:__
* __Static:__ One copy of a `static` method, class, or class member will exist
per `ApplicationDomain`, and will be shared across all instances of an object.
* __Constant:__ A property marked as `constant` has its value set inline and can
not be changed.  The value is actually compiled into the dll and is `static`.
* __Readonly:__ A property marked as `readonly` can be set inline or within the
constructor of a class, but not set again after that.  This is useful for
injecting values at run-time that you may not know at compile-time and you do
not want an application to be able to modify.  A `readonly` property may or may
not be `static`.

_Notes:_
* Most people will know constant and static but not readonly.  If a candidate
does not understand static they barely know C# or OOP.

---
__Q:__ What is a delegate?

__A:__ A delegate is a way of wrapping a method that matches a specific
signature.  A delegate is similar to a function pointer, but is type-safe (
allowing for inheritance variance.)  A single delegate can wrap many methods.

---
__Q:__ What is an extension method? Why would you use one?

__A:__ Extension methods are a special kind of static method, but they are
called as if they were instance methods on the extended type. They enable you to
"add" methods to existing types. Extension methods offer a few valuable
options, such as the ability to call the method on a null reference, and to
modify types for which source code is not available, such as those in the base
class libraries.

## Hard Questions

__Q:__ How do you ensure that objects used as a generic's type parameter
implement a specific interface?

__A:__ Generic type constraints are the term for this.  The `where` keyword in
.net is used for this, such as:
```csharp
public class MyGenericClass<T> where T : IComparable { }
```
A more complex example shows how you can actually assert that types adhere to
built-in types as well, or even are `new()`able:
```csharp
class MyClass<T, U, V>
    where T : class
    where U : struct
    where V : new
{ }
```

---


# In-person questions

## Easy Questions

## Med Questions

__Q:__ Explain the limitation of overriding an inherited / parent class member
that is not marked as `virtual`.

__A:__ Any member not marked a virtual that is overridden by an inheriting /
child class will return the result from the parent class when the child class
is referred to polymorphically as the parent.

```csharp
class A
{
  public virtual void First()
  {
    Console.PrintLine("A.First");
  }

  public void Second()
  {
    Console.PrintLine("A.Second");
  }
}

class B : A
{
  public override void First()
  {
    Console.PrintLine("B.First");
  }

  public new void Second()
  {
    Console.PrintLine("B.Second");
  }
}

class Test
{
  public static void Main(string[] args)
  {
    A b_as_A = new B();

    b_as_A.First();
    // OUTPUT: B.First
    b_as_A.Second();
    // OUTPUT: A.Second
    ((B)b_as_A).Second();
    // OUTPUT: B.Second
  }
}
```

---
__Q:__ What is an Anonymous Method?

__A:__ An anonymous method is a function, including parameters and return type,
that is not written as part of a class, but purely defined solely by a delegate.
Anonymous methods can be written to the `delegate` keyword or using the lambda
syntax.

## Hard Questions

__Q:__ Explain how .Net's Garbage Collection algorithm works

__A:__ .Net uses a mark-and-sweep GC algorithm.  When GC fires, it first
enumerates all the roots (like registers, global or static fields, local
variables on the stack, function arguments on stack, etc) and then starts
visiting the objects referenced by them recursively (essentially travelling the
nodes in the memory graph). When it reaches an object it marks it with a special
flag indicating that the object is reachable and hence not garbage. At the end
of this mark phase it gets into the sweep phase. Any object in memory that is
not marked by this time is garbage and the system disposes it.

More details here: http://blogs.msdn.com/b/abhinaba/archive/2009/01/30/back-to-basics-mark-and-sweep-garbage-collection.aspx

__Follow-up:__ What are the advantages and disadvantages of a mark-and-sweep GC
algorithm over other algorithms (such as a reference counter GC)?

__A:__ The primary advantage of mark-sweep is that it handles cyclic references
naturally. Moreover, no additional overheads are added while normal execution
(e.g. allocation, pointer manipulations). Combined with compaction it ensures
good locality of reference and reduced fragmentation and hence optimal
subsequent allocations.

However, mark-sweep pauses useful execution and walks entire memory marking
and sweeping it. Hence it adds large freezes which is un-acceptable in most
interactive systems. However, incremental variations of Mark-sweep are available
which works around this limitation. Mark-sweep also starts thrashing when memory
fills up as it fails to clean up memory and it gets triggered again and again as
memory approaches exhaustion. Self tuning GC helps in this scenario.

---

__Q:__ What does the `lock` key word do?  What argument should be provided to the lock keyword?

__A:__ 

1. The `lock` keyword marks a statement block as a critical section by obtaining the mutual-exclusion lock for a given object, executing a statement, and then releasing the lock.  The lock keyword ensures that one thread does not enter a critical section of code while another thread is in the critical section. If another thread tries to enter a locked code, it will wait, block, until the object is released.

2. The argument provided to the lock keyword **must be an object based on a reference type**, and is used to define the scope of the lock. In the example above, the lock scope is limited to this function because no references to the object lockThis exist outside the function.

    _bonus points_:  It is best to avoid locking on a public type, or on object instances beyond the control of your application. For example, lock(this) can be problematic if the instance can be accessed publicly, because code beyond your control may lock on the object as well. This could create deadlock situations where two or more threads wait for the release of the same object. As a result, it is best to lock a private or protected member that is not interned. 

---

# Whiteboard questions

## Easy Questions

## Med Questions

## Hard Questions
