*Questions related to .NET and C#, such as readonly vs. constant, how GC works, how reflection works.*

---

# Phone Screen Questions

## Easy Questions

## Med Questions

1. In C#, what is the difference between the 3 keywords `static`, `constant`, and `readonly`?

    `Answer`:
    * Static: One copy of a `static` method, class, or class member will exist per `ApplicationDomain`, and will be shared across all instances of an object.
    * Constant: A property marked as `constant` has its value set inline and can not be changed.  The value is actually compiled into the dll and is `static`.
    * Readonly: A property marked as `readonly` can be set inline or within the constructor of a class, but not set again after that.  This is useful for injecting values at run-time that you may not know at compile-time but you do not want an application to be able to modify.

    `Notes`:
    * Most people will know constant and static but not readonly.

## Hard Questions

---

# In-person questions

## Easy Questions

## Med Questions

## Hard Questions

---

# Whiteboard questions

## Easy Questions

## Med Questions

## Hard Questions