# Whiteboard Coding questions
These questions can be completed in any language and are "language feature agnostic".  If specific language features are used to short-cut/solve the problem, then a follow-up question should be asked: "How would you solve this without language feature _x_?"

#### A note about Big O Notation (`O`)
Big O specifically describes the worst-case scenario, and can be used to describe the execution time required or the space used (e.g. in memory or on disk) by an algorithm.

A Big O cheat sheet:
* `O(1)` - an algorithm that will always execute in the same time (or space) regardless of the size of the input data set
* `O(n)` - an algorithm whose performance will grow linearly and in direct proportion to the size of the input data set - this is common with algorithms that involve a loop
* `O(N^2)` - an algorithm whose performance is directly proportional to the square of the size of the input data set - this is common with algorithms that involve nested iterations over the data set (Deeper nested iterations will result in O(N^3), O(N^4), etc)
* `O(2^n)` - an algorithm whose growth will double with each additional element in the input data set - The execution time of an O(2^N) function will quickly become very large

_references_: 
* http://rob-bell.net/2009/06/a-beginners-guide-to-big-o-notation/
* http://en.wikipedia.org/wiki/Big_O_notation

### Things to keep in mind during these coding questions:
* Did the candidate complete the task?
* Did they require help?
* Does the solution appear to work?
* Do they show an ability to think through the problem even if they do know know the answer?
* If asked, can the candidate walk you through the code with a sample input; are they able to do this without issue?
* Does the candidate describe what they are thinking about / doing when they get stuck or do they stare at the board blankly?

### Possible follow up questions for the coding problems below
* What is _Big O_ for performance and space?
* Is the solution recursive or iterative?  What are the implications of this choice?
* How might you improve performance of the algorithm you chose?
* How can you ensure the algorithm functions as expected? (`answers`: step through code, **write unit tests**, etc)

## Remove Duplicates in a list (medium)
Write a function that, when given a list of strings (or numbers or whatever you choose), will return a new list with no duplicates.  Pseudocode is fine.

One possible solution:
```csharp
public IList<T> RemoveDuplicates<T>(IList<T> list)
{
    IList<T> noDupes = new List<T>();

    foreach (T item in list) {
        if (!Contains(noDupes, item))
        {
            noDupes.Add(item);
        }
    }

    return noDupes;
}

public bool Contains<T>(IList<T> list, T item) {
    bool exists = false;

    foreach (T listItem in list)
    {
        if (item.Equals(listItem))
        {
            exists = true;
            break;
        }
    }

    return exists;
}
```

The above algorithm can improve Big O from O(n^2) to O(n) by using a HashSet which provides O(1) look-up efficiency:

```csharp
public IList<T> RemoveDuplicates<T>(IList<T> list)
{
    IList<T> noDupes = new List<T>();
    HashSet<T> tracker = new HashSet<T>();

    foreach (T item in list) {
        if (!tracker.Contains(item))
        {
            tracker.Add(item);  // this can be O(n), but only when capacity is small
            noDupes.Add(item);
        }
    }

    return noDupes;
}
```

Big O of the above algorithm is O(n).

## Write a factorial function (medium)
Given Factorial is defined as follows:

|  n   |  n!  |
| ---- | ---- |
|  0   |  **1**   |
|  1   |  **1**   |
|  2   |  _2 * 1 =_ **2**   |
|  3   |  _3 * 2 * 1 =_ **6**  |
|  4   |  _4 * 3 * 2 * 1 =_ **24**  |
|  5   |  _5 * 3 * 2 * 1 =_ **120** |
|  .   |  . |
|  .   |  . |
|  n   |  _n * (n-1)!_ `<-- this is a HUGE hint and usually produces a recursive solution so avoid it w/ experienced developers`|


**Write a function that will take in _n_ and return _n!_.**

Two possible solutions:
```csharp
public UInt64 RecursiveFactorial(UInt32 n)
{
    if (n == 0 || n == 1)
    {
        return 1;
    }

    return n * RecursiveFactorial(n - 1);
}

public UInt64 LoopFactorial(UInt32 n)
{
    UInt64 result = 1;

    for (UInt32 i = n; i > 1; i--)
    {
        result = result * i;
    }

    return result;
}
```

Big O of the above algorithms is O(n).


## Write a recursive file search

Given a starting directory and a file name, write a recursive function that will search that directory and all sub-directories and return the location of that file.  For example, I might give you "C:\" and "foo.txt", and the file may be on your desktop.  Pseudocode is fine.

Simplest solution:

```csharp
using System.IO;

FileInfo FindFile(DirectoryInfo dir, string filename)
{
  foreach (var file in dir.GetFiles())
  {
    if (file.Name == filename) return file;
  }
  foreach (var subDir in dir.GetDirectories())
  {
    var foundPath = FindFile(subDir, filename);
    if (foundPath != null) return foundPath;
  }
  return null;
}
```

Notes:
* Some people will abbreviate this by using linq.
* This is not a test of `System.IO` or of `C#` syntax.  Tell them about `FileInfo` and `DirectoryInfo` if needed, or don't even require them.  You could just as easily return a string.  It's the recursion and the tree traversal that you care about.

## Write a function to reverse the digits of an integer?

```javascript
function reverseDigits(value){
   var retVal = 0;
   while(value > 0){
      retVal = (retVal * 10) + (value % 10);
      value = value / 10;
   }

   return retVal;
}
```

## Create a FindById() method for a linked list data structure (medium)
