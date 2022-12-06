# SQLI

> [all-labs](https://portswigger.net/web-security/all-labs)

## Chapter 1

> :hammer: SQL injection vulnerability in WHERE clause allowing retrieval of hidden data

最基本的`GET`型注入。

选取某分类分页，拦截请求后修改`category`参数。

```
'+OR+1=1--
```

返回全部商品卡片。

## Chapter 2

> :hammer: SQL injection vulnerability allowing login bypass

`POST`型注入。

同时有`username`和`password`，且目前已知`username`，在`username`注入。

```
administrator'--
```

