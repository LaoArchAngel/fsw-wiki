# Whiteboard Coding questions
These questions can be completed in any language and are "language feature agnostic".  If specific language features are used to short-cut/solve the problem, then a follow-up question should be asked: "How would you solve this without language feature _x_?"

## Remove Duplicates in a collection (easy)


## Reverse a String (easy)


## Create a FindById() method for a linked list datastructure (medium)


## Write a factorial function (medium)

## Write a recursive file search

Given a starting directory and a file name, write a recursive function that will search that directory and all sub-directories and return a pointer to that file.  For example, I might give you "C:\" and "foo.txt", and the file may be on your desktop.  Pseudocode is fine.

Simplest solution:

```
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