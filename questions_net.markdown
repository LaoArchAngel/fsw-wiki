*Questions related to .NET and C#, such as readonly vs. constant, how GC works, how reflection works.*

---

# Phone Screen Questions

## Easy Questions

1. What is the difference between reference types and value types?

    **Answer:**
    * Reference types are allocated on the heap. When passed into a method, the reference is copied, which means any changes to the object will affect the outer scope.
    * Value types are allocated on the stack. When passed into a method, the value is copied, which means changes to the value will not affect the outer scope.

2. What are the different access modifiers and what does each one mean?

    **Answer:**
    * `private`: Can be used only within the same class.
    * `protected`: Can only be used within the same class or its subclasses.
    * `internal`: Can only be used from within the same assembly.
    * `public`: Can be used from anywhere.

    **Follow-up:** What is the default access modifier (implied, if one is not explicitly provided) for:
       - Classes? `internal`
       - Member variables? `private`
       - Methods? `private`

3. What is the `virtual` keyword used for?

    **Answer:** The `virtual` keyword can be applied only to a method, to indicate that it can be overridden. Methods without the `virtual` keyword cannot be overridden in C# (unlike Java where methods are virtual by default and can only be made `final`).

## Med Questions

1. In C#, what is the difference between the 3 keywords `static`, `constant`, and `readonly`?

    `Answer`:
    * Static: One copy of a `static` method, class, or class member will exist per `ApplicationDomain`, and will be shared across all instances of an object.
    * Constant: A property marked as `constant` has its value set inline and can not be changed.  The value is actually compiled into the dll and is `static`.
    * Readonly: A property marked as `readonly` can be set inline or within the constructor of a class, but not set again after that.  This is useful for injecting values at run-time that you may not know at compile-time and you do not want an application to be able to modify.  A `readonly` property may or may not be `static`.

    `Notes`:
    * Most people will know constant and static but not readonly.  If a candidate does not understand static they barely know C# or OOP.

2. What is an extension method? Why would you use one?

    **Answer:** 

    Extension methods are a special kind of static method, but they are called as if they were instance methods on the extended type. They enable you to "add" methods to existing types. Extension methods offer a few valuable options, such as the ability to call the method on a null reference, and to modify types for which source code is not available, such as those in the base class libraries.

## Hard Questions

---

# In-person questions

## Easy Questions

## Med Questions

## Hard Questions

1. Explain how .Net's Garbage Collection algorithm works

    `Answer`: .Net uses a mark-and-sweep GC algorithm.  When GC fires, it first enumerates all the roots (like registers, global or static fields, local variables on the stack, function arguments on stack, etc) and then starts visiting the objects referenced by them recursively (essentially travelling the nodes in the memory graph). When it reaches an object it marks it with a special flag indicating that the object is reachable and hence not garbage. At the end of this mark phase it gets into the sweep phase. Any object in memory that is not marked by this time is garbage and the system disposes it.

    More details here: http://blogs.msdn.com/b/abhinaba/archive/2009/01/30/back-to-basics-mark-and-sweep-garbage-collection.aspx

    `Follow-up`: What are the advantages and disadvantages of a mark-and-sweep GC algorithm over other algorithms (such as a reference counter GC)?

    The primary advantage of mark-sweep is that it handles cyclic references naturally. Moreover, no additional overheads are added while normal execution (e.g. allocation, pointer manipulations). Combined with compaction it ensures good locality of reference and reduced fragmentation and hence optimal subsequent allocations.

    However, mark-sweep pauses useful execution and walks entire memory marking and sweeping it. Hence it adds large freezes which is un-acceptable in most interactive systems. However, incremental variations of Mark-sweep are available which works around this limitation. Mark-sweep also starts thrashing when memory fills up as it fails to clean up memory and it gets triggered again and again as memory approaches exhaustion. Self tuning GC helps in this scenario.

2. How do you ensure that objects used as a generic's type parameter implement a specific interface?

    `Answer`: Generic type constraints are the term for this.  The `where` keyword in .net is used for this, such as: `public class MyGenericClass<T> where T : IComparable { }`

    A more complex example shows how you can actually assert that types adhere to built-in types as well, or even are new()able:
`class MyClass<T, U, V>
    where T : class 
    where U : struct
    where V : new
{ }`

---

# Whiteboard questions

## Easy Questions

## Med Questions

## Hard Questions