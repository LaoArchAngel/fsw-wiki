# Whiteboard Coding questions
These questions can be completed in any language and are "language feature agnostic".  If specific language features are used to short-cut/solve the problem, then a follow-up question should be asked: "How would you solve this without language feature _x_?"

## Remove Duplicates in a collection (easy)


## Reverse a String (easy)


## Create a FindById() method for a linked list datastructure (medium)


## Write a factorial function (medium)

## Write a recursive file search

Given a starting path and a file name, write a recursive function that will search that directory and all sub-directories and return the full path to that file.  For example, I might give you "C:\" and "foo.txt", and the file may be on your desktop.

Simplest solution (pseudocode):

string FindFile(string dir, string filename)
{
  foreach (var file in dir.GetFiles())
  {
    if (file.Name == filename) return dir;
  }
  foreach (var subDir in dir.GetDirectories())
  {
    var foundPath = FindFile(subDir, filename);
    if (foundPath != null) return foundPath;
  }
  return null;
}

Some people will abbreviate this by using linq.