---
title: LNMP开发环境搭建
time: 2022-10-28
update: 2022-12-02
---

<br>

---

<div align=center>

<h1> LAMP环境搭建 </h1>

</div>

> :hammer: Linux版本: Ubuntu20.04  

<br>

<div align=center>

<h2> 0x01 安装 Apache </h2>

</div>

终端中输入以下命令安装`Apache Web`服务器。

```shell
sudo apt install -y apache2
```
查看`Apache`版本。

```shell
apache2 -v

// the first lilne of response
Server version: Apache/2.4.41 (Ubuntu)
```

使用以下命令检查`Apache`运行状态（ 安装后会自动启动 ）。

```shell
systemctl status apache2

// the first line of response
● apache2.service - The Apache HTTP Server
```

`Apache Web`服务启动后，在浏览器中访问`127.0.0.1`，显示`Apache2 Ubuntu Default Page`。

<br>

>`Apache`服务基本指令
>
>- 启动web服务器
>
>  ```shell
>  sudo systemctl start apache2
>  ```
>
>- 停止web服务器
>
>  ```shell
>  sudo systemctl stop apache2
>  ```
>
>- 重新加载`Apache`
>
>  ```shell
>  sudo systemctl reload apache2
>  ```
>
>- 设置`Apache`服务自启动
>
>  ```shell
>  sudo systemctl enable apache2
>  ```
>
>- 关闭`Apache`服务自启动
>
>  ```shell
>  sudo systemctl disable apache2
>  ```

<br>

<div align=center>

<h2> 0x02 安装 MySQL </h2>

</div>

<br>

命令安装`MySQL`。

```shell
sudo apt install mysql-server
```

查看`MySQL`版本。

```shell
sudo /etc/init.d/mysql startmysql --version

// display
mysql  Ver 8.0.31-0ubuntu0.20.04.1 for Linux on x86_64 ((Ubuntu))
```

启动`MySQL`服务。

```shell
sudo service mysql start
```

查看`MySQL`服务运行状态。

```shell
sudo service mysql status
```

关闭`MySQL`服务。

```shell
sudo service mysql stop
```

<div align=center>

<h2> 0x03 安装PHP </h2>

</div>

命令安装`PHP7`。

```shell
sudo apt install php
```

为了让`Apache`识别解析`php`文件，安装适合相应的插件。

```shell
sudo apt install libapache2-mod-php
```

装入`/var/www/html`目录中，创建一个`test.php`文件，输入如下代码，然后在浏览器中访问`127.0.0.1/test.php`，可访问到`phpinfo page`。

```php
<?php
	phpinfo();
?>
```

<br>

<div align=center>

---

小小的总结

---

最基本的`LAMP`环境搭建

实际上还不能达到开发的程度

随着后续的学习

:yum:笔记也会更新哦

</div>

