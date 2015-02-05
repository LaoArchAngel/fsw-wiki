# Testable Code

## Identifying Non-testable Code
* The code being tested creates its own dependency, therein hyper-extending the
scope of the unit test.
* The code expects a dependency passed in that is un-mockable.
* The return is too vague to test private method calls.

## Writing Testable Code
* Do not instantiate dependencies inside business logic.
  * Pass in dependencies either via constructor, properties, or method signature.
* Make dependencies interfaces that describe behavior rather than data.
  * Properties of an interface should describe behavior as well. Eg,
  [Keys](https://msdn.microsoft.com/en-us/library/system.collections.idictionary.keys.aspx)
  and
  [Values](https://msdn.microsoft.com/en-us/library/system.collections.idictionary.values.aspx) both describe the behavior of an
  [IDictionary](https://msdn.microsoft.com/en-us/library/System.Collections.IDictionary.aspx)
  because the behavior of a dictionary is such that a key indexes a larger /
  complex value object.
* Follow [SOLID](http://en.wikipedia.org/wiki/SOLID_%28object-oriented_design%29)
development principles.
    * The [Single Responsibility Principle](http://en.wikipedia.org/wiki/Single_responsibility_principle)
    applies to [methods as well as classes](http://www.developerfusion.com/article/137636/taking-the-single-responsibility-principle-seriously/).

## Refactoring Non-testable Code
* If non-testable code requires a dependency throughout the entire class, add
the dependency as a parameter to the constructor.
* If non-testable code requires a dependency in very few methods, add the
dependency as a parameter to the methods.
* Split code into one or multiple behavioral interfaces such that each interface
follows SRP.
  * A good example are the interfaces used by the
  [Dictionary \<TKey, TValue\>](https://msdn.microsoft.com/en-us/library/xfhwa508.aspx)
  class from the .NET Framework.  A single class implements multiple interfaces,
  each with a single responsibility.  A Dictionary<TKey,TValue> instance should
  be able to work anywhere the behavior of its interfaces is expected.
