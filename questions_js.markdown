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

    `Answer`: **D**ocument **O**bject **M**odel - object class that is visible and accessible to JavaScript and give access to all comment in and HTML page.


## Med Questions

1. *How do you use JavaScript to retrieve data from the server without refreshing the page?*
    
    `Answer`: using the XMLHttpRequest object
    
    `Partial Credit Answer`: using the AJAX functionality of an existing JS Framework (JQuery, Angular, etc..)

2. *What is the difference between 'var x = 3' and 'x = 3'?*

    `Answer`:  Using 'var' assigns the variable to the current scope, while not using 'var' assigns it to the global scope (unless x was previously defined with 'var' in the current scope)

3. *How do you add an item to an array?*

    `Answer`: Using the 'push' function (i.e. `array.push("value")` adds "value to the end of the array)

5. *What is the "This" keyword and what does it reference?*

    `Answer 1`: "this" refers to the "owner" of the function being executed

    `Answer 2`: "this" refers to the object a function is a method of

    `Answer Details`: The caller provides the "this" value. If the "this" value provided by the caller is not an object (including the case where it is null), then the "this" value is the global object.

6. *What is the prototype of an object?*

    `Answer 1`: It is a property that allows you to add properties (and methods) to all objects instantiated form that constructor function.

    `Answer 2`: By using this property, it is possible to create a base constructor function that contains some basic properties and methods, and then define different objects that inherit (and eventually override) all the properties defined in the base object.

## Hard Questions
1. *If a function doesn't have a return statement, what if anything is returned?*

    `Answer`: 'undefined' is returned, unless it's a constructor, in which case 'this' is returned

2. *What is a closure in JavaScript*

    `Answer`: A closure is an inner function that has access to the variables in the outer (enclosing) function’s scope chain. The closure has access to variables in three scopes; specifically: 
    1. variable in its own scope
    2. variables in the enclosing function’s scope
    3. global variables

3. *Explain DOM Event propagation.*

    `Answer`: When an event is registered on a DOM element, it will travel up through the nodes in the DOM. The event can be listened for on the element that the event originated on AND all of its parent nodes.

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

---

# AngularJS questions

## Easy Questions
1. *where do directives and controllers live?*
‘Answer’: in modules

2. *how do you create a module?*
`Answer`: angular.module(‘myModule’, []) where the first param is the modules name and the second parameter is an array of dependancies

3: *how do you get a module?*
`Answer`: angular.module(‘myModule’) with one param (the module’s name)

4. *if i define a property named ‘myNewProperty’ on an controller’s $scope, what syntax do i use to display that property’s value in a template?*
`Answer`: double mustache syntax like {{myNewProperty}}

5. *what is the significance of the ng-app?*
`Answer`: it is the name of the applications primary module

6. *where should you modify the dom?*
`Answer`: in a directive

## Med Questions

1. *name a few configurable properties of a directive*
`Answer`: restrict, require, scope, controller, link, controllerAs, bindToController, template, templateUrl, replace

2. *how does $templateCache work*
`Answer`: before requesting an .html file from the server, angular will check to see if that file exists in $templateCache first

3. *what two parameters does $scope.$watch accept?*
`Answer`: 2 functions. one which returns a value and one function which will be executed if the value changes.

4. *if i have code within a controller that i want to use in another controller, how do i share it?*
`Answer`: extract the shared code into a service or factory and inject it into both controllers

5. *what does ‘::’ indicate in a template?*
`Answer`: one way data binding

6. *how many digest cycles will angular run before throwing an exception?*
`Answer`: 10


## Hard Questions

1. *if you see a provider, such as myFactoryProvider, which phase are you in?*
`Answer`: config

2. *name two easy ways to optimize ng-repeat*
`Answer`: track by / one time data binding

3. *how do you unbind a watcher?*
`Answer`: $scope.$watch returns a function which will unbind the watch when executed

4. *when would i use link vs controller in a directive?*
`Answer`: use link when you need to access a dom element or if you do not need to expose an api for your directive. use controller to expose an api to other directives.

5. *what is the advantage of using a provider over a factory or service*
`Answer`: providers can be configured during the module config phase

6. *why is annotation important in angular?*
`Answer`: if you were to minify your scripts, the application would break because of the way angular’s dependency injection works

7. *explain how the digest cycle works for a $scope*
`Answer`: angular iterates through every watch and executes those watches functions if necessary until all watches values stop changing