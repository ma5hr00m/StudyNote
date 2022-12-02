---
title: git的介绍基本使用
time: 2022-11-11
update: 2022-11-11
---

> :yum:刚听说`Git`的时候，甚至以为是`github`的简称……
>
> [廖雪峰`git`教程](https://www.liaoxuefeng.com/wiki/896043488029600)

## 版本控制（ Version Control ）

> ### wiki的定义
>
> In [software engineering](https://en.wikipedia.org/wiki/Software_engineering), **version control** (also known as **revision control**, **source control**, or **source code management**) is a class of systems responsible for managing changes to [computer programs](https://en.wikipedia.org/wiki/Computer_program), documents, large web sites, or other collections of information. Version control is a component of [software configuration management](https://en.wikipedia.org/wiki/Software_configuration_management).

简单地说，**版本控制**就是对程序、文档等的更改进行记录，方便协同开发或者后期查找。

而`Git`，是目前非常优秀的一个分布式版本控制系统。

## `Git`工作流程

`Git`有三个分区： 工作区、暂存区、仓库区。

当我们对仓库内文件进行更改时，变动文件（ 包括新增文件 ）属于工作区，我们需要将变动后的文件移动至仓库区，如有必要再将本地仓库区的文件推送到远程服务器上。

在`Git`的控制下，工作区的文件不会直接转入仓库区，而是会经历缓存区的中转。

- 工作区 => 暂存区

  ```shell
  $ git add fileName
  ```

  如果要将本地仓库所有改动都进行提交，只需将 `fileName` 改为 `*` 。

- 暂存区 => 仓库区

  ```shell
  $ git commit -m "note"
  ```

  为了方便查找提交，`note`逐渐形成了一定的规范，目前使用最广的是`Angular`。

## 安装`Git`

`Ubuntu`系统下，·控制台中输入一行代码即可完成`Git`的安装。

```shell
$ sudo apt install git
```

安装完成后，还要在设置一下全局名称和邮箱。

```shell
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```



## `Git`基本指令

- 版本库初始化（ 也就是将目录初始化为`Git `可管理的本地仓库 ）

  ```shell
  $ git init
  ```

- 查询本地仓库状态

  ```shell
  $ git status
  ```

- 查询本地仓库的修改状态

  ```shell
  $ git diff
  ```

- 显示本地仓库所有提交日志

  ```shell
  $ git log
  ```

- 显示所有本地仓库`commit`操作命令

  ```shell
  $ git reflog
  ```

- 本地仓库连接到`github`远程仓库

  ```shell
  $ git remote add origin YourGithubSSH
  ```

- 查看本地分支

  ```shell
  $ git branch -a
  ```

  









## `Git`使用时涉及到的一些概念
