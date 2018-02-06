#### 创建控制器
```html
<div ng-app="myApp" ng-controller="myCtrl">
</div>
```

```javascript
const app = angular.module("myApp",[]);
app.controller("myCtrl",function($scope){
  $scope.binary = "";
})
```

#### 以安全的方式创建控制器
当angular项目中的js文件被压缩时，有时候$scope会被更简短的单词代替，所以建议使用安全模式定义控制器

```javascript
const app = angular.module("myApp",[]);
app.controller("myCtrl",["$scope",function($scope){}])
```

#### 控制器嵌套

- AngularJS应用的任何一个部分，无论它渲染在那个上下文中，都有父级作用域。对于ng-app所处的层级来讲，它的父级作用域就是$rootScope

  (在指令内部创建的作用域被称为孤立作用域)

  除了孤立作用域外，所有的作用域都是通过原型继承而来，默认情况下，AngularJS在当前作用域无法找到某个属性时，会在父级作用域中进行查找，一层层向上，直到抵达$rootScope。

  ```html
  <div ng-controller="ParentController">
  		<div ng-controller="ChildController">
  			<a ng-click="sayHello()">say</a>
  		</div>
  		{{person}}  //输出{"greeted":false,"name":"Ari lerner"}
  </div>
  var app = angular.module('myApp',[]);
    app.controller('ParentController',function($scope){
    	$scope.person = {greeted:false};
    });
    app.controller('ChildController',function($scope){
    	$scope.sayHello = function(){
    	$scope.person.name = "Ari lerner";
    }
   });
  ```