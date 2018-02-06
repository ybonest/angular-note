#### 1. 包含html

```
<body ng-app="">
<div ng-include="'runoob.htm'"></div>
</body>
```

#### 2. 包含AngularJS代码

```
<div ng-app="myApp" ng-controller="sitesCtrl"> 
  <div ng-include="'sites.htm'"></div>
</div>
<script>
var app = angular.module('myApp', []);
app.controller('sitesCtrl', function($scope, $http) {
    $http.get("sites.php").then(function (response) {
        $scope.names = response.data.records;
    });
});
</script>
```

其中sites.htm代码为

```
<table>
<tr ng-repeat="x in names">
<td>{{ x.Name }}</td>
<td>{{ x.Url }}</td>
</tr>
</table>
```

#### 3. 跨域包含

```
<body ng-app="myApp">
<div ng-include="'http://c.runoob.com/runoobtest/angular_include.php'"></div>
<script>
var app = angular.module('myApp', [])
app.config(function($sceDelegateProvider) {
    $sceDelegateProvider.resourceUrlWhitelist([
        'http://c.runoob.com/runoobtest/**'
    ]);
});
</script>
</body>
```

此外，还需要设置服务端允许跨域访问，

```
<?php
// 允许所有域名可以访问
header('Access-Control-Allow-Origin:*');
echo '<b style="color:red">我是跨域的内容</b>';
?>
```