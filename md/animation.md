**AngularJS 使用动画需要引入 angular-animate.min.js 库**

  ```
  <body ng-app="ngAnimate">
    隐藏 DIV: <input type="checkbox" ng-model="myCheck">
    <div ng-hide="myCheck"></div>
  </body>
  ```

* 如果应用中已经设置了应用名，可以把 ngAnimate 直接添加在模型中

  ```
  <body ng-app="myApp">
  	<h1>隐藏 DIV: <input type="checkbox" ng-model="myCheck"></h1>
  <div ng-hide="myCheck"></div>
  <script>
  	var app = angular.module('myApp', ['ngAnimate']);
  </script>
  ```