Angular Sails Bind
==================

An AngularJS service to bind Angular models with sailsjs backend models using socket.io.

Add it as a dependency to your angular app, and then bind any model IN JUST ONE LINE!!!!!

```javascript
  $sailsBind("<your model name here>", $scope);
```

What it does:

* Creates the model inside the $scope for you.
* Retrieves the model data from the backend using socket.
* Watches for changes made by the user in the UI and updates the backend immediately.
* Watches for changes made in the backend and updates the UI immediately.

Installation:

```shell
bower install angular-sails-bind
```
Code Quality
------------
[![Code Climate Rating](https://codeclimate.com/github/diegopamio/angular-sails-bind.png)](https://codeclimate.com/github/diegopamio/angular-sails-bind)

Usage
-----

A small example:

```javascript
var app = angular.module("MyApp", ['ngSailsBind']);
app.controller("ItemsCtrl", function ($scope, $sailsBind) {
  // To easily add new items to the collection.
  $scope.newItem = {};  
  /** This will:
  *     1. Add a "items" model to $scope. (pluralized)
  *     2. Get the data from your http://<examplesite.com>/item thru sailsjs socket get.
  *     3. Setup socket io so that, when something changes in the sailsjs backend, they will be reflected
  *        in the angular "items" model.
  *     4. Watch the "items" model for collection changes in angular (add and removal of items
  *        and send them to the backend using socket.
  **/
  $sailsBind("item", $scope);
```

```html
<div ng-controller="ItemsCtrl">
  <input ng-model="newItem.name"/><a href="" ng-click="items.push(newItem);newItem={}"></a>Add New
  <ul>
    <li ng-repeat="item in items">{{item.name}} <a href="" ng-click="items.splice(items.indexOf(item), 1)">remove</a></li>
  </ul>
</div>
```

Getting a subset of the model:

You can filter the initial model content by adding a third parameter to the $sailsBind function (thanks @Shalotelli for the request). 

```javascript
   $sailsBind("item", $scope, {"name": {"contains": "Foo"}};
```

This third parameter is a json that follows the "where" clause syntax, as documented in sails' find call: 
[http://beta.sailsjs.org/#!documentation/reference/Blueprints/FindRecords.html]()