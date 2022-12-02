---
title: Ubuntu Environment
time: 2022-10-21
---

# Ubuntu Environment Construction

## Default JAVA  Runtime Environment

### Install JRE&JDK

We can install default jre&jdk via **apt**.

Firstly, update the apt( management tool of Debian ).

```shell
sudo apt update
```

Install the default JRE and check the version.

```shell
sudo apt install default-jre
```

```shell
java -version

$ output
openjdk version &quot;11.0.16&quot; 2022-07-19
OpenJDK Runtime Environment (build 11.0.16+8-post-Ubuntu-0ubuntu120.04)
OpenJDK 64-Bit Server VM (build 11.0.16+8-post-Ubuntu-0ubuntu120.04, mixed mode, sharing)
```

Install the default JDK and check the version.

```shell
sudo apt install default-jdk
```

```shell
javac -version

$ output
javac 11.0.16
```

### Install Intellij  IDEA

We can install **Intellij IDEA Community** expediently via **snap**.

```shell
sudo snap install intellij-idea-community --classic
```

Wait a minute, and you can find the **Intellij IDEA** in your applications.

Creat a new project, and then, start your java development journey.

## GO Runtime Environment

### Install go

Just install golang via apt and check the version.

```shell
sudo apt install golang-go
```

```shell
go version

$ output
go version go1.13.8 linux/amd64
```

I chose the Vscode to run Go code instead of Goland IDE of JetBrains, so we can run Go code just add the plug-in named  "Go".

## Python Runtime Environment

### Built-in Python

Ubuntu 20.04 has a built-in python, enter the following command to check your python version.

```shell
python
```

You can run python code via vscode plug-in named "Python", but you might encounter this problem when you run `python` document in VsCode.

```shell
/bin/sh: 1: python: not found
```

The reason is that `python` is replaced with `python3` or `python2`.

We can solve it via the following command.

```shell
 sudo ln -s /usr/bin/python3 /usr/bin/python
```

Now, run your python document in VSCode successfully.

## Node.js Installation

We can install node.js via apt and check the version.

```shell
sudo apt install nodejs
```

```shell
node -v

$ output
v10.19.0
```

## PHP Runtime Environment

### Install PHP

Install `php` via apt and check the version.

```shell
sudo apt install php
```

```shell
php -v

$ output
PHP 7.4.3 (cli) (built: Aug 17 2022 13:29:56) ( NTS )
Copyright (c) The PHP Group
Zend Engine v3.4.0, Copyright (c) Zend Technologies
    with Zend OPcache v7.4.3, Copyright (c), by Zend Technologies
```

### VSCode Setting PHP

Firstly, add the following plug-ins.

```shell
PHP server
PHP intellisense
PHP debug
PHP extension pack
PHP intelephense
```

Create a new php document, and begin.

## MySQL Runtime Environment

-  [apt install MySQL](https://blog.csdn.net/lianghecai52171314/article/details/113807099)

```shell
sudo apt-get install mysql-server
```

- [click me](https://www.digitalocean.com/community/tutorials/how-to-install-mysql-on-ubuntu-20-04)


## Apache2 Runtime Envronment

```shell
sudo apt install apache2
```

```shell
sudo ufw app list

$ output 
Available applications:
  Apache
  Apache Full
  Apache Secure
  CUPS
```

```shell
sudo ufw allow 'Apache'
```

```shell
sudo ufw status
```

Enter the following command to start your Apache2 server.

```shell
sudo systemctl start apache2
```

You can verify weather your Apache2 server start via visiting the localhost url. If you operating correctly, you can see the Apache2 Ubuntu default page.

```http
http://127.0.0.1
```

Check and make sure the Apache server is running.

```shell
sudo systemctl status apache2

$ output
● apache2.service - The Apache HTTP Server
     Loaded: loaded (/lib/systemd/system/apache2.service; enabled; vendor preset: enabled)
     Active: active (running) since Fri 2022-10-21 18:48:15 CST; 12min ago
       Docs: https://httpd.apache.org/docs/2.4/
    Process: 1027 ExecStart=/usr/sbin/apachectl start (code=exited, status=0/SUCCESS)
   Main PID: 1108 (apache2)
      Tasks: 7 (limit: 18732)
     Memory: 20.7M
     CGroup: /system.slice/apache2.service
             ├─1108 /usr/sbin/apache2 -k start
             ├─1109 /usr/sbin/apache2 -k start
             ├─1110 /usr/sbin/apache2 -k start
             ├─1111 /usr/sbin/apache2 -k start
             ├─1113 /usr/sbin/apache2 -k start
             ├─1114 /usr/sbin/apache2 -k start
             └─3609 /usr/sbin/apache2 -k start

10月 21 18:48:15 mashroom-dell systemd[1]: Starting The Apache HTTP Server...
10月 21 18:48:15 mashroom-dell apachectl[1068]: AH00558: apache2: Could not reliably determine the serve>
10月 21 18:48:15 mashroom-dell systemd[1]: Started The Apache HTTP Server.
```

Meantime, you can stop the Apache server via following command.

```shell
sudo systemctl stop apache2
```





