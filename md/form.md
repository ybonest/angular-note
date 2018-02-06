#### 1.数据绑定

```
<body>
    <div ng-app="">
      <form>
        First Name: <input type="text" ng-model="firstname">
      </form>
      <h1>你输入的内容为: {{firstname}}</h1>
    </div>
    <p>修改输出框的内容，显示信息也会跟着变化。</p>
</body>
```

#### 2. Chekcbox(复选框)

```
<div ng-app="">
  <form>
    选中复选框，显示标题:
    <input type="checkbox" ng-model="myVar">
  </form>
  <h1 ng-show="myVar">My Header</h1>
</div>
```

#### 3. 单选框

```
<body ng-app="">
<form>
  选择一个选项:
  <input type="radio" ng-model="myVar" value="dogs">Dogs
  <input type="radio" ng-model="myVar" value="tuts">Tutorials
  <input type="radio" ng-model="myVar" value="cars">Cars
</form>
<div ng-switch="myVar">
  <div ng-switch-when="dogs">
     <h1>Dogs</h1>
     <p>Welcome to a world of dogs.</p>
  </div>
  <div ng-switch-when="tuts">
     <h1>Tutorials</h1>
     <p>Learn from examples.</p>
  </div>
  <div ng-switch-when="cars">
     <h1>Cars</h1>
     <p>Read about cars.</p>
  </div>
</div>
<p>ng-switch 指令根据单选按钮的选择结果显示或隐藏 HTML 区域。</p>
</body>
```

#### 4. 下拉菜单

```
<form>
  选择一个选项:
  <select ng-model="myVar">
    <option value="">
    <option value="dogs">Dogs
    <option value="tuts">Tutorials
    <option value="cars">Cars
  </select>
</form>

<div ng-switch="myVar">
  <div ng-switch-when="dogs">
     <h1>Dogs</h1>
     <p>Welcome to a world of dogs.</p>
  </div>
  <div ng-switch-when="tuts">
     <h1>Tutorials</h1>
     <p>Learn from examples.</p>
  </div>
  <div ng-switch-when="cars">
     <h1>Cars</h1>
     <p>Read about cars.</p>
  </div>
</div>
```

#### AngularJS输入验证

```
<form  ng-app="myApp"  ng-controller="validateCtrl" name="myForm" novalidate>
  <p>用户名:<br>
    <input type="text" name="user" ng-model="user" required>
    <span style="color:red" ng-show="myForm.user.$dirty && myForm.user.$invalid">
    <span ng-show="myForm.user.$error.required">用户名是必须的。</span>
    </span>
  </p>
  <p>邮箱:<br>
    <input type="email" name="email" ng-model="email" required>
    <span style="color:red" ng-show="myForm.email.$dirty && myForm.email.$invalid">
    <span ng-show="myForm.email.$error.required">邮箱是必须的。</span>
    <span ng-show="myForm.email.$error.email">非法的邮箱。</span>
    </span>
  </p>
  <p>
    <input type="submit"
    ng-disabled="myForm.user.$dirty && myForm.user.$invalid ||
    myForm.email.$dirty && myForm.email.$invalid">
  </p>

</form>
<script>
    var app = angular.module('myApp', []);
    app.controller('validateCtrl', function($scope) {
        $scope.user = 'John Doe';
        $scope.email = 'john.doe@gmail.com';
    });
</script>
```

| $dirty    | 表单有填写记录  |
| :-------- | -------- |
| $valid    | 字段内容合法的  |
| $invalid  | 字段内容是非法的 |
| $pristine | 表单没有填写记录 |
