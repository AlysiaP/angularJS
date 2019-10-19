# AngularJS
After moving from Texas to Oregon, I've had a lot of free time on my hands and am taking it upon myself to learn modern frameworks, improve best practices and grow as a developer.

Noticed there's a number of others who are in the same boat and created this repo to share my findings, record examples/experiments and hopefully showcase what all you can do with AngularJS. So, if you're ready to buckle down and learn, you're in the right place! Let's do this...

![myImage](https://media.giphy.com/media/XRB1uf2F9bGOA/giphy.gif)

## Table of Contents
- [Intro](#getting-started)
- [Applications](#angularjs-applications)
- [Expressions](#angularjs-expressions)
  - [Numbers](#angularjs-numbers)
  - [Strings](#angularjs-stings)
  - [Objects](#angularjs-objects)
  - [Arrays](#angularjs-arrays)
- [Modules](#angularjs-modules)
  - [Creating a Module](#creating-a-module)
  - [Adding a Controller](#adding-a-controller)
  - [Adding a Directive](#adding-a-directive)
  - [Modules and Controllers in Files]()
  - [Functions can Pollute the Global Namespace]()
  - [When to Load the Library]()
- [Directives](#angularjs-directives)
  - [ng-repeat](#the-ng-repeat-directive)
  - [ng-app](#the-ng-app-directive)
  - [ng-init](#the-ng-init-directive)
  - [ng-model](#the-ng-model-directive)
  - [Create new Directives](#create-new-directives)
  - [Restrictions](#restictions)
- [AngularJS Model](#angularjs-model)
  - [Two-Way Binding](#two-way-binding)
  - [Validate User Input](#validate-user-input)
  - [Application Status](#application-status)
  - [CSS Classes](#css-classes)
- [Data Binding](#angularjs-data-binding)
  
  
  
## Getting started

AngularJS is a JavaScript framework written in JavaScript and is distributed as a JavaScript file. Angular can be added to a web page with a script tag:

```
<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.9/angular.min.js"></script>
```

### AngularJS Extends HTML

AngularJS extends HTML with ng-directives, such as:

`ng-app` : defines an Angular application

`ng-model` : binds the value of HTML controls (input, select, textarea) to application data

`ng-bind` : binds application data to the HTML view

Example: 
```
<!DOCTYPE html>
<html>
  <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.9/angular.min.js"></script>
  <body>
    <div ng-app="">
      <p>Name: <input type="text" ng-model="name"></p>
      <p ng-bind="name"></p>
    </div>
  </body>
</html>
```

Example explained:
> AngularJS starts automatically when the web page has loaded. The **ng-app** directive tells AngularJS that the `<div>` element is the "owner" of an AngularJS application. The **ng-model** directive binds the value of the input field to the application variable name. The **ng-bind** directive binds the content of the `<p>` element to the application variable name.



## AngularJS Applications

AngularJS **modules** define AngularJS applications.
AngularJS **controllers** control AngularJS applications.
The **ng-app** directive define sthe application, the **ng-controller** directive defines the controller.

```
<div ng-app="myApp" ng-controller="myCtrl">
  First Name: <input type="text" ng-model="firstName">
  <br>
  Last Name: <input type="text" ng-model="lastName">
  <br>
  <br>
  Full Name: {{firstName + " " + lastName}}
</div>

<script>
  //module defining application
  var app = angular.module('myApp', []);

  // Controller controlling application
  app.controller('myCtrl', function($scope) {
    $scope.firstName= "John";
    $scope.lastName= "Doe";
  });
</script>
```



## AngularJS Expressions
AngularJS expressions are written indies double braces: `{{ expression }}`

Expressions can also be written inside a directive: `ng-bind="expression"`

AngularJS will resolve the expression, and return the result exactly where the expression is written.

**AngularJS expressions** are much like **JavaScript expressions**: They can contain literals, operators, and variables.

AngularJS will "output" data exactly where the expression is written:
```
<!DOCTYPE html>
<html>
  <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.9/angular.min.js"></script>
  <body>

  <div ng-app="">
    <p>My first expression: {{ 5 + 5 }}</p>
  </div>

  </body>
</html>
```
> If you remove the `ng-app` directive, HTML will display the expression as it is, without solving it.


AngularJS expressions bind AngularJS data to HTML the same way as the **ng-bind** directive.

```
<!DOCTYPE html>
<html>
  <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.9/angular.min.js"></script>
  <body>

  <div ng-app="">
    <p>Name: <input type="text" ng-model="name"></p>
    <p>{{name}}</p>
  </div>

  </body>
</html>
```


### AngularJS Numbers
AngularJS numbers are like JavaScript numbers:
```
<div ng-app="" ng-init="quantity=1;cost=5">
  <p>Total in dollar: {{ quantity * cost }}</p>
</div>
```
Same example using `ng-bind`:
```
<div ng-app="" ng-init="quantity=1;cost=5">
  <p>Total in dollar: <span ng-bind="quantity * cost"></span></p>
</div>
```
> Using `ng-init` is not very common. You will learn a better way to initialize data in the section about controllers.


### AngularJS Strings
AngularJS strings are like JavaScript strings:
```
<div ng-app="" ng-init="firstName='John';lastName='Doe'">
  <p>The name is {{ firstName + " " + lastName }}</p>
</div>
```


### AngularJS Objects
AngularJS objects are like JavaScript objects:
```
<div ng-app="" ng-init="person={firstName:'John',lastName:'Doe'}">
  <p>The name is {{ person.lastName }}</p>
</div>
```


### AngularJS Arrays
AngularJS arrays are like JavaScript arrays:
```
<div ng-app="" ng-init="points=[1,15,19,2,40]">
  <p>The third result is {{ points[2] }}</p>
</div>
```


### AngularJS Expressions vs. JavaScript Expressions
Like JavaScript expressions, AngularJS expressions can contain literals, operators, and variables.

Unlike JavaScript expressions, AngularJS expressions can be written inside HTML.

AngularJS expressions do not support conditionals, loops, and exceptions, while JavaScript expressions do.

AngularJS expressions support filters, while JavaScript expressions do not.



## AngularJS Modules
An AngularJS moduel defines an applications
The module is a container for the different parts of an application
The module is a containter for the application controllers.
Controllers always belong to a module.


### Creating a Module
A module is created by using the function `angular.module`:
```
<div ng-app="myApp">...</div>

<script>
  var app = angular.module("myApp", []);
</script>
```
The "myApp" parameter regeres to an HTML element in which the application will run.
Now you can add controllers, directives, filters, and more to your AngularJS application.


### Adding a Controller
Adding a controller to yoru application and refer to the controller with the `ng-controller` directive: 
```
app.controller("myCtrl", function($scope) {
  $scope.firstName = "John";
  $scope.lastName = "Doe";
});

</script>
```


### Adding a Directive
AngularJS has a set of built-in directives which you can use to add functionality to your application.

For a full reference, visit the [AngularJS directive reference](https://www.w3schools.com/angular/angular_ref_directives.asp).

In addition, you can use the module to add your own directives ot your applications:
```
<div ng-app="myApp" w3-test-directive></div>

<script>
var app = angular.module("myApp", []);

app.directive("w3TestDirective", function() {
  return {
    template : "I was made in a directive constructor!"
  };
});
</script>
```


### Modules and Controllers in Files
It's common in AngularJS applications to put the module and the controllers in JavaScript files.
In this example, "myApp.js" contains an application module definition, while "myCtrl.js" contains the controller:
```
<!DOCTYPE html>
<html>
  <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.9/angular.min.js"></script>
  <body>

    <div ng-app="myApp" ng-controller="myCtrl">
      {{ firstName + " " + lastName }}
    </div>

    <script src="myApp.js"></script>
    <script src="myCtrl.js"></script>

  </body>
</html>
```
#### myApp.js
```
var app = angular.module("myApp",[]);
```
> The [] parameter in the module definition can be used to define dependent modules. Without the [] parameter, you are not creating a new module, but retrieving an existing one.

#### myCtrl.js
```
app.controller("myCtrl", function($scope) {
  $scope.firstName = "John";
  $scope.lastName= "Doe";
});
```

### Functions can Pollute the Global Namespace
Global functions should be avoided in JavaScript. They can easily be overwritten or destroyed by other scripts.

AngularJS modules reduces this problem, by keeping all functions local to the module.

### When to Load the Library
While it is common in HTML applications to place scripts at the end of the `<body>` element, it is recommended that you load the AngularJS library either in the `<head>` or at the start of the `<body>`.

This is because calls to `angular.module` can only be compiled after the library has been loaded.

```
<!DOCTYPE html>
<html>
  <body>
    <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.9/angular.min.js"></script>

    <div ng-app="myApp" ng-controller="myCtrl">
      {{ firstName + " " + lastName }}
    </div>

    <script>
    var app = angular.module("myApp", []);
    app.controller("myCtrl", function($scope) {
      $scope.firstName = "John";
      $scope.lastName = "Doe";
    });
    </script>

  </body>
</html>
```
## AngularJS Directives

AngularJS lets you extend HTML with new attributes called **directives** with an `ng-` prefix.

For example, the `ng-init` directive *initializes* AngularJS application variables.

```
<div ng-app="" ng-init="firstName='John'">
  <p>The name is <span ng-bind="firstName"></span></p>
</div>
```

> Alternatively, you can use **data-ng-**, instead of **ng-**, if you want to make your page HTML valid as demonstrated below.

```
<div data-ng-app="" data-ng-init="firstName='John'">
  <p>The name is <span data-ng-bind="firstName"></span></p>
</div>
```


#### Data Binding
The `{{ firstName }}` expression in the example aboves is an AngularJS data binding expression.

Data binding in AngularJS binds expressions with data:

`{{ firstName }}` is bound with `ng-model="firstName"`


### The `ng-repeat` directive
The `ng-repeat` directive repeats an HTML element:

```
<div ng-app="" ng-init="names=['Jani','Hege','Kai']">
  <ul>
    <li ng-repeat="x in names">
      {{ x }}
    </li>
  </ul>
</div>
```

The `ng-repeat` directive actually **clones HTML elements** once for each item in a collection. 

The `ng-repeat` directive used on an array of objects:

```
<div ng-app="" ng-init="names=[
{name:'Jani',country:'Norway'},
{name:'Hege',country:'Sweden'},
{name:'Kai',country:'Denmark'}]">

<ul>
  <li ng-repeat="x in names">
    {{ x.name + ', ' + x.country }}
  </li>
</ul>

</div>
```

> AngularJS is perfect for database CRUD (Create Read Update Delete) applications. Just imagine if these objects were records from a database.


### The `ng-app` Directive
The `ng-app` directive defines the **root element** of an AngularJS application.

The `ng-app` directive will **auto-bootstrap** (automatically initialize) the application when a web page is loaded.


### The `ng-init` Directive
The `ng-init` directive defines **initial values** for an AngularJS application.

Normally, you will not use `ng-init`, but instead you will use a controller or module.

To read more on how you'll use `ng-init` as a controller or module, click (here)[#init].


### The `ng-model` Directive
The `ng-model` directive binds the value of HTML controls (input, select, textarea) to application data.

The `ng-model` directive can also: 
- Provide type validation for application data (number, email, required)
- Provide status for application data (invalid, dirty, touched, error)
- Provide CSS classes for HTML elements
- Bind HTML elements to HTML forms


### Create New Directives
In addition to all the built-in AngularJS directives, you can create your own directives.

New directives are created by using the `.directive` function

To invoke the new directive, make an HTML element with the same tag name as the new directive.

When naming a direction, you must use a camel case name, `myDirective`, but when invoking it, you must use `-` separated name, `my-directive`:

```
<body ng-app="myApp">

<my-directive></my-directive>

<script>
var app = angular.module("myApp", []);
app.directive("myDirective", function() {
  return {
    template : "<h1>Made by a directive!</h1>"
  };
});
</script>

</body>
```

You can invoke a directive by using:
- Element name : `<my-directive></my-directive>`
- Attribute : `<div my-directive></div>`
- Class : `<div class="my-directive"></div>`
- Comment : `<!-- directive: my-directive -->`

### Restrictions
You can restrict your directives to only be invoked by some of the methods.
For example, by adding a restrict property with the value "A", the directive can only be invoked by attributes:

```
var app = angular.module("myApp", []);
app.directive("myDirective", function() {
  return {
    restrict : "A",
    template : "<h1>Made by a directive!</h1>"
  };
});
```

The legal restrict values are:
- `E` for Element name
- `A` for Attribute
- `C` for Class
- `M` for Comment

By default the value is `EA`, meanign that both Element names and attribute naems can invoke the directive.



## AngularJS Model

### The ng-model Directive
The `ng-model` directive binds the value of HTML controls (input, select, textarea) to application data.

For example, with the `ng-model` directive, you can bind the value of an input field to a variable created in AngularJS.

```
<div ng-app="myApp" ng-controller="myCtrl">
  Name: <input ng-model="name">
</div>

<script>
  var app = angular.module('myApp', []);
  
  app.controller('myCtrl', function($scope) {
    $scope.name = "John Doe";
  });
</script>
```


### Two-Way Binding
The binding goes both ways. If the user changes the value inside the input field, the AngularJS property will also change it's value:

```
<div ng-app="myApp" ng-controller="myCtrl">
  Name: <input ng-model="name">
  <h1>You entered: {{name}}</h1>
</div>
```


### Validate User Input
The `ng-model` directive can provide type validation for application data (number, email, required):
```
<form ng-app="" name="myForm">
  Email:
  <input type="email" name="myAddress" ng-model="text">
  <span ng-show="myForm.myAddress.$error.email">Not a valid e-mail address</span>
</form>
```
In the example above, the span wil lbe displayed only if the expression in the `ng-show` attribute returns `true`.

> If the property in the `ng-model` attribute does not exist, AngularJS will create one for you

### Application Status
The `ng-model` directive can provide status for applicatoin data (valid, dirty, touched, error):
```
<form ng-app="" name="myForm" ng-init="myText = 'post@domain.com'">
  Email:
  <input type="email" name="myAddress" ng-model="myText" required>
  <h1>Status</h1>
  {{myForm.myAddress.$valid}}
  {{myForm.myAddress.$dirty}}
  {{myForm.myAddress.$touched}}
</form>
```

### CSS Classes
The `ng-model` directive provides CSS classes for HTML elemetns, depending on their status:
```
<style>
input.ng-invalid {
  background-color: lightblue;
}
</style>

<form ng-app="" name="myForm">
  Enter your name:
  <input name="myName" ng-model="myText" required>
</form>
```

The `ng-model` directive adds/removes the following classes, according to the status of the form field:
- ng-empty
- ng-not-empty
- ng-touched
- ng-untouched
- ng-valid
- ng-invalid
- ng-dirty
- ng-pending
- ng-pristine

## AngularJS Data Binding
