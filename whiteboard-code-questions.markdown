# Whiteboard Coding questions
These questions can be completed in any language and are "language feature agnostic".  If specific language features are used to short-cut/solve the problem, then a follow-up question should be asked: "How would you solve this without language feature _x_?"

## Remove Duplicates in a list (easy)
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

## Create a FindById() method for a linked list datastructure (medium)


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