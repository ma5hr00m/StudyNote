# Command Ijection

简单地说，就是过滤不严格，导致前端获取到的数据直接被后端函数执行，而这个函数可执行操作系统指令。

很多编程语言都支持执行系统命令，比如`c/c**`、`Java`、`PHP`、`GO`、`Rust`。

存在疑似注入点时（盲注），可通过添加`||`来测试注入点。