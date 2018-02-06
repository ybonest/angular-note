### 1. ng-app

* 指令初始化一个 AngularJS 应用程序。
* AngularJS应用程序的根元素

### 2. ng-init(初始化参数)

* 初始化参数

```html
<div ng-app="" ng-init="quantity=1;cost=5">
	<p>总价： <span ng-bind="quantity * cost"></span></p>
</div>
```

* 数组

```html
<div ng-app="" ng-init="points=[1,15,19,2,40]">
	<p>第三个值为 {{ points[2] }}</p>
</div>
```

### 3. ng-model(双向数据绑定)

* 指令把元素值（比如输入域的值）绑定到应用程序。
* 为应用程序数据提供类型验证（number、email、requrie）
* 为应用程序数据提供状态（invalid、dirty、touched、error）
* 为HTML元素提供CSS类
* 绑定HTML元素到HTML表单

```html
<div ng-app="myApp" ng-controller="myCtrl">
    名字: <input ng-model="name">
</div>

<script>
var app = angular.module('myApp', []);
app.controller('myCtrl', function($scope) {
    $scope.name = "John Doe";
});
</script>
```

```html
<form ng-app="" name="myForm" ng-init="myText = 'test@runoob.com'">
    Email:
    <input type="email" name="myAddress" ng-model="myText" required></p>
    <h1>状态</h1>
    {{myForm.myAddress.$valid}}
    {{myForm.myAddress.$dirty}}
    {{myForm.myAddress.$touched}}
</form>
```

### 4. ng-bind(单项数据绑定)

```html
<div ng-app="" ng-init="points=[1,15,19,2,40]">
	<p>第三个值为 <span ng-bind="points[2]"></span></p>
</div>
```

### 5. ng-controller(控制器)

* 控制器，在创建module模块后，可以使用ng-controller指令添加应用的控制器

```html
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
```



### 6. ng-repeat(循环)

* 数组循环

```html
<div ng-app="" ng-init="names=['Jani','Hege','Kai']">
  <p>使用 ng-repeat 来循环数组</p>
  <ul>
    <li ng-repeat="x in names">
      {{ x }}
    </li>
  </ul>
</div>
```

* 对象循环

```html
<div ng-app="" ng-init="names=[
{name:'Jani',country:'Norway'},
{name:'Hege',country:'Sweden'},
{name:'Kai',country:'Denmark'}]">
 
<p>循环对象：</p>
<ul>
  <li ng-repeat="x    in names">
    {{ x.name + ', ' + x.country }}
  </li>
</ul>
</div>
```

### 7. ng-show

```html
<form ng-app="" name="myForm">
    Email:
    <input type="email" name="myAddress" ng-model="text">
    <span ng-show="myForm.myAddress.$error.email">不是一个合法的邮箱地址</span>
</form>
```

### 8. ng-if

* ng-if指令可以根据表达式的值在DOM中生成或移除一个元素

  ```html
  <div ng-if="2+2==5">
  	Hi,I do exist
  </div>
  ```

### 9. ng-disabled

* **ng-disabled** 指令直接绑定应用程序数据到 HTML 的 disabled 属性。

  ```html
  <div ng-app="" ng-init="mySwitch=true">
      <p><button ng-disabled="mySwitch">点我!</button></p>
      <p><input type="checkbox" ng-model="mySwitch">按钮</p>
      <p>{{ mySwitch }}</p>
  </div>
  ```

### 10. ng-show

* **ng-show** 指令隐藏或显示一个 HTML 元素。

  ```html
  <div ng-app="">
      <p ng-show="true">我是可见的。</p>
      <p ng-show="false">我是不可见的。</p>
  </div>
  ```

### 11. ng-hide

* **ng-hide** 指令用于隐藏或显示 HTML 元素

  ```html
  <div ng-app="">
      <p ng-hide="true">我是不可见的。</p>
      <p ng-hide="false">我是可见的。</p>
  </div>
  ```

### 12. ng-click

* **ng-click** 指令定义了 AngularJS 点击事件。

  ```
  <div ng-app="" ng-controller="myCtrl">
    <button ng-click="count = count + 1">点我！</button>
    <p>{{ count }}</p>
  </div>
  ```

### 13. ng-switch

### 14. ng-switch-when

### 15. ng-bind-html

* 绑定 HTML 元素的 innerHTML 到应用程序数据，并移除 HTML 字符串中危险字符

  ```html
  <div ng-app="myApp" ng-controller="myCtrl">
  <p ng-bind-html="myText"></p>
  </div>
  <script>
  var app = angular.module("myApp", ['ngSanitize']);
  app.controller("myCtrl", function($scope) {
      $scope.myText = "My name is: <h1>John Doe</h1>";
  });
  </script>
  ```

### 16. ng-bind-template

* 规定要使用模板替换的文本内容

  ```html
  <div ng-app="myApp" ng-bind-template="{{firstName}} {{lastName}}" ng-controller="myCtrl"></div>
  <script>
  var app = angular.module("myApp", []);
  app.controller("myCtrl", function($scope) {
      $scope.firstName = "John";
      $scope.lastName = "Doe";
  });
  </script>
  ```

### 17. ng-blur

* 规定 blur 事件的行为

  ```html
  <input ng-blur="count = count + 1" ng-init="count=0" />
  <h1>{{count}}</h1>
  ```

### 18. ng-change

* 规定在内容改变时要执行的表达式

  ```html
  <body ng-app="myApp">
  <div ng-controller="myCtrl">
      <input type="text" ng-change="myFunc()" ng-model="myValue" />
      <p>The input field has changed {{count}} times.</p>
  </div>
  <script>
  angular.module('myApp', [])
  .controller('myCtrl', ['$scope', function($scope) {
      $scope.count = 0;
      $scope.myFunc = function() {
          $scope.count++;
      };
  }]);
  </script>
  </body>
  ```

### 19. ng-checked

* 规定元素是否被选中

  ```html
  <body ng-app="">
  <p>My:</p>
  <input type="checkbox" ng-model="all"> Check all<br><br>

  <input type="checkbox" ng-checked="all">Volvo<br>
  <input type="checkbox" ng-checked="all">Ford<br>
  <input type="checkbox" ng-checked="all">Mercedes
  </body>
  ```

### 20. ng-class

* 指定 HTML 元素使用的 CSS 类

  ```html
  <!DOCTYPE html>
  <html>
  <head>
  <meta charset="utf-8">
  <script src="http://cdn.static.runoob.com/libs/angular.js/1.4.6/angular.min.js"></script>
  <style>
  .sky {
      color:white;
      background-color:lightblue;
      padding:20px;
      font-family:"Courier New";
  }
  .tomato {
      background-color:coral;
      padding:40px;
      font-family:Verdana;
  }
  </style>
  </head>
  <body ng-app="">

  <p>选择一个类:</p>

  <select ng-model="home">
  <option value="sky">天空色</option>
  <option value="tomato">番茄色</option>
  </select>

  <div ng-class="home">
    <h1>Welcome Home!</h1>
    <p>I like it!</p>
  </div>

  </body>
  </html>
  ```


### 21. ng-class-even

* 类似 ng-class，但只在偶数行起作用

### 22. ng-class-odd

* 类似 ng-class，但只在奇数行起作用

### 23. ng-click

* 定义元素被点击时的行为

  ```html
  <button ng-click="count = count + 1" ng-init="count=0">OK</button>
  ```

### 24. ng-cloak

* 在应用正要加载时防止其闪烁

  ```html
  <div ng-app="">
  <p ng-cloak>{{ 5 + 5 }}</p>
  </div>
  ```