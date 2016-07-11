### UNIX系统文件I/O

  UNIX系统中大多数文件I/O都只用到5个函数： open()/read()/write()/lseek()/close()。这些函数经常被称为不带缓冲的I/O(unbuffered I/O)，
  
  不带缓冲是指每个read()和write()都调用内核中的一个系统调用。这些I/O函数不是ISO C的组成部分，但是它们是POSIX.1和Single UNIX Speci-
  
  fication 的组成部分。
  

### 目录

* [文件描述符](./the file descriptor)
* [](#)
* [](#)
* [](#)
* [](#)
* [](#)
* [](#)
* [](#)
