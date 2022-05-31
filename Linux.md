# Linux

## 常见目录及区别

### usr

> `/usr` 是系统核心所在，它是 **Unix System Resources** 的缩写，意思是 **Unix 系统资源** 。包含了所有的共享文件。它是 unix 系统中最重要的目录之一，涵盖了二进制文件，各种文档，各种头文件，还有各种库文件；还有诸多程序，例如 ftp，telnet 等等。**usr 是可共享的只读数据**。这意味着 /usr 应该可以在各种符合主机之间共享，并且不能被写入。任何特定于主机或随时间变化的信息都存储在其他地方。

/usr/lib：所有可执行文件所需要的库文件

/usr/local：这里主要存放那些手动安装的软件，即不是通过apt-get安装的软件

/usr/share：放置的是一些共享数据，比如帮助文档什么的。/usr/share/man：联机帮助文件；/usr/share/doc：软件杂项的文件说明等

### lib

`/lib` 文件夹是 **库文件目录** ，包含了所有对系统有用的库文件。简单来说，它是应用程序、命令或进程正确执行所需要的文件。在 `/bin` 或 `/sbin` 目录中的命令的动态库文件正是在此目录中。内核模块同样也在这里。

## 参考文档

[**Filesystem Hierarchy Standard**](https://refspecs.linuxfoundation.org/FHS_3.0/fhs/index.html)

