<div align=center>

# Golang | log库

## log库

</div>

`log库`为`golang`提供基本的日志功能。

> #### :question:什么是“日志文件”，为什么需要日志文件
>
> 计算机领域的日志文件是一个记录了发生在运行中的操作系统中或其它软件中的事件的文件，或者记录了在网络聊天软件的用户之间发送的消息的文件。日志记录是指保存日志的行为。
>
> ##### 事件日志 ( event logs )
>
> 记录了在系统运行期间发生的事件，以便于了解系统活动和诊断问题，以及了解复杂系统的活动轨迹。
>
> ##### 事务日志 ( transaction log )
>
> 采用于大多数数据库系统中，记录了对存储数据的更改，以允许数据库在发生崩溃或其他数据错误后恢复并维护存储数据的一致状态。
>
> ##### 消息日志
>
> 消息日志记录了通讯双方之间的通信，一般都是纯文本文件，但即时通信和支持文字聊天的客户端可能使用HTML或某种自定义格式保存消息，以便于阅读或加密。

### log快速上手

`log`默认输出到标准错误 ( `stderr` ) ，并主要提供了三类接口和三种调用方式。

> #### :question:什么是标准错误`stderr`？
>
> 标准错误是`linux | shell`下的概念，要理解标准错误还需要一点点前置知识。
>
> ##### 文件描述符
>
> `linux`中一切皆文件，为了表示和区分已打开的文件，`linux`给每个文件分配一个整数`ID`，被称为文件描述符。
>
> `shell`中一个命令运行时默认打开三个文件，默认使用文件描述符0, 1, 2指代这三个文件。
>
> ```shell
> stdin  0  标准输入 （键盘）
> stdout 1  标准输出 （终端）
> stderr 2  标准错误 （终端）
> ```
>
> ##### 输出重定向
>
> `>`表示覆盖，`>>`表示追加。`>`和 `>>` 默认为标准输出。
>
> ```shell
>  # 标准输出重定向 
> command 1>  file：以覆盖的方式，把 command 的正确输出结果输出到 file 文件中。
> command 1>> file： 以追加方式，把 command 的正确输出结果输出到 file 文件中。
> 
> # 标准错误输出重定向
> command 2>  file：以覆盖的方式，把 command 的错误信息输出到 file 文件中。
> command 2>> file：以追加的方式，把 command 的错误信息输出到 file 文件中。
> ```
>
> ##### 输入重定向
>
> 改变输入方向，不适用键盘，而是使用文件作为命令的输入。
>
> ```shell
> # 将 file 中的内容当做 command 的输入
> command < file
> 
> # 从标准输入中读取数据，直到遇到 分界符tag 停止
> command << tag
> 
> # 将 file1 作为 command 的输入， 并将 command 的结果输入到 file2 中
> command <file1 >file2
> ```
>
> ##### 标准输出和标准错误
>
> 通俗点说，标准输出和标准错误都是指执行指令后在`terminal`中打印出来的话。
>
> 命令正常执行时打印出来的是标准输出，而命令错误时打印出来的就是标准错误。
>
> 输出重定向在`log`库中的主要运用，就是**将本该打印到终端的命令反馈（ log日志 ）保存到日志文件中**。

#### `log`的三类接口及三种方法

简单写一下用法。

```shell
# Print()输出内容到 stderr
Print("ayy!")

# Prinln()相较于Print()多了自动换行
Println("ayy")

# Printf()允许通过占位符使用变量
ayy = "ayy"
Printf("%s", ayy)

# Fatal()输出内容到标准输出，然后调用 os.exit(1)， 退出程序并返回状态 1

# Panic()没搞懂...
```

> #### :question: `defer`关键字的作用
>
> 表示延迟调用，通常用于关闭一些资源
>
> ```go
> func main() {
> 	fmt.Println("start")
> 	defer fmt.Println("defer")
> 	fmt.Println("end")
> }
> 
> /**********
> print result of main():
> start
> end 
> defer
> ***********/
> ```



### `logger`配置

#### 信息显示

默认的`logger`配置只提供日志的时间信息，但我们可以使用`log`库中的方法对其进行修改，使其显示更多的信息。

使用`Flags()`函数返回标准`logger`的输出配置，调用`setFlags()`函数`logger`的输出配置。

```go
//log 标准库提供了如下的 flag 选项，它们是一系列定义好的常量。

const (
    // 控制输出日志信息的细节，不能控制输出的顺序和格式。
    // 输出的日志在每一项后会有一个冒号分隔： 例如2009/01/23 01:23:23.123123 /a/b/c/d.go:23: message
    Ldate         = 1 << iota     // 日期：2009/01/23
    Ltime                         // 时间：01:23:23
    Lmicroseconds                 // 微秒级别的时间：01:23:23.123123（用于增强Ltime位）
    Llongfile                     // 文件全路径名+行号： /a/b/c/d.go:23
    Lshortfile                    // 文件名+行号：d.go:23（会覆盖掉Llongfile）
    LUTC                          // 使用UTC时间
    LstdFlags     = Ldate | Ltime // 标准logger的初始值
)
```

下面是一个`setFlags()`使用实例。

```go
func main() {
 	log.SetFlags(log.Lshortfile | log.Ldate | log.Lmicroseconds)
    log.Printf("[ ma5hr00m login ]")
}
```

输出结果

```go
2022/12/03 11:56:59.061615 main.go:20: [ ma5hr00m login ]
```

#### 前缀

除了显示的信息，`log`还支持`SetPrefix()`，让我们为日志自定义前缀。

```go
func main() {
    log.SetPrefix("[ ma5hr00m ]")
	log.Println("< login >")
}
```

输出结果

```go
[ ma5hr00m ]2022/12/04 23:22:18 < login >
```

#### 输出位置

`log`默认输出到标准错误，使用`setOutput()`我们可以设置输出目的地。

使用标准`logger`时，我们会将配置写到`init()`中。

```go
// 写入同级目录下的 xx.log 文件中
func init() {
	logFile, err := os.OpenFile("./xx.log", os.O_CREATE|os.O_WRONLY|os.O_APPEND, 0644)
	if err != nil {
		fmt.Println("open log file failed, err:", err)
		return
	}
	log.SetOutput(logFile)
	log.SetFlags(log.Llongfile | log.Lmicroseconds | log.Ldate)
}
```



### 自定义`logger`

`log`默认的`logger`被称为`std`，意思是标准日志。我们可以直接修改`std`，也使用`log.New()`自定义一个`logger`。

```go
package main

import (
  "bytes"
  "fmt"
  "log"
)

type User struct {
  Name string
  Age  int
}

func main() {
  u := User{
    Name: "dj",
    Age:  18,
  }

  buf := &bytes.Buffer{}
  logger := log.New(buf, "", log.Lshortfile|log.LstdFlags)

  logger.Printf("%s login, age:%d", u.Name, u.Age)

  fmt.Print(buf.String())
}
```

`log.New()`接受三个参数：

- `io.Writer`：日志都会写到这个`Writer`中，可以是标准输出、文件甚至发送到网络；
- `prefix`：前缀，也可以后面调用`logger.SetPrefix`设置；
- `flag`：选项，也可以后面调用`logger.SetFlag`设置。

上面代码将日志输出到一个`bytes.Buffer`，然后将这个`buf`打印到标准输出。

> #### :question:  bytes.Buffer
>
> bytes.Buffer 是 Golang 标准库中的缓冲区，具有读写方法和可变大小的字节存储功能。
>
> [进一步了解戳这里](https://cloud.tencent.com/developer/article/1456243)

