# AngularJS

AngularJS is a JavaScript framework written in JavaScript and is distributed as a JavaScript file. Angular can be added to a web page with a script tag:

`<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.9/angular.min.js"></script>`

# AngularJS Extends HTML

AngularJS extends HTML with ng-directives, such as:

`ng-app` : defines an Angular application
`ng-model` : binds the value of HTML controls (input, select, textarea) to application data
`ng-bind` : binds application data to the HTML view

Example: 
`<!DOCTYPE html>
<html>
  <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.9/angular.min.js"></script>
  <body>
    <div ng-app="">
      <p>Name: <input type="text" ng-model="name"></p>
      <p ng-bind="name"></p>
    </div>
  </body>
</html>`

Example explained:
AngularJS starts automatically when the web page has loaded.
The ng-app directive tells AngularJS that the <div> element is the "owner" of an AngularJS application.
The ng-model directive binds the value of the input field to the application variable name.
The ng-bind directive binds the content of the <p> element to the application variable name.
  
# AngularJS Directives

AngularJS directives are HTML attributes with an ng prefix.

For example, the ng-init directive initializes AngularJS application variables.

`<div ng-app="" ng-init="firstName='John'">
  <p>The name is <span ng-bind="firstName"></span></p>
</div>`
