*Questions related to .NET and C#, such as readonly vs. constant, how GC works, how reflection works.*

---

# Phone Screen Questions

## Easy Questions

## Med Questions

1. In C#, what is the difference between the 3 keywords `static`, `constant`, and `readonly`?

    `Answer`:
    * Static: One copy of a `static` method, class, or class member will exist per `ApplicationDomain`, and will be shared across all instances of an object.
    * Constant: A property marked as `constant` has its value set inline and can not be changed.  The value is actually compiled into the dll and is `static`.
    * Readonly: A property marked as `readonly` can be set inline or within the constructor of a class, but not set again after that.  This is useful for injecting values at run-time that you may not know at compile-time and you do not want an application to be able to modify.  A `readonly` property may or may not be `static`.

    `Notes`:
    * Most people will know constant and static but not readonly.  If a candidate does not understand static they barely know C# or OOP.

## Hard Questions

---

# In-person questions

## Easy Questions

## Med Questions

## Hard Questions

1. Explain how .Net's Garbage Collection algorithm works

    `Answer`: .Net uses a mark-and-sweep GC algorithm.  When GC fires, it first enumerates all the roots and then starts visiting the objects referenced by them recursively (essentially travelling the nodes in the memory graph). When it reaches an object it marks it with a special flag indicating that the object is reachable and hence not garbage. At the end of this mark phase it gets into the sweep phase. Any object in memory that is not marked by this time is garbage and the system disposes it.

    'Follow-up': What are the advantages and disadvantages of a mark-and-sweep GC algorithm over a reference counter GC?

    The primary advantage of mark-sweep is that it handles cyclic references naturally. Moreover, no additional overheads are added while normal execution (e.g. allocation, pointer manipulations). Combined with compaction it ensures good locality of reference and reduced fragmentation and hence optimal subsequent allocations.

    However, mark-sweep pauses useful execution and walks entire memory marking and sweeping it. Hence it adds large freezes which is un-acceptable in most interactive systems. However, incremental variations of Mark-sweep are available which works around this limitation. Mark-sweep also starts thrashing when memory fills up as it fails to clean up memory and it gets triggered again and again as memory approaches exhaustion. Self tuning GC helps in this scenario.

---

# Whiteboard questions

## Easy Questions

## Med Questions

## Hard Questions