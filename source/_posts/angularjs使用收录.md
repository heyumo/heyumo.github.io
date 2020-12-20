---
title: angularjs使用收录
categories:
	一起前端喵喵叫
date: 2020-01-30 17:58:34
notshow: true
---
1、angular的表单提交方式有所不同，$http服务代替ajax与后台交互，格式为：
``` r
$http({
    method: 'GET',
    url: '/someUrl'
}).then(function successCallback(response) {
        // 请求成功执行代码
    }, function errorCallback(response) {
        // 请求失败执行代码
});
```
其中get方式的传输数据可使用：params{id:''001,name:'hezhiyu'}、data:{$.params($scope.user)}、data:{'id':'123456','name':'zhangsan'}, 无需申明其他属性
post方式需要申明headers属性:

``` r
$http({
    method:'post',
    url:'addUser',
    data:$.param($scope.user),
    headers: {
        'Content-Type': 'application/x-www-form-urlencoded'
    }
})

```
其中，如需使用data:{"orderId":orderId}，这种方式传递，需要transformRequest来改变格式
``` r
transformRequest: function(obj) {
    var str = [];
    for (var s in obj) {
        str.push(encodeURIComponent(s) + "=" + encodeURIComponent(obj[s]));
    }
    return str.join("&");
}

```
提交文件配合表单提交的方式：
``` r
var form = new FormData($("#formId")[0]);
var file = document.querySelector('input[type=file]').files[0];
$http({
    method:'post',
    url:'updateOrder',
    data:form ,
    headers: {
        'Content-Type': undefined
    },
    transformRequest: angular.identity
})

```
2、循环指令配合过滤器的使用，ng-repeat="wehchart in orderList | filter:{mediaType:2} | filter:{mediaOrderStatus:4}"，取值：{{wehchart.orderNo}}，这种多级过滤的方式不建议使用，因为后台数据量过大的情况不利于性能

3、ng-if指令
``` r
<span ng-if="wehchart.status==='0'" style="color: red">已下单,未支付</span>
<span ng-if="wehchart.status==='1'" style="color:green">支付完成</span>
```
4、ng-click与href
``` r
ng-click="deleteBlogCart(allCart.cartId)"
href="getMediaOrder?orderId={{wehchart.orderId}}&mediaType={{wehchart.mediaType}}"
```
5、解析html
定义过滤器：
``` r
app.filter('trustHtml',['$sce',function($sce){
    return function(data){
        return $sce.trustAsHtml(data);
    }
}]);
```
调用：
``` r
<span  ng-bind-html="rule.rulesContent | trustHtml"></span>
```