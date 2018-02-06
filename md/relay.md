#### 1. 依赖注入

* 依赖注入（Dependency Injection，简称DI）是一种软件设计模式，在这种模式下，一个或更多的依赖（或服务）被注入（或者通过引用传递）到一个独立的对象（或客户端）中，然后成为了该客户端状态的一部分。

#### 2. AngularJS的五种核心组件

##### 2.1  value 

* Value 是一个简单的 javascript 对象，用于向控制器传递值（配置阶段）：

  ```javascript
  // 定义一个模块
  var mainApp = angular.module("mainApp", []);

  // 创建 value 对象 "defaultInput" 并传递数据
  mainApp.value("defaultInput", 5);
  ...

  // 将 "defaultInput" 注入到控制器
  mainApp.controller('CalcController', function($scope, CalcService, defaultInput) {
     $scope.number = defaultInput;
     $scope.result = CalcService.square($scope.number);
     
     $scope.square = function() {
        $scope.result = CalcService.square($scope.number);
     }
  });
  ```

##### 2.2  factory

* factory 是一个函数用于返回值。在 service 和 controller 需要时创建。

  ```javascript
  // 定义一个模块
  var mainApp = angular.module("mainApp", []);

  // 创建 factory "MathService" 用于两数的乘积 provides a method multiply to return multiplication of two numbers
  mainApp.factory('MathService', function() {
     var factory = {};
     
     factory.multiply = function(a, b) {
        return a * b
     }
     return factory;
  }); 

  // 在 service 中注入 factory "MathService"
  mainApp.service('CalcService', function(MathService){
     this.square = function(a) {
        return MathService.multiply(a,a);
     }
  });
  ```

	##### 2.3  service

##### 2.4  provider

* AngularJS 中通过 provider 创建一个 service、factory等(配置阶段)。

  ```javascript
  // 定义一个模块
  var mainApp = angular.module("mainApp", []);
  // 使用 provider 创建 service 定义一个方法用于计算两数乘积
  mainApp.config(function($provide) {
     $provide.provider('MathService', function() {
        this.$get = function() {
           var factory = {};  
           
           factory.multiply = function(a, b) {
              return a * b; 
           }
           return factory;
        };
     });
  });
  ```

##### 2.5  constant

* constant(常量)用来在配置阶段传递数值，注意这个常量在配置阶段是不可用的。

  ```
  mainApp.constant("configParam", "constant value");
  ```

```html
<body>
  <h2>AngularJS 简单应用</h2>
  
  <div ng-app = "mainApp" ng-controller = "CalcController">
      <p>输入一个数字: <input type = "number" ng-model = "number" /></p>
      <button ng-click = "square()">X<sup>2</sup></button>
      <p>结果: {{result}}</p>
  </div>
  
  <script src="http://cdn.static.runoob.com/libs/angular.js/1.4.6/angular.min.js"></script>
  
  <script>
      var mainApp = angular.module("mainApp", []);
      mainApp.value("defaultInput", 5);
      
      mainApp.factory('MathService', function() {
        var factory = {};
        
        factory.multiply = function(a, b) {
            return a * b;
        }
        return factory;
      });
      
      mainApp.service('CalcService', function(MathService){
        this.square = function(a) {
            return MathService.multiply(a,a);
        }
      });
      
      mainApp.controller('CalcController', function($scope, CalcService, defaultInput) {
        $scope.number = defaultInput;
        $scope.result = CalcService.square($scope.number);

        $scope.square = function() {
            $scope.result = CalcService.square($scope.number);
        }
      });	
  </script>
  
</body>
```

```html
 <body>
      <h2>AngularJS 简单应用</h2>
      
      <div ng-app = "mainApp" ng-controller = "CalcController">
         <p>输入一个数字: <input type = "number" ng-model = "number" /></p>
         <button ng-click = "square()">X<sup>2</sup></button>
         <p>结果: {{result}}</p>
      </div>
      
      <script src="http://cdn.bootcss.com/angular.js/1.4.6/angular.min.js"></script>
      
      <script>
         var mainApp = angular.module("mainApp", []);
         
         mainApp.config(function($provide) {
            $provide.provider('MathService', function() {
               this.$get = function() {
                  var factory = {};
                  
                  factory.multiply = function(a, b) {
                     return a * b;
                  }
                  return factory;
               };
            });
         });
			
         mainApp.value("defaultInput", 5);
         
         mainApp.service('CalcService', function(MathService){
            this.square = function(a) {
               return MathService.multiply(a,a);
            }
         });
         
         mainApp.controller('CalcController', function($scope, CalcService, defaultInput) {
            $scope.number = defaultInput;
            $scope.result = CalcService.square($scope.number);

            $scope.square = function() {
               $scope.result = CalcService.square($scope.number);
            }
         });
			
      </script> 
   </body>
```
