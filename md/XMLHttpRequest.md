* $http是AngularJS中的一个核心服务，用于读取远程服务器的数据，使用格式：

```
$http({
    method: 'GET',
    url: '/someUrl'
}).then(function successCallback(response) {
        // 请求成功执行代码
    }, function errorCallback(response) {
        // 请求失败执行代码
});
```

* 简写方法

```
$http.get('/someUrl', config).then(successCallback, errorCallback);
$http.post('/someUrl', data, config).then(successCallback, errorCallback);
```

* 此外还有以下简写方法：

  - $http.get
  - $http.head
  - $http.post
  - $http.put
  - $http.delete
  - $http.jsonp
  - $http.patch