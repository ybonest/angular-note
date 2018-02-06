#### 1. ng-options

- - 使用ng-options创建选择框

```
<div ng-app="myApp" ng-controller="myCtrl">
    <select ng-init="selectedName = names[0]" ng-model="selectedName" ng-options="x for x in names">
    </select>
</div>
<script>
    var app = angular.module('myApp', []);
    app.controller('myCtrl', function($scope) {
        $scope.names = ["Google", "Runoob", "Taobao"];
    });
</script>
```

- 使用ng-repeat创建选择框

```
<select>
  <option ng-repeat="x in names">{{x}}</option>
</select>
```

对比ng-options，ng-repeat有一定局限性

- 数据源为数组时对比实例

```
<div ng-app="myApp" ng-controller="myCtrl">
  <p>选择网站:</p>
  <select ng-model="selectedSite">
      <option ng-repeat="x in sites" value="{{x.url}}">{{x.site}}</option>
  </select>

  <h1>你选择的是: {{selectedSite}}</h1>
</div>

<script>
  var app = angular.module('myApp', []);
  app.controller('myCtrl', function($scope) {
      $scope.sites = [
          {site : "Google", url : "http://www.google.com"},
          {site : "Runoob", url : "http://www.runoob.com"},
          {site : "Taobao", url : "http://www.taobao.com"}
      ];
  });
</script>
```

```
<div ng-app="myApp" ng-controller="myCtrl">
    <p>选择网站:</p>
    <select ng-model="selectedSite" ng-options="x.site for x in sites">
    </select>
    <h1>你选择的是: {{selectedSite.site}}</h1>
    <p>网址为: {{selectedSite.url}}</p>
</div>

<script>
    var app = angular.module('myApp', []);
    app.controller('myCtrl', function($scope) {
        $scope.sites = [
            {site : "Google", url : "http://www.google.com"},
            {site : "Runoob", url : "http://www.runoob.com"},
            {site : "Taobao", url : "http://www.taobao.com"}
        ];
    });
</script>
```

- 数据源为对象时对比实例

```
<div ng-app="myApp" ng-controller="myCtrl">
    <p>选择的网站是:</p>
    // 使用对象作为数据源, x 为键(key), y 为值(value):
    <select ng-model="selectedSite" ng-options="x for (x, y) in sites"> 
    </select>
    <h1>你选择的值是: {{selectedSite}}</h1>
</div>
<script>
    var app = angular.module('myApp', []);
    app.controller('myCtrl', function($scope) {
        $scope.sites = {
            site01 : "Google",
            site02 : "Runoob",
            site03 : "Taobao"
        };
    });
</script>
```