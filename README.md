# AngularJS

After moving from Texas to Oregon, I've had a lot of free time on my hands and am taking it upon myself to learn modern frameworks, improve best practices and grow as a developer. Noticed there's a number of other who are in the same boat and created this repo to share my findings, record examples/experiments and hopefully showcase what all you can do with AngularJS. So, if you're ready to buckle down and learn, you're in the right place! Let's do this...

![myImage](https://media.giphy.com/media/XRB1uf2F9bGOA/giphy.gif)

## Table of Contents
- [Intro](#getting-started)
- [Directives](#angularjs-directives)
- [Expressions](#angularjs-expressions)
  - [Numbers](#angularjs-numbers)
  - [Strings](#angularjs-stings)
  - [Objects](#angularjs-objects)
  - [Arrays](#angularjs-arrays)
- [Applications](#angularjs-applications)
- [Modules](#angularjs-modules)
  - [Creating a Module](#creating-a-module)
  - [Adding a Controller](#adding-a-controller)
  - [Adding a Directive](#adding-a-directive)
  - [Modules and Controllers in Files]()
  - [Functions can Pollute the Global Namespace]()
  - [When to Load the Library]()
- [Directives]()
  - [Intro to Directives]()
  - [ng-app]()
  - [ng-init]()
  - [ng-model]()
  - [Creating new Directives]()
  - [Restrictions]()
- [Data Binding]()
  
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
  
## AngularJS Directives

AngularJS directives are HTML attributes with an ng prefix.

For example, the **ng-init** directive *initializes* AngularJS application variables.

```
<div ng-app="" ng-init="firstName='John'">
  <p>The name is <span ng-bind="firstName"></span></p>
</div>
```
The span with ng-bind will take the variable of firstName and fill in that placeholder with the value of John when 

> Alternatively, you can use **data-ng-**, instead of **ng-**, if you want to make your page HTML valid as demonstrated below.

```
<div data-ng-app="" data-ng-init="firstName='John'">
  <p>The name is <span data-ng-bind="firstName"></span></p>
</div>
```

## AngularJS Expressions
AngularJS expressions are written indies double braces: `**{{ expression }}**`
Expressions can also be written inside a directive: `**ng-bind="expression"**`

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

## AngularJS Numbers
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

## AngularJS Strings
AngularJS strings are like JavaScript strings:
```
<div ng-app="" ng-init="firstName='John';lastName='Doe'">
  <p>The name is {{ firstName + " " + lastName }}</p>
</div>
```

## AngularJS Objects
AngularJS objects are like JavaScript objects:
```
<div ng-app="" ng-init="person={firstName:'John',lastName:'Doe'}">
  <p>The name is {{ person.lastName }}</p>
</div>
```
## AngularJS Arrays
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

## AngularJS Applications

AngularJS **modules** define AngularJS applications.
AngularJS **controllers** control AngularJS applications.
The **ng-app** directive define sthe application, the **ng-controller** directive defines the controller.

```
<div ng-app="myApp" ng-controller="myCtrl">

First Name: <input type="text" ng-model="firstName"><br>
Last Name: <input type="text" ng-model="lastName"><br>
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
