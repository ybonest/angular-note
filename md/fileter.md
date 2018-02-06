+ 在HTML模版绑定符号{{}}内通过 | 符号来调用过滤器

例：将字符串转为大写：`{{name|uppercase}}`

**以HTML形式使用过滤器时，如果需要传递参数给过滤器，只需在过滤器名字后加冒号即可**

例：`{{123.4567 | number:2}}` 

- 在JavaScript代码中可以通过**$filter** 来调用过滤器，例：

```javascript
app.controller('DemoController',['$scope','$filter',function($scope,$filter){
  $scope.name = $filter('lowercase')('Ari');
}])
```

- Angular内置过滤器

  1. currency --- 将数值格式化为货币格式 ，例：`{{ 123 | currency }}`

  2. date --- 将日期转化为需要的格式

     ```
     {{ today | date:'short' }} <!-- 8/9/1312:09PM -->
     {{ today | date:'fullDate' }} <!-- Thursday, August 09, 2013 -->
     {{ today | date:'longDate' }} <!-- August 09, 2013 -->
     {{ today | date:'mediumDate' }}<!-- Aug 09, 2013 -->
     {{ today | date:'shortDate' }} <!-- 8/9/13 -->
     {{ today | date:'mediumTime' }}<!-- 12:09:02 PM -->
     {{ today | date:'shortTime' }} <!-- 12:09 PM -->
      年份格式化
     四位年份：{{ today | date:'yyyy' }} <!-- 2013 -->
     两位年份：{{ today | date:'yy' }} <!-- 13 -->
     一位年份：{{ today | date:'y' }} <!-- 2013 -->
      月份格式化
     英文月份：{{ today | date:'MMMM' }} <!-- August -->
     英文月份简写：{{ today | date:'MMM' }} <!-- Aug -->
     数字月份：{{ today |date:'MM' }} <!-- 08 -->
     一年中的第几个月份：{{ today |date:'M' }} <!-- 8 -->
      日期格式化
     数字日期：{{ today|date:'dd' }} <!-- 09 -->
     一个月中的第几天：{{ today | date:'d' }} <!-- 9 -->
     英文星期：{{ today | date:'EEEE' }} <!-- Thursday -->
     英文星期简写：{{ today | date:'EEE' }} <!-- Thu -->
      小时格式化
     24小时制数字小时：{{today|date:'HH'}} <!--00-->
     一天中的第几个小时：{{today|date:'H'}} <!--0-->
     12小时制数字小时：{{today|date:'hh'}} <!--12-->
     上午或下午的第几个小时：{{today|date:'h'}} <!--12-->
      分钟格式化
     数字分钟数：{{ today | date:'mm' }} <!-- 09 -->
     一个小时中的第几分钟：{{ today | date:'m' }} <!-- 9 -->
      秒数格式化
     数字秒数：{{ today | date:'ss' }} <!-- 02 -->
     一分钟内的第几秒：{{ today | date:'s' }} <!-- 2 -->
     毫秒数：{{ today | date:'.sss' }} <!-- .995 -->
      字符格式化
     上下午标识：{{ today | date:'a' }} <!-- AM -->
     四位时区标识：{{ today | date:'Z' }} <!--- 0700 -->
     下面是一些自定义日期格式的示例：
     {{ today | date:'MMMd, y' }} <!-- Aug9, 2013 -->
     {{ today | date:'EEEE, d, M' }} <!-- Thursday, 9, 8-->
     {{ today | date:'hh:mm:ss.sss' }} <!-- 12:09:02.995 -->
     ```

  3. filter --- 从给定 ***数组*** 中选择一个子集，并将其生成一个新数组返回

     3. 1  这个过滤器第一个参数可以是字符串、对象或是一个用来从数组中选择元素的函数

     - 字符串

       返回所有包含这个字符串的元素，在参数前加 ! ，返回所有不包含，例：

       `{{ ['Ari','Lerner','Likes','To','Eat','Pizza'] | filter:'e' }}`

       <!--["Lerner","Likes","Eat"]-->

     - 对象

       AngularJS会将待过滤对象的属性同这个对象中的同名属性进行比较，如果属性值是字符串就会判断是否包含该字符串。

       如果希望对全部属性进行对比，可以将  **$**  当做键名。

       ```
       {{ [{
       'name': 'Ari',
       'City': 'San Francisco',
       'favorite food': 'Pizza'
       },{
       'name': 'Nate',
       'City': 'San Francisco',
       'favorite food': 'indian food'
       }] | filter:{'favorite food': 'Pizza'} }}
       ```

       <!--[{"name":"Ari","City":"SanFrancisco","favoritefood":"Pizza"}]-->

     - 函数

       对每个元素都执行这个函数，返回非假值得元素出现在新的数组中并返回

       ```javascript
       $scope.isCapitalized = function(str) {
       return str[0] == str[0].toUpperCase();
       };
       {{ ['Ari','likes','to','travel'] | filter:isCapitalized }}
       ```

     3. 2  filter过滤器传入第二个参数
        - true --- 用angular.equals(expected,actual)对两个值进行严格比较
        - false --- 进行区分大小写的子字符串比较
        - 函数 --- 运行这个函数，如果返回真值就接受这个元素

  4. json --- json过滤器可以将一个JSON或javascript对象转换成字符串

     ```javascript
     {{ {'name': 'Ari', 'City': 'SanFrancisco'} | json }}
     ```

     <!-- {"name": "Ari","City": "San Francisco"} -->

  5.  limitTo

     ​	limitTo过滤器会根据传入的参数生成一个新的数组或字符串，新的数组或字符串的长度取决于传入的参数，通过传入参数的正负值来控制从前面还是从后面开始截取。

     ​	如果传入的长度大于被操作数组或字符串的长度，那么整个数组或字符串都会被返回。

     ```
     {{ San Francisco is very cloudy | limitTo:3 }} //San
     {{ San Francisco is very cloudy | limitTo:-6 }} //cloudy
     {{ ['a','b','c','d','e','f'] | limitTo:1 }} //["a"]
     ```

  6.  lowercase/uppercase --- 过滤器将字符串转为小/大写。

     ```
     {{ "San Francisco is very cloudy" | lowercase }}
     {{ "San Francisco is very cloudy" | uppercase }}
     ```

     ```
     <div ng-app="myApp" ng-controller="namesCtrl">
     		<input type="text" ng-model='test'>
     		<ul>
     			<li ng-repeat="x in names | filter:test | orderBy:'country' ">
     				{{(x.name | uppercase)+', '+x.country}}
     			</li>
     		</ul>
     	</div>
     	<script>
     		var app = angular.module('myApp',[]);
     		app.controller('namesCtrl',function($scope){
     			$scope.names = [
     				{name:'Jani',country:'Norway'},
     		        {name:'Hege',country:'Sweden'},
     		        {name:'Kai',country:'Denmark'}
     			];
     		})
     	</script>
     ```