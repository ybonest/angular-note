在AngularJS中，服务是一个函数或对象

#### 1、$location服务

* 可以返回当前页面的URL地址

```javascript
var app = angular.module('myApp', []);
app.controller('customersCtrl', function($scope, $location) {
    $scope.myUrl = $location.absUrl();
});
```

#### 2. $http服务

* $http是AngularJS应用中最常见的服务，服务向服务器发送请求，应用响应服务器传送过来的数据

```javascript
var app = angular.module('myApp', []);
app.controller('myCtrl', function($scope, $http) {
    $http.get("welcome.htm").then(function (response) {
        $scope.myWelcome = response.data;
    });
});
```

#### 3. $timeout服务

* AngularJS $timeout服务对应了JS window.setTimeout函数

```javascript
var app = angular.module('myApp', []);
app.controller('myCtrl', function($scope, $timeout) {
    $scope.myHeader = "Hello World!";
    $timeout(function () {
        $scope.myHeader = "How are you today?";
    }, 2000);
});
```

#### 4. $interval 服务

* AngularJS **$interval** 服务对应了 JS **window.setInterval** 函数。

```javascript
var app = angular.module('myApp', []);
app.controller('myCtrl', function($scope, $interval) {
    $scope.theTime = new Date().toLocaleTimeString();
    $interval(function () {
        $scope.theTime = new Date().toLocaleTimeString();
    }, 1000);
});
```

#### 5、创建自定义服务

```javascript
var app = angular.module('myApp', []);
app.service('hexafy', function() {
	this.myFunc = function (x) {
        return x.toString(16);
    }
});
app.controller('myCtrl', function($scope, hexafy) {
  $scope.hex = hexafy.myFunc(255);
});
```

* 过滤器中使用服务

```html
<div ng-app="myApp">
	<h1>{{255 | myFormat}}</h1>
</div>

<script>
    var app = angular.module('myApp', []);
    app.service('hexafy', function() {
        this.myFunc = function (x) {
            return x.toString(16);
        }
    });
    app.filter('myFormat',['hexafy', function(hexafy) {
        return function(x) {
            return hexafy.myFunc(x);
        };
    }]);
</script>
```