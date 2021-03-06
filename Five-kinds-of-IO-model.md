## 五种I/O模型

--------------------------

- [x] 阻塞I/O 
- [x] 非阻塞I/O
- [x] I/O多路复用(select,poll,epoll)
- [x] 信号驱动I/O
- [x] 异步I/O

<br>

### 1.阻塞I/O模型：
	
	应用用程序调用一个I/O函数，导致应用程序阻塞，等待数据准备好。如果数据没有准备好，一直等待。数据准备好了，
	
	从内核拷贝到用户空间，I/O函数返回成功指示。
	

### 2.非阻塞I/O模型：
	
	我们把一个套接口设置为非阻塞就是告诉内核，当所请求的I/O操作无法完成时，不要将进程睡眠，而是返回一个错误。
	
	这样我们的I/O操作函数将不断的测试数据是否已经准备好，如果没有准备好，继续测试，直到数据准备好为止。在这
	
	个不断测试的过程中，会大量的占用CPU的时间。
	

### 3.多路复用I/O模型：

	I/O复用模型会用到select或者poll函数，这两个函数也会使进程阻塞，但是和阻塞I/O所不同的的，这两个函数可以同时
	
	阻塞多个I/O操作。而且可以同时对多个读操作，多个写操作的I/O函数进行检测，直到有数据可读或可写时，才真正调用
	
	I/O操作函数。
	

### 4.信号驱动I/O模型：

	首先我们允许套接口进行信号驱动I/O,并安装一个信号处理函数，进程继续运行并不阻塞。当数据准备好时，进程会收到一
	
	个SIGIO信号，可以在信号处理函数中调用I/O操作函数处理数据。。
	

### 5.异步I/O模型：

	调用aio_read()函数，告诉内核描述字，缓冲区指针，缓冲区大小，文件偏移以及通知的方式，然后立即返回。当内核将数
	
	据拷贝到缓冲区后，再通知应用程序。
	
	
<br>


### 五种I/O模型的比较：

	前四种模型的区别是第一阶段基本相同，第二阶段基本相同，都是将数据从内核拷贝到调用者的缓冲区。而异步I/O的两个阶
	
	段都不同于前四个模型。
	

### 同步/异步的区别 && 阻塞/非阻塞的区别

	　　同步和异步关注的是消息通信机制所谓同步，就是在发出一个调用时，在没有得到结果之前，该调用就不返回。但是一旦调用
	
	返回，就得到返回值了。换句话说，就是由调用者主动等待这个调用的结果。
	
	　　而异步则是相反，调用在发出之后，这个调用就直接返回了，所以没有返回结果。换句话说，当一个异步过程调用发出后，调用
	
	者不会立刻得到结果。而是在调用发出后，被调用者通过状态、通知来通知调用者，或通过回调函数处理这个调用。
	
	
	　　阻塞和非阻塞关注的是程序在等待调用结果（消息，返回值）时的状态（老板在查的时候，你是一只在等，还是每隔几分钟问一次）.
	
	阻塞调用是指调用结果返回之前，当前线程会被挂起。调用线程只有在得到结果之后才会返回。
	
	　　非阻塞调用指在不能立刻得到结果之前，该调用不会阻塞当前线程。


<br>


	同步就是同步，异步就是异步! 目前应用中阻塞和非阻塞是针对同步应用而言。io请求分两步：

	1. 先将数据从存储介质（磁盘，网络等）拷贝到内核缓冲区，此时称为数据准备好，可以被用户应用程序读取。

	2. 由用户应用程序拷贝内核缓冲区中的数据到用户缓冲区。

	同步，数据从存储介质拷贝到内核缓冲区（数据准备的过程）完成之后，需要用户自己将数据拷贝到用户缓冲区。

	异步，步骤1，2 用户都不关心，只要发起I/O请求，后面得到I/O结果即可。
	
	所以，前4种I/O模型都是同步的！！！
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
