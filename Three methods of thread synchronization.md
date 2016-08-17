## Linux下线程间同步的三种方式

------------------------------------------------

### 1.互斥锁（mutex）:通过锁机制实现线程间的同步。

	(1)初始化锁。在Linux下，线程的互斥量数据类型是pthread_mutex_t。在使用前,要对它进行初始化。
	   静态分配：pthread_mutex_t mutex = PTHREAD_MUTEX_INITIALIZER;
       动态分配：int pthread_mutex_init(pthread_mutex_t *mutex, const pthread_mutex_attr_t *mutexattr);
	
	(2)加锁。对共享资源的访问，要对互斥量进行加锁，如果互斥量已经上了锁，调用线程会阻塞，直到互斥量被解锁。
	   int pthread_mutex_lock(pthread_mutex *mutex);
       int pthread_mutex_trylock(pthread_mutex_t *mutex);
	
	(3)解锁。在完成了对共享资源的访问后，要对互斥量进行解锁。
	   int pthread_mutex_unlock(pthread_mutex_t *mutex);	
	
	(4)销毁锁。锁在是使用完成后，需要进行销毁以释放资源。
	   int pthread_mutex_destroy(pthread_mutex *mutex);

```cpp

		
		
		
```

<br>

### 2.条件变量(cond)：

	条件变量使我们可以睡眠等待某种条件出现。
	条件变量是利用线程间共享的全局变量进行同步的一种机制，主要包括两个动作：一个线程等待"条件变量的条件成立"而挂起；
	另一个线程使"条件成立"（给出条件成立信号）。为了防止竞争，条件变量的使用总是和一个互斥锁结合在一起。
	
```cpp

		
		
		
		
```

<br>

### 信号量（sem）：

	（1）信号量初始化。
		 int sem_init (sem_t *sem , int pshared, unsigned int value);
		 这是对由sem指定的信号量进行初始化，设置好它的共享选项(linux 只支持为0，即表示它是当前进程的局部信号量)，然后给它
		 一个初始值VALUE。
	（2）等待信号量。给信号量减1，然后等待直到信号量的值大于0。
		 int sem_wait(sem_t *sem);
	（3）释放信号量。信号量值加1。并通知其他等待线程。
		 int sem_post(sem_t *sem);
	（4）销毁信号量。我们用完信号量后都它进行清理。归还占有的一切资源。
		 int sem_destroy(sem_t *sem);

```cpp
		
		
		
		
```






















  
