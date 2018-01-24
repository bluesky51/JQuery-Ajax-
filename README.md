# jQuery的ajax

## 前提：要导入jQuery的js包

### 1.$.get()

####   1.1 该方法中参数介绍：

```js
$.get(url,params,function(data){},dataType);
/**
*url：请求服务器的资源的地址
*params： 请求参数
       方式一：
       方式二：
*function(data){}：请求结果的回调函数 ，data是结果数据
*dataType：返回的结果的数据类型，可以是json，xml,text。。。。。。
*/
```

####  1.2 示例：

```js
 $(document).ready(function() {
	   var url="Servlet01";
	   //方式一：提交的是key=value的键值对的字符串类型
	   //var params="username=pipixia&password=1234567";   
	   //方式二：提交的是json对象
	   var params={"username":"sky","password":"123"};
	   alert(params);
	   var dataType="json";
   	  $.get(url, params, function(data) {
   	  	  alert("结果:"+data.msg);
   	  }, dataType);
   }); 
```

### 2.$.post()

2.1 该方法中参数介绍：

```js
$.post(url,params,function(data){},dataType);
/**
*url：请求服务器的资源的地址
*params： 请求参数
       方式一：
       方式二：
*function(data){}：请求结果的回调函数 ，data是结果数据
*dataType：返回的结果的数据类型，可以是json，xml,text。。。。。。
*/
```

2.2 示例：

```js
$(document).ready(function() {
	   var url="Servlet01";
	   //方式一：提交的是key=value的键值对的字符串类型
	   //var params="username=pipixia&password=1234567";   
	   //方式二：提交的是json对象
	   var params={"username":"sky","password":"123"};
	   alert(params);
	   var dataType="json";
   	  $.post(url, params, function(data) {
   	  	  alert("结果:"+data.msg);
   	  }, dataType);
   }); 
```

### 综合案例： 

```js
$.get或者$.post完成一个表单提交功能:

备注：
  1.表单不需要写action。method和submit按钮
  示例：
  <form>
	用户名：<input type="text" name="username"/><br>
	密码：<input type="text" name="password"/><br>
	<input type="button" value="登录" id="btn"/>
 </form>

  使用jQuery的ajax提交：
     前提条件：表单必须序列化。
     序列化的方式：
        方式一： $("form").serialize()   key=value键值对组成的字符串形式
        方式二： $("form").serializeArray()  json对象结构的形式

   示例：
$(document).ready(function() {
	   $("#btn").click(function() {
			//jQuery的ajax提交表单数据需要进行表单序列化
			var url="Servlet01";
			var params=$("form").serialize();
			$.post(url, params, function(data) {
				 alert("===="+data.msg);
			}, "json");
	   });
   });
```

### 3.jQuery对象.load()

3.1 该方法中参数介绍：

```js
jQuery对象.load(url,params,function(data){})
/**
*url:服务器的资源地址
*params:请求参数
         传递key=value形式或者空参数(不传参数)是GET,
         传递参数是json对象类型的会转化成POST请求。
*function(data) 结果响应函数
*/
```

3.2 示例：

```html
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>Insert title here</title>
<script type="text/javascript" src="js/jquery-1.8.3.min.js"></script>
<script type="text/javascript">
   $(document).ready(function() {
	   $("input").click(function() {
	   	   //load()请求
	   	   var url="Servlet02";
	   	   var params="ss=22";
	   	   $(this).load(url,params,function(data) {
	   		   //得到的结果是具有json结构的字符串
	   		  //使用JSON.parse(str)转化成对象
	   		   var result= JSON.parse(data);
	   		   var msg1= result.msg;
	   		   $("span").html(msg1);
	   	   });
	   });
   });
</script>
</head>
<body>
<input type="button" value="发送请求"/><span></span>
</body>
</html>
```



### 4.$.ajax()

示例：

```js
	  /* 
	   	     url: 服务器的资源地址
	   		 type:请求方式GET,POST
	   		 data:请求参数
	   	     dataType: 结果类型
	   	     success:fn 成功的函数
	   	     error:fn   失败的函数
	   	 */
	   	   $.ajax({
	   		   "url":url,
	   		   "type":"GET",
	   		   "data":params,
	   		   "dataType":"json",
	   		   "success":function(data){
	   			   alert("000000===="+data.msg);   
	   		   },
	   		   "error":function(data){
	   			   alert("服务器繁忙，请稍后再试");
	   		   }
	   	   });
```

