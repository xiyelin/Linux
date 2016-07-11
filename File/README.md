### UNIX系统文件I/O

  UNIX系统中大多数文件I/O都只用到5个函数： open()/read()/write()/lseek()/close()。这些函数经常被称为不带缓冲的
  
  I/O(unbuffered I/O)，不带缓冲是指每个read()和write()都调用内核中的一个系统调用。这些I/O函数不是ISO C的组成
  
  部分，但是它们是POSIX.1和Single UNIX Specification 的组成部分。


<br>

### 目录

* [文件描述符](https://github.com/xiyelin/Linux/blob/master/File/The%20file%20descriptor.md)
* [open()](#https://github.com/xiyelin/Linux/blob/master/File/Open%20Function.md)
* [create()](#https://github.com/xiyelin/Linux/blob/master/File/Create%20Function.md)
* [close()](#https://github.com/xiyelin/Linux/blob/master/File/Close%20Function.md)
* [lseek()](#https://github.com/xiyelin/Linux/blob/master/File/Lseek%20Function.md)
* [read()](#https://github.com/xiyelin/Linux/blob/master/File/Read%20Function.md)
* [write()](#https://github.com/xiyelin/Linux/blob/master/File/Write%20Function.md)
* [I/O的效率](#https://github.com/xiyelin/Linux/blob/master/File/The-efficiency-of-the-I%5CO.md)
* [文件共享](#https://github.com/xiyelin/Linux/blob/master/File/File%20sharing.md)
* [原子操作](#https://github.com/xiyelin/Linux/blob/master/File/Atomic%20operation.md)
* [dup和dup2函数](#https://github.com/xiyelin/Linux/blob/master/File/dup%20and%20dup2.md)
* [sysc、fsync 和 fdatasync 函数](#https://github.com/xiyelin/Linux/blob/master/File/sysc%E3%80%81fsync%20and%20fdatasync%20Function.md)
* [fcntl()](#https://github.com/xiyelin/Linux/blob/master/File/Fcntl%20Function.md)


<br>

--------------------------------------------------------------------------------------------------







