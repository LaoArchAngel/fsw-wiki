*Questions related to JS and UI skills, such as: what is a JS prototype, what are services in angular, what is templating?*

---

# Phone Screen Questions

## Easy Questions

1. *What JS debugging tools do you prefer to use?*

    `Answer` (any/all are allowed):
    * Chrome developer tools
    * Firefox developer tools
    * Firebug
    * Fiddler

    `Follow-Ups`:
    * Ask “Why?” There are pos and cons of each.  Sometimes you need to use the debugging tools in the browser when you are debugging a problem only occurring on that browser.

2. *What is the difference between 'undefined' and 'null'?*

    `Answer`: 
    * undefined: a variable has been declared but has not yet been assigned a value
    * null: a variable has been assigned an empty value

3. *Is a function name required?*

    `Answer`: No - anonymous function have no name, and can be assigned to a variable or passed into another function

4. *What is the DOM?*

    `Answer`: **D**ument **O**bject **M**odel - object class that is visible and accessible to JavaScript and give access to all comment in and HTML page.


## Med Questions

1. *How do you use JavaScript to retrieve data from the server without refreshing the page?*
    
    `Answer`: using the XMLHttpRequest object
    
    `Partial Credit Answer`: using the AJAX functionality of an existing JS Framework (JQuery, Angular, etc..)

2. *What is the difference between 'var x = 3' and 'x = 3'?*

    `Answer`:  Using 'var' assigns the variable to the current scope, while not using 'var' assigns it to the global scope (unless x was previously defined with 'var' in the current scope)

3. *How do you add an item to an array?*

    `Answer`: Using the 'push' function (i.e. `array.push("value")` adds "value to the end of the array)

4. *What is a JavsScript Closure?*

    `Answer`: A closure is a function whose local variables are kept alive after the function has returned.

5. *What is the "This" keyword and what does it reference?

    `Answer1`: "this" refers to the "owner" of the function being executed
    `Answer2`: "this" refers to the object a function is a method of
    `Answer Details`: The caller provides the "this" value. If the "this" value provided by the caller is not an object (including the case where it is null), then the "this" value is the global object.


## Hard Questions
1. *If a function doesn't have a return statement, what if anything is returned?*

    `Answer`: 'undefined' is returned, unless it's a constructor, in which case 'this' is returned

2. *What is a closure in JavaScript*

`Answer`: A closure is an inner function that has access to the variables in the outer (enclosing) function’s scope chain. The closure has access to variables in three scopes; specifically: (1) variable in its own scope, (2) variables in the enclosing function’s scope, and (3) global variables.
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