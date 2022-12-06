<div align=center>

# Golang | io/ioutil库

## io/ioutil库

</div>

> #### :question: 什么是`I/O`？
>
> IO在计算机中指Input/Output，也就是输入和输出。由于程序和运行时数据是在内存中驻留，由CPU这个超快的计算核心来执行，涉及到数据交换的地方，通常是磁盘、网络等，就需要IO接口。
>
> IO编程中，Stream（流）是一个很重要的概念，可以把流想象成一个水管，数据就是水管里的水，但是只能单向流动。Input Stream就是数据从外面（磁盘、网络）流进内存，Output Stream就是数据从内存流到外面去。
>
> [戳这里了解详情](https://www.jianshu.com/p/8fb6d43a6692)