# Unit Testing
Unit tests are going to be required more and more in the coming months.
Eventually, [merge requests](MergeRequests) are going to be denied if unit tests
are considered to be missing or incomplete.

This document will help you understand what it is that unit tests should look
like, as well as provide a series of guides to get you started writing unit
tests.

## Purpose
The purpose of unit tests is often misunderstood.  Unit tests are not
(inheritently) meant to discover bugs.  Unit tests are meant to describe the
software and how it works.  Reading unit tests should give the reader a good
grasp of how to use the software and what responds to expect.

Unit tests do discover bugs, of course, but most often not in the code that is
currently being written.  Instead, while adding new code or editing existing
code, code elsewhere might break, and its unit tests fail.

## Guidelines
Good unit tests follow a set of very simple rules:
+ Unit tests should only test one thing.
  + This does not mean a unit test only tests one method.  It means that a unit
  test only tests one specific aspect of a method or service call.
  For example, pretend that you have method A that takes in value B and returns
  C.
    + ```csharp
    public C A(B)
    ```
      + If `B` is 0, `C` is null.
      + If `B` is odd, `C.IsEven` is false.
      + If `B` is odd, `C.Remainder` cannot be 0.
      + These would turn into three separate unit tests, even though two of them
      could be potentially tested in the same code.
+ Unit tests should not rely on external dependencies.
  + This means that any dependencies should be either faked or mocked, depending
  on whether code being tested depends on the dependency or not.
+ Unit tests should mock 1 dependency per test.
  + A fake and a mock are two different things, although they are very similar.
  A fake, simply, is a dependency that is being faked to test the code in the
  method that uses it.
  + A mock is a faked dependency in which the response of the dependency, and
  the method's reaction to that response, is being tested.
  + Fakes and mocks can both be done easily using one of the many mocking
  frameworks. We use [Moq](https://github.com/Moq/moq4/blob/master/README.md).
  + This rule is not concrete, but should be followed as much as possible.  If a
  test requires multiple mocks, it possibly means the method is overly complex.

## Resources
+ [Writing Testable Code](TestableCode)
+ [Testing Code using EFUnitOfWork](TestDatabase)
