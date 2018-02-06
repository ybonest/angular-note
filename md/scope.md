#### 1. Scope概述

* Scope（作用域）是应用在HTML（视图）和JavaScript（控制器）之间的纽带

* Scope是一个对象，有可用的方法和属性

* Scope可应用在视图和控制器上

  ```
  <div ng-app="myApp" ng-controller="myCtrl">
  	<h1>{{carname}}</h1>
  </div>

  <script>
      var app = angular.module('myApp', []);
      app.controller('myCtrl', function($scope) {
          $scope.carname = "Volvo";
      });
  </script>
  ```

  ```
  <div ng-app="myApp" ng-controller="myCtrl">
      <input ng-model="name">
      <h1>{{greeting}}</h1>
      <button ng-click='sayHello()'>点我</button>    
  </div>
   
  <script>
      var app = angular.module('myApp', []);
      app.controller('myCtrl', function($scope) {
          $scope.name = "Runoob";
          $scope.sayHello = function() {
              $scope.greeting = 'Hello ' + $scope.name + '!';
          };
      });
  </script>
  ```

#### 2. Scope作用范围

* 在大型项目中，HTML DOM中有多个作用域，这时就需要知道所使用的scope对应的哪一个作用域

  ```
  <div ng-app="myApp" ng-controller="myCtrl">
      <ul>
          <li ng-repeat="x in names">{{x}}</li>
      </ul>
  </div>

  <script>
  var app = angular.module('myApp', []);
  app.controller('myCtrl', function($scope) {
      $scope.names = ["Emil", "Tobias", "Linus"];
  });
  </script>
  ```

#### 3. 根作用域

* 所有的应用中都有一个`$rootScope`,它可以作用在ng-app指令包含的所有HTML元素中

* $rootScope可作用于整个应用中，是各个controller中scope的桥梁，用rootscope定义的值，可以在各个controller中使用

  ```
  <div ng-app="myApp" ng-controller="myCtrl">
      <h1>{{lastname}} 家族成员:</h1>
      <ul>
          <li ng-repeat="x in names">{{x}} {{lastname}}</li>
      </ul>
  </div>

  <script>
      var app = angular.module('myApp', []);
      app.controller('myCtrl', function($scope, $rootScope) {
          $scope.names = ["Emil", "Tobias", "Linus"];
          $rootScope.lastname = "Refsnes";
      });
  </script>
  ```